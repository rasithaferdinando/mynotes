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

- Drupal’s core templates are in /core/modules/system/templates
- The content for the clean templates at this moment displayed from page.html.twig
- Twig - templating language drupal uses
- To edit this content, copy this file and paste it in endymion folder

#### Disable cache and enable twig debugging
- copy `sites/example.settings.local.php` to `default` folder and rename it to `settings.local.php`. This is the local developing settings. These will be turned off once the site goes live
- To disable the cache uncomment the following line
`$settings['cache']['bins']['render'] = 'cache.backend.null';`
-
