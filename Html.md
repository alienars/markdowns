# HTML Snippets

## Simple Template

HTML

```html
    <!doctype html>
    <html lang="en">
    <head>
        <title>Title</title>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <meta name="apple-mobile-web-app-title" content="Name">
        <meta name="application-name" content="Name">
        <meta name="msapplication-TileColor" content="#dfdfdf">
        <meta name="theme-color" content="#dfdfdf">
        <meta name="keywords" content="keywords1,keywords2" />
        <meta name="description" content="description text" />
        <meta name="language" content="en" />
        <meta name="robots" content="index follow">
        <meta name="title" content="title">
        <link rel="manifest" href="./site.webmanifest">
        <link rel="canonical" href="canonicalLink" />
        <link rel="apple-touch-icon" sizes="180x180" href="./apple-touch-icon.png">
        <link rel="icon" type="image/png" sizes="32x32" href="./favicon-32x32.png">
        <link rel="icon" type="image/png" sizes="16x16" href="./favicon-16x16.png">
        <link rel="mask-icon" href="./safari-pinned-tab.svg" color="#dfdfdf">

        <link href="./full.css" rel="stylesheet" type="text/css">
    </head>
    <body>
        <div id="root"></div>
        
        <script src="./full.js"></script>
    </body>
    </html>
```

site.webmanifest

```json
    {
        "name": "-name-",
        "short_name": "-shortname-",
        "icons": [
            {
                "src": "/android-chrome-192x192.png",
                "sizes": "192x192",
                "type": "image/png"
            },
            {
                "src": "/android-chrome-384x384.png",
                "sizes": "384x384",
                "type": "image/png"
            }
        ],
        "theme_color": "#ffffff",
        "background_color": "#ffffff",
        "start_url": "-main url-",
        "display": "standalone"
    }
```