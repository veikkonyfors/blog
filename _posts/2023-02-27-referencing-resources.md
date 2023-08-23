---
layout: default
title:  "Referencing resources"
description: "Various ways to refer app resources"
tag: Android & Kotlin
katex: true
---

# Referencing resources

There is various ways to refer to resources of an Android App.
Trying to shed light on this here. For myself. And others as well, hopefully.

All resources in Android Studio app are defined in xml files located in res folder of you app. Typically there are subfolders for different kinds of resources. E.g. layout folder contains xml resource description files for layouts used by various activities.

As described in [R module]( ../../../2023/02/27/R-module.html), references in these xml files are compiled into a module with name R, from which they can then be referenced by the app.  
E.g. if you have file *res/menu/threedot_menu.xml* specifying *android:id="@+id/menuitem_about"*, you can refer to this with *R.menu.menuitem_about* in your app.

There is various ways how to make use of these R references.

Most Traditional way might be to use fields in R in a straight way, as below

	setContentView(R.layout.activity_main)
	container = findViewById(R.id.fragment_container)
	

or one could make use of more modern Binding way of doing it.
In Binding, compiler generates a class out of each layout. Class in named based on the name of the layout file.
For layout activity_main.xml class with name ActivityMainBinding is generated and for fragment_puzz2.xml class name will become FragmentPuzz2Binding. Binding is then used as below


	binding = FragmentPuzz2Binding.inflate(inflater, container, false)
	val root: View = binding.root
	val txtAnswerView: TextView = binding.txtAnswer


Surely there must be some other ways as well. We are talking about Android development here, you see. ;-)
