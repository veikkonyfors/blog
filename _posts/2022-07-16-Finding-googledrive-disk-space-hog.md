---
layout: default
title:  "Finding the disk space hog directories on googledrive"
description: "Find largest disk space consuming directories at Google Drive"
tag: Unix
---

## Finding the disk space hog directories on googledrive

### Introduction

Even though disk space is pretty cheap at cloud services nowadays, some are interested to keep cloud storage clean of waste. Few are even trying to get along with the initial free chunk of storage as long as possible.  
For people like that, I present a method to find out major disk space hogs in cloud. Handy for others as well, I would imagine.  
Hogs tend to be directories which either contain a few large files or tons of smaller ones at base level (i.e. not including subdirectories). For me these mostly are directories containing e.g. pictures and short videos of summer holidays, which I am used to gather in their own folders.  

Google Drive has currently initial 15GB of free storage, 100GB will be 1.99Eur/Month, 200GB 2.99Eur/Month and 2TB 9.99Eur/Month.  OneDrive and iCloud have similar plans. Among others.  
Initially I will cover Google Drive, but will be back with others as time permits.

Google itself provides a method to find largest individual files. At mydrive screen (https://drive.google.com/): 
- Hover the cursor over Storage summary on the lower left of the screen and click 
- you will be presented 'Files using Drive storage' screen
- Sort that into descending order by clicking 'Storage used' column header. 
- There you have the large files.

Unfortunately this does not reveal folders that have numerous not so big files. Like those folders of summer holiday photos.  

To find those you first have to mount Google Drive on a system of yours.  
Google Drive is a Fuse filesystem, one needs to install 'Google Drive Ocamlfuse' (google-drive-ocamlfuse) and related software to have it available.  

### Mounting Google Drive on Debian instance on Google Cloud Platform

I carried this out in my Debian instance at Google Cloud Platform by adhering to directions in these two links below   

[How to mount Google Drive on Linux &bull; Xmodulo.com](https://www.xmodulo.com/mount-google-drive-linux.html)  
[How to Install Google Drive Ocamlfuse on Debian &bull; tutorialforlinux.com](https://tutorialforlinux.com/2017/04/21/how-to-install-google-drive-ocamlfuse-on-debian-linux/)

Had to compose a bit to have a perfect hit. But that's what we most often have to do in the end. 

	
### Mounting Google Drive on Ubuntu 20.04 laptop

On Ubuntu installing google-drive-ocamlfuse is somewhat easier, using apt repository ppa:alessandro-strada/ppa.
	
	pappa@pappa-ThinkPad-X270:~$ sudo add-apt-repository ppa:alessandro-strada/ppa
	[sudo] password for pappa: 
	 Mount Google Drive on Ubuntu (via FUSE)
	 More info: https://launchpad.net/~alessandro-strada/+archive/ubuntu/ppa
	Press [ENTER] to continue or Ctrl-c to cancel adding it.
	
	Hit:1 http://fi.archive.ubuntu.com/ubuntu focal InRelease
	Ign:2 http://dl.google.com/linux/chrome-remote-desktop/deb stable InRelease                                                              
	Get:3 http://dl.google.com/linux/chrome/deb stable InRelease [1 811 B]                                                                   
	Get:4 http://ppa.launchpad.net/alessandro-strada/ppa/ubuntu focal InRelease [17,5 kB]                                                    
	Get:5 http://dl.google.com/linux/chrome-remote-desktop/deb stable Release [944 B]                     
	Hit:6 https://linux.teamviewer.com/deb stable InRelease                                                     
	Get:7 http://dl.google.com/linux/chrome-remote-desktop/deb stable Release.gpg [819 B]
	Get:8 http://security.ubuntu.com/ubuntu focal-security InRelease [114 kB]                 
	Get:9 http://dl.google.com/linux/chrome/deb stable/main amd64 Packages [1 095 B]
	Hit:10 http://ppa.launchpad.net/otto-kesselgulasch/gimp/ubuntu focal InRelease            
	Get:11 http://dl.google.com/linux/chrome-remote-desktop/deb stable/main amd64 Packages [713 B]
	Get:12 http://ppa.launchpad.net/alessandro-strada/ppa/ubuntu focal/main amd64 Packages [1 672 B]
	Get:13 http://ppa.launchpad.net/alessandro-strada/ppa/ubuntu focal/main Translation-en [1 196 B]
	Get:14 http://security.ubuntu.com/ubuntu focal-security/main amd64 Packages [1 631 kB]    
	Get:15 http://security.ubuntu.com/ubuntu focal-security/main i386 Packages [471 kB]
	Get:16 http://security.ubuntu.com/ubuntu focal-security/main Translation-en [277 kB]
	Get:17 http://security.ubuntu.com/ubuntu focal-security/main amd64 DEP-11 Metadata [40,8 kB]
	Get:18 http://security.ubuntu.com/ubuntu focal-security/main amd64 c-n-f Metadata [10,8 kB]
	Get:19 http://security.ubuntu.com/ubuntu focal-security/universe amd64 Packages [711 kB]
	Get:20 http://security.ubuntu.com/ubuntu focal-security/universe i386 Packages [557 kB]
	Get:21 http://security.ubuntu.com/ubuntu focal-security/universe amd64 DEP-11 Metadata [66,6 kB]
	Get:22 http://security.ubuntu.com/ubuntu focal-security/universe amd64 c-n-f Metadata [14,6 kB]
	Get:23 http://security.ubuntu.com/ubuntu focal-security/multiverse amd64 DEP-11 Metadata [2 464 B]
	Fetched 3 922 kB in 2s (1 595 kB/s)                                        
	Reading package lists... Done
	pappa@pappa-ThinkPad-X270:~$ sudo apt update
	Hit:1 http://fi.archive.ubuntu.com/ubuntu focal InRelease
	Ign:2 http://dl.google.com/linux/chrome-remote-desktop/deb stable InRelease                                        
	Hit:3 http://dl.google.com/linux/chrome/deb stable InRelease                                                                             
	Hit:4 http://ppa.launchpad.net/alessandro-strada/ppa/ubuntu focal InRelease                                                              
	Hit:5 http://dl.google.com/linux/chrome-remote-desktop/deb stable Release                                                                
	Hit:6 https://linux.teamviewer.com/deb stable InRelease                                                                                  
	Hit:7 http://ppa.launchpad.net/otto-kesselgulasch/gimp/ubuntu focal InRelease                         
	Hit:8 http://security.ubuntu.com/ubuntu focal-security InRelease                
	Reading package lists... Done
	Building dependency tree       
	Reading state information... Done
	6 packages can be upgraded. Run 'apt list --upgradable' to see them.
	pappa@pappa-ThinkPad-X270:~$ sudo apt install google-drive-ocamlfuse
	Reading package lists... Done
	Building dependency tree       
	Reading state information... Done
	The following packages were automatically installed and are no longer required:
	  libbs2b0 libfwupdplugin1 libllvm11 shim
	Use 'sudo apt autoremove' to remove them.
	The following NEW packages will be installed:
	  google-drive-ocamlfuse
	0 upgraded, 1 newly installed, 0 to remove and 6 not upgraded.
	Need to get 1 675 kB of archives.
	After this operation, 8 442 kB of additional disk space will be used.
	Get:1 http://ppa.launchpad.net/alessandro-strada/ppa/ubuntu focal/main amd64 google-drive-ocamlfuse amd64 0.7.30-0ubuntu1~ubuntu20.04.1 [1 675 kB]
	Fetched 1 675 kB in 1s (1 259 kB/s)                     
	Selecting previously unselected package google-drive-ocamlfuse.
	(Reading database ... 297841 files and directories currently installed.)
	Preparing to unpack .../google-drive-ocamlfuse_0.7.30-0ubuntu1~ubuntu20.04.1_amd64.deb ...
	Unpacking google-drive-ocamlfuse (0.7.30-0ubuntu1~ubuntu20.04.1) ...
	Setting up google-drive-ocamlfuse (0.7.30-0ubuntu1~ubuntu20.04.1) ...
	Processing triggers for man-db (2.9.1-1) ...
	pappa@pappa-ThinkPad-X270:~$ 
	pappa@pappa-ThinkPad-X270:~$ google-drive-ocamlfuse
	[10133:10133:0100/000000.439728:ERROR:sandbox_linux.cc(377)] InitializeSandbox() called with multiple threads in process gpu-process.
	Access token retrieved correctly.
	pappa@pappa-ThinkPad-X270:~$ mkdir ~/googledrive
	pappa@pappa-ThinkPad-X270:~$ google-drive-ocamlfuse ~/googledrive
	pappa@pappa-ThinkPad-X270:~$ cd googledrive/


### Finding the hog


After you have mounted Google Drive on your system, you just run the one-liner I have presented at [Finding the disk space hog](../../../2022/02/11/Finding-the-disk-space-hog.html) at the mountpoint where you mounted the drive. For most Unix boxes, including Linux, below works:

<!--find . -type d -exec du -sS {} \; &gt;/tmp/finddu.out 2&gt;/dev/null && cat /tmp/finddu.out <code>&#124;</code> sort -nr <code>&#124;</code> head-->

	find . -type d -exec du -sS {} \; >/tmp/finddu.out 2>/dev/null && cat /tmp/finddu.out | sort -nr | head

Sample output below.

	veikkonyfors@instance-1:~$ google-drive-ocamlfuse ~/googledrive/   # Mount the drive
	veikkonyfors@instance-1:~$ cd googledrive/  # cd there
	veikkonyfors@instance-1:~/googledrive$ find . -type d -exec du -sS {} \; >/tmp/finddu.out 2>/dev/null && cat /tmp/finddu.out | sort -nr | head -50
	5040689	./Google Photos
	2393937	./D610/pic/20110731_pätiälä
	1492605	./Pic/201808_sligo
	523633	./Pic/VeeraOTR022018
	369502	./.shared
	254384	./.shared/matkaaja
	239999	./Pic/whatsapp
	145551	./Pic/spania_teijo
	138355	./Pic
	107534	./Pic/Pappasusi_20082014
	100640	.
	95558	./Pic/Pappakatti
	91086	./Snd
	82478	./doc/qf
	67686	./doc/wheels
	61093	./D610/pic
	60448	./Pic/2003-11-27
	54435	./Pic/20140302_pappakalaksi
	54425	./D610/nyfors/dat/mov
	47527	./Pic/2003-09-06
	44821	./weto/src/cmd/meri/meritext/obsolete
	35757	./show
	35586	./Snd/ringtones
	34099	./D610/pic/20070614_kesalahti
	31958	./weto/src/cmd/meri/meritext
	25187	./doc
	22713	./weto/wrk/hil_koe
	21979	./huvi/paitsi/2019
	21709	./.shared/Week 2 Study material
	21434	./Pic/whatsapp/Sent
	19814	./weto/lib
	19128	./weto/src/cmd/hil_pp_new
	18659	./D610/nyfors/dev/setec
	18258	./weto/src/cmd/radar_server/save
	14829	./weto/src/cmd/meritele
	14512	./Pic/show
	13641	./huvi/dublin_sligo
	13506	./weto/src/cmd/gribsplit
	13255	./weto/etc/ila
	13113	./viware/wrk/EFM32_Zero_Gecko_ARM
	12831	./weto/src/cmd/getaws
	12124	./TIETO
	11037	./D610/pic/papankapula_200711225
	10856	./D610/nyfors/dev/iss/ekahau/.metadata/.plugins/org.eclipse.jdt.core
	10736	./D610/nyfors/dev/iss/ekahau/lib
	10718	./D610/pic/2004-02-16
	10403	./weto/src/cmd/postproc
	10387	./weto/src/cmd/ydinmasto
	10357	./D610/nyfors/dev/iss/moxa/.metadata/.plugins/org.eclipse.cdt.core
	10254	./D610/pic/20090717_pappa
	veikkonyfors@instance-1:~/googledrive$ 

