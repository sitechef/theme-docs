# ScreenHeight

Fixes an element to a percentage of the
screen height.

Useful for a horizontal strip which must always
be 30% of the screen height.


## Usage

HTML:

    <div class="my-element">
    </div>


SCSS:

    .my-element {
      width: 100%;
      position: relative;
    }


JS:

    var ScreenHeight = require('../lib/ScreenHeight.coffee');

    var screenHeight = new ScreenHeight(
      $('.my-element'), // the target element
      { // any overrides for the options
        height: 0.3, // set height to 30% of screen height
        mobile: false // disable on mobile
      }
    );


## Options

The ScreenHeight library can be customised to
to set min and max height, disable on desktop/mobile
and customise cutoffs for mobile and desktop:


    /**
     * Instantiate with options as second parameter
     */
    var screenHeight = new ScreenHeight(
      $('.my-element'),
      {
        // float - percentage of screen height
        height: 0.5,

        // height will not go below this height (pixels)
        minHeight: 150, // or false for no min

        // upper limit - height will not exceed this (pixels)
        maxHeight: 600, // or false for no max

        // apply to desktop
        desktop: true,

        // min width in pixels that marks when
        // a window is classed as 'desktop'
        desktopMinWidth: 641,

        // apply to mobile browsers
        mobile: true,

        // max width in pixels for screens classed
        // as 'mobile'
        mobileMaxWidth: 640
      }
    );
