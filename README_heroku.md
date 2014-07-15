### StrongLoop Suite Buildpack for Heroku 

StrongLoop Suite includes LoopBack, an open source mobile framework for creating RESTful, JSON, and other APIs. LoopBack ships with a mobile SDK and can be easily extended via community npm modules.

Also included in StrongLoop Suite is StrongOps, an operational console specifically for Node.js applications. StrongOps provides deep performance monitoring including CPU profiling, EventLoop stats, and more.

<h4> Prerequisites </h4>

<h5> Install StrongLoop tools </h5>

Install slc, the StrongLoop command line tool, with the following command: 
    $ npm install -g strong-cli

On some systems, you may need to run the command with system privileges: 
    $ sudo npm install -g strong-cli

This tool enables you to quickly create and scaffold LoopBack applications, and provides other capabilities. Follow the instructions in the next two sections to create and run the StrongLoop example and create your own LoopBack application.

<h5> Get the Heroku Toolbelt </h5>

Make sure you have a Heroku account and have installed the Heroku Toolbelt.
Login with the heroku command line:

    $ heroku login

<h5> Create your app </h5>
    
    $ cd myapp

You will need to init and commit your code:
    $ git init
    $ git add .
    $ git commit -m "init"

<h5> Heroku setup </h5>

Heroku apps require a Procfile. You’ll need to add this to the root of your app

Procfile:
web: slc run app.js

or if you want to start your app with clustering, 
web: slc run --cluster <no_of_workers> 

Make sure you add the Procfile to your repository:

    $ git add Procfile 
    $ git commit -m "adding Procfile"    

Get the buildpack

Create your Heroku app using the buildpack. When it completes push to heroku master to complete the installation of StrongLoop Suite on your dyno.

$ heroku apps:create --buildpack https://github.com/strongloop/strongloop-buildpacks.git

$ git push heroku master
The installation of the buildpack will register you for StrongOps monitoring. 

This will start your app with clustering enabled. If you want to monitor your app and supervise the cluster, you can create an account at strongloop.com.
Use the following command to generate an API key and save it to  strongloop.json  in the current directory:
$ slc strongops
Check in the file and redeploy your app. Login at strongloop.com and monitor your app. 

 
