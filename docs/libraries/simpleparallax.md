#SimpleParallax

Adds a parallax affect to an element or a collection of elements

Uses `window.requestAnimationFrame` and sets the transform
`translateY` to try and maximise smoothness


#Usage

HTML:

    <div class="parent-element">
      <div class="child-element"></div>
    </div>

SCSS:

    .parent-element {
      overflow: hidden;
      position: relative;
      height: 300px;
    }
    // ensure that the child element is slightly
    // larger than the parent
    .child-element {
      height: 400px;
      // optionally set it at an offset so that it
      // appears centered in the initial state
      top: -50px;
      position: absolute;
      left: 0;
    }

JS:

    var SimpleParallax = require('../lib/SimpleParallax.coffee');
    var sP = new SimpleParallax(
      $('.child-element'), // jquery element or a collection of elements
      {
        ratio: 0.5, // moves at half the speed of the scroll
        maxTransform: 50, // will move no more than 50px down
        minTransform: -50, // will move no more than 50px up
        unit: 'px' // | '%' transform will move in pixels or percentage
      }
    );

