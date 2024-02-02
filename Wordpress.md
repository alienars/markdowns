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

```php
    $posts = get_posts([
    'category_name' => 'logo',
    'post_status' => 'publish',
    'numberposts' => '1',
    'order' => 'ASC'
    ]);
```

```html
    <a id="wabtn" href="" class="btn-whatsapp-pulse">
    <i class="fab fa-whatsapp"></i>
    <div class="wc_whatsapp_secondary"><p>Need Help?</p></div>  
    </a>
```
```css
    .btn-whatsapp-pulse-border {
	bottom: 120px;
	right: 20px;
	animation-play-state: paused;
    }
```