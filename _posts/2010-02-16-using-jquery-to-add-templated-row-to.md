---
title: "Using jQuery to add a templated row to a html table"
layout: "post"
uuid: "5793453007485010068"
guid: "tag:blogger.com,1999:blog-6842749499040869174.post-5793453007485010068"
date: "2010-02-16 22:53:00"
updated: "2010-06-16 14:06:15"
description: 
blogger:
    siteid: "6842749499040869174"
    postid: "5793453007485010068"
    comments: "0"
categories: playing-with-technology
tags: [jQuery]
author: 
    name: "Johnny"
    url: "http://www.blogger.com/profile/05733316879665781472?rel=author"
    image: "http://img2.blogblog.com/img/b16-rounded.gif"
---

I wanted a quick easy way of adding rows to a table - preferably by designing the layout in html and then copying to where i needed it and changing the elements values where needed. This took me longer to figure out than it should have - so I thought I'd share it.
<linebreak>

The snippet copies a row from one table and inserts it to the target table.

{% highlight html %}

<table id=“dataTable”>
</table>
<table id=“templateTable” cellspacing=“0” style=“display: none;”>
	<tr id=“templateRow”>
		<td id=“nameRow” class=“rowItem” width=“25%”>
			<a></a>
		</td>
		<td id=“positionRow” class=“rowItem” width=“60%”>
		</td>
		<td id=“numberRow” class=“rowItem” width=“15%”>
		</td>
	</tr>
</table>

<script type=“text/javascript” src=“http://code.jquery.com/jquery-latest.js”></script>
<script type=“text/javascript”>
(document).click(function() {
	addNewRow("mailto://johnny@here.com", "John Ryan", 	"Developer", "555 123456");
	addNewRow("mailto://johnny@here.com", "Bill Smith", 	"Developer", "555 768648");
	addNewRow("mailto://johnny@here.com", "Buck Rogers", 	"Developer", "555 675843");
	addNewRow("mailto://johnny@here.com", "Frank Wlliams", 	"Developer", "555 675843");
});

// Copy the template row and insert it to the target table.
function addNewRow(link, name, position,number){
var clonedRow = $('#templateRow').clone(true);
(“#nameRow a”, clonedRow).attr(“href”, link);
("#nameRow a", clonedRow).html(name);
(“#positionRow”, clonedRow).html(position);
("#numberRow", clonedRow).html(number);
(dataTable).append(clonedRow);
}
</script>

{% endhighlight %}