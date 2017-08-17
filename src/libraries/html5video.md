#HTML5 Video

The `HTML5Video` library simplifies creating [Video.JS](http://videojs.com) players
to play `mp4` and `webm` videos either hosted by SiteChef
or from external services like Instagram.

##Requirements

In order for the `HTML5Video` to work, you must include the following
external libraries beforehand:


- JQuery 1.9+
- Nunjucks Slim ([dev](http://mozilla.github.io/nunjucks/files/nunjucks-slim.js)/[prod](http://mozilla.github.io/nunjucks/files/nunjucks-slim.min.js))
- The html5 video template (usually `templates/defaults/html5video.html`) ***must be pre-rendered*** and included in the html. (See [Frontend Templating](../assetpipeline.md#frontend-templates) for explanation)
- [Video.js](http://videojs.com)

e.g.

     <script type="text/javascript" src='https://cdnjs.cloudflare.com/ajax/libs/jquery/1.11.2/jquery.min.js'></script>
     <script type="text/javascript" src='https://cdn.rawgit.com/mozilla/nunjucks/master/browser/nunjucks-slim.min.js'></script>
     <!-- template.min.js is the generated, pre-rendered nunjucks template -->
     <script type="text/javascript" src='{{ assetsRoot }}js/template.min.js'></script>
     <script type="text/javascript" src='https://cdnjs.cloudflare.com/ajax/libs/video.js/4.11.3/video.js'></script>

##Usage

The library is designed to work with the `defaults/imageBuilder.html` [macro](../templating.md#rendering-images) which will write out the correct image metadata:

HTML (auto-rendered by [imageBuilder.html macro](../templating.md#rendering-images):

    <div class="image-continer">
      <img class="my-image" src='blank-image-path.png' id="124-11" data-id="124-11" data-src="https://cdn.s3.amazon.com/real-image-path.jpg" data-ratio="0.89" data-focus='{"x":0.2,"y":0.9}' data-video="" data-content-type="html5" data-video-srcs='{"mp4High":{"url":"https://cdn.amazon.com/myvideo.mp4"}}'>
      <div class="videoPlay" data-video-id="124-11" data-video-type="html5" data-video-srcs='{"mp4High":{"url":"https://cdn.amazon.com/myvideo.mp4"}'></div>
    </div>

JS:

    var HTML5Video = require('../lib/HTML5Video.coffee');
    var myVideo = new HTML5Video({
      target: $('.my-image'), // the image which is the preview
      video:{
        controls: true // show video controls
      },
      playerReady: function(){
        // call any video-related logic
        this.play(); // such as playing the video
      }
    });


##Options
