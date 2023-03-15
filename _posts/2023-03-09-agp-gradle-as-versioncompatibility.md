---
layout: default
title:  "Android Gradle Plugin compatibility with Gradle and Android Studio"
description: "Android Gradle Plugin compatibility with Gradle and Android Studio"
tag: Android & Kotlin
katex: true
---
# Android Gradle Plugin compatibility with Gradle and Android Studio
Suddenly my newly created projects started to complain:  

*Dependency 'androidx.appcompat:appcompat:1.6.1' requires libraries and applications that
      depend on it to compile against version 33 or later of the
      Android APIs.*
      
And really, dependency on app level build.gradle is *androidx.appcompat:appcompat:1.6.1* for newly generated projects:

	pappa@pappa-ThinkPad-X270:~/AndroidStudioProjects/MyApplication/app$ grep appcompat build.gradle 
	    implementation 'androidx.appcompat:appcompat:1.6.1'
	pappa@pappa-ThinkPad-X270:~/AndroidStudioProjects/MyApplication/app$ 
      
whereas in older projects had *androidx.appcompat:appcompat:1.5.1* in use instead, and are being built ok.  
At some point something must have changed to make Android Studio use newer version for newly generated projects. I am now aware of what caused this.

Recommendation in the error messages was:
* update this project's version of the Android Gradle plugin to one that supports 33
* update this project to use compileSdkVerion of at least 33
* Additionally Gradle version must be upgraded to support selected AGP version

How on earth I am going to do that?

**Solution**

Turned out to be a nightmare to try obey the recommended actions. Below some details from along the road.
Might be the easiest way is to  [upgrade Android Studio]( ../../../2023/03/12/upgrading-android-studio.html) to recent version, as suggested on some posts along the way.

Tried to set up below configuration

||old|new|defined in (relative to project root)|
|androidx.appcompat:appcompat:|1.5.1|1.6.1|app/build.gradle|
|compileSdkVerion|32|33|build.gradle|
|AGP|7.2.0|7.4.2|build.gradle|
|Gradle|7.3.3|7.5.1?|gradle/wrapper/gradle-wrapper.properties

Details:
Disregarding recommendation's order of actions, ended up on updating compiled sdk version to 33 first, left minSdk and targetSdk as they were:

	pappa@pappa-ThinkPad-X270:~/AndroidStudioProjects/MyApplication/app$ grep Sdk build.gradle 
	    compileSdk 33
	        minSdk 23
	        targetSdk 32
	pappa@pappa-ThinkPad-X270:~/AndroidStudioProjects/MyApplication/app$

Build went trough, but gave below warning:

	We recommend using a newer Android Gradle plugin to use compileSdk = 33
	
	This Android Gradle plugin (7.2.0) was tested up to compileSdk = 32
	
	This warning can be suppressed by adding
	    android.suppressUnsupportedCompileSdk=33
	to this project's gradle.properties
	
	The build will continue, but you are strongly encouraged to update your project to
	use a newer Android Gradle Plugin that has been tested with compileSdk = 33

App worked ok. Didn't want to suppress warning, but wanted to upgrade AGP instead.

Per info available at [Google AGP Maven pages](https://maven.google.com/web/index.html?q=com.android.tools.build#com.android.tools.build:gradle), decided to use AGP 7.4.2, which was latest stablish at the time.

Did change using 'File -> Project Structure'.  
Change ends up into project level build.gradle, with module names suggesting in no way they are for AGP:    

	pappa@pappa-ThinkPad-X270:~/AndroidStudioProjects/MyApplication$ grep 7.4.2 build.gradle
	    id 'com.android.application' version '7.4.2' apply false
	    id 'com.android.library' version '7.4.2' apply false
	pappa@pappa-ThinkPad-X270:~/AndroidStudioProjects/MyApplication$ 

Now I get error for the gradle version I have in use, not supporting AGP 7.4.2:

	The project is using an incompatible version (AGP 7.4.2) of the Android Gradle plugin. Latest supported version is AGP 7.2.0

My gradle version is 7.3.3:

	pappa@pappa-ThinkPad-X270:~/AndroidStudioProjects/MyApplication/gradle/wrapper$ grep distributionUrl gradle-wrapper.properties
	distributionUrl=https\://services.gradle.org/distributions/gradle-7.3.3-bin.zip
	pappa@pappa-ThinkPad-X270:~/AndroidStudioProjects/MyApplication/gradle/wrapper$ 

[Android Gradle plugin release notes](https://developer.android.com/studio/releases/gradle-plugin) tell 7.4. of AGP requires Gradle 7.5.  
7.5.1 being the latest as shown in [Gradle buildtool releases page](https://gradle.org/releases/)

Changed gradle to 7.5.1:

	pappa@pappa-ThinkPad-X270:~/AndroidStudioProjects/MyApplication/gradle/wrapper$ grep distributionUrl gradle-wrapper.properties
	distributionUrl=https\://services.gradle.org/distributions/gradle-7.5.1-bin.zip
	pappa@pappa-ThinkPad-X270:~/AndroidStudioProjects/MyApplication/gradle/wrapper$

But still the same problem. Thus it seems to be Android Studio itself that supports AGP only upto 7.2.0, not Gradle.  
And really, Chipmunk 2021.2.1 supports AGPs 3.2-7.2 as shown in 
(Android Gradle plugin and Android Studio compatibility)[https://developer.android.com/studio/releases#android_gradle_plugin_and_android_studio_compatibility]

So, options seem to be
- Upgrade Android Studio to a current release, and hope my projects wouldn't require major conversion work
- Turn of the warning of *This Android Gradle plugin (7.2.0) was tested up to compileSdk = 32*
- Change androidx.appcompat:appcompat: back to 1.5.1 for each newly created project
- Find out why newly created projects started to use 1.6.1 version of androidx.appcompat:appcompat instead of 1.5.1.
