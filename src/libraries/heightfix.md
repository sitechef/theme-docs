# Height Fix

For creating responsive elements where the height
scales proportionately to screen width.

*Useful for creating squares that fit screen width perfectly*

## Usage

Given the following html:

    <style>
      .box-row{
        position: relative;
        overflow: auto;
        width: 100%;
      }
      .box-row .box {
        width: 25%;
        float: left
        border: 0;
      }
    </style>
    <div class="box-row" >
      <div class="box-1 box" ></div>
      <div class="box-2 box" ></div>
      <div class="box-3 box" ></div>
      <div class="box-4 box" ></div>
    </div>

`HeightFix` can be used to ensure that the boxes
stay square as the screen resizes:

     var HeightFix = require('../lib/HeightFix.coffee'),
         heightFix = new HeightFix(
           $('.box-row .box'),
           {
             multiple: 4 // number of horizontal items
           }
         );


## Options

Following options are available

    var heightFix = new HeightFix(
      $('.my-element'),
      {
        // number of items
        // to fit in a width
        multiple: 4,

        // number of pixels to offset
        // from screen width
        offset: 0,

        // Refrence width
        // usually the window
        referenceWidth: $(window),

        // callback on resized
        resized: function($selector, height){
        }
      }
    );


