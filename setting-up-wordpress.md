### Setting Up Wordpress

### Step 1.
Login at https://login.konsoleh.co.za
Username: lastpass 
PW: lastpass

### Step 2:
Click on green ‘new order’ button
Step 3 
Click on web hosting
Click on basic package
South Africa
Next

### Step 4
Create a sub domain
Give domain name
(avula.dev.magneticcreative) needs to be this extension
Next

### Step 5
If price is 0 - Everything is all good
Accept Ts and Cs
Place Order

### Step 6
Click SSH in the left panel
Look for the domain name and click on it
Continue
(wait for domain to propegate)
Enable

### Step 7 - Add FTP user to the domain
Hetzner Dashboard
Manage Servers - drop down
Click on the server
Select the domain name that was created (avula.dev.mag)
Click on manage services in the left pane
FTP users
Reset password to - 12Magnetic34
Update

### Step 8
Copy username

### Step 9
Open terminal
Type in “ ‘ssh’ username@domain_url”
(ssh avulazkhli@avula2019.dev.mag.co.za)
Enter
Yes
Enter
Type password: 12Magnetic34

### Step 10 - inside the box (username has changed)
Cd public_html
Enter
Ls
Rm -rf index.html
It is now empty

### Step 11 - IF THERE IS A REPO ONLINE
Open Bitbucket
Check if there is an SSH KEY active in terminal - cat ~/.ssh/id_rsa.pub
Enter
If no such file, generate ssh key using ssh-keygen -t rsa -C “emailaddress@example.com”
Enter till its done
Run the cat command again--  cat ~/.ssh/id_rsa.pub
Copy SSH KEY

### Step 12
If you are not the admin of that repo, send your SSH key to the admin of that repo

### Step 13
TO DOWNLOAD A FRESH COPY OF WORDPRESS TO TARGET DOMAIN
In the public_html folder - run the following commands
`
curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
`
`
php wp-cli.phar core download
`

### Step 14 - Database
From KonsoleH dashboard
Go to the domain
Manage my sql on left pane
Add
Add
Keep wordpress database details open
In new tab, go to the actual domain that you created
Install Wordpress with database details
Switch between konsoleh and wordpress installation to check details
Database -> Database Name
Login -> Username
Full Password -> Password
Server -> Database Host
Keep prefix
Submit
Create title,username,password
Install

### Step 15 - Get the theme on new wordpress (to deploy a site) skip this step for later
From public_html - run command:  cd wp-content/themes
Ls
Git clone “project-repo-url” magnetic
Cd magnetic
Ls
Remove all except theme folder --- rm -rf folder/ folder/ folder/ file file file (everything you want to remove seperated by a space)
Move contents of theme to current directory ---  mv theme/* .

### IF YOU HAVE TO FTP FILES (NOT CONVENTIONAL METHOD)
Continue after step 10…
Use FTP client (filezilla or cyberduck)
In cyberduck..
Click connect to server icon (earth plus icon)
Select FTP from dropdown (default)
Copy domain username from hetzner - (vallezheaq)
Paste into cyberduck username field
Do the same with the domain password
In the server field - enter the domain you have created (no prefixes)
Connect
Continue
Enter public html
NB -Make sure the folder you are FTPing is zipped.
Make sure to compress the root files - Go into the folder and zip the files within - not the folder
Drag the newly created zip file into the public html folder in cyberduck

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
        'post_type' => 'mag_car',
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
