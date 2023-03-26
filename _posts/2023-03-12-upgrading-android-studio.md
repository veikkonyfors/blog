---
layout: default
title:  "Upgrading Android Studio"
description: "Upgrading Android Studio Chipmunk to Electric Eel using new Toolbox app"
tag: Android & Kotlin
katex: true
---
# Upgrading Android Studio

Had to upgrade my Android Studio, as it was a [nightmare to configure old Chipmunk version]( ../../../2023/03/09/agp-gradle-as-versioncompatibility.html) to function with newly required AGP plugin.

- [Upgrade itself](#upgrade-itself)
- [Complications after ugrade](#complications-after-upgrade)
	- [LiveData Transformations unresolved](#livedata-transformations-unresolved)


## Upgrade itself

What I had was a manually installed Android Studio Chipmunk, 2021.2.1 on Ubuntu 20.04.4 LTS. By manually installed I mean an installation from android-studio-2021.2.1.14-linux.tar.gz tarball. 

Took *Help-Check for Updates ...* per the old habit, it suggested to download new *Electric Eel* version.  
Which I did. Had android-studio-2022.1.1.21-linux.tar.gz now.  
When installing it, manually again, it turned out as if it would had been a a fresh new installation. I got worried what happens to all that stuff I have configured in Chipmunk along the road.

Googled a bit. After reading some pretty confusing pages, e.g about selecting channels for upgrade, which seemingly no longer exist, ended up on using the Toolbox app as suggested by Chipmunk *Settings-Appeareance & Behaviour -Updates*. It is available at [www.jetbrains.com/toolbox-app](https://www.jetbrains.com/toolbox-app/)

Manually installed *jetbrains-toolbox-1.27.3.14493.tar.gz* tarball and ran *jetbrains-toolbox*

It was straight forward job. Now I have Android Studio Electric Eel, 2022.1.1 Patch 2.

Toolbox is pretty effective, it also handles updates for related products, such as plugins and sdks:

<p style="text-align:center;">
<img src="../../../img/2023-03-12-upgrading-android-studio/eel_chk_updates.png" width="550" height="350"/>
</p>

Upgraded emulator and platform tools as well:

<p style="text-align:center;">
<img src="../../../img/2023-03-12-upgrading-android-studio/eel_tools_update.png" width="600" height="450"/>
</p>


## Complications after upgrade

### LiveData Transformations unresolved

Created a new project with Tabbed Activity template on Electric Eel. It did not compile correctly, left androidx.lifecycle.Transformations.map() as unresolved.  
Had an earlier project generated with Chipmunk from Tabbed Activity template as well. It works fine even now. Some dependency changes must have taken place, couldn't identify the source though.  
Instead, after a bit of chatGPT and Googling, turned out Transformations seems to be outdated in newer contexts, one should use methods available in LiveData instead.  

Changed the code to use map method of LiveData class itself

	val text: LiveData<String> = _index.map  
	
instead of Transformations.map(_index) method  

	val text: LiveData<String> = Transformations.map(_index)

Goes for other methods in Transformations as well, like switchMap. Spirit of the game nowadays is to use methods available in LiveData instead.  

Imports were changed also to:

	import androidx.lifecycle.*
	//import androidx.lifecycle.Transformations
	
from

	import androidx.lifecycle.LiveData
	import androidx.lifecycle.MutableLiveData
	import androidx.lifecycle.Transformations
	import androidx.lifecycle.ViewModel
