#ImageRotator

Rotates the class `current` over a series of child divs
at a given interval.

*Useful for creating image carousels*

If an element contains an image with the `data-content-type="html5"` tag
it will ignore the interval and wait for the 'videoEnded' event on the image


#Usage
Requires to have images nested inside divs and
to work with video, data-content-type must be set:

eg:

HTML:

    <div class="carousel-container">
      <div class="item-1 item">
        <img src="" data-content-type="image">
      </div>
      <div class="item-2 item">
        <img src="" data-content-type="html5">
        <!-- video logic -->
      </div>
      <div class="item-3 item">
        <img src="" data-content-type="image">
      </div>
    </div>

JS:

    var ImageRotator = require('./ImageRotator.coffee');
    var imageRotator = new ImageRotator({
      // target element
      item: $('.carousel-container .item'),
      // class to mark if element visible
      currentClass: 'my-current-class',
      // wait between change (ms)
      interval: 3000,
      /**
       * callback called when an item is set to 'current'
       * function is called with jQuery selector of element
       */
      callback: function($item){
      }
    });

