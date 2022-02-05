---
layout: default
title:  "Finding the disk space hog"
---


Pretty often I find myself in situation where the disk space on my MacBook air is running out. SSD disk is only 120GB.
The same goes on on my Lenovo Ubuntu laptop, even if the disk is a bit bigger there. I guess each and everyone has had the same problem over the times.

Routinely running production systems have procedures in place to clean up unessential information to release disk space.
But even there, every now and then it may happen disk space is running short. Pretty normal quick fix a'la ITIL is to add disk space.
At some point though, the support staff need to sort out is it just the businesses running better than ever requiring additional disk space,
or is there a disk space HOG around.

What can one do? One should dig up the space HOG.

In my experience the issue can be two fold: There can be some huge files around, or there can be tons of small files accumulated somewhere.
In both cases those should be found somehow.

In Unix systems, du command is most often used to detect the problem spots with disk space. Du alone is a bit laborious though.
One need to iterate sometimes quite a few times to find the spot. That's because of du's recursive nature of incorporating the whole directory subtree into total amount.

What I have learnt is that one really should pinpoint directories individually, or separately, how much of disk space is used by flat files in each.
Could be HUGE file or a few, or could be tons of smaller ones not being regularly cleaned up.

Below Unix oneliner accomplishes exactly that

find . -type d -exec du -sS {} \; <code>&#124;</code> sort -nr <code>&#124;</code> head

Unfortunately not all Unix systems have du with -S option available natively (S for separate). 
E.g. MacOSX is based on BSD (Berkeley Software Distribution), where du doesn't recognize -S. For such systems, below a bit more cumbersome bash oneliner will do the job. Requires Perl though.

NOTE!!!!
Copy pasting the below command into the command line doesn't seem to work currently. Need to sort out why.

IFS=$'\n'; for i in $(find . -type d); do cd $i;find . -maxdepth 1 -type f -exec du {} \; <code>&#124;</code> cut -f 1 -d' ' <code>&#124;</code> perl -ne'$s=<>; while(<>) {$s+=$_;} chomp $s; print "$s "'; pwd; cd -; done  <code>&#124;</code> grep ^[0-9] <code>&#124;</code> sort -nr <code>&#124;</code> head

Sample below. Having a look on the first one revealed thousands of left over cached files from skype. Suspecting the second one is similar case from Chrome.

Veeras-Air:~ pappa$ IFS=$'\n'; for i in $(find . -type d); do cd $i;find . -maxdepth 1 -type f -exec du {} \; | cut -f 1 -d' ' | perl -ne'$s=<>; while(<>) {$s+=$_;} chomp $s; print "$s "'; pwd; cd -; done  | grep ^[0-9] | sort -nr | head
709544 /Users/pappa/Library/Caches/com.skype.skype/fsCachedData
609384 /Users/pappa/Library/Caches/Google/Chrome/Default/Cache/Cache_Data
476600 /Users/pappa/Library/Application Support/Skype/live#3aveikkonyfors/media_messaging/emo_cache_v2
447328 /Users/pappa/Downloads
425272 /Users/pappa/Library/Application Support/Skype/veikkonyfors/media_messaging/emo_cache_v2
410456 /Users/pappa/Library/Caches/Google/Chrome/Default/Code Cache/js
97648 /Users/pappa/Library/Application Support/Google/Chrome/Default/Extensions/fahmaaghhglfmonjliepjlchgpgfmobi/1.399.2_2/polymer/miniplayer_polymer
97296 /Users/pappa/Library/Caches/com.apple.helpd/SDMHelpData/AppleExtra/English
94664 /Users/pappa/Library/Mail/V4/923DC53A-62A7-42CB-B119-1BEA8FAB7EBC/[Gmail].mbox/All Mail.mbox/01BC001E-D7A3-4209-9D21-24643F0B0B0E/Data/2/Messages
91808 /Users/pappa/Library/Application Support/Google/Chrome/Default/Extensions/fahmaaghhglfmonjliepjlchgpgfmobi/1.399.2_2/polymer/miniplayer_polymer_v2
Veeras-Air:~ pappa$ 
