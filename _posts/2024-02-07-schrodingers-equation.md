---
layout: default
title:  "Schrödinger's Equation"
description: "Schrödinger's Equation for a Dummy"
tag: Quantum Mysteries
katex: true
---

## Schrödinger's Equation

What does it mean when they say Schrödinger's Equation  

$$iℏ\frac{∂\Psi}{∂t}−\hat{H}\Psi=0$$  

would describe status and dynamics of a quantum system?  

That's a mystery for me. As it is for most of the people. That's why this article is present at Quantum Mysteries category.  

In short, this is a [differential equation](../../../2024/02/05/differential-equations), for which the solution, $\Psi$, is to be found. Once found, it can be used to predict whereabouts of the system over time.

In there:  
$\hat{H}$ is [hamiltonian operator](#hamiltonian-operator), which describes total energy levels of the system under investigation.  
$$i$$ is imaginary unit (i.e. $$\sqrt{-1}$$)  
$$h$$ is reduced Planck's constant  
$$\frac{∂\Psi}{∂t}$$ is first derivate of $\Psi$ (a.k.a. $\Psi'$)  
$$\Psi$$ is the function to be solved

Sometimes $$\Psi$$ is written in ket notation $$\vert\Psi\rangle$$.  
This indicates wave function to be solved is not a scalar one, but a column vector instead. It has as many rows as there is columns on the rows of the $\hat{H}$ operator. Each $$\Psi_i$$ component describes the function for the system's state in question.

## Hamiltonian operator

Hamiltonian operator is a nxm matrix giving energy and status for possible states on specific times.
To Be Continued . . .

## Other forms of Schrödinger equation

$$i\hbar\frac{\partial}{\partial t} \Psi(\mathbf{r},t) = \left [ -\frac{\hbar^2}{2\mu}\nabla^2 + V(\mathbf{r},t) \right ] \Psi(\mathbf{r},t)$$

$$\nabla^2 \Psi(x,y,z,t) -\dfrac{1}{c^2}\dfrac{\partial ^2 \Psi(x,y,z,t) }{\partial t^2}=0$$