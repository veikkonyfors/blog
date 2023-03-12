---
layout: default
title:  "Upgrading Android Studio"
description: "Upgrading Android Studio Chipmunk to Electric Eel using new Toolbox app"
tag: Android & Kotlin
katex: true
---
# Upgrading Android Studio

Had to upgrade my Android Studio, as it was a [nightmare to configure old Chipmunk version]( ../../../2023/03/09/agp-gradle-as-versioncompatibility.html) to function with newly required AGP plugin.

What I had was a manually installed Android Studio Chipmunk, 2021.2.1 on Ubuntu 20.04.4 LTS. By manually installed I mean an installation from android-studio-2021.2.1.14-linux.tar.gz tarball. 

Took *Help-Check for Updates ...* per the old habit, it suggested to download new *Electric Eel* version.  
Which I did. Had android-studio-2022.1.1.21-linux.tar.gz now.  
When installing it, manually again, it turned out as if it would had been a a fresh new installation. I got worried what happens to all that stuff I have configured in Chipmunk along the road.

Googled a bit. After reading some pretty confusing pages, e.g about selecting channels for upgrade, which seemingly no longer exist, ended up on using the Toolbox app as suggested by Chipmunk *Settings-Appeareance & Behaviour -Updates*. It is available at [www.jetbrains.com/toolbox-app](https://www.jetbrains.com/toolbox-app/)

Manually installed *jetbrains-toolbox-1.27.3.14493.tar.gz* tarball and ran *jetbrains-toolbox*

It was straight forward job. Now I have Android Studio Electric Eel, 2022.1.1 Patch 2.
