# Wordpress ACF Plugin Snippets

## load posts details


```php
    <?php
    while (have_posts()) : the_post();
    ?>

    // START HTML CODES
    <img src="<?php bloginfo('template_url'); ?>/assets/logod.png" alt="PAIR Finance" />
    <ul class="breadcrumb">
        <li><a href="<?php echo get_site_url(null, $path, $scheme); ?>"> &#11164 خانه</a></li>
        <li><a href="<?php echo get_site_url(null, $path, $scheme); ?>/estate"> &#11164 جستوجو</a></li>
    </ul>

    <?php echo get_home_url(); ?>
    <?php bloginfo('template_url'); ?>
    <?php the_field('room'); ?>
    <?php the_content(); ?>
    <?php echo $post->post_title ?>

    <?php if( get_field('img1') ): ?>
    <div class="carousel-item active">
        <img src="<?php the_field('img1'); ?>" alt="First slide">
    </div>
    <?php endif; ?>


    <a href="<?php echo get_home_url(); ?>/contact/">ارتباط با ما</a>
    <script type="text/javascript" src="<?php bloginfo('template_url'); ?>/assets/main.min.js" id="pf_script-js"></script>
```

## load posts

```php
    <?php
    //BEFORE START LOOP
    $postPerPageVar = 1;
    if (isset($_GET["province"]) && isset($_GET["type"])) {
        if ($_GET["province"] == 'all' && $_GET["type"] == 'all') {
            $posts = get_posts(array(
                'posts_per_page'    => $postPerPageVar,
                'post_type'         => 'estate',
                'paged' => get_query_var('paged') ? get_query_var('paged') : 1,
            ));
        } else if (($_GET["province"] == 'all') && !($_GET["type"] == 'all')) {
            $posts = get_posts(array(
                'posts_per_page'    => $postPerPageVar,
                'post_type'         => 'estate',
                'paged' => get_query_var('paged') ? get_query_var('paged') : 1,
                'meta_key'      => 'type',
                'meta_value'    => $_GET["type"]
            ));
        } else if (!($_GET["province"] == 'all') && ($_GET["type"] == 'all')) {
            $posts = get_posts(array(
                'posts_per_page'    => $postPerPageVar,
                'post_type'         => 'estate',
                'paged' => get_query_var('paged') ? get_query_var('paged') : 1,
                'meta_key'      => 'province',
                'meta_value'    => $_GET["province"]
            ));
        } else {
            $posts = get_posts(array(
                'posts_per_page'    => $postPerPageVar,
                'post_type'         => 'estate',
                'paged' => get_query_var('paged') ? get_query_var('paged') : 1,
                'meta_query'    => array(
                    'relation'      => 'AND',
                    array(
                        'key'       => 'province',
                        'value'     => $_GET["province"],
                        'compare'   => '='
                    ),
                    array(
                        'key'       => 'type',
                        'value'     => $_GET["type"],
                        'compare'   => '='
                    )
                )
            ));
        }
    } else {
        $posts = get_posts(array(
            'posts_per_page'    => $postPerPageVar,
            'post_type'         => 'estate',
            'paged' => get_query_var('paged') ? get_query_var('paged') : 1,
        ));
    }

    foreach ($posts as $post) {
    ?>


        //MAIN LOOP START


        <?php the_field('img1'); ?>
        <?php echo $post->guid ?>
        <?php the_field('year'); ?>
        <?php echo $post->post_title ?>


        //MAIN LOOP end


    <?php }; ?>

    <?php if ((sizeof($posts) + 1 > $postPerPageVar)) { ?>

        //PAGINATION START
        
        <div id="paginationDiv">
            <button class="nav-previous alignleft paginationbtn">
                <?php next_posts_link('قبلی'); ?>
            </button>
            <button class="nav-next alignright paginationbtn">
                <?php previous_posts_link('بعدی'); ?>
            </button>
        </div>
    <?php
    } else {
    ?>

        <img src="<?php bloginfo('template_url'); ?>/assets/notfound.svg" alt="" />
        <span>موردی پیدا نشد</span>

    <?php } ?>




















    // HTML FILTERS
    <form method="get" action="#post-210">
    <button class="btnset" style="color:#fff;">جستجو</button>
    <select name="province" id="provinceSel">
        <option value="all" selected>All</option>
        <option value="denia1">Denia1</option>
        <option value="denia2">Denia2</option>
        <option value="denia3">Denia3</option>
    </select>
    </form>


















    // JS READ GET REQUEST
    if((window.location.href.indexOf("province") > -1) && (window.location.href.indexOf("type") > -1)) {
        //in search
        
        const questionMark = window.location.href.split("?");
        const hashtagMark = questionMark[1].split("#");
        const andCharacter = hashtagMark[0].split("&");
        andCharacter.forEach(function (param){
            let paramArr = param.split("=")
            if (paramArr[0] == 'type'){
                document.getElementById("typeSel").value = paramArr[1];
            }else if(paramArr[0] == 'province'){
                document.getElementById("provinceSel").value = paramArr[1];
            }else{
                
            }
        });
    }else{
        //out search
        
    }
```

