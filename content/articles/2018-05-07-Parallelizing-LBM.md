# Parallelizing Lattice-Boltzmann methods

It's a well-known fact that Lattice-Boltzmann methods for simulating
stuff with computers are suited to *direct* parallelization, in this
post I will talk about a simple and straight parallelization of a 
simulation of fluid dynamics using Lattice-Boltzmann method.

This is intended just as a quick and dirty introduction, just to show
or illustrate the idea of how easy is to parallelize these methods.

## What are Lattice-Boltzmann methods?
While this is not intended to explain what Lattice-Boltzmann methods are,
it's useful to give a small and vague introduction to them.

Lattice-Boltzmann methods (LBM for now on) are methods for numerically
solving virtually any differential equation that can be expressed as a
conservation or continuity equation somehow. Since mass, energy, 
momentum, charge and **many** other things are conserved under the 
appropriate conditions in nature, you can see how LBMs are a extremely
powerful tool to simulate nature with computers.

In layman's terms, the basic fundamental idea is imagining a hypothetical
micro-world with some very rigid but powerful rules that, at the end in
the macroscopic or relevant scale it reproduces the behaviour dictated by
some differential equation of interest.

More specifically, you discretize your space in a grid of nodes, as people
commonly do when dealing with computer simulations. Then you attach to
each node, a bunch of vectors of posible propagations, commonly called 
velocities, such that whatever is in that node can only _flow_ according
to these velocities to the neighbors. There are many ways of choosing these
velocities, and depends on what you want to achieve there are better ones 
than others, one of the common and good ones for 2D problems is showed in
the following picture

ACÁ IMAGEN DE UN D2Q9

You also associate some probabilty distribution to the nodes and its 
different propagation velocities.

There are **many** details involved and a lot of math, but it turns out
that these simple rules could always reproduce **exactly** the behaviour
dictated but the differential equation you want to solve.

## Implementing parallelization on CPU

It's a well-known fact that Lattice-Boltzmann methods are suited for 
direct parallelization, since in its conventional form it's almost a 
purely local computation that is performed at every step. That is, 

## Beyond CPU

Idea here is to talk about implementation in OpenACC and actually implement it.
