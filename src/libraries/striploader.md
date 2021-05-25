# Strip Loader

*For use in websites where the content for each
of the subpages of the landing page is loaded
in horizontal "strips".*

This is to be used on the landing page.
It dynamically loads and templates the content
for each of the first level children of the landing page.

Strips are loaded dynamically so that the SEO benefits
of having separate URLs for each subsection of the website
are not compromised

## Requirements

For the StripLoader to work it requires the following libraries:

- JQuery 1.9+
- [Lodash](http://lodash.com/)/[Underscore](http://underscorejs.org)
- Nunjucks Slim ([dev](http://mozilla.github.io/nunjucks/files/nunjucks-slim.js)/[prod](http://mozilla.github.io/nunjucks/files/nunjucks-slim.min.js))
- All Nunjucks templates used in redering strips ***must be pre-rendered*** and included in the html. (See [Frontend Templating](../assetpipeline.md# frontend-templates) for explanation)


## Usage

Create a holder div on the landing page template:

HTML:

    <div id="new-strips"></div>


Require and instantiate the Strip Loader library
with the array of menu "children" (see [Menu Struct](../datastructure.md# menu-struct))

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

#### 1. While Loading

The "new-strips" div will be populated with

    <div class="strip-holder loading"><div class="icon icon-spin"></div></div>

for each page to be loaded

#### 2. When Loaded

The full templated page will replace the above "holder"


## Options

The striploader can be started with the following options:

    var myLoader = new StripLoader(
      menuChildren, // array of data - menu struct
      {
        /**
         * Callback function called when
         * a strip has been templated and loaded
         * into the DOM.
         * @param {Object} JQuery element for the row
         */
        loadedCallback: function($strip){
        },
        /**
         * The css selector for the container
         * of the strips
         */
        appendLocation: '# my-strip-container',
        /**
         * The endpoint for the ajax request
         * for the category (must end with trailing /)
         */
        endpoint: 'api/category/',
        /**
         * Callback when all rows have been loaded
         */
        allLoadedCallback: function(){},
        /**
         * Callback called when error in AJAX fetch
         */
        errorCallback: function(err){},
        /**
         * raw html used as the "strip" placeholder
         * while the data is being loaded and templated
         */
        holderHtml: '<div class="strip-holder loading"></div>',
        /**
         * the path of the template to be
         * used for the pageStrip
         * N.B. this template *MUST* be pre-rendered
         * and included for frontend-rendering
         */
        template: 'pageStrip.html',
        /**
         * Site Root URL
         */
        siteRoot: '/',
        /**
         * By default ajax loads are throttled
         * to this value in ms
         */
        templateDelay: 100 // 100ms
      }
    );

