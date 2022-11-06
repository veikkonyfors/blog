---
layout: default
title:  "Kotlin constructors"
description: "Constructing a class in Kotlin in various ways"
tag: Kotlin
katex: true
---
# Constructing a class in Kotlin

As a C++ or Java developer, constructing a class wasn't a burden, as far as I can recall it.  
In Kotlin, though, there seems to be so many various ways in setting up a class. I was a bit confused to start with. But in the end one just has to pick up one's preferred way of constructing a class, best suiting to case in hand.

## Primary constructor and constructor keyword

One can construct a class using constructor keyword. Like below

	class MotorBike constructor(val make: String, val model: String, val displacement:Int, var miles)
	{ /*...*/ }
	
One can leave the constructor keyword away, if there is no additional specifiers for the class, i.e. it would simply be

	class MotorBike (val make: String, val model: String, val displacement:Int, var miles:Int)
	{ /*...*/ }
	
Thus, properties for a class can be specified on classes' specifier line between parentheses. One has to be careful to have either val or var keyword preceding parameter, otherwise parameter doesn't make it up to a property. Didn't bother to try what happens if some have var or val, some don't. Perhaps I'll do it one day. ;-)

One can specify properties also in the old-fashioned way, i.e. moving them into the body block. Like

	class MotorBike()
	{
		val make:String?=null
		val model:String
		val displacement:Int
		var miles:Int=0
        
        init{
            model=""
            displacement=0
        }

The ? qualifier in the end of the type means value can be null. Without ?, compiler wouldn't allow null values.  
Properties need to be initialized in this approach, otherwise they should be declared abstract. More on abstract stuff later on, hopefully. Initialization can take place in initializers, more on them later, as well, hopefully.  
In above case all properties were initialized, in a way or another. ;-)
Flexible, isn't it? Quite a few permutations available. Only one would know which way to go. ;-)

One can mix up the header method with the body method also, as below

	class MotorBike(val make:String)
	{
		val model:String
		val displacement:Int
		var miles:Int=0
        
        init{
            displacement=0
            model=""
    }

By compiler default, in the above, make can be null and will be initialized to null.


In C++, all this would had been something like

	class MotorBike {
		itsMake String;
		itsModel String;
		itsDisplacement int;
		
		 public: MotorBike(make:String. model String, displacement int, miles int) {
        itsMake=make;
        itsModel=model
        itsDisplacement=displacement;
        itsMiles=miles;
    	}
	};

Of course, in C++, or Java, we would have lots of other permutations as well. Some initialized here and some there.

## Secondary constructors

## Additional properties

## Initializers



