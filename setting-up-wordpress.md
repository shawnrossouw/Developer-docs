### Setting Up Wordpress


#### Create new project folder.

CD into project folder with terminal

Clone wordpress boilerplate repo from github

Make sure docker is not running

Inside working folder and when boilerplate is cloned run the following command
```bash
docker-compose up -d
```

Open browser and navigate to localhost 8000 where docker.yml points to and set up wordpress with the wordpress installer.

Log into wp-admin

Activate theme

Set up custom post types.

Copy ACF and Migrate DB pro plugins to the project plugin folders.

Create "inc" folder and sub folders custom-post-types and theme setup (already set up in new WP boilerplate)

require “filepath/ggg.php”; - to pull in partials inside functions.php
require_once “filepath/fff.php”;

### CUSTOM POST TYPE

A post type you create. Built in post types is pages, posts and comments etc. 

Register post type.
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
#### Custom post type Query posts
```php
<?php $query = new WP_Query(array(
        'post_type' => 'mag_client',
        'posts_per_page' => 6,
        'paged' => (get_query_var('paged')) ? get_query_var('paged') : 1
      )); ?>
```
Then loop through post types;
```php
<?php if ($query->have_posts()): ?>
<?php while ($query->have_posts()): $query->the_post(); ?>
        
<?php endwhile; ?>        
<?php else: ?>
   <p>There are no posts available</p>
<?php endif; ?>
```
Edit the name with what post type you need.
Place the above code in a function and give it a name like ‘setup’

#### Set up hooks in wordpress

Best time to set up hooks is after the theme has been setup
To add a hook, run the function
```php
 add_action('init','setup');
 ```
First string is to you initialize the hook, second is what you want to hook
The above register post type has been placed in a ‘setup’ function


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

```php 
-Archive-name_type.php
``` 
(blog listing page, in wordpress sense more than one page, not old page)
```php 
-Single-name_type.php 
```
(single version of blog listing page)

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

To get permalink
```html
<a href="<?php the_permalink(); ?>" class="">
```
To get post thumbnail
```php
<?php echo get_the_post_thumbnail(); ?>
```
#### ACF

NB - Rules
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
