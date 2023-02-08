---
layout: default
title:  "Git for dummies"
description: "Global Information Tracker tutorial"
tag: Unix
---

Turned out I knew very little of git, even if I have used it for years.
Trying to clarify basic matters here below, for myself mainly. But why not for other dummies as well. ;-)

- [Storage hierarchy](#storage-hierarchy)
	- [Local working copy](#local-working-copy)	
	- [Staging area](#staging-area)
	- [Local .git repository](#local-git-repository)
		- [Location](#location)
		- [Structure](#structure)
		- [Manipulation](#manipulation)
	- [Remote git directory](#remote-git-directory)
- [Standard command line use](#standard-command-line-use)
	- [Differing lines](#differing-lines)	
	- [Moving files between storage levels](#moving-files-between-storage-levels)
	- [Status of repository](#status-of-repository)
		- [Overall status](#overall-status)
		- [Remote vs local status](#remote-vs-local-status)
	- ### Mods in remote not available locally yet

# Storage hierarchy

## Local working copy
The first level, starting from developer's side, is the local working copy. It is maintained on your workstation's project directory.  
Once project is under git control, it is associated with a .git directory, which is typically located at the same system as project's local working copy. All required bits and peaces needed for git version control are maintained in this .git directory tree.

## Staging area
Next level, the stating area, is a middle ground between local working copy and local .git repository.  One can select mods to incorporate into next commit to local .git repo by adding those to staging area prior to commit. Only mods in stating area will be committed. Helps organizing you commits e.g. into logical groups.  
Stating area is actually incorporated in local .git repository itself, but as a separate logical entity to enable logical grouping for the mods in each commit.

## Local git repository
### Location
I tend to locate my .git repository under my projects root directory. However, that's not probably obeying best practices, due to backup and other reasons.  
Eclipse suggests locating .git repository alongside project directory at the same level.  
One can always try to issue 'git rev-parse --git-dir'to try to find out where the .git directory is located, if it is not obvious.

### Structure
Local .git directory has a proprietary internal structure to maintain modification history in an efficient and flexible form. Unlike some other version control systems, e.g. scm and svn, git maintains modification information in packed, compressed and crypted formats like git pack and zlib. This makes browsing modification with standard text oriented tools impossible.

### Manipulation
Git tools exist to deal with these formats, like 'git unpack-objects' and 'git cat-file' but those are beyond standard use scope.  
Standard way of manipulating git repository involve use of commands like 'git add', 'git diff', 'git commit', 'git push' etc ...
GUI development environments, like Eclipse, Android Studio and PyCharm, hide these commands into their GUI.


## Remote git directory
Remote git directory makes colaboration with projects flexible, as remote repositories are located in internet (or alike) making them accessible world round.  
I mysel am using GitHub hosted services, but there a numerous alternatives for it or one could even maintain a remote git repository of one's own.


# Standard command line use
Below some common git commands to find out information on the state of repository.  
Commands are issued at the project repository directory, where the .git subdirectory lies.

## Differing lines
Use **git diff** command in it's various variations

### Between working copy and local repository

	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git diff
	diff --git a/bikes.txt b/bikes.txt
	index 16d38c8..db578de 100644
	--- a/bikes.txt
	+++ b/bikes.txt
	@@ -1,2 +1,2 @@
	 T250, GT550,  DR125, xv535, DR750, DR650, DR800, DR800, GPZ600, GSX750, 
	-FZR1000, R6, R1, GSXR600, R1, GSXR1000, GPZ1100, 10r, TL1000
	+FZR1000, R6, R1, GSXR600, R1, GSXR1000, GPZ1100, 10r, TL1000, KTM Duke 125
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$
	
Staged files are considered as being already in the local repo, no diffs listed.


### Between local repository and remote repository
**git diff \<remote_branch_name\>..\<local_branch_name\>**

	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git diff origin/main..HEAD
	diff --git a/bikes.txt b/bikes.txt
	index 16d38c8..db578de 100644
	--- a/bikes.txt
	+++ b/bikes.txt
	@@ -1,2 +1,2 @@
	 T250, GT550,  DR125, xv535, DR750, DR650, DR800, DR800, GPZ600, GSX750, 
	-FZR1000, R6, R1, GSXR600, R1, GSXR1000, GPZ1100, 10r, TL1000
	+FZR1000, R6, R1, GSXR600, R1, GSXR1000, GPZ1100, 10r, TL1000, KTM Duke 125
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ 

## Moving files between storage levels

### Working copy and staging area

Add mod to staging area: **git add**  

	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git add bikes.txt
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git diff
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ 

Unstage the mod: **git restore**

	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git restore --staged bikes.txt
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git diff
	diff --git a/bikes.txt b/bikes.txt
	index db578de..ae9a7e6 100644
	--- a/bikes.txt
	+++ b/bikes.txt
	@@ -1,2 +1,3 @@
	 T250, GT550,  DR125, xv535, DR750, DR650, DR800, DR800, GPZ600, GSX750, 
	-FZR1000, R6, R1, GSXR600, R1, GSXR1000, GPZ1100, 10r, TL1000, KTM Duke 125
	+FZR1000, R6, R1, GSXR600, R1, GSXR1000, GPZ1100, 10r, TL1000, KTM Duke 125,
	+KTM Duke 170
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ 
	
### Staging area to local repo
**git commit** 

	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git commit
	[master 56d080f] test
	 1 file changed, 1 insertion(+), 1 deletion(-)
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ 
	
### Local repo to remote repo
**git push** 


## Status of repository

### Overall status
**git status**

	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git status
	On branch master
	Your branch is ahead of 'origin/main' by 1 commit.
	  (use "git push" to publish your local commits)
	
	Changes to be committed:
	  (use "git restore --staged <file>..." to unstage)
		modified:   bikes.txt
	
	Changes not staged for commit:
	  (use "git add <file>..." to update what will be committed)
	  (use "git restore <file>..." to discard changes in working directory)
		modified:   bikes.txt
	
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$  
	
In the above we have 
- 1 local commit that has not been pushed to remote
- bikes.txt has been staged but not committed
- bikes.txt has changed in working tree

i.e. there's a discrepancy between working copy and the staged one.

If one wants to 
- keep staged and working copies distinct -> commit the staged mod first
- get rid of staged copy -> git restore --staged bikes.txt
- stage working copy overriding the previous staged one -> git add bikes.txt
- replace working copy with staged one -> git restore bikes.txt

### Remote vs local status
During the previous **git status**, we actually had a mod in remote repository of which the local repo was unaware of. To make local repo aware of remote changes, one has to issue **git fetch**.  
Afterwards the status shows we also have one remote change to be applied locally, if we so wish.

	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git fetch
	remote: Enumerating objects: 5, done.
	remote: Counting objects: 100% (5/5), done.
	remote: Compressing objects: 100% (3/3), done.
	remote: Total 3 (delta 2), reused 0 (delta 0), pack-reused 0
	Unpacking objects: 100% (3/3), 695 bytes | 347.00 KiB/s, done.
	From ssh://github.com/veikkonyfors/gitest
	   b83c2c6..197b291  main       -> origin/main
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ 


	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git status
	On branch master
	Your branch and 'origin/main' have diverged,
	and have 1 and 1 different commits each, respectively.
	  (use "git pull" to merge the remote branch into yours)
	
	Changes to be committed:
	  (use "git restore --staged <file>..." to unstage)
		modified:   bikes.txt
	
	Changes not staged for commit:
	  (use "git add <file>..." to update what will be committed)
	  (use "git restore <file>..." to discard changes in working directory)
		modified:   bikes.txt
	
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ 
	
In this situation, if we try to push out local repo to remote, we encounter a problem:

	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git push
	To ssh://github.com/veikkonyfors/gitest
	 ! [rejected]        main -> main (non-fast-forward)
	error: failed to push some refs to 'ssh://git@github.com/veikkonyfors/gitest'
	hint: Updates were rejected because the tip of your current branch is behind
	hint: its remote counterpart. Integrate the remote changes (e.g.
	hint: 'git pull ...') before pushing again.
	hint: See the 'Note about fast-forwards' in 'git push --help' for details.
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ 
	
	Even pull doesn't work:
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git pull
	error: Your local changes to the following files would be overwritten by merge:
		bikes.txt
	Please commit your changes or stash them before you merge.
	Aborting
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$
	
Lets commit first as suggested, with some preliminary steps:

	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git add bikes.txt
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git diff --staged
	diff --git a/bikes.txt b/bikes.txt
	index db578de..3f66725 100644
	--- a/bikes.txt
	+++ b/bikes.txt
	@@ -1,2 +1,9 @@
	-T250, GT550,  DR125, xv535, DR750, DR650, DR800, DR800, GPZ600, GSX750, 
	-FZR1000, R6, R1, GSXR600, R1, GSXR1000, GPZ1100, 10r, TL1000, KTM Duke 125
	+T250, GT550,  DR125, xv535, DR750, DR650, DR800, DR800, GPZ600, 2*GSX750, 
	+FZR1000, R6, R1, GSXR600, R1, GSXR1000, GPZ1100, 10r, TL1000, KTM Duke 125,
	+KTM Duke 170
	+kukkuu
	+miu
	+mau
	+iihahaa
	+ammuu
	+hau
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git commit
	[main b155cee] Pre merge
	 1 file changed, 9 insertions(+), 2 deletions(-)
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ 
	
Now let's see what was the difference between local and remote:

	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git diff origin/main..HEAD
	diff --git a/bikes.txt b/bikes.txt
	index ae7602e..3f66725 100644
	--- a/bikes.txt
	+++ b/bikes.txt
	@@ -1,2 +1,9 @@
	-T250, GT550,  -->TSR125<--, DR125, xv535, DR750, DR650, DR800, DR800, GPZ600, GSX750, 
	-FZR1000, R6, R1, GSXR600, R1, GSXR1000, GPZ1100, 10r, TL1000
	+T250, GT550,  DR125, xv535, DR750, DR650, DR800, DR800, GPZ600, 2*GSX750, 
	+FZR1000, R6, R1, GSXR600, R1, GSXR1000, GPZ1100, 10r, TL1000, KTM Duke 125,
	+KTM Duke 170
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ 

There was the TSR125 added on the remote, which was not locally available.
Thus I don't want to pull/merge to override with the remote copy.

Pushing local to remote won't work:

	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git push
	To ssh://github.com/veikkonyfors/gitest
	 ! [rejected]        main -> main (non-fast-forward)
	error: failed to push some refs to 'ssh://git@github.com/veikkonyfors/gitest'
	hint: Updates were rejected because the tip of your current branch is behind
	hint: its remote counterpart. Integrate the remote changes (e.g.
	hint: 'git pull ...') before pushing again.
	hint: See the 'Note about fast-forwards' in 'git push --help' for details.
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ 
	
One has to pull the remote first and then incoporate the local changes, then add, commit and push:

	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git pull
	Auto-merging bikes.txt
	CONFLICT (content): Merge conflict in bikes.txt
	Automatic merge failed; fix conflicts and then commit the result.
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ 

Try merge

	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git merge
	error: Merging is not possible because you have unmerged files.
	hint: Fix them up in the work tree, and then use 'git add/rm <file>'
	hint: as appropriate to mark resolution and make a commit.
	fatal: Exiting because of an unresolved conflict.
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git pull
	error: Pulling is not possible because you have unmerged files.
	hint: Fix them up in the work tree, and then use 'git add/rm <file>'
	hint: as appropriate to mark resolution and make a commit.
	fatal: Exiting because of an unresolved conflict.
	
Well, the pull changed it, see what we have now

	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git diff
	diff --cc bikes.txt
	index cb72779,ae7602e..0000000
	--- a/bikes.txt
	+++ b/bikes.txt
	@@@ -1,9 -1,2 +1,14 @@@
	++<<<<<<< HEAD
	 +T250, GT550,  TSR125, DR125, xv535, DR750, DR650, DR800, DR800, GPZ600, 2*GSX750, 
	 +FZR1000, R6, R1, GSXR600, R1, GSXR1000, GPZ1100, 10r, TL1000, KTM Duke 125,
	 +KTM Duke 170
	 +kukkuu
	 +miu
	 +mau
	 +iihahaa
	 +ammuu
	 +hau
	++=======
	+ T250, GT550,  TSR125, DR125, xv535, DR750, DR650, DR800, DR800, GPZ600, GSX750, 
	+ FZR1000, R6, R1, GSXR600, R1, GSXR1000, GPZ1100, 10r, TL1000
	++>>>>>>> 197b2912fba9c41a1f716a7d21ea33c38bb41c36
	
Let's do what was suggested, add + commit
	
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git add
	Nothing specified, nothing added.
	Maybe you wanted to say 'git add .'?
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git add bikes.txt 
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git diff
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git merge
	fatal: You have not concluded your merge (MERGE_HEAD exists).
	Please, commit your changes before you merge.
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git commit
	[main ec60227] Merge branch 'main' of ssh://github.com/veikkonyfors/gitest into main
	
And then merge?
	
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git merge
	Already up to date.
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$
	
Ahaa, merge combined local and remote to working copy. Now we just have to edit it how we wan't it to be. Then add, commit & push

	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ cat bikes.txt
	<<<<<<< HEAD
	T250, GT550,  TSR125, DR125, xv535, DR750, DR650, DR800, DR800, GPZ600, 2*GSX750, 
	FZR1000, R6, R1, GSXR600, R1, GSXR1000, GPZ1100, 10r, TL1000, KTM Duke 125,
	KTM Duke 170
	kukkuu
	miu
	mau
	iihahaa
	ammuu
	hau
	=======
	T250, GT550,  TSR125, DR125, xv535, DR750, DR650, DR800, DR800, GPZ600, GSX750, 
	FZR1000, R6, R1, GSXR600, R1, GSXR1000, GPZ1100, 10r, TL1000
	>>>>>>> 197b2912fba9c41a1f716a7d21ea33c38bb41c36
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$
	
After editing

	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ cat bikes.txt
	T250, GT550,  TSR125, DR125, xv535, DR750, DR650, DR800, DR800, GPZ600, 2*GSX750, 
	FZR1000, R6, R1, GSXR600, R1, GSXR1000, GPZ1100, 10r, TL1000, KTM Duke 125,
	KTM Duke 170

Add, commit and push

	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git add bikes.txt
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git commit
	[main ddb7198] Edited merge
	 1 file changed, 1 insertion(+), 11 deletions(-)
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git push
	Enumerating objects: 22, done.
	Counting objects: 100% (22/22), done.
	Delta compression using up to 4 threads
	Compressing objects: 100% (18/18), done.
	Writing objects: 100% (18/18), 1.72 KiB | 1.72 MiB/s, done.
	Total 18 (delta 11), reused 0 (delta 0)
	remote: Resolving deltas: 100% (11/11), completed with 2 local objects.
	To ssh://github.com/veikkonyfors/gitest
	   197b291..ddb7198  main -> main
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ 

Local and remote now the same

	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git diff origin/main..HEAD
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$

And as we wish it to be

	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ cat bikes.txt
	T250, GT550,  TSR125, DR125, xv535, DR750, DR650, DR800, DR800, GPZ600, 2*GSX750, 
	FZR1000, R6, R1, GSXR600, R1, GSXR1000, GPZ1100, 10r, TL1000, KTM Duke 125,
	KTM Duke 170

pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$

### Find out staged files
**git diff --staged** 

	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git diff --staged
	diff --git a/bikes.txt b/bikes.txt
	index db578de..ae9a7e6 100644
	--- a/bikes.txt
	+++ b/bikes.txt
	@@ -1,2 +1,3 @@
	 T250, GT550,  DR125, xv535, DR750, DR650, DR800, DR800, GPZ600, GSX750, 
	-FZR1000, R6, R1, GSXR600, R1, GSXR1000, GPZ1100, 10r, TL1000, KTM Duke 125
	+FZR1000, R6, R1, GSXR600, R1, GSXR1000, GPZ1100, 10r, TL1000, KTM Duke 125,
	+KTM Duke 170
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ 

### There's a change in local repo not yet in remote
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$ git status
	On branch master
	Your branch is ahead of 'origin/main' by 1 commit.
	  (use "git push" to publish your local commits)
	
	nothing to commit, working tree clean
	pappa@pappa-ThinkPad-X270:~/wrk/gitestws/gitest$
