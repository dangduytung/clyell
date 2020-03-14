---
layout: page
title: "Heroku"
permalink: /heroku/
---

##### 1. Install library
~~~
npm install express  --save
npm install nodemon  --save
~~~

##### 2. Create file server.js
~~~
const path = require("path");
const express = require("express");
const app = express();
app.use(express.static(__dirname + '/angular-build'));
app.get('/*', function(req,res){
res.sendFile(path.join(__dirname, 'angular-build', 'index.html'))
});
// Start the app by listening on the default Heroku port
app.listen(process.env.PORT || 8080);
~~~

##### 3. Change
~~~
"start": "nodemon server.js"            # Change in package.json
"engines": {                            # Change in package.json
    "node" : "~version",                # Check version : node -v
    "npm" : "~version"                  # Check version : npm -v
}
"outputPath": "angular-build"           # Change in angular.json
~~~

##### 4. Build
~~~
ng build                                # Build to folder angular-build
~~~

##### 5. Heroku
~~~
# Install Heroku CLI
https://devcenter.heroku.com/articles/heroku-cli#download-and-install

# Login
heroku login

# Initialize
git init
heroku git:remote -a angular-app-deploy

# Check
heroku buildpacks             # First, ensure that your application is using the heroku/nodejs buildpack
https://dashboard.heroku.com/apps/{app}/activity    # Check activity

# Deploy
git add .
git commit -am "initial commit deploy"
git push heroku master

# Other
heroku git:clone -a [app]           # Clone
~~~