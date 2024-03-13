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

### It's a differential equation

In short, this is a [differential equation](../../../2024/02/05/differential-equations), for which the solution, $\Psi$, is to be found. Once found, it can be used to predict whereabouts of the system over time.

In there:  
$\hat{H}$ is [hamiltonian operator](#hamiltonian-operator), which describes total energy levels of the system under investigation.  
$$i$$ is imaginary unit (i.e. $$\sqrt{-1}$$)  
$$h$$ is reduced Planck's constant  
$$\frac{∂\Psi}{∂t}$$ is first derivate of $\Psi$ (a.k.a. $\Psi'$)  
$$\Psi$$ is the function to be solved

### Solving it gives wave function

Differential equations are hard or even impossible to solve analytically. This is especially true for Schrödinger equation with a quantum system anything larger than a couple of measurables.  
Thus wave function is commonly solved using numerical methods with computers.

Once you have wave function available, you can get status of the quantum system out of it.

### State vector describes system's state at specific spot

Sometimes $$\Psi$$ is written in ket notation $$\vert\Psi\rangle$$.  

$$iℏ\frac{∂\vert\Psi\rangle}{∂t}−\hat{H}\vert\Psi\rangle=0$$ 

Which is a bit misleading to my taste.  
You see, $$\vert\Psi\rangle$$ represents a column vector. I have it hard to imagine how a column vector could be a solution to Schödinger equation. Solution has to be a function, not a vector, which is not a function at all!

Instead, ket $$\vert\Psi\rangle$$ gives the state of the system at specific spot and is called the **state vector**. You get $$\vert\Psi\rangle$$ by assigning values of the specific spot to $$\Psi$$.

What's the spot then. Depends on your system. Often quantum systems are dependent on time and 3D location, in which case we can say  $$\Psi(t_i, x_j, y_k, z_l) = \vert\Psi\rangle$$ at specific time $$t_i$$ and 3D location $$\{x_j, y_k, z_l\}$$

$$\vert\Psi\rangle$$ has then an element with an imaginary value for each possible permutation of all measurables with all their possible values. Each element gives probability amplitude of the combination in question. By taking a conjugate square of it one gets the probability of the system being in this state when observed.

Easy to say, hard to lay ;)
Preparing a simple sample . . .

## Hamiltonian operator

Hamiltonian operator is a square matrix giving energy and status for possible state transitions.   
If there is N quantum states to deal with, $\hat{H}$ operator is a NxN matrix. Each entry describes energy and dynamics between specific pair of states. E.g. $$\hat{H}_{ij}$$ describes interaction from state i to state j and will be applied on $$\Psi_j$$, i.e. the function describing jth state: $$\hat{H}_{ij}\cdot\Psi_j$$

## Other forms of Schrödinger equation

$$i\hbar\frac{\partial}{\partial t} \Psi(\mathbf{r},t) = \left [ -\frac{\hbar^2}{2\mu}\nabla^2 + V(\mathbf{r},t) \right ] \Psi(\mathbf{r},t)$$

$$\nabla^2 \Psi(x,y,z,t) -\dfrac{1}{c^2}\dfrac{\partial ^2 \Psi(x,y,z,t) }{\partial t^2}=0$$


### Relation of state function and state vector

$$|\psi\rangle = \int d^3r\;\psi(\mathbf{r})|\mathbf{r}\rangle$$

$$\psi(\mathbf{r})=\langle\mathbf{r}|\psi\rangle$$