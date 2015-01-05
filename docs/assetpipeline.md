#Generating Production Assets

By default, most SiteChef themes come with a ready-made
[Gulp](http://gulpjs.com/) asset pipeline which is automatically
compiled on `sitechef serve`. Assets are also recompiled on filechange
using either [Gulp-Watch](https://github.com/floatdrop/gulp-watch) or
using [Jump-Up](https://github.com/campbellwmorgan/jump-up), a watcher and
desktop notifier.

***N.B. if you have not recently executed `sitechef serve`, remember to run
`gulp` before `sitechef publish` to ensure that your assets are compiled***

#Configuration

The configuration for which assets are compiled is contained in `gulpfile.js`
and imports different scripts from the `gulpTasks/` directory.


##Javascript

To keep frontend code reusable and modular, default themes on SiteChef come
setup with a [Browserify](http://browserify.org/) pipeline.

Individual modules are compiled into a single javascript file which is written
to `dist/js/app.js`. It is then minimified using
[Uglify.js](https://github.com/mishoo/UglifyJS) and written to
`dist/js/app.min.js`.

The default entry point for compilation is `js/app.js`

The compilation process can be altered in `gulpTasks/gulp-js.js`

###Browserify

With Browserify one can import a module into a script with the CommonJS syntax:

    var myModule = require('./myModule.js');

It is also possible to include NPM modules using the Node.js require syntax,
although they must first be installed with `npm install`

    var async = require('./async.js');

In order to be able to use a function in another module, you must set the
`module.exports` variable:

    // in myFunction.js
    module.exports = function(){
      // do something clever
    }

This can now be used in `app.js` like follows:


    // app.js
    var myFunction = require('./myFunction.js');

    myFunction();



##Coffeescript

Most [SiteChef modules](libraries/index.md) are written in
[Coffeescript](http://coffeescript.org/) and are
usually extensible using coffeescript `class` - `extends` syntax.

Coffeescript files are compiled like the javascript files above: first compiled
with Browserify, then minified with UglifyJS

The default entrypoint is `coffee/app.coffee' and files are compiled to
`dist/js/app.js` and `dist/js/app.min.js` respectively.

***N.B. If you use coffeescript be sure to comment out the `js` gulp task in
`gulpfile.js` otherwise your `app.js` may be overwritten***


##SCSS

SASS/SCSS is only compiled for the purposes of previewing your theme locally using
`sitechef serve`. The production stylesheets are compiled on the SiteChef
servers on a per-customer basis. [Read More about SCSS compilation
here](scss.md)

The temporary SCSS files are compiled to the `tmp/` and are *not* uploaded to
the server on `sitechef publish`.

The configuration file for compiling SCSS is by default `gulpTasks/gulp-sass.js`

This should not require modification.

##Frontend Templates

Backend html templates can be used on the frontend by compiling them to
javascript.

They are compiled to javascript by Nunjucks in order to render faster and so
that only the `nunjucks-slim.js` is required instead of the larger `nunjucks.js`

Every template that you wish to use on the frontend must be included in the
array in `gulpTasks/gulp-template.js`

The Gulp task will then render each template to javascript, concatenate them
into `dist/js/template.js` then minimify to `dist/js/template.min.js`

Edit the array `frontendTemplates` in the `gulpTasks/gulp-template.js` file :

    // list any templates
    // used on the frontend here
    // NB ensure that you add all
    // templates included by otherh templates
    var frontendTemplates = [
        'pageStrip.html',
        'staticPageStrip.html',
        'galleryStrip.html',
        'headerMacro.html',
        'overlayImage.html',
        'overlayImageItem.html',
        'galleryThumbnailItem.html',
        'thumbGalleryStrip.html',
        'blogStrip.html',
        'defaults/imageBuilder.html',
        'defaults/html5video.html',
        'defaults/shareLinks.html'
      ];

