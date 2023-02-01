---
layout: default
title:  "Git for dummies"
description: "Global Information Tracker tutorial"
tag: Unix
---

Turned out I knew very little of git, even if I have used it for years.
Trying to clarify basic matters here, for myself mainly.

# Local working copy
The first level, starting from developer's side, is the local working copy. It is maintained on your workstation's project directory.  
On project root directory there is a .git subdirectory indicating git is taking care of version control for this project. All required bits and peaces needed for git version control are maintained in this .git directory tree.

If you have made a change on your local file copy, you can find out what the changes are with 'git diff' command, issued at the project root directory, where the .git subdirectory lies.
