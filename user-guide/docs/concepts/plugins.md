# Plugins

You can create plugins to use with Grasshopper.

Each plugin can have UI in the Grasshopper Admin, as well as arbitrary functionality.

A plugin is a directory whose path is passed in as an option of `grasshopper-cms`:

```javascript
require('grasshopper-cms')
    .start({
        ...,
        grasshopper : {
            plugins: [
                {
                    name: 'test',
                    label: 'Test Plugin',
                    icon: 'fa-user',
                    path: path.join(__dirname, './plugins/test')
                },
                {
                    // this plugin gets no ui in the admin
                    name : 'headless',
                    path: path.join(__dirname, './plugins/headless')
                }
            ],
            ...
        }
    })
```

A plugin can have an optional `startup.js` file. This file can synchronously or asynchrounously
return an express router. This express router will be attached to `${options.grasshopper.adminMountPoint}/${plugin.name}`.

This mean that in a `startup.js` file you can do arbitrary setup work and / or create a router to use.
The endpoints created can be used in conjunction with the admin ui.

To create the admin UI you need two files. A front end JS file and a CSS file.

Each plugin can have a `public` directory. Content of this `public` directory will be served at:
`${adminMountPoint}/${plugin.name}`. The JS file should be in `public/scripts/main.js`. The CSS file should be in
`public/styles/main.css`.

The icon field can be a font awesome icon and the label field will be displayed in the left hand sidebar of the admin.

To see the examples above in action, check out the [demo app](https://github.com/grasshopper-cms/grasshopper-demo/tree/master/plugins).

--- 

[Edit Page](https://github.com/grasshopper-cms/grasshopper-docs/blob/master/user-guide/docs/concepts/plugins.md)