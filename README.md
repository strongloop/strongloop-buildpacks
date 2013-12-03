### StrongLoop Suite Buildpack for Pivotal's CloudFoundry

StrongLoop Suite includes LoopBack, an open source mobile framework for creating RESTful, JSON, and other APIs. LoopBack ships with a mobile SDK and can be easily extended via community npm modules.

Also included in StrongLoop Suite is StrongOps, an operational console specifically for Node.js applications. StrongOps provides deep performance monitoring including CPU profiling, EventLoop stats, and more.

Finally, StrongLoop Suite is built on top of StrongNode, a supported package of Node.js. StrongNode contains certified and tested modules for developing, testing and maintaining enterprise Node.js applications. The StrongNode package also includes advanced debugging, clustering, support for private npm registries and other enterprise tools

<h4> Prerequisites </h4>

<h5> Get StrongLoop Suite </h5>

Download and install [StrongLoop Suite](http://www.strongloop.com/strongloop-suite/downloads/)

<h5> Get the Cloud Foundry command line tool </h5>

Create an account on http://run.pivotal.io/

Install the cf command line tools, and check their official CLI guide here:
http://docs.cloudfoundry.com/docs/using/managing-apps/cf/

    $ gem install cf
     
Login into the Cloud Foundry PaaS:

    $ cf target api.run.pivotal.io
    $ cf login

<h4> How to use the Strongloop Suite </h4>

Quickly get started on how to use StrongLoop Suite, StrongNode and StrongOps by heading over to [Quickstart] (http://docs.strongloop.com/strongops/#quick-start)
Or 
Explore the entire [documentation](http://docs.strongloop.com/).

<h4> Deploying on Cloud Foundry </h4>

Once you have created a sample app, please also add a **Procfile** in the root folder of your app (same place as **package.json**).
The only line in this **Procfile** should be the start command of your web app.

For example:

    $ cat Procfile
    web: slc run .

When you are satisfied that all's ok, get ready to push your app to Cloud Foundry.

There is a trick to speed up your push process and avoid possible conflict - remove local **node_modules** before push:

    $ rm -rf node_modules
    
    $ cf push --buildpack=https://github.com/strongloop/dist-paas-buildpack

Note:  The first time you run cf push, you will need to specify all the
       parameters - this will create a new application at Cloud Foundry.
       Default values will work fine if you just keep pressing Enter :)

Subsequent pushes just need the `cf push` command - you only need to
specify all those options the first time you create the app (push).

This will now download and configure StrongLoop Suite on Cloud Foundry,
install the dependencies as specified in the sample application's
package.json file (or npm-shrinkwrap.json if one exists).

That's it, you can now checkout your application at the
app url/domain you set for your Cloud Foundry app.

