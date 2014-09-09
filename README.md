yolo-cyril
==========

Haring Center Header image work;

Here is the code I am using for my Twenty Twelve child theme. The slider seems to work but it's jumpy/jerky and seems to be running into the main nav. I can try fixing the CSS on the Soliloquy plugin but wanted to see if this it what I should be doing. The code that you supplied generated "a syntax error on line 108" when I removed the following code:

</a>
			<?php endif; // end check for removed header image ?>

It seemed to work okay but very jumpy. 

I'm still working on adding in header images on the other pages but wanted to check this first.

Thanks,
Carol

<?php
/**
 * The Header for our theme.
 *
 * Displays all of the <head> section and everything up till <div id="main">
 *
 * @package WordPress
 * @subpackage Twenty_Twelve
 * @since Twenty Twelve 1.0
 */
?><!DOCTYPE html>
<!--[if IE 7]>
<html class="ie ie7" <?php language_attributes(); ?>>
<![endif]-->
<!--[if IE 8]>
<html class="ie ie8" <?php language_attributes(); ?>>
<![endif]-->
<!--[if !(IE 7) | !(IE 8)  ]><!-->
<html <?php language_attributes(); ?>>
<!--<![endif]-->
<head>
<meta charset="<?php bloginfo( 'charset' ); ?>" />
<meta name="viewport" content="width=device-width" />
<title><?php wp_title( '|', true, 'right' ); ?></title>
<link rel="profile" href="http://gmpg.org/xfn/11" />
<link rel="pingback" href="<?php bloginfo( 'pingback_url' ); ?>" />

<!-- Begin Stylesheets -->
<link rel="stylesheet" type="text/css" media="all" href="<?php bloginfo( 'stylesheet_url' ); ?>" />
<!-- End Stylesheets -->

<!-- link to the CSS files for this menu type -->
<link rel="stylesheet" media="screen" href="http://www.haring.caroltompkinsdesign.com/wp-content/themes/Haring_child2014new/css/superfish.css">


<!-- link to the JavaScript files (hoverIntent is optional) -->
<!-- if you use hoverIntent, use the updated r7 version (see FAQ) -->
<script src="http://www.haring.caroltompkinsdesign.com/wp-content/themes/HaringChild2014new/js/hoverIntent.js"></script>
<script src="http://www.haring.caroltompkinsdesign.com/wp-content/themes/HaringChild2014new/js/superfish.js"></script>

<!-- Fonts Here -->
<?php // Loads HTML5 JavaScript file to add support for HTML5 elements in older IE versions. ?>
<!--[if lt IE 9]>
<script src="<?php echo get_template_directory_uri(); ?>/js/html5.js" type="text/javascript"></script>
<![endif]-->
<?php wp_head(); ?>
<!-- GOOGLE ANALYTICS Here -->
</head>

<body <?php body_class(); ?>>
<div id="page" class="hfeed site">
	<header id="masthead" class="site-header" role="banner">
		<!-- #masthead-inner added to make container with relative position -->
		<div id="masthead-inner">
			<!-- #utility menu added to create secondary menu in header -->
			<nav id="utility-menu">
				<?php wp_nav_menu( array( 'theme_location' => 'utility-menu', 'container_class' => 'utility-menu' ) ); ?>
			</nav><!-- end #utility-menu -->
		     <!-- #site-group replaced deprecated hgroup; spans replace h1 and h2 headers in site elements -->
			<div id="site-group">
<!-- Begin LOGO  -->
<div id="logo">
<h1>
<a href="http://www.haring.caroltompkinsdesign.com"><img src="http://www.haring.caroltompkinsdesign.com/wp-content/themes/Haring_child2014new/images/logo.png" alt="logo for Haring Center" title="Haring Center" width="326" height="111" class="alignleft1 size-full" /></a></h1>

</div>
				<span class="site-title"><a href="<?php echo esc_url( home_url( '/' ) ); ?>" title="<?php echo esc_attr( get_bloginfo( 'name', 'display' ) ); ?>" rel="home"><?php bloginfo( 'name' ); ?></a></span>
				<span class="site-description"><?php bloginfo( 'description' ); ?></span>
			</div><!-- end #site-group -->
 			
			<nav id="site-navigation" class="main-navigation" role="navigation">
				<h3 class="menu-toggle"><?php _e( 'Menu', 'twentytwelve' ); ?></h3>
				<a class="assistive-text" href="#content" title="<?php esc_attr_e( 'Skip to content', 'twentytwelve' ); ?>"><?php _e( 'Skip to content', 'twentytwelve' ); ?></a>
				<?php /*?><?php wp_nav_menu( array( 'theme_location' => 'primary', 'menu_class' => 'nav-menu' ) ); ?><?php */?>

<!-- Superfish -->
<?php
// Adding a menu to the theme, registered in functions.php
// see http://codex.wordpress.org/Function_Reference/wp_nav_menu
wp_nav_menu( array( 'theme_location' => 'my_main_menu', 'menu_class' => 'sf-menu' ) );
?>
<!-- End of Superfish -->
			</nav><!-- end #site-navigation -->
<!-- header image moved BELOW navigation -->
<?php
					// Added Conditional to Hook In Slider On Home Page Else Display Featured Image As Header if Correct Size
				if ( is_front_page() && function_exists( 'soliloquy_slider' ) ) soliloquy_slider( '258' );
					else if ( is_singular() && has_post_thumbnail( $post->ID ) &&
							( /* $src, $width, $height */ $image = wp_get_attachment_image_src( get_post_thumbnail_id( $post->ID ), array( $header_image_width, $header_image_width ) ) ) &&
							$image[1] >= $header_image_width ) :
						// Houston, we have a new header image!
						echo get_the_post_thumbnail( $post->ID, 'post-thumbnail' );
					else :
						// Compatibility with versions of WordPress prior to 3.4.
						if ( function_exists( 'get_custom_header' ) ) {
							$header_image_width  = get_custom_header()->width;
							$header_image_height = get_custom_header()->height;
						} else {
							$header_image_width  = HEADER_IMAGE_WIDTH;
							$header_image_height = HEADER_IMAGE_HEIGHT;
						}
						?>
					<img src="<?php header_image(); ?>" width="<?php echo $header_image_width; ?>" height="<?php echo $header_image_height; ?>" alt="" />
				<?php endif; // end check for featured image or standard header ?>
			
			
			<?php $header_image = get_header_image();
			if ( ! empty( $header_image ) ) : ?>
				<a href="<?php echo esc_url( home_url( '/' ) ); ?>"><img src="<?php echo esc_url( $header_image ); ?>" class="header-image" width="<?php echo get_custom_header()->width; ?>" height="<?php echo get_custom_header()->height; ?>" alt="" /></a>
			<?php endif; ?>	<!-- end header image -->
	    </div><!-- end #masthead-inner -->
	</header><!-- #masthead header-->

	<div id="main" class="wrapper">
