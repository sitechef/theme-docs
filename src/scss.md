SiteChef uses [SASS](http://www.sass-lang.com) to generate CSS.
SCSS files are currently compiled using version `3.1.2` of node-sass


#Writing SCSS/SASS

See the [SASS website](http://www.sass-lang.com/guide) for a full SASS guide.

There are two variants of SASS: `scss` which is not indented and follows the
conventions of css more closely and `sass` which is indented, but arguably
faster to write

#Important Variables

In order to link your production assets (images, fonts, etc)
with your production stylesheet it is important that you use our inbuilt
variables when specifying asset paths

###1. `imageUrl(<your-image.png>)`

If you want to refer to any images in your `dist/img/` folder in your SCSS files
use the SASS shorthand function `imageUrl()` and inside the path of the image
relative to the `dist/img/` folder.

eg.

    .container {
      background: imageUrl(mybackground.png) top center no-repeat;
    }

when in production will render to

    .container {
      background:
      url(https://sitechefthemes.s3.amazonaws.com/themes/xx-xx/dist/img/mybackground.png)
      top center no-repeat;
    }

###2. `$assetsRoot`

This is a string of the absolute root of your `dist/` folder when in production.

If you are linking images, please use the above `imageUrl()` function in
preference.

The most common use-case would be for linking fonts in the `dist/font/` directory

eg.

    @font-face {
      font-family: "Bespoke Font";
      src: url($assetsRoot + "fonts/BespokeFont.eot");
      font-weight: normal;
      font-style: normal;
    }

will render in production to

    @font-face {
      font-family: "Bespoke Font";
      src: url("https://sitechefthemes.s3.amazonaws.com/themes/xx-xx/dist/fonts/BespokeFont.eot");
      font-weight: normal;
      font-style: normal;
    }


#Compilation

CSS Stylesheets are generated from the SCSS files in the `scss/` directory.

SiteChef creates SASS variables for each of the design options that the user has
selected at https://admin.sitechef.co.uk/wizard/theme/customise

The CSS file included on the user's website is generated from two files:

1. [defaults.scss](#defaultsscss)
2. [theme.scss](#themescss)

The user's overrides for colours, fonts and options are injected as SASS
variables in between (1.) and (2.).

See the [documentation about the
theme.json](configfiles/themejson.md#variables) for instructions for setting the
variables users can alter in the online theme editor.

##defaults.scss

This file should contain any variables that users might overwrite in the online
theme editor.

For example, if in your `theme.json` file you have defined the colour
`bodyFont`:

      {
        "meta":{
          "name":"My Demo Theme"
        },
        "variables":{
          "colours":[
            {
              "id":"bodyFont",
              "name":"Body Font Colour"
            }
          ]
        }

      }

You might set it to be `blue` as a default. If the user selects an alternative
colour, `$bodyFont` will be overwritten.

Your `defaults.scss` would include:

    $bodyFont: blue;

##theme.scss

The theme.scss is the main entry point for your theme.
In order to keep your scss file structure simple, we recommend that you keep
this file small and include other SCSS files for each section of the website.

For example:

    // My Demo theme: theme.scss


    @import 'foundation'; // import the foundation framework

    // set some styles for the html tag
    html {
      margin: 0;
      height: 100%;
    }

    // import all of the subsections

    @import 'navigation'; // this assumes you have another file
    //  'navigation.scss' in the same folder

    @import 'headers'; // styles for the header tags


#Included Libraries

SiteChef bundles three external libraries which should not be added to the
`scss/` folder. They can all be accessed by the `@import` statement:

##Bourbon

[Bourbon](http://bourbon.io/docs/) is a SASS mixin library that simplifies
repitious css generation like vendor-prefixing

The current Bourbon version used by SiteChef is `4.1.0`

eg.

    @import 'bourbon';
    p {
      @include box-sizing(border-box);
    }

will generate the following css

    p {
      -webkit-box-sizing: border-box;
      -ms-box-sizing: border-box;
      -moz-box-sizing: border-box;
      box-sizing: border-box;
    }

##Foundation

[Foundation](http://foundation.zurb.com/docs/) is a frontend css framework that
simplifies the creation of responsive websites that work across multiple screen
dimensions.

SiteChef only bundles the SCSS for Foundation so if you plan to use their
frontend javascript functionality, make sure to add their scripts to the
`dist/js/` folder in your theme.

The current version of Foundation used by SiteChef is `5.5.2`

To import foundation:

    @import 'foundation';
    // override any of the default foundation
    // settings
    $button-font-family: 'Verdana';

##Bootstrap

[Bootstrap](http://getbootstrap.com/getting-started/) is aguably the most
popular frontend css framework. Like [Foundation](#foundation), it also speeds
up the development process when creating responsive websites and saves time when
styling form elements and alerts.

Like Foundation, SiteChef does not automatically bundle Bootstrap's frontend
javascipt files, so remember to save them to the `dist/js` folder before
publishing your theme.

The current version of Bootstrap Sass used by SiteChef is `3.3.3`

To import bootstrap:

    @import 'bootstrap';


