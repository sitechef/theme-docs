#Twitter

Loads and templates a users' twitter feed


*N.B. requires `jQuery`, `lodash`, `nunjucks.slim.min` and `moment.js`*

##Usage

Destination HTML:
*(Where tweets will be appended)*

        <div class="latest-tweets"></div>

Twitter Template `twitter.html`
*(Must be included in the [frontend template list](../assetpipeline.md#frotnend-templates))*

        {#
         Template to be used on frontend
         for rendering twitter feeds
         #}
        <div class="latest-tweets-inside">
          <div class="title-area">
            <h3><a href="https://twitter.com/{{ screen_name }}" target="_blank"><i class="icon icon-twitter"></i> Tweets</a></h3>
          </div>
          {# repeater for tweets from server #}
          <ul class="tweets">
            {% for tweet in tweets %}
            <li class="tweet">
              <span class="tweet-text">{{ tweet.tweet | safe }}</span>
              <span class="tweet-age">{{ tweet.age }}</span>
            </li>
            {% endfor %}
          </ul>

        </div>


JS:

    var Twitter = require('../lib/Twitter.coffee');

    twitter = new Twitter($('.latest-tweets'));

##Data Structure

The data structure for each tweet is the same
as [the official twitter tweet structure](https://dev.twitter.com/overview/api/tweets), however two fields are added:

- **tweet** `string` - the tweet text with links replaced
- **age** `string` - the age of the tweet e.g "1 hour", "1 day"

The field **screen_name** `string` is also added at the root


Example data for the template is:

        {
            screen_name: '_sitechef',
            tweets: [
                {
                    tweet: 'Latest information from <a href="https://twitter.com/_sitechef>@_sitechef</a>',
                    age: '2 hours',
                    // .... all other standard
                    // twitter fields
                    // e.g.
                    created_at: 'Thu Feb 12 13:38:36 +0000 2015,'
                    "in_reply_to_status_id": 565864218704875520
                    // ...
                }
            ]
        }


##Options

        var options = {
            // path of the frontend template
            template: 'twitter.html',
            // endpoint relative to site root
            // for retrieving twitter information
            endpoint: 'api/streams/twitter',
            // text shown when there's a connection error
            connectionError: 'Connection Error',
            // absolute base url for the site
            siteRoot: window.siteRoot || '/'
        };

        var twitter = new Twitter($('.latest-tweets'), options);

