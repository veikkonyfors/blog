---
layout: default
title:  "Using Dokka"
description: "How to document Kotlin modules in Android Studio"
tag: Android & Kotlin
katex: true
---

# Using Dokka

Wanted to document my Kotlin modules.  

Simplest way was to incorporate [KDoc](https://kotlinlang.org/docs/kotlin-doc.html) commentary and generate it to html with [Dokka](https://kotlinlang.org/docs/dokka-introduction.html).

Didn't bother to install any kdoc generating plugins, like Kdoccer.  
Please also note, that Dokka doesn't generate @param, @return and such tags at all, but documents those values in its own way automatically.   
It was mentioned somewhere, that using @param, @return etc is not the recommended way of documenting nowadays.


To make Dokka work did the following:
		
Included  
 
    id 'org.jetbrains.dokka' version '1.8.10'
    
as the first plugin in your **app gradle.build** (**Not** in project one as suggested on some pages)

<p style="text-align:center;">
<img src="../../../img/2023-03-16-using-dokka/dokka_app_plugin.png" width="400" height="250"/>
</p>

Make dokkaHTML task visible in gradle tasks (Not visible by default on my Electric Eel version of Android Studio):  

*File-Settings-Experimental* take tap off from *Only include test tasks . . .*  
followed by *File-Sync project with Gradle files*  

<p style="text-align:center;">
<img src="../../../img/2023-03-16-using-dokka/dokka_gradle_task_enable.png" width="600" height="450"/>
</p>

<p style="text-align:center;">
<img src="../../../img/2023-03-16-using-dokka/dokka_gradle_tasks.png" width="600" height="450"/>
</p>

Run dokkaHtml by double clicking it on gradle tasks.

by default docs will be generated under build/dokka/html.  

Left click index.html and select *open in - Browser*

<p style="text-align:center;">
<img src="../../../img/2023-03-16-using-dokka/dokka_build_html.png" width="500" height="500" />
</p>
<p style="text-align:center;">
<img src="../../../img/2023-03-16-using-dokka/dokka_build_html2.png" width="500" height="500" />
</p>
