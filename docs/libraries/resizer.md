#Resizer

The resizer dynamically resizes
any items to fit within a parent container

By default this container is the window.

*This is especially useful for dynamically resizing
images for full-screen galleries*

##Basic Usage

Require the resizer library and instantiate it.

*If the HTML attribute `data-ratio` exists, it will use this ratio
(item height / item width) to calculate the resized dimensions*


HTML:

    <div class="image-container" style="width:500px,height:400px">
      <img class="child-image" data-ratio="1.4">
    </div>

Javascript:

    // import the resizer library (using browserify)
    var Resizer = require('../lib/Resizer.coffee');

    // instantiate with options
    var imageResize = new Resizer($('.child-image'),
      {
        sizeReference: $('.image-container')
      }
    );

##Options


    var myResizer = new Resizer($('.item-to-be-resized'),
      {
        // the element that constrains our resize target
        sizeReference: $(window),

        // number of pixels to offset
        // resize target from 'sizeReference' dimensions
        padding:{
          top: 0 // usually pixels
          left: 10
          bottom: function(){
            // but can be a function returning integer
            return 40;
          },
          right: 0
        },

        // alignment within
        // container
        align:{
          // should alignment be applied
          apply: true,

          // vertical alignment:
          // top|middle|bottom
          vertical: 'middle',

          // horizontal alignment:
          // left|center|right
          horizontal: 'right'
        },

        // resize after window `onResize` event
        bindToResize: true,

        // number of ms to debounce after window resize
        debounce: 200,

        // callback called after resize of target
        resizedCallback: function(dimensions, $element){
          // dimensions = {
          // width: {Integer} width of element
          // height: {Integer} height of element
          // top: {Integer} margin-top offset from container
          // left: {Integer} margin-top offset from container
          //}
        },

        // ensure width/height dont fall
        // below these minimums
        min: {
          width: 400, // integer value or false
          height: 100 // integer value or false
        },

        // ensure width/height dont go
        // above these maximums
        max: {
          width: 4000, // integer value or false
          height: 1000 // integer value or false
        },

      }
    );

