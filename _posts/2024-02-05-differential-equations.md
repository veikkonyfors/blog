---
layout: default
title:  "Differential Equations"
description: "Differential Equations for a Dummy"
tag: Differential Equations
katex: true
---

# Differential Equations

Oh dear!  

Trying to grasp essence of  [Schrödinger's wave equation](../../../2024/02/07/schrodingers-equation) went high over my head. What an earth does it mean to say equation

$$iℏ∂|\Psi⟩∂t−H|\Psi⟩=0$$

describes quantum mechanical system's state and dynamics.

Turned out it is a differential equation.  
Differential equations define dependencies and correlations of a certain function and it's derivates. Differential equations are good for modeling various systems' behaviour over time and given parameters.  
Differential equations for a system are deduced by using rules, properties and other known attributes of the system.  
Once you have a good enough equation, you can solve it to get the function to predict how the system behaves over time.

Specifically, by solving wave function $$\Psi$$ out from [Schrödinger's wave equation](../../../2024/02/07/schrodingers-equation), one can predict whereabouts of the quantum mechanical entity. System itself is very much described by the Hamiltonian operator $$H$$.

Well, anyway, one more path to catch on the quantum way: how to solve differential equations.  
I will present here some of the methods for solving differential equations.

- [Simple differential equations](#simple-differential-equations)
- [Separating differential equations](#separating-differential-equations)
- [Linear first-order differential equations](#separating-differential-equations)


## Simple differential equations
Simple differential equations are ones, that only contain derivates of the function, not the function itself. Like 


$$y'+2x-1 = 0 \implies y'=-2x+1$$

These can be solved by simply integrating both sides of the equation

$$\int y' = \int -2x+1dx \implies y = -x^2 + x +C$$

where C is constant.  C can have an arbitrary value, thus there is indefinite amount of solutions.  
Often one has an intial condition specified, which limits the number of solutions.  
In our sample, intial condition

$$y(-1) = 1$$

will give

$$y = -x^2 + x +3$$

as solution.


## Separating differential equations

## Linear first-order differential equations