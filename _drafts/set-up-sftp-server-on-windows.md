---
layout: post
title:  "Set up an SFTP Server on Windows"
date:   2014-01-23 00:00:00
categories: playing-with-technology

---

Unfortunately, Windows does not come with a sFTP option in Internet Information Server so you will need to install third party software to get this up and running. The good news is, is that it is trivially easy. I use [FreeSSHd]

##First setup a folder and user
- Create a new user in Computer Management called
	- TestFreeSshUser with password FreeSshUserPwd
- Create a new folder called
	- c:\TestFreeSsh
	- Add the user to the folder and give them read/write access

## Configure FreeSSHd for username password
- SHH Tab: Choose the listen address to be the public IP Address of your server
- Authentication Tab: 
	- Password authentication=Allowed
	- Public Key authentication=disabled
- SFTP Tab: set directory to share
- Users Tab: 
	- Add a user who has access to the folder 
	- Check the SFTP tag
- Server Status Tab: Click to start the SSH Server

##Troubleshooting:

How to resolve "You don't have administrator rights! freeSSHd will close!" error message while launch freeSSHd? This [troubleshoot link] has a solution.

[FreeSSHd]: http://www.freesshd.com
[troubleshoot link]: http://osskb.blogspot.ie/2013/10/how-to-resolve-you-dont-have.html
