---
layout: post
title:  "Getting up and running with Heroku"
date:   2013-01-18 00:00:00
categories: playing-with-technology
tags: [Cloud, Development, Heroku, Technology]

---

Feeling a little overwhelmed with all the various Cloud technologies around these days? This post is a quick introduction that will explain a bit about Heroku and show you how to get a website up and running on it in a matter of minutes.

Well, what is Heroku?

Heroku is a Platform as a Service (PaaS) Cloud implementation, meaning that like other PaaS clouds


(e.g. Microsoft’s Azure) it provides a base architecture that you can build your applications on and deploy them to. This architecture is called the Heroku Stack, a complete deployment environment including the base operating system, the language runtime and associated libraries. The current stack called Celderon Cedar and is based on Ubuntu 10.04.  It’s onto this stack that you put your web or worker applications or in Heroku talk, slugs which are bundles of your source, fetched dependencies, the language runtime, and compiled/generated output of the build system which are ready for execution.

The powerful nature of this implementation is the number of popular technologies it supports. Applications can be built using using Java, Node,js, Ruby, Rails, Python, Scala, Closjure and many more. A deployment is simply a push of the slug to the Git repository that underpins you application.

Scalability is achieved through “Dynos”, which can be looked on as generously sized isolated processes rather than the number of virtual or physical servers. Increasing the number of Dynos that host your application is a simple matter of using the slider to up the allocation… and the price.

Developers Note:  a single Dyno is free, so great to play with. It does however go to sleep after inactivity to is not always suitable for production applications, but is nice to have.

![heroku](../img/heroku1.png?raw=true)

###Creating a Heroku Web Application

We’re going to create a very simple but good looking website using Ruby. All this will do is display a static page like this one patchapps-webapp-sinatra.herokuapp.com. All website code was created from the HTML5 templates available on www.initializr.com.

###First get setup

Create an account by logging on to https://get.heroku.com/ and following the “Sign up for Heroku”
Get the tools by installing the Heroku Toolbelt for your development operating system.
Login to Heroku

{% highlight bash %}
	
$ heroku login
Enter your Heroku credentials.
Email: username@domain.com
Password (typing will be hidden):
Authentication successful.
{% endhighlight %}
	
###Create an Application

Using the tools downloaded and installed earlier we will create a new app with the Heroku create command. This will create an application in your Heroku account with a Git repository underneath it. If you do not supply a name, a default one will be provided.

{% highlight bash %}

$ heroku create
Creating stormy-shelf-5302... done, region is us
http://stormy-shelf-5302.herokuapp.com/ | git@heroku.com:stormy-shelf-5302.git

{% endhighlight %}

That's it. If you browse to the location given then you'll see the default site set up. You can now push html to this to create a static site or go futther and create a *nodejs* or *ruby* site to give more flexibility and create a dynamic site.


