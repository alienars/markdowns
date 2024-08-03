## add custom color schema


```js
    color-palette-1 = [
        '#31466e : mainBG', 
        '#ece6f6 : text&icons', 
        '#3C5788 : hovers', 
        '#F79009 : badges', 
        '#98b3e3 : links'
    ]
    color-palette-2 = [
        '#31466e : mainBG', 
        '#ece6f6 : text&icons', 
        '#3C5788 : hovers', 
        '#F79009 : badges', 
        '#f3a238 : links'
    ]
```
(change all these colors in "admin-color-scheme.css" file)

```php
    function additional_admin_color_schemes()
    {
        wp_admin_css_color(
            'CustomName',
            __('CustomName'),
            plugin_dir_url(__FILE__) . 'admin-color-scheme.css',
            ['#31466e', '#ece6f6', '#3C5788', '#F79009']
        );
    }
    add_action('admin_init', 'additional_admin_color_schemes');
```

## set custom admin color schema after activating plugin

```php
    function set_color_scheme()
    {
        $scheme = 'CustomName';
        $args = array(
            'meta_key' => 'admin_color',
            'meta_value' => 'fresh'
        );

        $users = get_users($args);
        foreach ($users as $user) {
            update_user_meta($user->ID, 'admin_color', $scheme);
        }
    }
    register_activation_hook(__FILE__, 'set_color_scheme');
```

## get posts with custom type and get all custom meta

```php
    $args = array(
        'post_type' => 'products',
        'posts_per_page' => 6
    );
    $query = new WP_Query($args);
    if ($query->have_posts()) {
        while ($query->have_posts()) {
        $query->the_post();

        $meta_title = get_post_meta(get_the_ID(), 'product-title', true);
        $post_link = get_permalink();
```

```html
<a href="<?php echo esc_html($post_link) ?>"><?php echo esc_html($meta_title) ?></a>
```

```php
        }
    } else {
        echo 'Products Not Found';
    }
```
# Plugin JetEngine

## load "options pages" values on theme

add this code to "functions.php" in template files

```php
    function echo_je_option($pageName, $optionName) {
        $key = $pageName . '::' . $optionName;
        $option_value = jet_engine()->listings->data->get_option($key);

        if (empty($option_value)) {
            echo '<div style="opacity:0.3;">';
            echo '<strong>(' . $pageName . ') is empty</strong> ';
            echo '</div>';
        } else {
            echo $option_value;
        }
        // return $option_value;
    }
```

use this code on top of all pages with "options value" for load data simpler

```php
    function echoOptF($optionName)
    {
        $pageName = 'main-page';
        echo_je_option($pageName, $optionName);
    }
```

after you can use this code to load your custom option value

```php
    echoOptF("main-logo");
```

```html
    <img src="<?php echoOptF("main-logo"); ?>">
```

