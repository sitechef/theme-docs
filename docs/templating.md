SiteChef uses [Nunjucks](http://mozilla.github.io/nunjucks/) with some minor
[modifications](#templating-differences).

Nunjucks is a javascript templating language heavily inspired by Python's
[Jinja2](http://jinja.pocoo.org/docs/dev/)

#Basics

The templates are compiled using `index.html` as the starting point.
An effort has been made to keep the subsections as modular as possible.
This is a very basic overview of the templating language.
A more thorough description can be found [here](http://mozilla.github.io/nunjucks/templating.html),
but *please be aware of the following [exceptions](#templating-differences)*

Variables and any content you wish to output into the text are encircled by
double curly braces `{{ variable }}`

Logic and any expressions are enclosed by a single curly brace and the
percentage sign: `{% if something %}{% endif %}`

###Template Data Structure

See [here](datastructure.md) for a complete list of the data available to you

#Templating Language

##Variables

Variables are written inside double curly braces: `{{ variable }}`

Children of items are specified in a notation similar to javascript.
For example, with the object `var myItems = { item1: 'My Item', 'item2:'Second Item'};`
`item2` can be referred to as `{{ myItems.item2 }}`


For example the code:

        <h1 class="restaurant-name">{{ preferences.restaurantName }}</h1>

would render the following HTML if the variables preferences.restaurantName is 'My Restaurant':

        <h1 class="restaurant-name">My Restaurant</h1>

##SiteChef Variables

SiteChef includes a number of variables specified in the [data structure](datastructure.md) list that are important when referring to frontend assets.

The most important is `assetsRoot` which contains the absolute path of the `dist/` directory.

For example to include your minified `app.min.js` script, you would write thef following html:

    <script type="text/javascript" src='{{ assetsRoot }}js/app.min.js'></script>

Unless you are referring to a library available on a public CDN like [CDNJS](https://cdnjs.com), use the `assetsRoot` variable to ensure that they are accessible both in development locally and in production.

##Including Other Templates

There are two principal ways of including other template files in your templates: `include` and `extends`

###1. Include

HTML from other templates can be included as a block using the `include` syntax.

For example, if you have a template for the main website navigation and you call it `navigation.html`,
you can include it in your main `index.html` like this:

    <div class="container">
        {% include 'navigation.html' %}
    </div>

###2. Extends

Extend allows you to use another page as a starting point, then selectively modify elements
of the page. Each element you would like to override is delimited by "blocks" eg:

    {% block menu %}
        <ul class="my-meny">
        </ul>
    {% endblock %}

And so, your base page (`base.html`) might look like this:

    <div class="container">
        {% block myTitle %}
            <h1>My Main Title</h1>
        {% endblock %}
    </div>

And you would like your  `about.html` template to be the
same as the `base.html` except with a different title.
Your `about.html` page would look like this:

    {% extends 'base.html %}
    {% block myTitle %}
        <h2>My Different Title</h2>
    {% endblock %}

##Rendering Images

Rendering images attractively across platforms can be tricky.
SiteChef has developed a number of [frontend libraries](libraries/index.md)
which simplify this process by resizing images before they have loaded
and managing html5 video content or videos from Vimeo or Youtube.

To ensure these libraries work seamlessly, use the "imageBuilder.html" macro
to generate the html for any full resolution images (ie not thumbnails)

1. First import the macro: `{% from 'defaults/imageBuilder.html' import imageBuild %}`
2. Iterate through your images calling the image builder:


        {# this is an example from blog post template #}
        {% for post in content.blogPosts %}
            <div class="blog-post">
                <h1>{{ post.title }}</h1>
                {# check if there is a featured image #}
                {% if post.featuredImage %}
                    {# There is, so use imageBuild to create the image #}
                    {{ imageBuild(post.featuredImage, 'post-image', false, true) }}
                {% endif %}
            </div>
        {% endfor %}


The imageBuild macro takes the following parameters:

* *ImageData*: {Object} data object for the image
* *ImageClass*: {String} a class to apply to the image
* *ShowMobileVersion*: {Boolean} display the mobile version of the image
* *LazyLoad*: {Boolean} write the src of the image to data-src instead to enable lazy-loading


##Filters

Filters modify variables and follow a `|` and the variable: `{{ variable | filter }}`

For example, where `customerName = 'Andrew Smith'`

    <div class="customer-name">{{ customerName | upper }}</div>

would render to

    <div class="customer-name">ANDREW SMITH</div>

N.B. the filters available with SiteChef is **not** entirely the same
as those specified in [the Nunjucks Documentation](http://mozilla.github.io/nunjucks/templating.html#filters)
See [below](#filter-reference) for an absolute list of what you can use

##Filter Reference

These are the available filters:



#####abs
*function(number)* Return the absolute value of the argument
#####batch
see [here](http://jinja.pocoo.org/docs/dev/templates/#batch)
#####capitalize
see [here](http://jinja.pocoo.org/docs/dev/templates/#capitalize)
#####default
see [here](http://jinja.pocoo.org/docs/dev/templates/#default)
#####escape (aliased as e)
see [here](http://jinja.pocoo.org/docs/dev/templates/#escape)
#####first
see [here](http://jinja.pocoo.org/docs/dev/templates/#first)
#####join
see [here](http://jinja.pocoo.org/docs/dev/templates/#join)
#####json_encode
*function(mixed)* Return the input JSON encoded
#####last
see [here](http://jinja.pocoo.org/docs/dev/templates/#last)
#####length
see [here](http://jinja.pocoo.org/docs/dev/templates/#length)
#####lower
see [here](http://jinja.pocoo.org/docs/dev/templates/#lower)
#####nl2br
*function(string)* Return the input with linebreaks replaced as `<br/>`
#####replace
see [here](http://jinja.pocoo.org/docs/dev/templates/#replace)
#####reverse
see [here](http://jinja.pocoo.org/docs/dev/templates/#reverse)
#####round
see [here](http://jinja.pocoo.org/docs/dev/templates/#round)
#####rnd
*function(number)* Return a random integer between 0 and *number*
#####safe
*function(string)* Does not escape html in the string

eg

    <script type="text/javascript">
        var myBigObject = {{ myBigObject | json_encode | safe }};
    </script>

outputs a raw json-encoded object for use in frontend javascript

#####slice
see [here](http://jinja.pocoo.org/docs/dev/templates/#slice)
#####sort
see [here](http://jinja.pocoo.org/docs/dev/templates/#sort)
#####title
see [here](http://jinja.pocoo.org/docs/dev/templates/#title)
#####trim
see [here](http://jinja.pocoo.org/docs/dev/templates/#trim)
#####upper
see [here](http://jinja.pocoo.org/docs/dev/templates/#upper)
#####urlencode
see [here](http://jinja.pocoo.org/docs/dev/templates/#urlencode)
#####wordcount
see [here](http://jinja.pocoo.org/docs/dev/templates/#wordcount)


The following Nujucks filters **cannot** be used with SiteChef. *You will find that
they may work when using `sitechef serve` but **will not work in production**.*

* center
* dictsort
* float
* groupby
* indent
* int
* list
* random
* string
* truncate


#Frontend Templates

Backend templates in the `templates/` folder can also be used in frontend
javascript code.

In order to be able to access frontend templates in your code, you will
need to do three things:

##Frontend Template Guide

####1. Compile Selected Templates to Javascript

This can be done automatically using the Gulp task `templates`. You will need to edit the configuration file `gulp-templates` and add all templates referenced and any templates included or imported. See [here](assetpipeline.md#frontend-templates) for detailed instructions and an example.

####2. Include the `Nunjucks Slim` library in your html

Add the following tag to your html before the main `app.js` script:

    <script type="text/javascript" src="https://cdn.jsdelivr.net/nunjucks/1.0.0/nunjucks-slim.min.js"></script>

####3. Ensure that the `template.min.js` script is included in your html

The asset pipeline compiles the templates to `template.js` and the minified `template.min.js` javascript files in the `dist/js` folder.

Ensure that one of these scripts is included before your `app.js`/ `app.min.js`:

    <script type="text/javscript" src='{{ assetsRoot }}js/template.min.js'></script>

*Note that the variable "assetsRoot" is used instead of an absolute path, this
ensures that the file can be found whether in production or running locally in
development*

####4. Require our `nunjucksEnv.js` script and render template

Assuming that you are using the default asset pipeline, the following
example would template `myTemplate.html` with the the data `{item1:'myItem', item2:'my second item'}`:

    // assumes this is "js/app.js"

    var NunjucksEnv = require("../lib/nunjucksEnv.js");

    // construct our nunjucks environment
    // 'nunjucks' should be available globally
    // after including the above script

    var env = NunjucksEnv.make(nunjucks);

    // the environemnt is now ready to template

    var myData = {
        item1: 'myItem',
        item2: 'my second item'
    };
    var myRenderedContent = env.render("myTemplate.html", myData);

#Widget Pages

SiteChef enables users to include "widgets" in some free text fields.
These widgets are rendered separately to the main template render.
Currently there are two available widgets:

1. Contact Widget - requires the template `contactPage.html`
2. Food Menu Widget - requires the template `foodMenu.html`

More detail is available in the description of the [widget data structure](datastructure.md#widgets)


#Templating Differences

The main difference between SiteChef's templating system and Nunjucks are the filters.
Please stick to the [absolute list above](#filter-reference) to ensure that your
theme works in production.

##Unavailable Nunjucks Functionality

The following Nunjucks features will **not work in production** on the backend:

###[asnycEach](http://mozilla.github.io/nunjucks/templating.html#asynceach)

###[asyncAll](http://mozilla.github.io/nunjucks/templating.html#asyncall)

###[raw](http://mozilla.github.io/nunjucks/templating.html#raw)

###[call](http://mozilla.github.io/nunjucks/templating.html#call)

###[use of regular expressions](http://mozilla.github.io/nunjucks/templating.html#regular-expressions)

Raw regular expressions cannot be used inline or in filters

###[cycler function](http://mozilla.github.io/nunjucks/templating.html#cycleritem1-item2-itemn)

###[joiner function](http://mozilla.github.io/nunjucks/templating.html#joiner-separator)

