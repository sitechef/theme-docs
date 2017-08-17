#JQuery CleverCrop

Positions images so that they appear cropped according
to a focus point selected by the SiteChef user.

CleverCrop uses a user-selected "focus" point to
set the position of an element within a parent element
which has overflow: `hidden`


##Usage

Assuming that you have used the `imageBuild` [macro](../templating.md#rendering-images)
to render the image html

###1. Add the script src tag

Ensure that the file `jquery.cleverCrop.js` or
`jquery.cleverCrop.min.js` is in your `dist/js` folder
and that jQuery is included before

Add this tag to your scripts section:

    <script type="text/javascript" src='{{ assetsRoot }}js/jquery.cleverCrop.min.js'></script>

###2. Execute the function on a jQuery element

Example rendered HTML:

    <!-- parent div must have overflow set to
    'hidden' and position to 'absolute' or 'relative' -->
    <div class="parent" >
        <img src='myImage.jpeg' data-focus='{x:0.2,y:0.8}' data-ratio="0.6" class="my-image">
    </div>

Javascript:

    $('.my-image').cleverCrop()

##Options

The plugin takes a number of optional overrides


    $('.element').cleverCrop({

     parent: $('.another-parent'), // override for parent

     onResize: true, // {Boolean} bind to resize

     focus: {x:0.4,y:0.6}, //override focus

     crop: true, // crop image or fit

     refresh: function(){} // callback on done
    });

