---
layout: default
title:  "Kotlin gettes and setters"
description: "Kotlin gettes and setters"
tag: Android & Kotlin
katex: true
---
# Kotlin getters and setters

In Kotlin, one has default getters and setters for each and every property of a class. One makes use of those simply by referring to property with 'object.property' type of reference.

So one doesn't have to compose methods getThis() and setThat() to access the properties, as one has to do e.g. in Java and C++. Unless of course if one declares property to public, which isn't recommended by some best practices.

One can compose custom getters and setters if one wishes to do so, though. Following the property specification, a specification starting with get()= and/or set()= defines custom getter and setter for that property. 
E.g. if one want's to get the property always with a blank in the end, one could do as has been done in the below fraction of code:

	class MotorBike2(val make:String, _model:String, _displacement:Int, _miles:Int)
		{
	        val model:String
	        get()=field+" "	// In order to be able to specify a custom getter, property needs to be in the block
	        val displacement:Int
			 var miles:Int
			 . . .

Full code is available at [Kotlin constructor article]("Kotlin constructors" ../../../../../2022/11/04/kotlin-constructors.html).




