#Data Structure

##Core Data

####Every page is templated with the following data structure
####You can view your theme data in your data snapshot file at `.sitechef/data.json`


**{**

&nbsp; uid `integer`            *the internal id of the site*
&nbsp; environment `string`     *`development` if running locally or `production`*
&nbsp; assetsRoot `string`      *the absolute url of the assets folder of your theme (this will be the `dist/` folder)*
&nbsp; imageRoot `string`       *the absolute path of the user-uploads CDN*<span id="image-root"></a>
&nbsp; siteRoot `string`        *The absolute root of the theme*
&nbsp; storageRoot `string`     *the absolute root of any user-uploaded documents*
&nbsp; logo `string`            *html for the logo*
&nbsp; logoUrl `string`         *the absolute url of the standard resolution logo*
&nbsp; pageType `string`        *The type of page being rendered*
&nbsp;                          *`root` - this is the landing page*
&nbsp;                          *`subcategory` - any child of the frontpage*
&nbsp;                          *`media` - a static page describing a user-uploaded image/video*
&nbsp;                          *`post` - a static blog post *
&nbsp; [preferences](#preferences-struct) `struct`     *list of user-set variables*
&nbsp; [socialMedia](#socialmedia-array) `array`     *User social media links*
&nbsp; [meta](#meta-struct) `struct`            *user-specific configuration automatically generated*
&nbsp; [menu](#menu-array) `array`              *the main site navigation hiearchy with nested children*
&nbsp; [menuChildren](#menu-array) `array`      *If the current page has children, they are listed here - useful for submenus*
&nbsp; [content](#content-struct) `struct`          *data about the current page*

**}**


##Preferences Struct

####Preferences are user-generated options

**{**
&nbsp; currentTemplate `string`       *active template name*
&nbsp; siteLogo `string`              *relative url of logo to [image root](#image-root)*
&nbsp; siteLogo_2x `string`           *relative url of logo for retina to [image root](#image-root)*
&nbsp; comingSoon `bool`              *whether or not the site is coming soon*
&nbsp; restaurantName `string`
&nbsp; restaurantDescription `string`
&nbsp; restaurantGeo `object`         *Latitude and longitude of restaurant for maps and geo-tagging*
&nbsp;    **{**
&nbsp;         lat `float`
&nbsp;         lng `float`
&nbsp;    **}**
&nbsp; address1 `string`
&nbsp; address2 `string`
&nbsp; postcode `string`
&nbsp; phone `string`
&nbsp; email `string`                 *official venue email (not the users's)*
&nbsp; openingHours `string`
&nbsp; googleAccount `string`         *google analytics account code*
&nbsp; twitter `string`               *twitter handle*
&nbsp; instagram `string`             *instagram url*
&nbsp; facebook `string`              *facebook page url*
**}**

##SocialMedia Array

####Links to user's social media services

**[**
&nbsp;  *These are not always available and*
&nbsp;  *vary according to whether the user has entered them*
&nbsp;  facebook `string`
&nbsp;  twitter `string`
&nbsp;  instagram `string`
&nbsp;  pinterest `string`
&nbsp;  email `string`
**]**

##Meta Struct

####Server-generated user settings

**{**
&nbsp; favIcon `string`               *absolute path of the favicon*
&nbsp; logo `string`                  *rendered html of the logo*
&nbsp; isMobile `string`              *is this being viewed on a mobile device - **only works in production** *
&nbsp; imageRoot `string`             *Absolute root of the CDN for user content*
&nbsp; siteRoot `string`              *absolute path of site root*
&nbsp; customJS `string`              *frontend javascript variables*
&nbsp; templatePreferences `struct`   *User options selected by the current user*
&nbsp;    **{**
&nbsp;      colours `struct`         *user colour options by id*
&nbsp;      fonts `struct`           *user font options by id*
&nbsp;      variables `struct`       *user colour options by id*
&nbsp;    **}**
**}**

##Menu Array

####Nested site hierarchy for rendering the navigation

**[**
&nbsp;  [Menu](#menu-struct) `struct`
**]**

##Menu Struct

####A Cut-down version of the [Content Struct](#content-struct)

**{**
&nbsp;  id `int`             *id of page*
&nbsp;  importance `int`     *higher number pages appear first order*
&nbsp;  name `string`        *name /title of page*
&nbsp;  url `string`         *slug or relative url of page*
&nbsp;  path `string`        *absolute url of page*
&nbsp;  published `bool`     *whether or not the page has been published*
&nbsp;  isExternal `bool`    *is this an external link*
&nbsp;  showOnMobile `bool`  *display this page when viewed on mobile*
&nbsp;  level `int`          *`0` is frontpage, `1` subcategory, `2` child of subcategory*
&nbsp;  parent `object`      *information about the parent item of this menu*
&nbsp;    **{**
&nbsp;         id `integer`
&nbsp;    **}**
&nbsp;  children `array`
&nbsp;  **[**
&nbsp;    [Menu](#menu-struct) `struct`
&nbsp;  **]**
**}**

##Content Struct

####The core content for the current page

**{**
&nbsp;  id `int`                    *the unique id of this page*
&nbsp;  name `string`               *Page title - what appears in the navigation*
&nbsp;  description `string`        *the page summary*
&nbsp;  body `string`               *the body with widgets rendered - use in preference to **rawBody** *
&nbsp;  rawBody `string`            *body before widgets have been rendered*
&nbsp;  parent `struct`
&nbsp;  **{**
&nbsp;      id `int`                *Id of the parent page*
&nbsp;  **}**
&nbsp;  items `array`
&nbsp;  **[**
&nbsp;      [Item](#item-struct) `struct`
&nbsp;  **]**
&nbsp;  uri `string`                *the absolute path form site root eg `/gallery`*
&nbsp;  url `string`                *slug for this page eg. 'gallery'*
&nbsp;  level `int`                 *what level in site hierarchy:*
&nbsp;                                  *`0` - Front page*
&nbsp;                                  *`1` - Child of Front page *
&nbsp;                                  *`2` - Child of child of front page*
&nbsp;  type `string`               *the current page format - use the `format` integer in preference*
&nbsp;                                  *as this is internationalized*
&nbsp;  format `int`                *the current page format*
&nbsp;                                  *`0` - Gallery*
&nbsp;                                  *`1` - Blog*
&nbsp;                                  *`2` - Food Menu*
&nbsp;                                  *`3` - Stream - ie raw data from instragram*
&nbsp;                                  *`4` - Static Page *
&nbsp;                                  *`5` - External Link*
&nbsp;                                  *`6` - Contact Page*
&nbsp;  showOnMobile `bool`         *display this page when viewed on mobile*
&nbsp;  linkImage `string`          *absolute path of the image to use when external sites show a preview of this page*
&nbsp;  [featuredImage](#item-struct) `struct`      *featured image for this section (Image)*
&nbsp;  htmlTitle `string`          *text for the brower tab title*
&nbsp;  metaDescription `string`    *text for the meta description for the page*
&nbsp;  lastUpdated `string`        *date formatted YYYY-MM-DD hh:ii:ss*
&nbsp;  customSettings `struct`     *[OPTIONAL] this is contingent on page type*
&nbsp;  **{**
&nbsp;      galleryType `string`    *Type of gallery: `carousel` or `mosaic`*
&nbsp;      location `object`       *Location override*
&nbsp;  **}**
&nbsp;  blogPosts `array`           *Only present when `format` is `1`*
&nbsp;  **[**
&nbsp;      [Blog Post](#blog-post-struct) `struct`
&nbsp;  **]**
**}**

##Item Struct

####Data for an image or video

**{**
&nbsp;  id `int`                    *id of the item*
&nbsp;  title `string`              *Image/Video Title*
&nbsp;  description `string`        *Image/Video Description (can contain HTML)*
&nbsp;  type `string`               *the type of item*
&nbsp;                              *`image`  - a jpeg*
&nbsp;                              *`html5`  - html5 video hosted by SiteChef*
&nbsp;                              *`youtube`  - a youtube video to embed*
&nbsp;                              *`vimeo`  - a vimeo video to embed*
&nbsp;  tags `string`               *User-tagged data*
&nbsp;  slug `string`               *url to static version of this item*
&nbsp;  [image](#image-struct) `struct`     *Image Data*
&nbsp;  [video](#video-struct) `struct`     *Youtube/Vimeo Metadata*
&nbsp;  [videoData](#video-data-struct) `struct`     *[OPTIONAL] HTML5 Video Data*
**}**

##Image Struct

####Data for accessing different versions of images

**{**
&nbsp;  large `struct`              *large image (max 1200px)*
&nbsp;  **{**
&nbsp;      src `string`            *Absolute path of large image*
&nbsp;  **}**
&nbsp;  mobile `struct`              *mobile image (max 600px)*
&nbsp;  **{**
&nbsp;      src `string`            *Absolute path of mobile image*
&nbsp;  **}**
&nbsp;  thumbnail `struct`          *thumbnail image (max 200px)*
&nbsp;  **{**
&nbsp;      src `string`            *Absolute path of thumb image*
&nbsp;  **}**
&nbsp;  ratio `float`               *width-height ratio of image = `height / width `*
&nbsp;  focus `struct`              *user-selected position of most importance*
&nbsp;  **{**
&nbsp;      x `float`               *0-1 - 1 is far right, 0 far left*
&nbsp;      y `float`               *0-1 - 1 is top, 0 bottom*
&nbsp;  **}**
**}**

##Video Struct

####Data for embedding youtube/vimeo videos

**{**
&nbsp;  id `string`             *youtube|vimeo id*
&nbsp;  type `int`              *Type of video*
&nbsp;                            *`0` - Vimeo*
&nbsp;                            *`1` - Youtube*
&nbsp;                            *`2` - HTML5*
**}**

##Video Data Struct

####This is only available when item is an HTML5 video

**{**
&nbsp;  baseName `string`       *unique filename base*
&nbsp;  versions `struct`       *available video versions*
&nbsp;  **{**
&nbsp;      [mp4High](#html5-struct) `struct`   *Best quality mp4*
&nbsp;      [mobile](#html5-struct) `struct`    *low quality mp4*
&nbsp;      [webM](#html5-struct) `struct`      *high quality webm*
&nbsp;      [thumbnails](#html5-struct) `struct`  *auto-generated thumbnails*
&nbsp;  **}**
**}**

##HTML5 Struct

####This is automatically generated by [Zencoder](https://app.zencoder.com/docs/api/outputs)

**{**
&nbsp;  id `string`             *unique id for video*
&nbsp;  url `string`            *absolute path to video*
&nbsp;  duration_in_ms `int`    *total duration of video*
&nbsp;  height `int`            *height in px*
&nbsp;  width `int`             *width in px*
&nbsp;  ...
&nbsp;  thumbnails `array`
&nbsp;  **[**
&nbsp;      **{**
&nbsp;        label `string`
&nbsp;        images `array`
&nbsp;          **[**
&nbsp;              **{**
&nbsp;                  url `string`
&nbsp;                  format `string`
&nbsp;                  dimensions `string`
&nbsp;              **}**
&nbsp;          **]**
&nbsp;      **}**
&nbsp;  **]**
**}**


##Blog Post Struct

####An individual blog post

**{**
&nbsp;  id `int`                    *blog post id*
&nbsp;  body `string`               *raw body before widgets have been rendered*
&nbsp;                              ***N.B. use `renderedBody` instead for templating***
&nbsp;  category_id `int`           *the id of the parent page*
&nbsp;  [featuredImage](#item-struct) `struct`      *featured image for this section (Image)*
&nbsp;  gallery `array`             *list of images for the gallery*
&nbsp;   **[**
&nbsp;      [Item](#item-struct) `struct`
&nbsp;   **]**
&nbsp;  htmlTitle `string`          *text for the brower tab title*
&nbsp;  metaDescription `string`    *text for the meta description for the page*
&nbsp;  postDate `string`           *date formatted YYYY-MM-DD hh:ii:ss*
&nbsp;  published `bool`            *whether page has been published*
&nbsp;  renderedBody `string`       *body to display once widgets have been rendered*
&nbsp;  slug `string`               *url fragment for this post*
&nbsp;  summary `string`            *text summary for blog pst*
&nbsp;  tags `string`               *comma delimited list of tags*
&nbsp;  title `string`              *Blog title*
&nbsp;  updatedAt `string`          *last saved date*
**}**



