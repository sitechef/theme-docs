#CarouselGallery

Generates a carousel gallery which rotates
through a series of images/video
at a given speed

Additionally uses [JQuery Clever Crop](clevercrop.md) to
position images to cover background

Waits for any HTML5 videos to end before moving onto
the next item in the carousel

*Library functions by adding and removing a class `current`
from a series of children of an element*


##Usage

HTML:

        <div class="carousel-container">
          <div class="item-1 background-image loading">
            <img src="" data-content-type="image" class="bg-image">
          </div>
          <div class="item-2 background-image loading">
            <img src="" data-content-type="html5" class="bg-image">
            <!-- video logic -->
          </div>
          <div class="item-3 background-image loading">
            <img src="" data-content-type="image" class="bg-image">
          </div>
        </div>

SCSS:

    .carousel-container {
        width: 100%;
        overflow: hidden;
        height: 400px;
        position: relative;
    }

    .background-image {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        // default z-index is 0
        z-index: 0;
        // add transition for fade time
        // n.b. this include requires Bourbon
        @include transition(opacity 1s);
        // default opacity is 0
        opacity: 0;
        // when current class is applied
        // change to opaque
        &.current {
          opacity: 1;
        }
        // optionally hide it while image loading
        &.loading {
          opacity: 0;
        }
    }


JS:

       var CarouselGallery = require('../lib/CarouselGallery.coffee');

       $(document).ready(function(){
         var carouselGallery = new CarouselGallery(
           $('.carousel-container'), // parent element of gallery
           { // list of options (see below for full list)
             interval: 6000, // 6s delay in between rotation
          }
         );
       });


##Advanced Options

The CarouselGallery library can
be configured by passing any of the
following options as the second argument
on instantiation


    var options = {

      /*
       * @var {Integer} -
       *   number of ms to pause between images
       */
      interval: 5000,

      /*
       * @var {String} - class of images to apply clever crop to
       */
      imageClass: '.bg-image',

      /*
       * @var {String} - class of each background container
       */
      containerClass: '.background-image',

      /*
       * @var {Boolean} Apply clever crop to images (zoom to cover)
       */
      cleverCrop: true,

      /*
       * @var {Object} clever crop overrides
       */
      cleverCropOptions: {},

      /*
       * @var {Object} Settings for Screen Height
       */
      screenHeight: {

        /*
         * @var {Boolean} Fix height of
         *         carousel to percentage of screen
         */
        apply: true,

        /*
         * @var {Float} 0-1 percentage of screen height
         */
        height: 0.6
      },

      /*
       * @var {Boolean} - auto-play html5 video on mobile devices
       */
      videoOnMobile: false,


      /*
       * @var {Function} -
       *     @param {JQueryElement} Current item
       *     @param {Integer} 0-based index for active item
       */
      currentCallback: function($item, index) {}
    };

