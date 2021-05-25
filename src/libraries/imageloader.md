# Image Loader

Notifies when images have loaded

Additionally performs lazy-loading so images
are not loaded until section of screen visible
and removes loading spinners

## Usage


To lazy load the image:
1. Set the src to a transparent image
2. Set the image url in the `data-src` tag
3. Add the `lazyLoad` class
4. Optionally refer to a spinner to remove when loaded
  by class in the `data-spinner` attribute

HTML:

     <div class="container loading">
       <img class="my-images lazyLoaded" src="blank.png" data-src="http://cdn.com/my-real-image.png" data-spinner=".my-spinner">
       <div class="my-spinner"></div>
     </div>

JS:

     var ImageLoader = require('./ImageLoader.coffee'),
         loader = new ImageLoader({
           selector: $('.my-images'),
           callback: function($myLoadedImage){
             // my image has loaded
             // so remove loading class from parent
             $myLoadedImage.parents('.loading')
             .removeClass('loading');
           }
         });

## Options


    var loader = new ImageLoader({
      /*
       * {string} class name of images loaded lazily
       */
      lazyClass: 'lazyLoaded',

      /*
       * {integer} timeout in ms to wait for loading
       */
      maxWait: 7000,

      /*
       * {integer} number of pixels below viewport
       *           when considered in view
       */
      inViewOffset: 200,

      /*
       * {JQuery Element} jQ selector for image(s)
       */
      selector: false,

      /*
       * {JQuery Element} jQ selector for container where scroll
       * changes are observed
       */
      scrollSelector: $(window),

      /*
       * {Function} callback when image is in view
       */
      inView: function($image) {},

      /*
       * {Function} callback when image has loaded
       */
      callback: function($img) {
        return $img.parents('.loading').removeClass('loading');
      }
    });
