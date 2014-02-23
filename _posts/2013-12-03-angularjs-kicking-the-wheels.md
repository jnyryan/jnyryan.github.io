---
layout: post
title:  "AngularJS: Kicking the tyres"
date:   2013-12-03 00:00:00
categories: playing-with-technology
tags: [angularjs, nodejs]
---

AngularJS is a fairly nifty framework that’s pitched as “HTML enhanced for web apps”. It’s designed to fill some of the gaps that HTML leaves when declaring dynamic content in web-applications, like improving managing dynamic views and extending the HTML vocabulary for applications. The overall outcome is a very well structured set of libraries that really speed up development and reduce the amount of code that needs to be written to achieve some finicky UI tasks.
<linebreak>
I decided to take it for a test drive and see how long it would take me to write a very simple web application that retrieves data from RESTful service and allows it to be displayed and filtered on the client. The answer -all in, it must have taken me an hour to get this up and running. I was very impressed with the level of documentation available and the ease with which I could apply it. **The full listing can be seen on [https://github.com/patchapps/angularjs-node]()**. The files of interest are under the Public folder, i did wrap this in a nodeJs project. For those who don’t know NodeJS, you can simply copy the Public folder to any web server and hit public/views.index.html

So What is Angular? At it’s most simple it’s a library or javascript file that you include in your html page, that gives you loads of extra functionality. Here’s a basic HTML page with angularJS included.

{% highlight html %}
<!DOCTYPE html> 
<html> 
  <head> 
  <title>John Ryans angularJS with nodejs kickstart</title> 
</head> 
<body> 
    <div ng-app="myApp"> 
        <input type="text" ng-model="data.message"> 
        <h1>{{item.name}}</h1> 
  </div> 
  <script type="text/javascript"
   src="https://ajax.googleapis.com/ajax/libs/angularjs/1.0.1/angular.min.js">
   </script> 
</body> 
</html>
{% endhighlight %}


In this snippet, you will see three things that do not appear in an ordinary html page.When the page loads, the angularJS library is kicked off and looks for directives. The “ng-app” directive tells it that everything in this div belongs to this named App called myApp. The “ng-model” directive is allowing us to set up a data binding with it’s corresponding bound item in the curly braces. This app when run will echo anything typed into the text box into the H1 – that’s pretty neat for no code!

AngularJS also allows for us to create controllers and bind them to html elements, passing data around the system. In this example we see a div bound to a controller that passes data to it and displays it in a table. The script creates a JSON object and passed it back to the view which binds it to the DIV. Still neat for a few lines of code!

{% highlight html %}
<div ng-controller="TestStaticDataCtrl"> 
    <div class="panel">Search : <input type="text" ng-model="searchText"> </div> 
        <table class="panel" width=100%> 
            <thead> 
                <tr> 
                    <td>Name</td> 
                    <td>Year</td> 
                </tr> 
            </thead> 
            <tr ng-repeat="item in movieData.items"> 
                <td>{{item.name}}</td> 
                <td>{{item.year}}</td> 
            </tr> 
        </table> 
    </div> 
</div>

<script> 
function TestStaticDataCtrl($scope, MovieData){ 
    var MovieData = {}; 
    MovieData.items = [ 
        { name: "Monsters Inc 2", year: "2013" }, 
        { name: "Star Wars", year: "1977" }, 
        { name: "Toy Story", year: "1977" },   
    ] 
  $scope.movieData = MovieData; 
} 
</script>
{% endhighlight %}

That’s just a quick introduction to AngularJS, there is ton to learn and use. A great resource i found and from which i took my examples is [http://egghead.io/lessons](). 

Enjoy.