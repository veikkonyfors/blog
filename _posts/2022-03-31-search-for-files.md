---
layout: default
title:  "Search for files"
description: "Search for files containing given string through the whole directory tree"
tag: Unix
---

## Search for files

Have you ever misplaced or lost a file that you know you have in your computer somewhere. Containing specific sentences or keywords you know that exist there. But you just can't find where in the world the file lies on the disk. I surely have been in that circumstance quite a few times.

Of course you can search using standard Unix commands find and grep, piped one after each other to see the file surely is there somewhere. But the problem remains, you don't know where. One has to do a bit more to find out the location.

Most linux distributions have "grep -r" or rgrep available, that show the location as well. But other Unix systems seldomly have it natively available.  
For those system one can use the below one-liner to do the thing.  
It also has a few advantages over the rgep, for which reason I make use of this one-liner also in Linux systems.


find . -type f ! -name &apos;*.swp&apos; -exec grep -I -q . {} \; -print |
xargs -i{} perl -lne &apos;print &quot;$ARGV: $_&quot; if /ViW..e/&apos; {} |
grep -v .metadata  

  
Sample:  
pappa@pappa-ThinkPad-X270:~/wrk$ find . -type f ! -name '*.swp' -exec grep -I -q . {} \; -print | xargs -i{} perl -lne 'print &quot;$ARGV: $_&quot; if /ViW..e/' {} | grep -v .metadata  
./ihop_jupyterlab/ihop_sent.py: # 26.10.2021 VN/ViWare  
./ihop_jupyterlab/ihop.py: # 26.10.2021 VN/ViWare  
./ihop_jupyterlab/ihop.ipynb:     "# 26.10.2021 VN/ViWare\n",  
./ihop_jupyterlab/.ipynb_checkpoints/ihop_sent-checkpoint.py: # 26.10.2021 VN/ViWare  
./ihop_jupyterlab/.ipynb_checkpoints/ihop-checkpoint.ipynb:     "# 26.10.2021 VN/ViWare\n",  
./ihop_jupyterlab/.ipynb_checkpoints/ihop_org-checkpoint.py: # 26.10.2021 VN/ViWare  
./ihop_jupyterlab/ihop_org.py: # 26.10.2021 VN/ViWare  
./githubpagesws/veikkonyfors.github.io/hybrid.html: ,<a href="#void" title="ViWare Oy" style="color:black;">ViWare</a>  
./githubpagesws/blog/_posts/2022-03-31-search-for-files.md: xargs -i{} perl -lne 'print "$ARGV: $_" if /ViW..e/' {} |  
./eclws/util/senseword/senseword.py:     VN/ViWare 20211201  
./eclws/util/senseword/main.py:     VN/ViWare 20211201  
./eclws/util/shell/oneliners.md: \# Pipes each file to xargs running a perl one-liner to print path+line containing ViWare  
./eclws/util/shell/oneliners.md: \# Searched string can be a RegExp, e.g. /ViWa..e/ would find ViWare lines as well.  
./eclws/util/shell/oneliners.md:   xargs -i{} perl -lne 'print "$ARGV: $_" if /ViWare/' {} | \  
./eclws/util/shell/frgrep.sh: #         © VN/ViWare     12.1.2022           frgrep.sh          Original 20th Century  
./eclws/util/shell/frgrep.sh: #         find . -type f ! -name '*.swp' | xargs -i{} perl -lne 'print "$ARGV: $_" if /ViWare/' {}  
./eclws/util/shell/frgrep.md: \#                © VN/ViWare     12.1.2022           frgrep.sh          Original 20th Century  
./eclws/util/shell/frgrep.md: \#                find . -type f ! -name '*.swp' | xargs -i{} perl -lne 'print "$ARGV: $_" if /ViWare/' {}  
pappa@pappa-ThinkPad-X270:~/wrk$ 

Explained:    
Finds non-binary flat files from current directory tree with name not ending to .swp  
Pipes each file to xargs running a perl one-liner to print path+line containing words matching regexp  "ViWa..e"  
Finally skipping lines containing .metadata using grep -v , as we do not want to see the huge number of files in metadata of some IDE.  
