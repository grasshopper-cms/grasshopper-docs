# Road Map

Things to work on can be found in the issues sections of each project:

* [Grasshopper-CMS](https://github.com/grasshopper-cms/grasshopper-cms/issues)
* [Grasshopper-API](https://github.com/Solid-Interactive/grasshopper-api-js/issues)
* [Grasshopper-Core](https://github.com/Solid-Interactive/grasshopper-core-nodejs/issues)
* [Grasshopper-Admin](https://github.com/Solid-Interactive/grasshopper-admin/issues)
* [Grasshopper-Docs](https://github.com/grasshopper-cms/grasshopper-docs/issues)
* [Grasshopper-Cli](https://github.com/Solid-Interactive/grasshopper-cli/issues)

## Direction

### Grasshoper-CMS

`Grasshopper-CMS` is being built out as the single npm needed to include Grasshopper in a project.

To help testing `Grasshopper-CMS` a [demo project](https://github.com/grasshopper-cms/grasshopper-demo/issues) should be created, using a standard express / VueJS stack.

Once the demo app is stable, [Grasshopper-CLI](https://github.com/Solid-Interactive/grasshopper-cli/issues/22) should be updated to have the demo app as a choice for one of the scaffolding options.

Making plugins work with both node_modules and [local directories](https://github.com/grasshopper-cms/grasshopper-cms/issues/4) is important, and
polishing the [grasshopper-cms ui](https://github.com/grasshopper-cms/grasshopper-cms/issues/6) is also important.

### Docs

The user-guide should be finished out so that no reference are made to the old docs.

### Core Functionality

Finishing [multiple collections](https://github.com/Solid-Interactive/grasshopper-core-nodejs/issues/96) is the highest priority. [Updating to use BB and latest Mongoose](https://github.com/Solid-Interactive/grasshopper-core-nodejs/issues/82) should be quick and will help avoid some hard to trace bugs.


