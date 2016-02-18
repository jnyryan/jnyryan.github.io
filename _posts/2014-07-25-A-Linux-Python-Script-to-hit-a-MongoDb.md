---
title: "A Linux Python Script to hit a MongoDb"
layout: "post"
date: "2014-07-25 00:00:00"
updated: "2014-07-25 00:00:00"
description: "A Linux Python Script to hit a MongoDb"
categories: development
tags: [python, mongodb, development]
---

The life of a polygot programmer is never done. Changing  from language to language frequently can leave heads muddled and hair tousled. So whenever something takes me longer than it should, either due to complexity or hangover - I tend to write it up either in a [gist](https://gist.github.com/) or blog post. So here's one I struggled with for a while and it's not that hard.  

I wanted to create a quick script to hit a [MongoDb](https://www.mongodb.org/) database. "But this is not a difficult task" I hear some say. My issue was one of tools rather than code. I spend a lot of my time switching between .Net, nodejs, bash and ruby. None of which i find good for small scripts either due to portability, setup or the programming style. I wanted to find a solution that one I bootstrapped I would be able to do similar scripts in minutes. So my time was spent debating the pros and cons of various scripting languages over implementing the few lines of code. Eventually I settled on *python*, mainly because I am very amateur at it and figured it's a great tool for little jobs like this.

First, I assume you have MongoDb somewhere, in this case installed on your local server.  

Now if you don't have pythong installed, well install it using [Distribute](http://packages.python.org/distribute/), the python setup manager.    

``` bash
curl -O http://python-distribute.org/distribute_setup.py
python distribute_setup.py    
easy_install pip  
```

We're also going to install pymongo, a package for accessing MongoDB.
``` bash
python -m pip install pymongo
```

And finally here's some python to hit the database:    

``` python
import pymongo    
connection = pymongo.Connection("localhost", 27017)    
db = connection.test    
db.name    
db.my_collection.save({"Name": "John"})  
db.my_collection.save({"Name": "Frank"})
db.my_collection.save({"Name": "Bill"})   
db.my_collection.find_one()    
for item in db.my_collection.find(): print item["Name"]
```
