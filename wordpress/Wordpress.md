# Wordpress Snippets

## increase upload size wp

.htaccess

```bash
    php_value upload_max_filesize 64M
    php_value post_max_size 64M
    php_value max_execution_time 300
    php_value max_input_time 300
```

php.ini

```bash
    upload_max_filesize = 64M
    post_max_size = 64M
    max_execution_time = 300
```

## wp custom post type

```php
    function create_posttype()
    {
        register_post_type(
            'news',
            // CPT Options
            array(
                'labels' => array(
                    'name' => __('news'),
                    'singular_name' => __('News')
                ),
                'public' => true,
                'has_archive' => false,
                'rewrite' => array('slug' => 'news'),
            )
        );
    }
    // Hooking up our function to theme setup
    add_action('init', 'create_posttype');

    function cw_post_type_news()
    {
        $supports = array(
            'title', // post title
            'thumbnail', // featured images
        );
        $labels = array(
                'name' => _x('news', 'plural'),
                'singular_name' => _x('news', 'singular'),
                'menu_name' => _x('news', 'admin menu'),
                'name_admin_bar' => _x('news', 'admin bar'),
                'add_new' => _x('Add New', 'add new'),
                'add_new_item' => __('Add New news'),
                'new_item' => __('New news'),
                'edit_item' => __('Edit news'),
                'view_item' => __('View news'),
                'all_items' => __('All news'),
                'search_items' => __('Search news'),
                'not_found' => __('No news found.'),
            );
        $args = array(
                'supports' => $supports,
                'labels' => $labels,
                'public' => true,
                'query_var' => true,
                'rewrite' => array('slug' => 'news'),
                'has_archive' => true,
                'hierarchical' => false,
            );
        register_post_type('news', $args);
    }
    add_action('init', 'cw_post_type_news');
```

## get posts from db

one

```php
    $posts = get_posts([
        'category_name' => 'logo',
        'post_status' => 'publish',
        'numberposts' => '1',
        'order' => 'ASC'
    ]);
```

all

```php
    $posts = get_posts([
        'category_name' => 'logo',
        'post_status' => 'publish',
        'numberposts' => '-1',
        'order' => 'ASC'
    ]);
    $i = 0;
    foreach ($posts as $post) {
        $attr = array(
            'class' => 'my-gallery-img glrys glry-img-' . $i,
            'id' => 'main-logo',
            'width' => 'auto',
        );

        if (has_post_thumbnail()) :
            echo get_the_post_thumbnail_url($post->ID, 'full');
            echo get_the_post_thumbnail($post->ID, array(331, 60), $attr);
        endif;
    }
```

## menu and submenu slugs & location key

```bash
    Menu		Submenu		Location key		Slugs
    Dashboard				2		index.php
    –		Home		0		index.php
    –		Updates		10		update-core.php
    Posts				5		edit.php
    –		All Posts		5		edit.php
    –		Add New		10		post-new.php
    –		Categories		15		edit-tags.php?taxonomy=category
    –		Post Tags		16		edit-tags.php?taxonomy=post_tag
    Media				10		upload.php
    –		Library		5		upload.php
    –		 Add New		10		media-new.php
    Links				15		link-manager.php
    –		All Links		5		link-manager.php
    –		Add New		10		link-add.php
    –		 Link Categories		15		edit-tags.php?taxonomy=link_category
    Pages				20		edit.php?post_type=page
    –		All Pages		5		edit.php?post_type=page
    –		 Add New page		10		post-new.php?post_type=page
    Comments				25		edit-comments.php
    Appearance				60		themes.php
    –		Themes		5		themes.php
    –		Menu		10		nav-menus.php
    –		 Widgets		7		Widgets.php
    Plugins				65		plugins.php
    –		Installed Plugins		5		plugins.php
    –		 Add New		10		plugin-install.php
    –		Editor		15		plugin-editor.php
    Users				70		users.php
    –		 Users list		5		users.php
    –		 Add new user		10		user-new.php
    –		 Edit your profile		15		profile.php
    Tools				75		tools.php
    –		All tools		5		tools.php
    –		 Import		10		import.php
    –		 Export		15		export.php
    Settings				80		options-general.php
    –		 General Options		10		options-general.php
    –		 Writing		15		options-writing.php
    –		 Reading		20		options-reading.php
    –		 Discussion		25		options-discussion.php
    –		 Media		30		options-media.php
    –		 Permalinks		40		options-permalink.php
    Seperator				4
    Seperator1				59
    Seperator2				99
```

## remove widgets from Dashboard

```php
    function remove_dashboard_widgets()
    {
        global $wp_meta_boxes;
        unset($wp_meta_boxes['dashboard']['normal']['core']['dashboard_right_now']);
        //Removed recent comments widget
        unset($wp_meta_boxes['dashboard']['normal']['core']['dashboard_activity']);
        //Removed incoming links widget
        unset($wp_meta_boxes['dashboard']['side']['core']['dashboard_quick_press']);
        //Removed Other WordPress News widget
        unset($wp_meta_boxes['dashboard']['side']['core']['dashboard_primary']);
        //Removed WordPress Blog widget
    }
    add_action('wp_dashboard_setup', 'remove_dashboard_widgets');
```

## renaming admin submenu item

```php
    function edit_admin_menu_name() {
        global $menu;
        global $submenu;
        $menu[20][0] = 'My Pages'; // Changing the name of Page
        $submenu['edit.php?post_type=page'][5][0] = 'All My Pages';
        $submenu['post-new.php?post_type=page'][10][0] = 'Add a New Page';
    }
    add_action( 'admin_menu', 'edit_admin_menu_name');
```

## renaming admin menu item

```php
    function custom_admin_menu_name()
    {
        global $menu;
        $menu[20][0] = 'My Pages';
    }
    add_action('admin_menu', 'custom_admin_menu_name');
```

## custom wp login logo

```php
    <?php function modify_admin_logo() { ?>
        <style type="text/css">
            #login h1 a, .login h1 a {
                background-image: url(<?php echo get_stylesheet_directory_uri(); ?>/custom-logo.png);
                height: 84px;
                width: 84px;
                background-size: 84px 84px;
                background-repeat: no-repeat;
                padding-bottom: 30px;
            }
        </style>
    <?php } ?>
    add_action( 'login_enqueue_scripts', 'modify_admin_logo' );
```

## custom links wp admin toolbar

```php
    function modify_admin_toolbar( $admin_bar ) {
    // admin toolbar first level item
    $admin_bar->add_menu( array(
    'id' => 'quick-links',
    'title' => 'Quick Links',
    'href' => '#',
    'meta' => array(
    'title' => __( 'Quick Links'),
    ),
    ) );
    // admin bar second level item
    $admin_bar->add_menu( array(
    'id' => 'quick-link-one',
    'parent' => 'quick-links',
    'title' => 'All Settings',
    'href' => admin_url( 'options.php' ),
    'meta' => array(
    'title' => __( 'All Settings'),
    'class' => 'quick-links-class'
    ),
    ) );
    // admin bar second level item
    $admin_bar->add_menu( array(
    'id' => 'quick-link-two',
    'parent' => 'quick-links',
    'title' => 'All Posts',
    'href' => admin_url( 'edit.php' ),
    'meta' => array(
    'title' => __( 'All Posts' ),
    'class' => 'quick-links-class'
    ),
    ) );
    }
    add_action( 'admin_bar_menu', 'modify_admin_toolbar', 100 );
```

## dynamic copyright date

function

```php
    function wpb_copyright() {
        global $wpdb;
        $copyright_dates = $wpdb->get_results("
        SELECT
        YEAR(min(post_date_gmt)) AS firstdate,
        YEAR(max(post_date_gmt)) AS lastdate
        FROM
        $wpdb->posts
        WHERE
        post_status = 'publish'
        ");
        $output = '';
        if($copyright_dates) {
        $copyright = "© " . $copyright_dates[0]->firstdate;
        if($copyright_dates[0]->firstdate != $copyright_dates[0]->lastdate) {
        $copyright .= '-' . $copyright_dates[0]->lastdate;
        }
        $output = $copyright;
        }
        return $output;
    }
```

call

```php
    <?php echo wpb_copyright(); ?>
```

## add menu button

```php
    add_action('admin_menu', 'custom_menu');
    function custom_menu()
    {
        add_menu_page(
            'Page Title',
            'سالید وب',
            'edit_posts',
            'menu_slug',
            'page_callback_function',
            'dashicons-screenoptions'
        );
    }
    function page_callback_function()
    {
        echo "<h1>Hello World!</h1>";
    }
```

## custom dashboard widgets

```php
    add_action('wp_dashboard_setup', 'my_custom_dashboard_widgets');
    function my_custom_dashboard_widgets()
    {
        global $wp_meta_boxes;
        wp_add_dashboard_widget('custom_help_widget', 'Tehran Note', 'custom_dashboard_help');
    }
    function custom_dashboard_help()
    {
        $my_theme = wp_get_theme();
        echo '<p>نام قالب : ' , esc_html($my_theme->get('Name')) , '</p>';
        echo '<p>توسعه دهنده : ' , esc_html($my_theme->get('Author')) , '</p>';
        echo '<p>نسخه : ' , esc_html($my_theme->get('Version')) , '</p>';
        echo '<p>از اعتماد شما متشکریم</p>';
    }
```

## custom dashboard logo

```php
    function wpb_custom_logo() {
    echo '
        <style type="text/css">
        #wpadminbar #wp-admin-bar-wp-logo > .ab-item .ab-icon:before {
        background-image: url(' . get_bloginfo('stylesheet_directory') . '/images/custom-logo.png) !important;
        background-position: 0 0;
        color:rgba(0, 0, 0, 0);
        }
        #wpadminbar #wp-admin-bar-wp-logo.hover > .ab-item .ab-icon {
        background-position: 0 0;
        }
        </style>
    ';
    }
    //hook into the administrative header output
    add_action('wp_before_admin_bar_render', 'wpb_custom_logo');
```

## custom admin css

```php
    function admin_css()
    {
        echo '<style>
            #wpadminbar {
                    background: #000000 !important;
            }
            </style>
        ';
        wp_enqueue_style('admin_css', get_template_directory_uri() . '/css/admin.css');
    }
    add_action('admin_head', 'admin_css');
```

or

```php
    function admin_css() {
        wp_enqueue_style( 'admin_css', get_template_directory_uri() . '/css/admin.css' );
    }
    add_action('admin_head', 'admin_css' );
    #Here /css/admin.css is the location that contains my admin style sheet. You can change it according to your convenience.
```

## remove menu item

```php
    function wi_remove_menu_pages() {
		remove_menu_page('tools.php');
        remove_menu_page('users.php');
        remove_menu_page('plugins.php');
        remove_menu_page('edit-comments.php');
        remove_menu_page('edit.php');
        remove_menu_page('upload.php');
        remove_menu_page('edit.php?post_type=page');
        remove_submenu_page('edit.php?post_type=page', 'post-new.php?post_type=page');
        remove_submenu_page('users.php', 'user-new.php');
    }
    add_action( 'admin_menu', 'wi_remove_menu_pages' );
```

## notification php composer

https://github.com/jolicode/JoliNotif

```bash
    composer require "jolicode/jolinotif"
```

```php
    include __DIR__ . '/vendor/autoload.php';
    use Joli\JoliNotif\Notification;
    use Joli\JoliNotif\NotifierFactory;
    function notificationCreator($title,$body)
    {
        $notifier = NotifierFactory::create();
        $notification =
            (new Notification())
            ->setTitle($title)
            ->setBody($body)
            ->setIcon(__DIR__ . '/path/to/your/icon.png')
            ->addOption('subtitle', 'This is a subtitle') // Only works on macOS (AppleScriptNotifier)
            ->addOption('sound', 'Frog') // Only works on macOS (AppleScriptNotifier)
        ;
        $notifier->send($notification);
    }
    notificationCreator("salam", "pashmaki");
```

## run query woocommerce

```php
    if (in_array('woocommerce/woocommerce.php', apply_filters('active_plugins', get_option('active_plugins')))) {
        // Put your plugin code here

        // If you want use WooCommerce functions, do that after WooCommerce is loaded
        add_action('woocommerce_loaded', 'my_function_with_wc_functions');
    }
    function my_function_with_wc_functions()
    {
        global $wpdb;
        $results = $wpdb->get_results("SELECT * FROM sf_wc_order_stats WHERE status = 'wc-processing' ");
        print_r($results);
    }
```

## woocommerce active?

```php
    if (in_array('woocommerce/woocommerce.php', apply_filters('active_plugins', get_option('active_plugins')))) {
        // Put your plugin code here

        // If you want use WooCommerce functions, do that after WooCommerce is loaded
        add_action('woocommerce_loaded', 'my_function_with_wc_functions');
    }

    function my_function_with_wc_functions()
    {
        
    }
```

## custom dashboard widget

```php
    function my_dashboard_widget_function()
    {
        //It’s just a simple text but you can use complex code here	
        echo 'This theme is brought to you by <strong><a href = "https://www.wordpressintegration.com/"> WordPressIntegration</a></strong>, the best PSD to WordPress conversion service on the internet.';
    }
    function adding_my_dashboard_widgets()
    {
        wp_add_dashboard_widget('wp_dashboard_widget', 'Made By WordPressIntegration', 'my_dashboard_widget_function');
    }
    add_action('wp_dashboard_setup', 'adding_my_dashboard_widgets');
```

## custom menu item name

```php
    function custom_admin_menu_name()
    {
        global $menu;
        $menu[20][0] = 'My Pages';
        print_r($menu);
    }
    add_action('admin_menu', 'custom_admin_menu_name');
    function edit_admin_menu_name()
    {
        global $menu;
        global $submenu;
        $menu[20][0] = 'My Pages'; // Changing the name of Page
        $submenu['edit.php?post_type=page'][5][0] = 'All My Pages';
        $submenu['post-new.php?post_type=page'][10][0] = 'Add a New Page';
    }
    add_action('admin_menu', 'edit_admin_menu_name');
```

## notificaton js

https://javascript.plainenglish.io/show-desktop-notifications-with-javascript-d554a28f0b87

```php
    function adminotif()
    {
        echo '<script>
    console.log(Notification.permission);
    if (Notification.permission === "granted") {
        console.log("we have permission");
    } else if (Notification.permission !== "denied") {
        Notification.requestPermission().then(permission => {
            console.log(permission);
        });
    }

    function showNotification() {
    const notification = new Notification("New message incoming", {
        body: "Hi there. How are you doing?",
        icon: "http://cdn.sstatic.net/stackexchange/img/logos/so/so-icon.png"

    })
    notification.onclick = (e) => {
        window.location.href = "https://google.com";
    };
    }

    showNotification()
    </script>';
    }
    add_action('admin_head', 'adminotif');
```

## custom admin footer

```php
    function custom_footer_admin()
    {
        echo 'Made by WordPressIntegration. If you are facing any problem with the theme, feel free to Contact Us';
    }
    add_filter('admin_footer_text', 'custom_footer_admin');
```

## is admin?

```php
    if (!is_admin()) {
        echo "You are viewing the theme";
    } else {
        echo "You are viewing the WordPress Administration Panels";
    }
```
