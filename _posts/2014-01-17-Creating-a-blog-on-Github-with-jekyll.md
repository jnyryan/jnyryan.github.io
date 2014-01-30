---
layout: post
title:  "Creating a blog on Github Pages with jekyll"
date:   2014-01-17 00:00:00
categories: playing-with-technology
tags: [web-design]
---
I like simplicity and this is it in a nutshell. Create some text files and push them to GIT. How coos is that, managing your blog and deplying it using source control. Nerds say Y.E.S. Here's how to get a blog up and running in minutes - without paying for hosting or worrying about someone hacking your WordPress site.

#Getting a simple page up on Github Pages.
- Log into your Github account
- create a new repository called  *your_user_name.github.io*
- Add an index.html to the repository, commit it and push it up. Use the snippet below if your too lazy to type your own.

{% highlight html %}
<!DOCTYPE HTML>
<html>
<body>
	This is my page
</body>
</html>
{% endhighlight %}


- Now goto *your_user_name.github.io* and marvel at your technical prowess!

#Now for something more advanced - A Blog
Github also supports *Jekyll* which according to rubygems.org is a "simple, blog aware, static site generator. It allows you to set up a folder structure to manage 
- posts
- drafts
- includes
- styles
- layout

Then adding content is as simple as adding new files to the folder and pushing them to github. 

## Create a new github blog with Jekyll
Setting up a new blog is simple. Install the ruby gem, and initialise the site to create a default structure of files and folders. Then push it up to GitHub. you can also run a local server to test your site using jekylls *serve* option - adding **--draft** allows you to see anyting in the draft folder. Here's what to do:

	gem install jekyll
	jekyll new your_user_name.github.io
	cd your_user_name.github.io
	jekyll serve --draft
	
And just push it to github to test it!

##To create a post
Create new html or markdown file using the convention YYYY-MM-DD-this-is-the-title-of-my-post.html

Then create add content similar to the snippet. Notice at the top, is the *front matter* which describes the post.

	---
	layout: post
	title: My Blog
	categories: thoughts
	date	
	---
	Here are my thoughts for the day.


Now push this to your GitHub repo *your_user_name.github.io*

Play around with the files in the folder structure and you'll see very quickly what to do.