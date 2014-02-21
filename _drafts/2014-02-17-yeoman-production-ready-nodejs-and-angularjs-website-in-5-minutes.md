---
layout: post
title:  "Yeoman: Production ready nodejs and anjularjs website in 5 minutes"
date:   2014-02-17 10:43:00
categories: playing-with-technology
description: 
tags: [web, nodejs, design, development]

---

Getting your app from a playground state to a production ready application is usually a project in itself. So why not just cut out that part and start with a production ready set-up. Enter Yeoman. It's a generator like any other but scaffolds up your website and packages it ready-to-deploy.



``` bash
# install dependancies
npm install -g yo
npm install -g generator-webapp
npm install -g generator-angular

# scaffold out a AngularJS project
yo angular
# run tests
grunt test
# run in development server
grunt serve
# build application for deployment
grunt

```