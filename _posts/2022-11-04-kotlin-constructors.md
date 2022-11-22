---
layout: default
title:  "Kotlin constructors"
description: "Constructing classes in Kotlin in various ways"
tag: Android & Kotlin
katex: true
---
# Kotlin constructors

As a C++ or Java developer, constructing a class wasn't a burden, as far as I can recall it.  
In Kotlin, though, there seems to be so many various ways in setting up a class. I was a bit confused to start with. But in the end one just has to pick up one's preferred way of constructing a class, best suiting to case in hand.

Here's what I have come up to from all the possibilities.

## Primary constructor

Most concise way to construct a class is with primary constructor. Like below

	class MotorBike (val make: String, val model: String, val displacement:Int, var miles:Int=10)
	{ /*...*/ }
	
Properties for a class are specified on classes' specifier line, between the parentheses. One has to be careful to have either val or var keyword preceding parameter, otherwise parameter doesn't make it up to a property. A default value can also be specified here, as for miles above.

If the class has some additional specifications, like annotations, constructor keyword need to be introduced after class name and before the constructor part:

	class MotorBike1 @MustBeDocumented constructor(val make: String, val model: String, val displacement:Int, var miles:Int)
	{ }

Properties can also be specified in the body block. One can even mix up these two means; some properties specified in header between parenthesis and some in the body block. Like in the below working sample:

	// All four properties specified on primary constructor line, 
	//miles even with a default value
	class MotorBike1(val make:String, val model:String?, val displacement:Int, var miles:Int=10)
	{
	
	}	
	
	// Three first properties specified on constructor line, fourth item, 
	// _miles, without var keyword, is a parameter used to initialize the property, miles, 
	// which is specified in the body.
	class MotorBike2(val make:String, _model:String, _displacement:Int, _miles:Int)
		{
	        val model:String
	        get()=field+" "	// In order to be able to specify a custom getter, property needs to be in the block
	        val displacement:Int
			 var miles:Int
	        
	        init{
	            model=_model
	            displacement=_displacement
	            miles=_miles
	        }
	    }
	
	
	fun main() {
	    // miles not given, default will be used
	    MotorBike1("Suzuki","Dr800",800).also{println(it.make+ it.model+ it.displacement+ it.miles)}
	    // miles are given,but as kind of a plain parameter, used to initilize the property defined in block
	    MotorBike2("Suzuki","Dr750",750,100).also{println(it.make+" "+it.model+ it.displacement+" "+ it.miles)}
	
	}
	
Output produced:

SuzukiDr80080010  
Suzuki Dr750 750 100

Per the experience so far, I am going to stick on the primary constructor method in simpler cases.
When some more functionality is required for some of the properties, like [custom getters or setters]("Kotlin getters and setters" ../../../getters-setters.html), or initializers, I will specify those properties in body.


## Secondary constructors

A class can have one or more secondary constructors on top of primary one, or even without one.
Secondary constructors are not that commonly used, mostly they will be utilized with inheritance. But I could imagine there is some use cases for those even with non-inherited classes.

Below sample illustrates use of a secondary constructor together with a primary one, without inheritance. Point with secondary constructors might be one can use constructors with different number of parameters, leaving the unspecified properties to rely on their default values.

	// class MotorBike3 has one primary constructor with property make alone
	// Properties model, displacement and miles are specified in body, with default values.
	// With the secondary constructor one can instantiate the class with all, the properties given.
	class MotorBike3(val make:String)
	{
		var model:String="N/A"
		get()=field+" "	// In order to be able to specify a custom getter, property needs to be in the block
		var displacement:Int=-1
		var miles:Int=-1
		constructor(_make:String, _model:String, _displacement:Int, _miles:Int=10) : this(_make) {
			model=_model
			displacement=_displacement
			miles=_miles
		}
	}	
	
	fun main() {
		MotorBike3("Suzuki").also{println(it.make+" "+it.model+ it.displacement+" "+ it.miles)}
		MotorBike3("Suzuki","Dr650",650).also{println(it.make+" "+it.model+ it.displacement+" "+ it.miles)}
		MotorBike3("Suzuki","Dr650",650,43800).also{println(it.make+" "+it.model+ it.displacement+" "+ it.miles)}
	}

Output:  
Suzuki N/A -1 -1   
Suzuki Dr650 650 10  
Suzuki Dr650 650 43800  


