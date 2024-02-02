## increase upload size wp

.htaccess

```bash
    php_value upload_max_filesize 64M
    php_value post_max_size 64M
    php_value max_execution_time 300
    php_value max_input_time 300
```

php.ini

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

## wp custom post type

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

