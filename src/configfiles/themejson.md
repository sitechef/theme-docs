# The "theme.json" file

The `theme.json` contains the general settings for your theme.

It is a JSON formatted file with the two keys: `meta` and `variables`

##"meta"

`meta` describes the theme for SiteChef users and uses the following keys:

#### name
<div class="indented">

The Main title for the theme. *This was set when you cloned the theme*

</div>
#### description
<div class="indented">

A short description about your theme. *This was set when you cloned the theme*

</div>
#### screenshot
<div class="indented">

The filename of an image in the `dist/img/` folder to be shown
to SiteChef users on the admin section e.g. `myscreenshot.png`

</div>

##"variables"

`variables` is an object containing the options that a SiteChef user will be permitted
to edit using the Theme Editor at https://admin.sitechef.co.uk/.
These variables are dynamically injected into your SCSS files and made
available in your `theme.scss` file. See [Stylesheets](../scss.md) for a more detailed explanation.

It is broken down into three arrays: `variables`, `fonts` and `colours`.

#### variables
<div class="indented">
Creates a dropdown in the theme customisation section.

It is an array of objects with the following keys: `id`, `name`, `options`

    {
        "id":"myOptionId", // the id to be used in SCSS: $myOptionId
        "name":"My Option Title", // a description that the customer sees
        "options":{ // a key:value hash of options
            "stringAssigned":"Description in drop-down"
            "anotherString":"Option 2"
        }
    }

In the above example, the SiteChef user will be presented
with a dropdown under the heading of "My Option Title"
with two options "Description in drop-down" and "Option 2"
If the user selects "Option 2", the following SCSS
will be injected:

    $myOptionId:'anotherString';


</div>
#### colours
<div class="indented">

Creates a colour selector in the theme customisation section

<img style="display:block" src="img/colour_selection.png">

It is an array of objects with the keys: `id`, `name`

eg:

    {
      "id":"scssIdForColour",
      "name":"Title For Customer"
    }

Once a user has selected the colour `# 009922`, the following will be injected into
the scss file:

    $scssIdForColour: # 009922;

</div>
#### fonts
<div class="indented">

Creates a font dropdown in the theme customisation section

<img style="display:block" src="img/font_selection.png">

Array of objects with keys : `id`, `name`

eg:

    {
      "id":"titleFont", # id for scss mixin
      "name":"Title" # title that customer sees sees
    }

If the user selects the font "arial", "bold", 90%, uppercase,
font-spacing 2px
the scss will be injected with the following mixin:

    @mixin titleFont($size){
      font:{
        family: 'arial';
        style: normal;
        weight: bold;
        size: ($size * 0.9);
      }
      text-transform: uppercase;
      letter-spacing: 2px;
    }


</div>
