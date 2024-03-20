---
layout: default
title:  "Schrödinger's Equation"
description: "Schrödinger's Equation for a Dummy"
tag: Quantum Mysteries
katex: true
---

# Schrödinger's Equation

What does it mean when they say Schrödinger's Equation  

$$iℏ\frac{∂\Psi}{∂t}−\hat{H}\Psi=0$$  

would describe status and dynamics of a quantum system?  

That's a mystery for me. As it is for most of the people. That's why this article is present at Quantum Mysteries category.  

## It's a differential equation

In short, this is a [differential equation](../../../2024/02/05/differential-equations), for which the solution, $\Psi$, is to be found. Once found, it can be used to predict whereabouts of the system over time.

In there:  
$\hat{H}$ is [hamiltonian operator](#hamiltonian-operator), which describes total energy levels of the system under investigation.  
$$i$$ is imaginary unit (i.e. $$\sqrt{-1}$$)  
$$h$$ is reduced Planck's constant  
$$\frac{∂\Psi}{∂t}$$ is first derivate of $\Psi$ (a.k.a. $\Psi'$)  
$$\Psi$$ is the function to be solved

## Solving it gives wave function

Differential equations are hard or even impossible to solve analytically. This is especially true for Schrödinger equation with a quantum system anything larger than a couple of measurables.  
Thus wave function is commonly solved using numerical methods with computers.

Once you have wave function available, you can get status of the quantum system out of it.

## State vector describes system's state at specific spot

Sometimes $$\Psi$$ is written in ket notation $$\vert\Psi\rangle$$.  

$$iℏ\frac{∂\vert\Psi\rangle}{∂t}−\hat{H}\vert\Psi\rangle=0$$ 

Which is a bit misleading to my taste.  
You see, $$\vert\Psi\rangle$$ represents a column vector. I have it hard to imagine how a column vector could be a solution to Schödinger equation. Solution has to be a function, not a vector, which is not a function at all!

Instead, ket $$\vert\Psi\rangle$$ gives the state of the system at specific spot and is called the **state vector**. You get $$\vert\Psi\rangle$$ by assigning values of the specific spot to $$\Psi$$.

What's the spot then. Depends on your system. Often quantum systems are dependent on time and 3D location, in which case we can say  $$\Psi(t_i, x_j, y_k, z_l) = \vert\Psi\rangle$$ at specific time $$t_i$$ and 3D location $$\{x_j, y_k, z_l\}$$

$$\vert\Psi\rangle$$ has then an element with an imaginary value for each possible permutation of all measurables with all their possible values. Each element gives probability amplitude of the combination in question. By taking a conjugate square of it one gets the probability of the system being in this state when observed.

Easy to say, hard to lay ;) Preparing a simple sample . . .

### Let's start with an easy system of one measurable.

We have a system with two four sided dices. Each dice, when thrown, give a digit from 1 to 4. Our only measurable in this system is the sum of the two digits.  
The sum can be from 2 to 8. Probabilities for each of the sums: 2 - 1/16, 3 - 2/16, 4 - 3/16, 5 - 4/16, 6 - 3/16, 7 - 2/16, 8 1/16.  

As there is 7 possible outcomes after measurement (2, 3, 4, 5, 6, 7 or 8), and only one measurable, our state vector has 7 items, one for each of the sums.  
Each item gives probability amplitude for measuring the sum in question, probability amplitudes being usually imaginary numbers. Taking the absolute square of this number then gives the probability of the measurement ending up in this state.   
Absolute square for an imaginary number is the number multiplied by its [complex conjugate]( "imaginary part's sign changed to opposite").  Like
$$\left| a + bi \right|^2 = (a+bi)*(a-bi) = a^2+b^2$$  

In our sample here, the probability of the first outcome, 1/16, would be given by probability amplitude of $$1/4 + 0i$$. Also $$1/\sqrt{32} + 1/\sqrt{32}i$$ would fulfill the condition, as would all imaginary numbers on a imaginary plane circle with radius of 1/16. But for simplicity we deal this with ordinary real numbers.   

So, we need a vector with 7 items. Taking absolute square of each should give the probability for measuring that sum. 
Thus our state vector would look like this

$$\begin{pmatrix} 1/4 \\ \frac{\sqrt{2}}{4}\\ \frac{\sqrt{3}}{4}\\ 2/4\\  \frac{\sqrt{3}}{4}\\ \frac{\sqrt{2}}{4}\\ 1/4 \end{pmatrix}$$

This simple dice sample is time independent, i.e. each and every throw has the same propability vector. But if we would have it somehow manipulated in such a way, that probability density would vary between rounds, we would have a varying state vectors for varying rounds. Our sample would become 'round-dependent', time-dependent in a way.  
Our wave function would also be 'round-dependent' $$\Psi(i)$$, where i stands for the round. Solution would be 'round-specific' state vector $$\Psi(i) = \vert\Psi_i\rangle$$

 
### Sample with two measurables.

This will be a bit harder.  
We have a six digit dice and a two coins in our sample system. Measurables are digit from dice and heads or tails from the two coins summed up, head being 0 and tail being 1.  Latter comes with 3 degrees of freedom: 0, 1 or 2.
There are 18 possibilities the state can end up being when measured (i.e. after throw). Thus state vector is 18 items long.  
Carrying on with probabilities in some time. . .

## Hamiltonian operator

Hamiltonian operator is a square matrix giving energy and status for possible state transitions.   
If there is N quantum states to deal with, $\hat{H}$ operator is a NxN matrix. Each entry describes energy and dynamics between specific pair of states. E.g. $$\hat{H}_{ij}$$ describes interaction from state i to state j and will be applied on $$\Psi_j$$, i.e. the function describing jth state: $$\hat{H}_{ij}\cdot\Psi_j$$

## Other forms of Schrödinger equation

$$i\hbar\frac{\partial}{\partial t} \Psi(\mathbf{r},t) = \left [ -\frac{\hbar^2}{2\mu}\nabla^2 + V(\mathbf{r},t) \right ] \Psi(\mathbf{r},t)$$

$$\nabla^2 \Psi(x,y,z,t) -\dfrac{1}{c^2}\dfrac{\partial ^2 \Psi(x,y,z,t) }{\partial t^2}=0$$


### Relation of wave function and state vector

$$|\psi\rangle = \int d^3r\;\psi(\mathbf{r})|\mathbf{r}\rangle$$

$$\psi(\mathbf{r})=\langle\mathbf{r}|\psi\rangle$$