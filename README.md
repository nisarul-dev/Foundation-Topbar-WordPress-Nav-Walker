# Foundation Topbar WordPress Nav Walker
An WordPress Navwalker object that displays Foundation CSS framework's Topbar Nav Menu

[Foundation-Topbar-WordPress-Nav-Walker](https://github.com/nisarul-media/Foundation-Topbar-WordPress-Nav-Walker)

## Get a Foundation Topbar Like this:
![Foundation Top Bar Screenshot](https://user-images.githubusercontent.com/65971192/158076929-e963bc8c-ae8d-4ef9-8f7f-1b8553da76fa.jpg)


## To use:

`Step-0:` It is an optional step if you didn't setup Foundation Framework in your theme yet. Enqueue necessary CSS and JS files to get Foundation Framework up and running.
#### functions.php
```php
add_action( 'wp_enqueue_scripts', function() {
    // CSS
    wp_enqueue_style( 'foundation-style', get_stylesheet_directory_uri() . '/css/foundation.min.css', array(), '6.7.4', 'all' );

    // JS
    wp_enqueue_script( 'jq', get_stylesheet_directory_uri() . '/js/vendor/jquery.js', array( ), '3.6.0', true );
    wp_enqueue_script( 'what-input', get_stylesheet_directory_uri() . '/js/vendor/what-input.js', array( 'jq' ), '5.2.10', true );
    wp_enqueue_script( 'foundation-script', get_stylesheet_directory_uri() . '/js/vendor/foundation.min.js', array( 'jq', 'what-input' ), '6.7.4', true );
    wp_enqueue_script( 'my-script', get_stylesheet_directory_uri() . '/js/app.js', array( 'jq', 'what-input', 'foundation-script' ), '1.0.0', true );
} );
```
<br>

`Setp-1:` Copy and paste the [Foundation_Top_Bar_Nav_Walker](https://github.com/nisarul-media/Foundation-Topbar-WordPress-Nav-Walker/blob/main/functions.php) class into the functions.php file of your theme.
<br><br>

`Setp-2:` Register a new menu by adding the follow code into the functions.php file of your theme.
#### functions.php
```php
add_action( 'after_setup_theme', function () {
    register_nav_menu( 'main-menu', 'Header Navigation Menu' );
} );
```
<br>

`Setp-3:` Add the following html code in your header.php file or wherever you want to place your menu.
#### header.php
```html
...
<header>
    <div class="title-bar" data-responsive-toggle="responsive-menu" data-hide-for="medium">
        <button class="menu-icon" type="button" data-toggle="responsive-menu"></button>
        <div class="title-bar-title menu"><a href="<?php echo esc_url( home_url( '/' ) ); ?>" class="menu-text" rel="home"><?php bloginfo( 'name' ); ?></a></div>
    </div>

    <div class="top-bar" id="responsive-menu">
        <div class="menu hide-for-small-only">
            <a href="<?php echo esc_url( home_url( '/' ) ); ?>" class="menu-text" rel="home"><?php bloginfo( 'name' ); ?></a>
        </div>

        <div class="top-bar-left">
            <?php wp_nav_menu([
                'theme-location' => 'main-menu',
                'container'      => false,
                'menu_class'     => 'menu',
                'items_wrap'     => '<ul id="%1$s" class="dropdown %2$s"  data-dropdown-menu>%3$s</ul>',
                'walker'         => new Foundation_Top_Bar_Nav_Walker(),
            ]); ?>
        </div>

        <div class="top-bar-right">
            <form action="<?php echo esc_url( home_url( '/' ) ); ?>" method="GET">
                <ul class="menu">
                    <li><input type="search" placeholder="Search" value="<?php echo get_search_query(); ?>" name="s"></li>
                    <li><button type="submit" class="button">Search</button></li>
                </ul>
            </form>
        </div>
    </div>
</header>
...
```
<br>
