# Configs

When starting grasshopper cms, you must call it with your configs:

```
const configs = require('./configs');
const gh = require('grasshopper-cms');

gh.start(configs)
   .then(result => {
      // at this point gh.authenticatedRequest and gh.grasshopper are available
   });
```

The following configs can be passed in via gh-cms:

```javascript
{
    app, // the express app
    express, // express itself
    plugins: [], // an array of plugins to load
    admin : {
        username: 'the-admin-username',
        passowrd: 'the-admin-password'
    },
    adminMountPoint, // route admin is at. default is /admin
    apiMountPoint, // route api is at. default is /api
    mode: 'develop', // develop mode give extra debugging
    env,
    grasshopper: {
      assets,
      crypto,
      db: {
         type: 'mongodb',
         defaultPageSize: 100000,
         //see here for connection string information: https://www.npmjs.com/package/mongoose#connecting-to-mongodb
         host:  'mongodb://127.0.0.1:27017/grasshopper-demo',
         database:  'grasshopper-demo',
         debug:  true
      },
      server: {
         proxy: true,
         host:  'localhost',
         https: false,
         maxFilesSize: 16000000
      }
    },
    logger: {
        adapters : [{
            type : 'console',
            application : 'ghdemo',
            machine : 'dev'
        }]
    },
    port: 3000,
    verbose: true    
}
```

The following configs are passed to `grasshopper-api` via the cms:

* `grasshopper.server`
    * this can be left out altogether or passed in as an object
    * `grasshopper.server.proxy` if `grasshopper.server.proxy === true` then a router will be returned from initializing grasshopper api, and no standalone express app will be created. This is meant to be used in the case you have an express app you want to mount the grasshopper api router on.
    * `grasshopper.server.https` truthy if grassopper should handle SSL - this is only meant for dev envirnoments. Nginx or Apache should handle SSL on production / staging. `server.https` should be an object if it is truthy.
    * `grasshopper.server.https.key` relative path to ssl key from `process.cwd()`
    * `grasshopper.server.https.cert` relative path too ssl cert file from `process.cwd()` 
* `sessions` 
    * set to truthy if you want cookies managed sessions
    * default: `undefined` 

---

[Edit Page](https://github.com/grasshopper-cms/grasshopper-docs/edit/master/user-guide/docs/usage/configs.md)
