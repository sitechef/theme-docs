# JSON Api

All SiteChef websites have a JSON api that is available via standard AJAX requests

They are available by the endpoint `/api/`

# Endpoints


##`/api/media/{item_id}` GET

Fetches data about a a particular item

### Parameter item_id `int` *id of item*

### Returns [Item Struct](datastructure.md# item-struct)

##`/api/category/{page_id}` GET

Fetches data for a particular page

### Parameter page_id `int` *id of page*

### Returns [Content Struct](datastructure.md# content-struct)


##`/api/blogpost/{post_id}` GET

Fetches data for a particular page

### Parameter post_id `int` *id of post*

### Returns [Blog Post Struct](datastructure.md# blog-post-struct)

##`/api/streams/instagram` GET

Fetches user's instagram feed

### Parameter post_id `int` *id of post*

### Returns `array` [[Item Struct](datastructure.md# item-struct), [Item Struct](datastructure.md# item-struct), ...]

##`/api/mailchimp/subscribe/{site_id}` POST

Adds a visitor to the SiteChef user's mailchimp list

### Request Body

The body variables are as set by the mailchimp user.
By default they are:

    {
        "FNAME":"<FirstName>",
        "LNAME":"<LastName>",
        "LNAME":"<LastName>"
    }


### Parameter post_id `int` *site id*

### Returns `object`

    {
        "succes": true, //boolean
        "errors":[] // any errors
    }

