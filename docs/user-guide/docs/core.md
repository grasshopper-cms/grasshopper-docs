# Core

## Events

Grasshopper emits events that can be subscribed to in order to customize
behavior:

Below are example of hooking into all changes on contentTypes and content:

```
grasshopper
    .core.event.channel('/type/*')
    .on('save', function(kontx, next) {
    
        next();
    });

grasshopper
    .core.event.channel('/content/*')
    .on('save', function(kontx, next) {
    
        next();
    });
```

## Pro tip:

To access raw mongo:

```
// access to mongo driver
grasshopper.core.db.content.model.collection

// so you can do stuff like
grasshopper.core.db.content.model.collection.find({
    $text: {
        $search: term}}).toArray()
```