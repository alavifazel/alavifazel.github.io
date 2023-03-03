---
layout: post
title:  Cellular Automata (CA)
permalink: cellular-automata
description: Introduction to Cellular Automata and it's extensions
date:   2023-03-03 05:19:46 +0330
categories: cs
---

## Cellular Automata
Perhaps, you are already familiar with the concept of Finit [Finite Automata](https://en.wikipedia.org/wiki/Deterministic_finite_automaton).
Essentially, Cellular Automata (CA), is grid-like model (considering the 2D version of it, but there are also 3D) which is made up of tiny Finite state machines.
In this model, each cell has a state and by receiving inputs from its neighbouring cells, makes a transition to a new state.
To use FSM for simulation purposes, the program has to periodically run the model to trigger the transision.
Here, the CA behaves the same.

However, there are also extensions to CA such as Asynchronous Cellular Automata that each cell updates according to its dedicated time.

In the classical definition of Cellular Automata (and subsequently, the Synchronous Cellular Automata), all cells update simultaneously in each time step, and there is no way to specify different execution time for different cells. 
However, in the Asynchronous Cellular Automata, the time base set (Cn), is added to both update only the cells that can potentially change state, and also, to specify different timestamps for updating each cell (if it is desired). In other words, in the case that we only want the efficiency of execution, we can convert a regular Synchronous Cellular Automata to a Asynchronous Cellular Automata, but all cells in the Cn set will have the same time associated with their execution. 