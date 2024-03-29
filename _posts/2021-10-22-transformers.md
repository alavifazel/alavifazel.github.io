---
layout: post
title:  "Transformers"
permalink: transformers
description: Basic construction of transformers and the physics behind them
date:   2021-10-22 05:19:46 +0330
categories: ee
---

# Table of Contents

1.  [Introduction](#introduction)
    1.  [Transformers: The basics](#transformers-the-basics)
        1.  [Solenoid connected to an AC Source](#solenoid-connected-to-an-ac-source)
    2.  [Transformers: Basic Construction](#transformers-basic-construction)
        1.  [Impedance transfer in Transformers](#impedance-transfer-in-transformers)
    3.  [Equivalent circuit of a real Transformer](#equivalent-circuit-of-a-real-transformer)
    4.  [Measuring the values of the equivalent circuit](#measuring-the-values-of-the-equivalent-circuit)
        1.  [open-circuit test](#open-circuit-test)
        2.  [short-circuit test](#short-circuit-test)


<a id="introduction"></a>

# Introduction

Transformer is a device that takes an AC input and produces an AC output
with the same frequency, but a *different voltage level*. These devices
are used in circuits such as audio amplifiers, phone chargers and power transmission.
In the example of power transmission, we often need to transmit electrical
power energy over large distances due the fact that generators are often
apart from the consumers (factories, urban users and etc). These wires
that transmit these electrical powers from generators to consumers have
some resistivity just like any other wire, and from Ohm's law the
voltage drop across these wires are calculated by:

$$V = RI$$

By knowing the voltage drop, calculating the power consumption of these
wires (which is getting wasted and converted to heat) is simply done by
multiplying it by its current $$I$$:

$$P_{wires} = RI^2$$

Which tells us is that the power loss in the lines are proportional to
the square of its current $I$$ times the constant \$$R$$. This is where
transformers come in use. These devices decrease the current (while
keeping the same power by increasing voltage level); Hence decreasing
the power loss in these wires substantially. These kind of transformers
are also known as *step up transformers*.

Since the voltage level received on the end point of these power lines
are enormous, we need to use transformers again but this time to
decrease the voltage level (hence increasing the current respectively).
We do this process to make the voltage level in a safe and usable level.
These transformers that decrease the voltage level are also known as
*step down transformers*.


<a id="transformers-the-basics"></a>

## Transformers: The basics

Working principal of a transformer is *Faraday's law of induction*. This
physical law states that if we have a closed-path conductor (such as a
loop of wire) and a changing magnetic field is passing though it, there
will be an induced *electromotive force*<sup><a id="fnr.1" class="footref" href="#fn.1">1</a></sup> on the wire. Moreover,
the strength of this induced EMF is proportional to the instantaneous
rate of change of this magnetic field. This law is mathematically
written as:

$$\varepsilon = - \frac{d \phi}{dt}$$

Which tells us that induced electromotive force is equal to the first
derivative of magnetic *flux* in respect to time.<sup><a id="fnr.2" class="footref" href="#fn.2">2</a></sup>

Flux in general, is a measurement of how much a quantity is passing
through a surface (magnetic field strength in this case). Hence it is
defined as:

$$\phi = \iint\limits_S B.ds$$

Where $$B$$ is the magnetic flux density (in units of **Tesla** or *T* for
short) /dot-product/ed with differential surface elements $$ds$$ (in
meters squared). Although this formula can be used to calculate any
magnetic flux, in transformers we exclusively deal with fluxes that have
(ideally) constant magnetic flux density through a flat surface. Thus we
can simplify it to:

$$\phi = B.A = BA\cos \theta$$

($$B$$ magnetic flux density and $$A$$ area of surface.)

Scientists dedicated a new unit for the flux which is called **Weber** or
*Wb*. Hence flux of 1 Weber is equivalent of a 1 meters squared surface
passing 1 Tesla magnetic fields *perpendicular* at each point of this
surface.

With our definition of magnetic flux for constant $$B$$ fields through a
flat surface, we can write the *law of induction* as:

$$\varepsilon = -\frac{d(B.A)}{d t}$$

In electric machinery, this instantaneous change in magnetic flux
typically happens in one of two cases. Either the magnetic field density
is constant and the surface is changing (More accurately, the
intersection between these constant magnetic density with a surface are
rotationally changing); As it happens in *generators*. Where the other
case is when the surface is constant but the magnetic field density is
changing; As we'll see this happens in the *transformers*.

There are number of ways to have a constant surface but *changing*
magnetic field. The most trivial one perhaps is to hold a permanent
magnet near a conductor and rapidly sliding alongside it. This is a
method that can be demonstrated in labs but it's not a useful case for
us. What we are interested instead, is the change in a changing magnetic
field produces by a current-carrying wire. In general, a
current-carrying wire produces an magnetic field around it. The strength
of this field can be obtained by:

$$B = \frac{\mu_o I}{2 \pi r}$$

$$I$$ as current in unit of Amperes, $$r$$ as the distance from wire and
$$\mu_o$$ a constant that makes the units work in the SI system.

![img](/assets/img/3/magnetic_field_around_a_wire.png)

If we make a solenoid out of this wire, it forms a (nearly) uniform
magnetic field strength inside of it <sup><a id="fnr.3" class="footref" href="#fn.3">3</a></sup>:

![img](/assets/img/3/solenoid.png)

In this case, the strength of this magnetic field can be calculated by:

$$B = \mu_o N I / L$$

($$N$$ is number of wire turns and $$L$$ the length of the solenoid.)

When we have an solenoid and a current starts passing through it, by law
of induction, voltage gets induced in the solenoid (in the same wires
that was making it up). This voltage is also called **back EMF** and is
always opposing the change in current.<sup><a id="fnr.4" class="footref" href="#fn.4">4</a></sup> Note that an ideal solenoid
that has no resistivity doesn't consume nor generates any electrical
power; But merely holds it. For example, if a *back EMF* was caused as
an effect of instantaneous positive change in the current, same voltage
would apply when it wanted to drop i.e. having a negative instantaneous
change in the current later on.

If we have a tightly wound solenoid, we can write the formula of
induction as:

$$\varepsilon = -N\frac{d\phi}{dt}$$

($$N$$ is the number of wire turns and $$\phi$$ the flux produced by *each*
loop)


<a id="solenoid-connected-to-an-ac-source"></a>

### Solenoid connected to an AC Source

When the electrical source of a solenoid is sinusoidal AC signal, the
flux getting produced inside of it gets a sinusoidal form as well:

$$\phi(t) = \phi_{m} \sin \omega t$$

Substituting into the formula of induction:

$$\varepsilon = -N \frac{d\phi}{dt} = - N \frac{d (\phi_{m} \sin \omega t)}{dt} = -N \frac{\phi_{m} d (\sin \omega t)}{dt} = N \phi_{m} \omega \cos \omega t$$

Which implies that having a sinusoidal flux makes the induced voltage on
the solenoid sinusoidal as well. Calculating *RMS* for this function we
get:

$$\varepsilon_{rms} = \frac{N \phi_{m} \omega}{\sqrt{2}}$$

And since the coils in a solenoid have a constant surface, this formula
can also be written as:

$$\varepsilon_{rms} = \frac{N B_{m} A (2\pi f)}{\sqrt{2}} \approx 4.44NB_{m}Af$$

($$N$$ is number of turns, $$B_m$$ Maximum field density, $$A$$ surface and
$$f$$ frequency)


<a id="transformers-basic-construction"></a>

## Transformers: Basic Construction

What happens if we hold two solenoids close to each other in a way that
the magnetic flux of one solenoid passes through the other one as well?
(ideally all of it).

![img](/assets/img/3/basic_transformer.png)

In this setup if we connect a sinusoidal AC source to one of these
coils, not only an *EMF* gets induced in the first coil, but also in the
second coil as well. This effect comes from the fact that the magnetic
flux of the first coil (hence its change over time) passes through the
second one too. Let's denote the first one $$E_1$$ and the latter as
$$E_2$$. These values can be obtained by:

$$\begin{aligned}
    & E_1 = 4.44N_1B_{m}Af \\
    & E_2 = 4.44N_2B_{m}Af
    \end{aligned}$$

And since all of these parameters except $$N_1$$ and $$N_2$$ are same for
both of these coils, we can simply divide them to get their ratio:

$$\frac{E_1}{E_2} = \frac{N_1}{N_2}$$

This relation simply means that the ratio of induced voltage on each
side is proportional to the number coil turns in that side. The setup we
have here is the basic construction of a transformer and equation (1) is
the main formula we use to describe a transformer. For short it is also
written as *$$N_1$$:$$N_2$$*. For example a *1:10* transformer increases the
voltage level of a sinusoidal AC signal by the multiple of $$10$$.

The ratio $$\frac{N_1}{N_2}$$ of a transformer is also called *turn ratio*
and is denoted by **a**:

$$\frac{N_1}{N_2} = a$$

An ideal transformer doesn't consume nor generate any power<sup><a id="fnr.5" class="footref" href="#fn.5">5</a></sup>; Hence
the input and output power remain the same. This means that the change
in voltage level of output is accompanied by a change in its current
level, by amount that the formula of power $$P(t) = V(t).I(t)$$ gives the
same value for the output as input.

$$P_1 = P_2\] \[E_1.I_1 = E_2.I_2$$

Therefore:

$$\frac{E_1}{E_2} = \frac{I_2}{I_1} = a$$

(all functions of time $$t$$)

One thing to note that is in real transformers, the wire turns are
wrapped around a ferromagnetic material such as iron. The presence of
this core makes the induction effect stronger.


<a id="impedance-transfer-in-transformers"></a>

### Impedance transfer in Transformers

When we have a transformer with load on the secondary side:

![img](/assets/img/3/with_impedance.png)

Using transformer formula we can calculate how does this load is seen
from the primary side's perspective. For an ideal transformer:

$$E_1.I_1 = E_2.I_2$$

From Ohm's law:

$$E = ZI$$

Therefore:

$$Z_1.I_1^2 = Z_2.I_2^2 \\
\frac{Z_1}{Z_2} = (\frac{I_2}{I_1})^2 = a^2 \\
Z_1 = Z_2a^2$$

With this formula we can replace the transformer and it's secondary side
load, by a single load $$Z_1$$. This process is called *impedance
transfer*.


<a id="equivalent-circuit-of-a-real-transformer"></a>

## Equivalent circuit of a real Transformer

In practice, a real transformer doesn't output the same power as it's
input. This difference is caused by voltage drop in the resistivity of
coils, the core and other factors we will discuss in this section. Let's
first see what is the equivalent circuit of a real transformer, then we
would ration about it's each part.

![img](/assets/img/3/real_transformer.png)

As shown in the diagram, this circuit is made up by both *series* and
*parallel* elements.

The series elements are the result of the *coils* in each side. More
precisely, $$R_1$$ and $$R_2$$ are due resistivity and the inductor elements
$$X_1$$ and $$X_2$$ due the main inductive effect of the first and second
coils respectively.

The parallel elements $$R_c$$ and $$X_m$$ are core losses of the
transformer. $$R_c$$ is called *magnetization resistivity* and $$X_m$$ is
the effect of *flux leakage*. Flux leakage is the flux that doesn't get
fully captured by the other side (in some sense it gets "wasted"). We
can think of this leakage, analogous by having a simple inductor without
it's flux getting passed to the other one. Notice that these two
elements are in parallel to each other because these impedances, affect
the input voltage independently yet simultaneous.

This somewhat complicated equivalent circuit can be simplified for power
transformers with a few approximations. In transformers the current that
flows through the parallel elements ($$R_c$$ and $$X_m$$) is a fraction of
the current in series elements. With this physical property we can
remove the parallel elements in practical sense, thus simplifying the
equivalent circuit greatly to:

![img](/assets/img/3/transformer_approx1.png)

Therefore by substituting with equivalent elements:

![img](/assets/img/3/transformer_approx2.png)

Furthermore if the transformer is designed for 1 MVA powers or more, the
impedance of resistance element $$R_e$$ is negligible compared to the
inductance $$X_e$$ therefore can be discarded. Hence:

![img](/assets/img/3/transformer_approx3.png)

This circuit is as simplified as we can get and it's used for modeling
power transformers in engineering applications.


<a id="measuring-the-values-of-the-equivalent-circuit"></a>

## Measuring the values of the equivalent circuit

So far we've seen the equivalent circuit of a real transformer. But how
can we find the values of it's components? In this regard we perform two
physical experiments on our transform namely *open-circuit* and
*short-circuit* test. With these tests, the parameters of equivalent
circuit can be measured with a very good approximation.


<a id="open-circuit-test"></a>

### open-circuit test

With this experiment we can find the values of parallel elements: $$X_m$$
and $$R_c$$. The way that this test works is as follows:

1.  We open-circuit one side of the transformer.

2.  While the side is open-circuited, we apply the maximum line voltage

to the other side and simultaneously we measure power and current on the
side as well.

Since there is no load on the secondary side, a current will flow
through the first series element ($$R_1$$ and $$X_1$$) as well as the
excitation branch ($$R_c$$ and $$X_m$$). The impedance of series elements
are substantially lower than the elements in excitation branch. Hence we
can conclude that approximately all the voltage drop of our input signal
has occurred in the excitation branch.

Now that we have the value of input voltage (from our source) and we
measured the power and current as well, we can use these formulas to
calculate the elements $$R_c$$ and $$X_m$$.

$$\cos \phi = \frac{P}{U I} \\
\sin \phi = \sqrt{1 - \cos^2 \phi} \\
I_c = I \cos \phi \\ 
I_m = I \sin \phi \\
X_m = \frac{U}{I_m} \\
R_c = \frac{U}{I_c}$$

($$P$$ and $$I$$ are the measured power and current respectively, and $$U$$
the applied voltage from our source.)

A note here: In step (2) we choose the low-voltage side for measurements
because it's safer and easier to work with.


<a id="short-circuit-test"></a>

### short-circuit test

This experiment is performed to determine the values of series elements.
The steps are:

1.  We short-circuit one side of the transformer.

2.  While the side is short-circuited, we slowly increase the voltage on

the other side until we get the maximum line *current*; And as before,
we measure both power and current as well.

Since the secondary side is short-circuited, applying a very small
voltage in the primary side causes maximum current to flow in the
transformer. Small voltage different between two input terminals means
that the current that flows in the parallel elements ($$R_c$$ and $$X_m$$)
is negligible and therefore can be ignored. This approximation implies
that all voltage drop in this experiment is caused by the series
elements.

Having the measurement values:

$$P = (R_1 + R_2)I^2 \\
P = R_e I^2 \\
R_e = \frac{P}{I^2} \\
Z_e = \frac{U}{I} \\
X_e = \sqrt{Z_e^2 - R_e^2}$$

(As before $$P$$ and $$I$$ are the measured power and current respectively,
and $$U$$ the applied voltage from our source.)

The types of transformers we discussed in this article are known as
*single-phase* transformers and they operate with power lines consisting
of a single phase signals. Although the most transformers that are used
in practice are *three-phase*, the basic concepts behind them are
similar to single-phase ones.

These documents are published under an open license (see the project's
root directory for more info), and were intended to be part of an open
and a collaborative project. Feel free to fork this document, send pull
request and also give your feedback. Thanks for reading!


# Footnotes

<sup><a id="fn.1" href="#fnr.1">1</a></sup> Electromotive force or EMF for short, is the force that causes
the electrons to move in a wire.

<sup><a id="fn.2" href="#fnr.2">2</a></sup> A note here, the negative sign ($$-$$) merely implies that the
induced voltage is in the opposite direction which the changed in
flux happened; and has no effect on the magnitude of the induced
voltage.

<sup><a id="fn.3" href="#fnr.3">3</a></sup> We skip the proof here but it has a straightforward proof that
can be found on the web.

<sup><a id="fn.4" href="#fnr.4">4</a></sup> The component *inductor* we saw in Article 1 was exactly a type
of solenoid; With the difference that inductors also of a core.
Presence of a core makes their induction effect stronger.

<sup><a id="fn.5" href="#fnr.5">5</a></sup> The reason for this property comes from physical properties of
transformers. Specifically the effect of 'Special Relativity'.
Although understanding this theory doesn't directly affect how we
understand the working of these devices, we would still have a
look at this theory in a separated article and also how does the
'magnetic effect' gets created in the first place.
