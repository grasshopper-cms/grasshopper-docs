# Quick Start

This is how to get started using Grasshopper...

Grasshopper is a headless CMS with an admin. It can be used to build both apis and websites.

To get started require grasshopper-cms and init with your config object:

```javascript
const express = require('express');
const app = express();
const grasshopper = require('grasshopper-cms');


grasshopper
    .start({
        app,
        express,
        // Other configs here
    })
    .then(() => {
        
        // grasshopper.authenticatedRequest is now available
        // grasshopper.grasshopper is now available
        
        console.log('listening on port 3000');
        app.listen(3000);
    })
    .catch(err => {
        console.log('startup error', err);
    })
```

For an example config object see the [grasshopper-demo](https://github.com/grasshopper-cms/grasshopper-demo/blob/master/index.js#L9).

In the example above, `app` is a standard express app. You can set it up as you normally would for a website or api. 
You can inform your models with queries via `grasshopper.authenticatedRequest`, and you can view the admin at https://localhost:3000/admin .

## Queries

Queries are promise based. Query content involves looking for content by `_id`, by querying for fields on the document, or query for meta
data on the document.

A Grasshopper content item has this form:

```json
{
    _id
    fields : {
        
    },
    meta : {
       type,
       node,
       labelfield,
       typelabel,
       created,
       lastmodified
    }
}
```

The keys for `meta` are stable. The keys for `fields` are defined in the admin by modifying the content type.

So querying all 

```javascript
return ghService
    .authenticatedRequest.content.query({
        filters : [
            {
                key : 'fields.title',
                cmp : '=',
                value : 'My Post'
            },
            {
                key : 'meta.typelabel',
                cmp : '=',
                value : 'Standard Post'
            }
        ],
        nodes: [
            // The id of the node
            '58943396364f3b528af81f80'
        ],
        options : {
            sort: {
                'fields.title' : 1
            }
        }
    })
```


## Pro tip:

To access raw mongo:

```
// access to mongo driver
grasshopper.core.db.content.model.collection

// so you can do stuff like
grasshopper.core.db.content.model.collection.find({
    $text: {
        $search: term}}).toArray();

// add an index        
grasshopper.core.db.content.model.collection.ensureIndex('fields.slug' (err, res) => { console.log(err, res); });        
```

---

[Edit Page](https://github.com/grasshopper-cms/grasshopper-docs/edit/master/user-guide/docs/index.md)
