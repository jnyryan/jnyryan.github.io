---
layout: post
title:  "NodeJS - What's it all about"
date:   2013-11-18 00:00:00
categories: playing-with-technology
tags: [nodejs]

---

NodeJs is a fairly popular technology at the moment that was invented to solve a very simple problem – Ryan Dahl it’s inventor just wanted to upload a file with an accurate progress bar. A humble beginning that developed quite nicely into a platform that “uses an event-driven, non-blocking I/O model that makes it lightweight and efficient, perfect for data-intensive real-time applications that run across distributed devices”. With JavaScript at it’s core it provides developers with the opportunity to develop applications with server and client side components written in the same language.  Under the covers it uses the JavaScript V8 runtime with Node wrapping around this engine providing additional functionality to build network applications. it’s written in C… nice and fast.
<linebreak>
It’s a nice sales pitch, but since it’s what I do, I thought I’d take a look at getting it up and running and see what it’s all about. First point to note is that it’s built on the JavaScript V8 runtime for which node provides a wrapper. Good to know that it’s foundation is a solid well tested engine, and also it’s written in C… nice and fast.

Now, NodeJS not a web framework, but libraries  exist for it and can be added to it. It also isn’t a all purpose language – it’s written specifically to solve the problems around building scalable network applications- recommended for Web Socket server like chat applications, and file upload clients … that work in a non blocking manner so that the files can be worked on while they upload. Also good for real-time data applications, like data feeds with ticker, news and pricing.

A significant point to note is that NodeJS is not multithreaded,  and code is written as if you’re dealing with a single threaded server. So understanding Blocking versus non-blocking code is important. To handle this it’s uses an EventLoop based on callbacks. This can be tricky to get used to at first and some times infuriating when trying to build workflows, but as you write more code the patterns become more obvious.

I’ve created a few code snippets to demonstrate how NodeJS works but have a more detailed practical example located in github at  [https://github.com/patchapps/nodejs-webapp-on-heroku](https://github.com/patchapps/nodejs-webapp-on-heroku)

In the examples below you can see a blocking and not blocking routine to read a file. The first will wait until the file contents are read to print “Done” to console, the second will print “Done” and then when the files is read, the callback ( or embedded closure) will be invoked to print out it’s contents. Note that both these files will be read at the same time and so will complete faster than the synchronous invocation

## Creating a quick but impressive example

{% highlight javascript %}
// synchronous file read
var f1= fs.readFileSync(‘myfile1.txt’) 
var f2= fs.readFileSync(‘myfile2.txt’) 
console.log(f1); 
console.log(f2); 
console.log(“Done!”); 

// asynchronous file read
var callback = function(err, contents){ console.log(contents);}
var f1= fs.readFileSync(‘myfile1.txt’, callback); 
var f2= fs.readFileSync(‘myfile2.txt’, callback); 
console.log(“Done!”);
{% endhighlight %}

So let’s create the simple web server and see what it does. Call the file below server.js

{% highlight javascript %}
//server.js
var http = require(‘http’); 
http.createServer(function(request, response) {})
	.listen(8080); 
response.writeHead(200); 
response.write("<html>Hi</html>"); 
response.end(); 
setTimeout(	function(){}, 5000); 
response.write("the server is running");

{% endhighlight %}

To run this app from a shell run “node server.js”

The code above uses the ‘http’ module, which creates a http server and listens from requests on port 8080. When the code is first, node creates a list of known events to listen for – in this case the ‘request’, ‘connection’ and ‘close’ events are registered. When it finishes executing the script it goes into an Event Loop, here it will listen for the registered events such as requests coming in – these in turn get added to an event queue and are executed one at a  time. When a request is received it invokes its response callback which sends a properly formed HTML packet back to the user. Not a massive amount of code to get a web server up and running is it?

## Node Packet Manager

Another nice feature is that nodejs comes with a packet manager called ‘npm’ or Node Packet Manager. This is an extremely handy tool for pulling down dependencies and allows you to encapsulate them in the application you are writing or install them globally for all your node application to use. 

The packages available are growing all the time, ranging from helper function libraries like “underscore.js” to full MCV frameworks like “express.js”. 

NPM comes with the Nodejs installation and new packages are installed using the command “npm install *packagename*”. It very smartly maintains version compatibility by dowloading the packages to a “nodes_modules” folder in each application. 

If you download a package it will have it’s own “node_modules” folder with it’s own dependencies – in this way versions conflicts are avoided. Packages can also be installed globally using the “-g” switch – however the local versions are always probed first.

##So what now? 

Well install NodeJS from [http://www.nodejs.org](http://www.nodejs.org/), read it’s API documentation and checkout the packages available from [https://npmjs.org](https://npmjs.org).

 
##Some very useful packages

	npm install -g underscore
	npm install -g supervisor
	npm install -g grunt
	npm install -g prettyjson
	npm install -g node-inspector
	npm install -g nodev
	npm install -g connect
	npm install -g forever
	npm install -g forever-monitor


- *Underscore* is a utility-belt library for JavaScript that provides a lot of the functional programming support that you would expect in core 
- *Node Supervisor* is used to restart programs when they crash. It can also be used to restart programs when a .js file changes. 
- *Grunt* is a javascript task runner 
- *PrettyJSON* - format json nicely 
- *Node Inspector* is a debugger interface for node.js using the Blink Developer Tools 
- *nodev* ssists with the running and debugging of node.js based applications in development. nodev launches node-inspector alongside your app, and will reload everything when files change 
- *Connect* is a middleware framework for node, shipping with over 18 bundled middleware and a rich selection of 3rd-party middleware 
- *Forever* A simple CLI tool for ensuring that a given script runs continuously 
- *forever-monitor* The core monitoring functionality of forever without the CLI 
