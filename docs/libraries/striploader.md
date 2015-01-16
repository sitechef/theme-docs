#Strip Loader

*For use in websites where the content for each
of the subpages of the landing page is loaded
in horizontal "strips".*

This is to be used on the landing page.
It dynamically loads and templates the content
for each of the first level children of the landing page.

Strips are loaded dynamically so that the SEO benefits
of having separate URLs for each subsection of the website
are not compromised

##Usage

Create a holder div on the landing page template:

HTML:

    <div id="new-strips"></div>


Require and instantiate the Strip Loader library
with the array of menu "children" (see [Menu Struct](../datastructure.md#menu-struct))

Ensure that 'nunjucks-slim.min.js' is included both in the html
and in the `dist/js` folder

Javascript:

    var StripLoader = require('../lib/StripLoader.coffee');
    var myLoader = new StripLoader(
      menuChildren, // menu children is from menu struct above
      { // options - see below
        loadedCallback: function($row){
         // '$row' is the strip that has just been loaded
        }
      }
    );

Result:

####1. While Loading

The "new-strips" div will be populated with

    <div class="strip-holder loading"><div class="icon icon-spin"></div></div>

for each page to be loaded

####2. When Loaded

The full templated page will replace the above "holder"



