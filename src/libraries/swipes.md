# Swipes

Provides Swiping/Panning and translate interactions
on top of [Hammer.js](http://hammerjs.github.io/)

*Most useful in galleries where you want an image to
follow your touch*

***N.B. Requires Hammer.js included in the html.***

***Hammer.js IS NOT IE8 compatible so only include it within an an [IE Conditional tag](http://www.quirksmode.org/css/condcom.html)***

## Usage

HTML:

    <div class="my-element">
        <div class="my-move-element"></div>
    </div>

JS:

    var Swipes = require('../lib/Swipes.coffee');
    var swipes = new Swipes({
        // element that touch is bound to
        target: $('.my-element'),
        // element that will be translated
        moveElement: $('.my-move-element'),
        // only listen in the horizontal direction
        direction: 'horizontal',
        // function to be executed on swipe
        leftCallback: function(velocity){
            console.log('Swiped left!');
        }
    });

## Options


Use the following options to tailor the swipe
response

    var options = {
      /*
       * Selector for the element
       * to bind the touch interactions to
       * @var {String|JQueryElement}
       */
      target: ".overlay-item",

      /*
       * Selector to translate on move
       * @var {String|JQueryElement}
       */
      moveElement: ".overlay-item",

      /*
       * Minimum move after which translate action
       * should be recognised
       * @var {Integer} pixels
       */
      minMove: 20,

      /*
       * @var {Boolean} should the 'moveElement' be translated
       */
      moveTranslate: true,

      /*
       * @var {Boolean} fade the 'moveElement' out as it is translated
       */
      moveOpacity: false,

      /*
       * @var {Integer} after this number of pixels, relevant callback is called
       */
      moveLimit: 130,

      /*
       * @var {Float} translate by touch-change * this amount
       */
      moveMultiplier: 1.2,

      /*
       * @var {String} 'both'|'vertical'|'horizontal' respond to directions
       */
      direction: 'both',

      /*
       * @var {Boolean} dont automatically bind
       */
      dontBind: false,

      /*
       * @var {Boolean} lock drag to axis
       */
      lockToAxis: true,

      /*
       * @var {Integer} debounce the callbacks by this in ms
       */
      debounceTime: 750,

      /*
       * @var {Function} on swipe/drag right callback
       */
      rightCallback: function(pixelSpeed) {},

      /*
       * @var {Function} on swipe/drag left callback
       */
      leftCallback: function(pixelSpeed) {},

      /*
       * @var {Function} on swipe/drag up callback
       */
      upCallback: function(pixelSpeed) {},

      /*
       * @var {Function} on swipe/drag down callback
       */
      downCallback: function(pixelSpeed) {}
    };

    var swipes = new Swipes(options);




