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
    admin : {
        username: 'the-admin-username',
        password: 'the-admin-password'
    },
    mode: 'develop', // develop mode give extra debugging
    env,
    grasshopper: {
      adminMountPoint, // route admin is at. default is /admin
      apiMountPoint, // route api is at. default is /api    
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
      plugins: [
        {
          name: 'test',
          label: 'Test Plugin',
          icon: 'fa-user',
          path: path.join(__dirname, './plugins/test')      
        }
      ], // an array of plugins to load
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

* `grasshopper.assets`
   * this is used to define whether using s3 or the local disk to store images
   
```   
"assets": {
    "default" : "local",
    "tmpdir" : "{absolute path to tmp directory}",
    "engines": {
        "local":{
            "path":"{absolute path to public asset folder}",
            "urlbase":"{full url base to serve files from}"
        }
    }
}
```

default : This determines which engine will serve assets
tmpdir : Absolute path on your local system where temporary files will be saved. Make sure it has correct permissions.
engines : Each engine listed will be used for creating and updating assets, but only the one listed in default will be used for serving assets.   

```
            assets: {
                default: 'amazon',
                engines: {
                    local: {
                        accessKeyId:  variables.aws.accessKeyId,
                        bucket:  variables.aws.bucket,
                        region:  variables.aws.region,
                        secretAccessKey:  variables.aws.secretAccessKey,
                        urlbase:  variables.aws.urlbase
                    }
                },
                "filenameSpaceReplacement": "-"
            },
```

filenameSpaceReplacement : When uploading assets to Amazon S3, spaces in filenames will be replaced with the character(s) provided here.
   
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
