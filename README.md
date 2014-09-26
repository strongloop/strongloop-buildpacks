StrongLoop provides:

 * LoopBack, an open-source Node.js framework that enables you to create dynamic end-to-end REST APIs with little or no coding. For more information, see http://loopback.io.
 * StrongLoop Controller, a Node devops system.  See [StrongLoop Controller docs](http://docs.strongloop.com/display/SLC/StrongLoop+Controller) for more information.
 * StrongLoop Agent (StrongOps), an operational console for Node.js applications that provides deep performance monitoring including CPU profiling, event loop statistics, and more.  See [StrongLoop Agent docs](http://docs.strongloop.com/pages/viewpage.action?pageId=3834736) for more information.

The StrongLoop Heroku Buildpack installs the StrongLoop Controller command-line tool (slc) and the add-on provisions a
 [StrongOps](http://www.strongloop.com/ops) monitoring account.

## Prerequisites

Before starting, on your local system:

 - If you have not already done so, install Node.js : [Download native installers](http://nodejs.org/download)
 for Windows or Mac OS; for Linux,
 see [Installing Node.js via package manager](https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager).
 - Install StrongLoop software:
   ```term
   $  npm install -g strongloop
   ```
 - Make sure you have installed the [Heroku Toolbelt](https://toolbelt.heroku.com/).

## Create your app

Follow the instructions in 
[Getting started with LoopBack](http://docs.strongloop.com/display/LB/Getting+started+with+LoopBack) to create a LoopBack application.

Just enter:

```term
$ slc loopback
```

You'll be prompted to pick a name and directory for the new application; for example, if you entered `myapp` for the application and
directory name:

```
$ cd myapp
```
Update `package.json` to add the following line so the app will use the latest stable version of Node.js:

```term
...
    "engines": {
        "node": "0.10.x"
    }
...
```

Then create a Git repository and commit your code:

```term
$ git init
$ git add . 
$ git commit -m "init"
```

## Heroku setup

Create a Procfile in the root directory of your app that contains the following: 

    web: slc run 

Make sure you add the Procfile to your repository:

```term
$ git add Procfile 
$ git commit -m "adding Procfile"
```

### Get the buildpack

Login with the Heroku command line:

```term
$ heroku login
```

Create your Heroku app using the buildpack. When it completes, push to Heroku
master to complete the installation of StrongLoop on your dyno.

```term
$ heroku apps:create --buildpack https://github.com/strongloop/strongloop-buildpacks.git
$ git push heroku master
```

Test it out

```term
$ heroku open
```

### How to check your dashboard on Heroku
Once you have created your app, its time to look at the instrumentation. 
Navigate to the [Heroku dashboard](https://dashboard.heroku.com)
and find your app. Once you've found your app, click on **Heroku app dashboard** to
view the various dynos and add-ons for your app. Click on the StrongLoop add-on to view the StrongOps Control Panel.
The StrongLoop Ops dashboard is
accessible by clicking on the grey button "StrongOps Dashboard".

The dashboard can also be accessed via the CLI:

```term
$ heroku addons:open strongloop
Opening strongloop for sharp-mountain-4005…
```

## Run your app in a cluster

To run your application in a cluster, update the start command in the Procfile:

```term
$ web: slc run --cluster <n>
```

Where `<n>` is a postive integer indicating the number of worker processes to use.

Commit your changes and redeploy the app:

```term
$ git add Procfile
$ git commit -m "Started clustered app" Procfile
$ git push heroku master
```

Once you have set this up, you can control the cluster through the StrongLoop dashboard: simply click on the **Cluster** tab.

## Collect application metrics

To collect metrics to send to a StatsD server, update the start command in the Procfile:

```term
$ web: slc run --metrics <statsd-url>
```

Where `<statsd-url>` is the URL of your StatsD server with format `statsd:[//host[:port]][/scope]`.

Commit your changes and redeploy the app:

```term
$ git add Procfile
$ git commit -m "Collect metrics using strong-agent" Procfile
$ git push heroku master
```
For more information on how to use the StrongLoop Agent API to get performance metrics, see
[On-premises monitoring](http://docs.strongloop.com/display/SLA/On-premises+monitoring).

## Troubleshooting

After configuration, StrongOps is automatic. If you should experience any issues, please let us know immediately by
[email](mailto:callback@strongloop.com)

## Migrating between plans

**NOTE: Carefully manage the migration timing to ensure proper application function during the migration process.**

Use the `heroku addons:upgrade` command to migrate to a new plan.

```term
$ heroku addons:upgrade strongloop:newplan
-----> Upgrading strongloop:newplan to sharp-mountain-4005... done, v18 ($49/mo)
       Your plan has been updated to: strongloop:newplan
```

## Removing the add-on

Remove StrongOps with the following command.

**WARNING: This will destroy all associated data and cannot be undone!**

```term
$ heroku addons:remove strongloop
-----> Removing strongloop from sharp-mountain-4005... done, v20 (free)
```

## Support

Submit all StrongOps support and runtime issues via the [Heroku Support channels](support-channels).
Any non-support related issues or product feedback is welcome at [callback@strongloop.com](mailto:callback@strongloop.com). 
