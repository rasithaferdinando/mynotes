# Drupal 8 Theming
http://watch-learn.com/series/drupal-8-theming  
https://www.youtube.com/watch?v=a9u0B1F650U  

## Drupal 8 Theming - Part 01 - Theme Setup

#### Creating a clean theme
- root/themes/custom/<theme_name> i.e. endymion  
- In Drupal 6 or 7 theming, only need to have a .info file.  
- In 8 .info file is a yaml file  
- Create endymion.info.yml file inside the theme folder and enter this:  
```
name: Endymion
description: Drupal 8 Starter Theme
type: theme
core: 8.x
```
This creates an empty theme which you can activate and use from admin panel

#### Remove unwanted css (if they show up in the source view)
`Administration >> Configuration >> Performance`
- Uncheck Aggregate CSS files & Aggregate JavaScript files. Click `Save Configuration`
- Click button Clear all caches
- Reload the site and view source. A list of css files will display. Since some might be required by admin controls, logout and reload. The remaining list of css are the ones that we can remove without breaking admin functions.
- Add the following to endymion.info.yml
```
stylesheets-remove:
    - core/themes/.../<file.name>.css
```
- And `Administration // Configuration // Development`. Clear all caches

#### Add CSS and JavaScript files
- Create `/endymion/endymion.libraries.yml`. This is where to define CSS and JS
- For  css:
```
global-css:
    css:
        theme:
            css/styles.css: {}
```
- For  JS:
```
global-js:
    js:
        js/main.js: {}
    Dependencies: -> define dependencies here. I.e. jquery
        - core/jquery
```
- Include `global-css` and `global-js` in the info file under libraries. i.e.:
```
libraries:
    - endymion/global-css
    - endymion/global-js
```
- CSS file will in the head and the javascript file will be at the bottom of the page

## Drupal 8 Theming - Part 02 - Disable Cache, Enable Twig Debug

- Drupal’s core templates are in `/core/modules/system/templates`
- The content for the clean templates at this moment displayed from page.html.twig
- Twig - templating language drupal uses
- To edit this content, copy this file and paste it inside endymion folder

#### Disable cache and enable twig debugging
- *Have a local local developing settings config*: copy `sites/example.settings.local.php` to `sites/default/` folder and rename it to `settings.local.php`. This will be turned off once the site goes live.
- *Disable the cache*: uncomment the following line in `settings.local.php`
`$settings['cache']['bins']['render'] = 'cache.backend.null';`
But nothing will happen as we need to go to `settings.php` and uncomment the following lines which takes the `settings.local.php` into consideration.
```
if (file_exists($app_root . '/' . $site_path . '/settings.local.php')) {
  include $app_root . '/' . $site_path . '/settings.local.php';
}
```
- In `default.services.yml`, there are settings to disable cache, enable auto_reload and debug to true. But they won't work unless you rename the file to `services.yml`. But because we're setting up a local dev environment, a better way is to copy these settings to `development.services.yml` file as follows:
```
parameters:
    twig.config:
        debug: true
        auto_reload: true
        cache: false
```

### Drupal 8 Theming - Part 03 - Gulp.js, Sass, LiveReload

- Download the `Olympos theme` zip file to `sites/d8theming/Assets/`
- From under `olympos-master` folder:  
    - Copy `gulpfile.js` and `package.json` to the root
    - Copy `images`, `js`, `lib` and `sass` to `themes/custom/endymion`
- Delete `themes/custom/endymion/js/olympos.min.js` -> because we don't need this as we're calling `js/main.js`
- Go to `themes/custom/endymion/sass/` and remove heading comments as it is required only by Wordpress.
- Now to setup gulpfile.js. All we have to do is rename paths. Rename `/wp-content/themes/olympos` to `/themes/custom/endymion`
- For sass task, save it to css directory by defining destination as:
`.pipe(gulp.dest('./themes/custom/endymion/css'));`
- For JavsScript, uglify as:
`.pipe(uglify('main.js'))`
- Update the watch function to watch:  
```
gulp.watch(['./themes/custom/endymion/css/style.css',  
'./themes/custom/endymion/**/*.twig',  
'./themes/custom/endymion/js/*.js'], ...  
```
- Install all the modules required by gulpfile.js. `npm install`
- Run `gulp watch`
- For sass update reload didn't work


## Drupal 8 Theming - Part 04 - Blocks and Regions

- Blocks are in Regions
- `Structure // Block Layout` and click `Demonstrate block regions (Endymion)` to show
- We're going to define our own regions. In `themes/custom/endymion/endymion.info.yml` add:
```
regions:
    content: 'Main Content'
    header: 'Header'
    footer: 'Footer'
    sidebar: 'Sidebar'
```
- Now in `page.html.twig` define regions on our page and remove the ones you dont'
```
```
## Drupal 8 Theming - Part 05 - Let's Update Drupal 8
- skipping this because we're using the latest version

## Drupal 8 Theming - Part 06 - Theming the Header

#### Define our home page
- What is being output from `page.html.twig` can be seen in twig debug comments:
```
<!-- BEGIN OUTPUT from 'themes/custom/endymion/page.html.twig' -->
HERE'S THE OUTPUT
<!-- END OUTPUT from 'themes/custom/endymion/page.html.twig' -->
```
- As suggested in twig debug output, we're renaming `page.html.twig` to `page--front.html.twig`
- Clear cache and reload. The comments will say have the new page.
- Next the header of that front page. Two ways - 1. The drupal way and 2. the other way (replacing {{ page.header }} with the html without using a separate header file). We're proceeding with the drupal way.
- If you inspect the header, the html comments will say:  
`<!-- BEGIN OUTPUT from 'core/themes/stable/templates/block/block--system-branding-block.html.twig' -->`
- Which means its in `Structure // Blocks // Header // Site Branding`
- Configure to make changes (i.e. hide logo etc.)
- What we want to do is to overwrite this file `block--system-branding-block.html.twig`.
- Eg - We want the logo image link to be different
- Copy `templates` folder which contains all including `block--system-branding-block.html.twig` to `endymion` so we can customize any template.
- Clear cache and refresh. The templates will be read by new location now.
