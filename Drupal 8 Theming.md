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
- And `Administration //Configuration // Development`. Clear all caches

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
... Copy `gulpfile.js` and `package.json` to `sites/d8theming`
- Copy `themes/custom/endymion`
