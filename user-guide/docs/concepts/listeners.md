# Listeners

Listeners can be setup via grasshopper core:

```javascript
require('grasshopper-cms')
    .start(configs)
    .then(result => {
        // result.grasshopper.core is core
```

Here is [an example of using listeners](https://github.com/Solid-Interactive/Recipes/blob/master/app/listeners.js#L12).

More example, the system/db start [is handled internally by grasshopper-cms](https://github.com/grasshopper-cms/grasshopper-cms/blob/758570696c893e9dafb80459904953fe6310a097/index.js#L31):

```javascript
// Event examples
grasshopper.core.event.channel('/type/*')
    .on('save', function(kontx, next) {
        memoize.clearCache();
        next();
    });
grasshopper.core.event.channel('/type/' + constants.ids.recipes)
    .on('parse', function(payload, next) {
        // do stuff
        next();
    });
grasshopper.core.event.channel('/system/db')
    .on('start', function(payload, next){
        logger.debug('starting grasshopper');
        next();
    });    
```

You can listen to various events on types or content. The callback receives a payload and a next method. The
document is at `payload.args.fields` and `payload.args.meta`.

You can modify the document as needed and call `next` when ready. This allows the creation of computed properties. It is often
useful to store these as read only fields.

Listeners [are setup here in GH Core](https://github.com/grasshopper-cms/grasshopper-core-nodejs/blob/master/lib/event/listeners.js).

The events you can subscribe to can be seen in [the runners](https://github.com/grasshopper-cms/grasshopper-core-nodejs/tree/master/lib/runners).
For example the [content events](https://github.com/grasshopper-cms/grasshopper-core-nodejs/blob/master/lib/runners/content.js) are


Available event [filters](https://github.com/Solid-Interactive/grasshopper-core-nodejs/blob/master/lib/event/channel.js) 
are: `nodes`, `types`, `contentids`, `system`. 

Below are the gh method calls with their associated events:

### [Assets](#assets)

#### [assets.copy]()
* **Events:** parse, validate, out, copy

#### [assets.delete]()
* **Events:** parse, validate, out, delete

#### [assets.deleteAll]()
* **Events:**  parse, validate, out, delete

#### [assets.find]()
* **Events:** parse, validate, out

#### [assets.list]()
* **Events:** parse, validate, out

#### [assets.rename]()
* **Events:** parse, validate, out, rename

#### [assets.save]()
* **Events:** parse, validate, out, save


### [Content](#content)

#### [content.deleteById]()
* **Events:** parse, validate, out, delete

#### [content.getById]()
* **Events:** parse, validate, out

#### [content.getFullById]()
* **Events:** parse, validate, out

#### [content.insert]()
* **Events:**  parse, validate, out, save

#### [content.query](/grasshopper-core-nodejs/documentation.html#queries)
* **Events:** out

#### [content.queryFull](/grasshopper-core-nodejs/documentation.html#queries)
* **Events:** out

#### [content.update]()
* **Events:** parse, validate, out, save

### [Content Types](#content-types)

#### [contentTypes.deleteById]()
* **Events:**  parse, validate, out, delete

#### [contentTypes.getById]()
* **Events:** parse, validate, out

#### [contentTypes.insert]()
* **Events:** parse, validate, out, save

#### [contentTypes.list]()
* **Events:**  parse, validate, out

#### [contentTypes.update]()
* **Events:** parse, validate, out

#### [contentTypes.query]()
* **Events:** out

### [Nodes](#nodes)

#### [nodes.deleteById]()
* **Events:** parse, validate, out, delete

#### [nodes.getById]()
* **Events:** parse, validate, out

#### [nodes.getChildren]()
* **Events:** parse, validate, out

#### [nodes.insert]()
* **Events:** parse, validate, out, save

#### [nodes.move]()
* **Events:** parse, validate, out, save

#### [nodes.query]()
* **Events:** parse, validate, out

#### [nodes.saveContentTypes]()
* **Events:** parse, validate, out

#### [nodes.update]()
* **Events:** parse, validate, out, save

### [Tokens](#tokens)

#### [tokens.deleteById]()
* **Events:** parse, validate, out, delete

#### [tokens.getNew]()
* **Events:** parse, validate, out

#### [tokens.impersonate]()
* **Events:** parse, validate, out

#### [tokens.logout]()
* **Events:** parse, validate, out

### [Users](#users)

#### [users.deleteById]()
* **Events:** parse, validate, out, delete

#### [users.getByEmail]()
* **Events:** parse, validate, out

#### [users.getById]()
* **Events:** parse, validate, out

#### [users.insert]()
* **Events:** parse, validate, out, save

#### [users.linkIdentity]()
* **Events:** parse, validate, out, save

#### [users.list]()
* **Events:** parse, validate, out

#### [users.query]()
* **Events:** parse, validate, users, out

#### [users.unlinkIdentity]()
* **Events:** parse, validate, out, save

#### [users.update]()
* **Events:** parse, validate, out, save

---

[Edit Page](https://github.com/grasshopper-cms/grasshopper-docs/edit/master/user-guide/docs/concepts/listeners.md)
