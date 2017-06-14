# Updating Admin

Updating admin should be done in [Grasshopper-CMS](https://github.com/grasshopper-cms/grasshopper-cms).

1. Clone grasshopper-cms
1. run `npm link` from its root. 
1. Clone [grasshopper-demo](https://github.com/grasshopper-cms/grasshopper-demo)
1. run `npm link grasshopper-cms` from its root. 
1. from the root of gh-demo run `bin/seedDb`
1. from the root of gh-demo run `bin/start`

At this point you are able to view the admin at http://localhost:3000/admin . Make your updates to grasshopper-cms/plugins/admin/src

To access the admin:

| Username | Password |
|---|---|
| admin | TestPassword |

If you want to pull in a non minified version of the admin, pass in `mode: 'develop'` as an option.

Once done with your changes:

1. run `bin/minify.js` from grasshopper-cms/plugins/admin. This will minify your updates.

Now you are ready to publish. Semantic version bump, git commit, and do an `npm publish` from grasshopper-cms. Then bump the
grasshopper-cms version number in grasshopper-demo.

---

[Edit Page](https://github.com/grasshopper-cms/grasshopper-docs/edit/master/contribution-guide/docs/updating-admin.md)
