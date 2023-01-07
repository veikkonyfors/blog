---
layout: default
title:  "Nabla Operator"
description: "Nabla Operator explained"
tag: Vector Calculus
katex: true
---

## Nabla Operator

Nabla operator, $\nabla$, describes the gradient of a scalar field in multiple dimensions.  
It is a mathematical vector operation, widely used in physics, e.g. in connection of [Maxwell equations](../../../2022/04/28/maxwell-equations).

In three dimensions, as used in Maxwell equations, operation is as below:

$\nabla f = \left( \frac{\partial f}{\partial x}, \frac{\partial f}{\partial y}, \frac{\partial f}{\partial z} \right)$  
Or  
∇f(x,y,z) = (∂f/∂x, ∂f/∂y, ∂f/∂z)
       = (f(x+1,y,z)-f(x,y,z), f(x,y+1,z)-f(x,y,z), f(x,y,z+1)-f(x,y,z))

So, if you would have a scalar field like below (in 2 dimensions only, 3 would be harder to present):  

|40|60|60|60|60|
|60|85|85|85|60|
|60|85|100|85|60|
|60|65|85|85|60|
|60|60|60|60|60|

you would end up having a vector field as follows

|(10.0,10.0)|(12.5,10.0)|(22.5,0.0)|(22.5,0.0)|(10.0,-10.0)|
|(10.0,12.5)|(12.5,12.5)|(20.0,10.0)|(12.5,-12.5)|(0.0,-22.5)|
|(0.0,22.5)|(10.0,20.0)|(0.0,0.0)|(0.0,-20.0)|(0.0,-22.5)|
|(0.0,22.5)|(-12.5,12.5)|(-20.0,0.0)|(-12.5,-12.5)|(0.0,-22.5)|
|(-10.0,10.0)|(-22.5,0.0)|(-22.5,0.0)|(-22.5,0.0)|(-10.0,-10.0)|

As an image  

<p style="text-align:center;">
<img src="../../../img/2023-01-06-nabla-operator/vfield.png" width="200" height="200"/>
</p>


Shortly said, nabla tells into which direction scalar field is changing at each monitored spot.

