---
layout: default
title:  "Finding the disk space hog directories on googledrive"
description: "Find largest disk space consuming directories at Google Drive"
tag: Unix
---

## Finding the disk space hog directories on googledrive

Even though disk space is pretty cheap at cloud services nowadays, some are interested to keep cloud storage clean of waste. Few are even trying to get along with the initial free chunk of storage as long as possible.  
For people like that, I present a method to find out major disk space hogs. Handy for others as well, I would imagine.  
Hogs tend to be directories which either contain a few large files or tons of smaller ones at base level (i.e. not including subdirectories). For me these tend to be directories containing e.g. pictures and short videos of summer holidays, which I tend to gather in their own folders.  

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
I carried this out in my Debian instance at Google Cloud Platform by adhering to directions in these two links below   

[How to mount Google Drive on Linux &bull; Xmodulo.com](https://www.xmodulo.com/mount-google-drive-linux.html)  
[How to Install Google Drive Ocamlfuse on Debian &bull; tutorialforlinux.com](https://tutorialforlinux.com/2017/04/21/how-to-install-google-drive-ocamlfuse-on-debian-linux/)

Had to compose a bit to have a perfect hit. But that's what we most often have to do in the end. 

After that, you just run the one-liner I have presented at [Finding the disk space hog](../../../2022/02/11/Finding-the-disk-space-hog.html) at the mountpoint where you mounted the drive. For most Unix boxes, including Linux, below works:

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
