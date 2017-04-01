# Authentication

Authentication is built into the default Grasshopper admin, but you will often want to add authentication to other
parts of your site.

You can always implement your own login flow. You can also use the login flow built into the admin. To do this attach
the authorization middleware from Grasshopper-CMS to your routes. The admin middleware is located at
[plugins/admin/src/middlewares/auth.middleware.js](https://github.com/grasshopper-cms/grasshopper-cms/blob/master/plugins/admin/src/middlewares/auth.middleware.js).

The authorization middleware will check if your auth cookie contains a valid auth token. If it does not, the middleware
will redirect to `res.loginRedirect || ${adminMountPoint}/login` You can customize the login url as you see fit.

The login for the admin will redirect to get param `redirect`.

Here is how you would login protect an entire site, and make sure users are returned to the page they were trying to 
access after logging in via the Grasshopper admin:

```javascript
grasshopper
    .start(options)
    .then(() => {
       app.use('/', [
           (req, res, next) => {
               res.loginRedirect = `/admin/login?redirect=${req.originalUrl}`;
               next();
           },
           require('grasshopper-cms/plugins/admin/src/middlewares/auth.middleware')
       ]); 
    });
```

The order of method calls is important here. You want to make sure you call this downstream from starting grasshopper,
otherwise you will password protect the login page too.
---
[Edit this Page](https://github.com/grasshopper-cms/grasshopper-docs/edit/master/user-guide/docs/usage/authentication.md)
