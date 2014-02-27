---
title: "Changing the Powershell prompt"
layout: "post"
uuid: "3739848345035981201"
guid: "tag:blogger.com,1999:blog-6842749499040869174.post-3739848345035981201"
date: "2010-02-25 13:19:00"
updated: "2012-06-08 14:46:28"
description: 
blogger:
    siteid: "6842749499040869174"
    postid: "3739848345035981201"
    comments: "0"
categories: playing-with-technology
tags: [Powershell]
author: 
    name: "Johnny"
    url: "http://www.blogger.com/profile/05733316879665781472?rel=author"
    image: "http://img2.blogblog.com/img/b16-rounded.gif"
---

I wanted a way to change the powershell prompt, in particular to:
- Display the current path in the Shell window
- Change the prompt to “[LineNumber]:”
- Show the stcck level when “pushd” is used

Then a colleague showed me this.
<linebreak>
Add the following function to your current profile - it’s an override for the prompt method:

{% highlight bash%}
function prompt {

#the old script...

#function prompt { "$" }

# FIRST, make a note if there was an error in the previous command
$err = !$?

# Make sure Windows and .Net know where we are (they can only handle the FileSystem)
[Environment]::CurrentDirectory = (Get-Location -PSProvider FileSystem).ProviderPath

# Also, put the path in the title ... (don't restrict this to the FileSystem
$Host.UI.RawUI.WindowTitle = "> {0} ({1})" -f $pwd.Path,$pwd.Provider.Name

# Determine what nesting level we are at (if any)
$Nesting = "$([char]0xB7)" * $NestedPromptLevel

# Generate PUSHD(push-location) Stack level string
$Stack = "+" * (Get-Location -Stack).count

# my New-Script and Get-PerformanceHistory functions use history IDs
# So, put the ID of the command in, so we can get/invoke-history easier
# eg: "r 4" will re-run the command that has [4]: in the prompt
$nextCommandId = (Get-History -count 1).Id + 1

# Output prompt string
# If there's an error, set the prompt foreground to "Red", otherwise, "Yellow"
if($err) { $fg = "Red" } else { $fg = "Yellow" }

# Notice: no angle brackets, makes it easy to paste my buffer to the web
Write-Host "[${Nesting}${nextCommandId}${Stack}]:" -NoNewLine -Fore $fg

return " "
}
{% endhighlight%}
	
The easiest way to do this is:

1. In PS type “$profile” this will show you the location of the current active profile
2. Open that file in notepad and paste the function above into it
3. In PS type “.$profile” to reload the altered profile
