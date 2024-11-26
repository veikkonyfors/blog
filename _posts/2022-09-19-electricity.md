---
layout: default
title:  "Electricity"
description: "Wrap-up of electricity"
tag: Electromagnetism
katex: true
---

## Electricity

First bit in [electromagnetism](../../../2022/09/18/electromagnetism).

### Electric charge
If an object has more electrons than protons, object's charge is said to be negative. Positive if vice versa. Neutral otherwise.  
An electron's charge is called elementary charge and is marked with $e$  
Unit of measure for electric charge is Coulomb (C).  
Electric charge is denoted by letter Q.

$1C = \frac{e}{1.60217653\cdot10^{-19}} \hspace{1em} \hspace{1em} i.e. \hspace{1em} 1C \sim 6.242\cdot 10^{18}e$

### Electric force
When you have two electric charges , Q and q, nearby each other, they will have a force affecting between them. Opposite charges have attractive force between them, like charges repel each other. Let's say charges are at distance r, in which case the force between them is characterized by formula

<a name="coulombslaw"></a>
$\text{Coulomb's law:} \hspace{1em} \vec{F_{e}}= \frac{1}{4\pi\epsilon_{0}} \frac{Qq}{r^2}  \sim  \frac{kg\cdot m^3}{s^2\cdot C^2}\cdot \frac{C^2}{m^2}=\frac{kg m}{s^2}=N$  
Note: Vector force is along line connecting charges. Positive force is repulsive, negative is attractive.

$\text{Where $\epsilon_{0}$ is vacuum permittivity:} \hspace{1em}\epsilon_{0}=8.8541878128(13)×10^{-12} \frac{F}{m}$

$F=farad \sim \frac{s^{4}A^{2}}{kgm^{2}} $


### Electric Field
An electric charge (Q) creates an electric field around it.
If another electric charge (q) is put in this field, at any point of it, there is force affecting this charge. This force is described by Coulomb's law.
  
Strength of the electric field at each  point is defined to be the force effecting a charge Q at that point divided by Q itself:  

$\vec{E}=\frac{\vec{F}}{q}=\frac{1}{4\pi\epsilon_{0}} \frac{Q}{r^{2}}$

*Q* &nbsp; is the source charge constituting electric field $\vec{E}$, which induces electric force $\vec{F}$ affecting charge *q*&nbsp; put at the distance of *r*&nbsp; from the source charge *Q*.

$\text{Unit of vacuum permittivity}=\frac{s^{4}A^{2}}{kgm^{3}}$

$\implies \text{Unit of } \vec{E} \text{ :} \hspace{1em} \frac{kgm^{3}}{s^{4}A^{2}} \frac{As}{m^2}= \frac{kgm}{s^{3}A}=
\frac{kgm}{s^{3}\frac{C}{s}} = \frac{kgm}{s^{2}\cdot C} = \frac{N}{C}$ 

### Electric current
Electric field makes electric charges to move in it. Moving electric electric charges create an electric current in turn.  
Electric current is measured by amperes (amps, A): One Coulomb of elementary charges in a second.

$1A=1\frac{C}{s}, \implies C=As$

On a metallic wire, an electric field is created within it when it's ends are connected to a power supply. This makes loosely connected electrons on outer shell of the metal atoms to start moving in the field. These electrons are 'valence' electrons participating in adjacent atoms' bonding to each other into a crystal structure. They are left as a kind of electron cloud with electrons being free to move in the electric field.  
Power supply is a device with two poles, with the other (negative) having more electrons than the other (positive). Power supplies can be created e.g. with chemical reactions or electromagnetic radiation.

Moving electric charges can also be bigger entities, like [ions](../../../2022/09/20/ions.html). If table salt, $Na^+ Cl^-$ is dissolved in water, $Na^+$ and $Cl-$ ions get separated due to water molecules dipole effect. Once an electric field is generated in this liquid, ions start to travel along the field.
 
### A single charge's potential energy in [homogeneous]( "electric force is the same in every point of field. Exists e.g. between two metallic plates with opposite charges") electric field
In each point of homogeneous electric field a force of $\vec{F}=\vec{E}q$ acts on a charge q.  
When a charge moves in a homogeneous electric field a distance of $\Delta x$, a work of 
$W=\vec{F}\Delta x$ is performed, by which amount potential energy is also changed.  
Thus, potential energy of e.g. an electron becomes $W=E_p=\vec{E}e\Delta x$ when compared to electron's starting point.  

It is interesting how this correlates with gravitational potential energy $E_g=mgh$.  
Objects mass $m$ relates to electric charge $e$, $h$ relates to $\Delta x$ and acceleration of gravity $g$ relates to $\vec{E}$. Only that $g$ is a simplified constant derived empirically to fit exactly gravitational field $\vec{g}$ on earth's surface.  
The further charge is from another, the more is potential energy, the less is electric force.  
The same goes with gravity on earth. The higher the object, the bigger potential energy and the less gravity.

### Voltage in electric field
As described above, potential energy of a charge between two points in a field is $E_p=\vec{E}q\Delta x$.  
To get a more generalized view of electric field's 'strength', we get potential energy per unit of charge:  

$V=\frac{\vec{E_p}}{Q}$.  

Thus we get a generic feature describing the field itself, independently from the charge in question.  
This is called the voltage of the electric field and we mark it by $V$.  
It's unit is Volt, marked $V$. One volt stands for voltage between two points when one Joule is required to move a charge of one Coulomb between the points 

$[V]=\frac{J}{C}=\frac{N\cdot m}{As}=\frac{\frac{kg\cdot m^2}{s^2}}{As}
=\frac{kg\cdot m^2}{As^3}$

_Note!_  
As potential is $V=\frac{\vec{E_p}}{e}$ and $E_p=\vec{E}e\Delta x$, we get $V=\frac{\vec{E}e\Delta x}{e}=\vec{E}\Delta x$. 
Thus unit of electric field's strength can also be expressed as

$[E]=\frac{V}{m}=\frac{\frac{J}{C}}{m}=\frac{N\cdot m}{As\cdot m}=\frac{N}{C}$

_Note II !_  
With electricity, it is not relevant how far the charge is moving to perform the work (= potential energy). As it is in Newtonian work.  
This has been a bit mind boggling for me.  
Take a 12V motorcycle battery. One Coulomb's charge takes 12 Joules to move between poles, no matter is the wire 8cm or 1 meter.  
I let myself understand that as each and every electron moving on the wire are side by side, repelling each other, this is what makes the distance irrelevant.

