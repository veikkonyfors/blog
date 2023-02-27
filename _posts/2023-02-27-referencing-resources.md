---
layout: default
title:  "Referencing resources"
description: "Various ways to refer app resources"
tag: Android & Kotlin
katex: true
---

# Referencing resources

There is alternative ways to refer to resources of an Android App. Most Traditional way might be to use   

*setContentView(R.layout.activity_main)*,   

or one could make use of more modern  

*binding = ActivityMainBinding.inflate(layoutInflater); setContentView(binding.root)*  

way of doing it. Sure there is something else in between and afterwards. We are talking about Android development here, you see. ;-)

Trying to shed light on this here. For myself. And others as well, hopefully.