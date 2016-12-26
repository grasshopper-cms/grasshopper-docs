# Project Overview

## Pieces

* [Grasshopper-CMS](https://github.com/grasshopper-cms/grasshopper-cms/issues)
* [Grasshopper-API](https://github.com/Solid-Interactive/grasshopper-api-js/issues)
* [Grasshopper-Core](https://github.com/Solid-Interactive/grasshopper-core-nodejs/issues)
* [Grasshopper-Admin](https://github.com/Solid-Interactive/grasshopper-admin/issues)
    * Deprecated. Being moved into `Grasshopper-CMS`
* [Grasshopper-Docs](https://github.com/grasshopper-cms/grasshopper-docs/issues)
* [Grasshopper-Cli](https://github.com/Solid-Interactive/grasshopper-cli/issues)

`Grasshopper-Core` contains the basic functionality and interacts with the database. CRUD and search operations and done with core.

`Grasshopper-API` exposes `Grasshopper-Core` via an http api. It also exposes core as a returned object to be used directly in an app.

`Grasshopper-CMS` starts up `Grasshopper-API` for you. It also exposes the admin ui. `Grasshopper-CMS` is the only Grasshopper related npm you need to install when
using Grasshoper in a project.


