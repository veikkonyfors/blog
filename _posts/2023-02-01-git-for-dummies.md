---
layout: default
title:  "Git for dummies"
description: "Global Information Tracker tutorial"
tag: Unix
---

Turned out I knew very little of git, even if I have used it for years.
Trying to clarify basic matters here, for myself mainly.

# Storage hierarchy

## Local working copy
The first level, starting from developer's side, is the local working copy. It is maintained on your workstation's project directory.  
Once project is under git control, it is associated with a .git directory, which is typically located at the same system as project's local working copy. All required bits and peaces needed for git version control are maintained in this .git directory tree.

## Staging area
Next level, the stating area, is a middle ground between local working copy and local .git repository.  One can select mods to incorporate into next commit to local .git repo by adding those to stating area prior to commit. Only mods in stating area will be committed. Helps organizing you commits e.g. into logical groups.  
Stating area is actually incorporated in local .git repository itself, but as a separate logical entity to enable logical grouping for the mods in each commit.

## Local .git repository
I tend to locate my .git repository under my projects root directory. However, that's not probably obeying best practices, due to backup and other reasons.  
Eclipse suggests locating .git repository alongside project directory at the same level.  
One can always try to issue 'git rev-parse --git-dir'to try to find out where the .git directory is located, if it is not obvious.  
Local .git directory has a proprietary internal structure to maintain modification history in an efficient and flexible form. Unlike some other version control systems, e.g. scm and svn, git maintains modification information in packed, compressed and crypted formats like git pack and zlib. This makes browsing modification with standard text oriented tools impossible. Git tools exist to deal with these formats, like 'git unpack-objects' and 'git cat-file' but those are beyond standard use scope.  
Standard way of manipulating git repository involve use of commands like 'git add', 'git diff', 'git commit', 'git push' etc ...
GUI development environments, like Eclipse, Android Studio and PyCharm, hide these commands into their GUI.


## Remote git directory
Remote git directory makes colaboration with projects flexible, as remote repositories are located in internet (or alike) making them accessible world round.  
I mysel am using GitHub hosted services, but there a numerous alternatives for it or one could even maintain a remote git repository of one's own.


# Standard command line use

If you have made a change on your local file copy, you can find out what the changes are with 'git diff' command, issued at the project root directory, where the .git subdirectory lies.

To move a local working copy of a file to stating area, use 'git add' command. Once in stating area, 'git diff' no longer shows changes in local working copy.

'git status' shows:
- state of your local repository if compared to the remote one
- modified files not staged yet
- files in your staging area

