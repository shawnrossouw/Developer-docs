### PLUGIN INSTALL

https://github.com/wp-premium/advanced-custom-fields-pro

Extract plugin and copy the folder to the project plugin folder.
Create inc folder and sub folders custom-post-types and theme setup

require “filepath/ggg.php”; - to pull in partials inside functions.php
require_once “filepath/fff.php”;

### CUSTOM POST TYPE

A post type you create. Built in post types is pages, posts and comments etc. 

#### Register post type.

```php
register_post_type( 'mag_car',
  array(
    'labels' => array(
      'name' => __( 'Cars' ),
      'singular_name' => __( 'Car' ),
      'menu_name' => 'Cars',
      'edit_item' => 'Edit Car',
      'view_item' => 'View Car',
      'add_new' => 'Add Car',
      'add_new_item' => 'Add New Car'
    ),
    'public' => true,
    'has_archive' => true,
    'supports' => array('title', 'editor', 'thumbnail'),
    'rewrite'=> array( 'slug' => 'cars' )
  )
);
```

#### Register taxonomy

```php
register_taxonomy(
  'car_make',
  'mag_car',
  array(
    'labels' => array(
      'name' => __( 'Makes' ),
      'add_new_item' => __('Add new Make')
    ),
    'rewrite' => array( 'slug' => 'car-make' ),
    'hierarchical' => true
  )
);
```

Inside theme folder

-Archive-name_type.php (blog listing page, in wordpress sense more than one page, not old page)
-Single-name_type.php (single version of blog listing page)

Register Archive page
Create post type in theme setup/functions.php
Set Header and footer in archive.php
Deploy to live site
Make sure post type is in wordpress menu
Refresh permalinks by saving it again

To display taxonomy name on front end using “terms”

```php
<?php
$terms = get_the_terms(get_the_ID(), 'car_make');
foreach($terms as $term):?>
<span>
<? echo $term ->name ?>
</span>
<?php endforeach; ?>
```

Or

```php
<?php foreach(get_terms(array(‘taxonomy’ => ‘project_type’))as $term): ?>
<?php echo &term =>name; ?>
```

To get permalink
```php
<a href="<?php the_permalink(); ?>" class="">
```

To get post thumbnail
```php
<?php echo get_the_post_thumbnail(); ?>
```

### ACF

#### NB - Rules
Post type is equal to the custom post type name. 
On the front end
```php
<?php the_field(‘field name’); ?>
```
Repeater fields: holds multiple values;
```php
<?php foreach(get_field('colors') as $color): ?>
<span style="background: <?php echo $color['color'] ?>"></span>
 <?php endforeach; ?>
 ```
Repeater fields on a options page:
```php
<?php if( have_rows('repeater', 'option') ): ?>
    <ul>
    <?php while( have_rows('repeater', 'option') ): the_row(); ?>
        <li><?php the_sub_field('title'); ?></li>
    <?php endwhile; ?>
    </ul>
<?php endif; ?>
```

### Hooks

NB!! Good time to initiate hooks is after theme-setup inside a function. Ex post types

To create post type that doesn’t live inside the theme folder. 
In wp-content folder create mu-plugins. Create new file post-type.php
Inside the file create function like below: 

```php
<?php
function setup(){
   register_post_type( 'events',
   array(
     'labels' => array(
       'name' => __( 'Events' ),
       'singular_name' => __( 'Event' ),
       'menu_name' => 'Events',
       'edit_item' => 'Edit Event',
       'view_item' => 'View Event',
       'add_new' => 'Add Event',
       'add_new_item' => 'Add New Event'
     ),
     'public' => true,
     'has_archive' => true,
     'supports' => array('title', 'editor', 'thumbnail'),
     'rewrite'=> array( 'slug' => 'cars' )
   )
 );
}

add_action('init','setup');
```

To Activate Advanced Custom Fields
Copy ACF from other previous projects and paste it into the plugins folder of current project.
Go to wordpress backend and activate the plugin
Click on updates
Copy the activation key from google drive and paste it into input
Activate plugin

Options-page = global settings/content
Global options page via ACF

```php
acf_add_options_page(array(
 'page_title'=>'Site Settings',
 'menu_title'=>'General',
));
```

Example pulling acf field from backend with field in options page
```php
<h1><?php the_field('field_name', 'option'); ?></h1>
```
### SEARCH PAGE RESULTS
```html
<main class="posts">
 <div class="posts-inner">
```
```php
<?php if(have_posts()): ?>
 <?php while(have_posts()): the_post(); ?>
       <!--POST BLOCK-->
       <a href="<?php the_permalink(); ?>" class="post">
         <div class="post-img">
    <?php responsive_img(get_the_ID(), 'full'); ?>
           <div class="post-category <?php echo get_the_category()[0]->slug; ?>">
     <?php echo get_the_category()[0]->cat_name; ?>
           </div>
           <!--INSERT POST CATEGORY HOOK-->
         </div>
         <div class="post-title">
    <?php the_title(); ?>
         </div>
         <div class="post-date">
    <?php echo get_the_date(); ?>
         </div>
       </a>
       <!--END POST BLOCK-->

 <?php endwhile; ?>
<?php else: ?>
     <p>There are currently no posts.</p>
<?php endif; ?>
 </div>
</main>
```

### Responsive Images
```php
<?php responsive_img(get_post_thumbnail_id(), 'large'); ?>
```

### Displaying a custom parent and child(sub category) taxonomy of a custom post type:
```php
foreach( get_terms( 'products-category', array( 'hide_empty' => false, 'parent' => 0 ) ) as $parent_term ) {
  // display top level term name
  echo $parent_term->name . '<br>';
  foreach( get_terms( 'products-category', array( 'hide_empty' => false, 'parent' => $parent_term->term_id ) ) as $child_term ) {
    // display name of all childs of the parent term
    echo $child_term->name . '<br>';
  }
}
```

### WHEN DEPLOYING TO A LIVE SITE…

Do not send the plugins to the new site with migrate DB pro.. Only send the database and the media files. Make sure the live site already has the same plugins in the backend.

Refresh the permalinks after it has been deployed





