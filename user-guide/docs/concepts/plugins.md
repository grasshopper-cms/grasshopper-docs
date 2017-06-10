# Plugins

You can create plugins to use with Grasshopper.

Each plugin can have UI in the Grasshopper Admin, as well as arbitrary functionality.

A plugin is a directory whose path is passed in as an option of `grasshopper-cms`:

```javascript
require('grasshopper-cms')
    .start({
        ...,
        grasshopper: {
            plugins: [
                {
                    name: 'test',
                    label: 'Test Plugin',
                    icon: 'fa-user',
                    path: path.join(__dirname, './plugins/test')
                },
                {
                    // this plugin gets no ui in the admin
                    name: 'headless',
                    path: path.join(__dirname, './plugins/headless')
                },
                {
                    // this plugin template is server-rendered
                    name: 'server-rendered',
                    path: path.join(__dirname, './plugins/server-rendered'),
                    icon: 'fa-server',
                    label: 'Server Rendered',
                    template: 'template.pug'
                }
            ],
            ...
        }
    })
```
## Options
#### `path`: required

The path to the plugin's directory.

#### `name`: required

The slug of the plugin.

#### `label`: optional

The label of the plugin used in the admin sidebar.

#### `icon`: optional

The icon paired with the label in the sidebar.

#### `template`: optional

The path to the plugin's server-rendered pug template, relative to the plugin's directory.

## Example

All plugin files are optional.

```
plugins
|   plugin-name
    |   startup.js // name not configurable
    |   template.pug // name configurable with template option
    |   public
        |   scripts
            |   main.js
        |   styles
            |   main.css
```

#### `startup.js`

Required format:

```
/**
 * @param {Object} grasshopper - The grasshopper app
 * @param {Object} grasshopper.grasshopper - The grasshopper api
 * @param {Object} grasshopper.authenticatedRequest - The grasshopper database connection
 * @param {Object} grasshopper.middlewares - Built in middlewares
 * @param {Object} app - The express app
 */
module.exports = function(grasshopper, app) {
    // do whatever you want here
}
```

Startup can synchronously or asynchrounously return an express router. This express router will be attached to `${options.grasshopper.adminMountPoint}/${plugin.name}`. Use this to do any arbitrary setup work and / or create a router to use. The endpoints created can be used in conjunction with the admin ui.

#### `template.pug`

required format:

```
extends /plugin.layout.pug

block app
    .your.pug.here
```

Load data into your template by attaching a `.get` middleware to your `startup.js` router.

#### `public`

These files are statically served at `${adminMountPoint}/${plugin.name}`

##### `/scripts/main.js`

Automatically included on the plugin page. Use this to spin up a javascript app.

##### `/styles/main.css`
Automatically included on the plugin page. Use this to style your plugin page.

To see the examples above in action, check out the [demo app](https://github.com/grasshopper-cms/grasshopper-demo/tree/master/plugins).

--- 

[Edit Page](https://github.com/grasshopper-cms/grasshopper-docs/blob/master/user-guide/docs/concepts/plugins.md)
