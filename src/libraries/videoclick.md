# VideoClick

Uses image data to replace a placeholder image
for a video with an auto-playable HTML5/Youtube/Vimeo video


## Usage

Template HTML:

Use the `imageBuilder.html` macro in the `templates/defaults` folder to create
an image with a 'play button'

      {% from 'defaults/imageBuilder.html' import imageBuild %}
      <div class="image-item">
        {{ imageBuild(item, 'my-placeholder-image') }}
      </div>

***N.B. Ensure that the nunjucks-slim.js is included in the frontend and that
the templates `defaults/html5video.html`, `defaults/youtube.html` and
`defaults/vimeo.html` are exported in `gulpTasks/gulp-templates.js`***

JS:

      var VideoClick = require('../lib/VideoClick.coffee');

      var videoClick = new VideoClick({
        selector: $('.image-item .videoPlay'),
        end: function($div, data){
          console.log("User has finished playing video");
        }
      });

## Options

      var options = {

        /*
         * @var {String} src of vimeo video manager
         */
        vimeo: 'http://a.vimeocdn.com/js/froogaloop2.min.js',

        /*
         * @var {String} src of youtube api
         */
        youtube: 'http://www.youtube.com/iframe_api',

        /*
         * @var {String} cdn src of video js
         */
        html5: "https://cdnjs.cloudflare.com/ajax/libs/video.js/4.1.0/video.js",

        /*
         * @var {JQueryElement} Element to bind click to
         */
        selector: $('.videoPlay'),

        /*
         * default templates to use
         * when building the players
         */
        template: {

          /*
           * @var {String} youtube template
           */
          youtube: 'defaults/youtube.html',

          /*
           * @var {String} vimeo templtae
           */
          vimeo: 'defaults/vimeo.html',

          /*
           * @var {String} html5 template
           */
          html5: 'defaults/html5video.html'
        },

        /*
         * Callback when video bound and
         * any external (api) libraries loaded
         * @var {Function}
         */
        loaded: function() {},

        /*
         * @var {Function} called at the end of the video
         */
        end: function($playDiv, data) {},

        /*
         * @var {Function} called on playback progress
         *                 (not always available on all platforms)
         */
        progress: function($playDiv, data, e) {}
      };

      var videoClick = new VideoClick(options);


