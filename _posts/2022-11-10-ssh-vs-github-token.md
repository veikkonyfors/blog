---
layout: default
title:  "Ssh vs GitHub token with Android Studio and Eclipse"
description: "Accessing GitHub with Android Studio and Eclipse, using personal access token or ssh"
tag: Android & Kotlin
katex: true
---
# Ssh vs GitHub token with Android Studio and Eclipse

GitHub access is nowadays based on Personal Access Token, by default.  

Problem is, that token expires in a month or so and needs to be regenerated and reinstalled at IDE.
How to do that is not very intuitive or well documented for Android Studio nor Eclipse. And tends to vary between versions of IDE's.

I propose to make use of ssh-key based connection.  
But I'll document also token switching to some degree in the end.

## SSH based access

### Setting up ssh key pair

In order to use ssh protocol to connect to GitHub, you must have configured ssh at your workstation and at Github. Instructions to do that at [GitHub: connecting-to-github-with-ssh](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) are pretty intuitive. Please follow them.  

You can test ssh is working properly as follows:  

	pappa@pappa-ThinkPad-X270:~$ ssh -T git@github.com
	Hi veikkonyfors! You've successfully authenticated, but GitHub does not provide shell access.
	pappa@pappa-ThinkPad-X270:~$ 

### Switch to ssh connection

*Eclipse:*  
Project Explorer - your repository - Team - Remote - Configure Push to Upstream, enter Uri
ssh://git@github.com/\<youraccount\>/\<yourrepo\>  (without .git suffix!)

*Android Studio:*  
Git -> ManageRemotes - Git Remotes dialog: Edit Uri to
ssh://git@github.com/\<youraccount\>/\<yourrepo\> 	(without .git suffix!)


## Acces by personal access token

### Generate token at github
Go to https://github.com/settings/tokens and generate a token. You have to be logged on to GitHub.  
Regenerating token, once the previous has expired, goes the same way.  
Please note: repo, workflow, read:org and gist scopes are required for the generated key.
Copy the token for transfer it to you IDE.  

### Add token to Android Studio
If you already have GitHub integrated to your IDE using a previous token, but you need to take a new token into use, you will have to delete previous setting first and then creating a new. At least that was the only way I figured out how to do it.

Delete old setting:  
Git -> ManageRemotes in the menu bar.  
In the Git Remotes dialog, highlight your repo and press '-' to remove it.
One can locate Git Remotes dialog also from Git tab on bottom of the IDE, select >Remote and right click.
Of course, depending on version, the names and locations might differ.

Create new connection:
Git -> ManageRemotes, press '+',
enter Name for the repo and Url in form https://github.com/\<youraccount\>/\<reponame\>

Once you use this connection then, it presents a 'Log In to GitHub' dialog

<p style="text-align:center;">
<img src="../../../img/2022-11-10-ssh-vs-github-token/GitHub-Login-1.png" width="200" height="100"/>
</p>

Select 'Use Token' and paste the copied token when requested.
'Log In via GitHub . . .' seems to be for JetBrains IDE only.


### Add token into Eclipse
TBD

