# Analytics

Sends Google Analytics events on all anchor clicks

## Usage

Simply require and instantiate with the parent element of the anchors


     var Analytics = require('./Analytics'),
         // binds every anchor in <body>
         analytics = new Analytics($('body'));
