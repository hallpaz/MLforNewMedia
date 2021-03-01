----
layout: default
title: Deep Implicits
nav_order: 3
----

# Representing the World Implicitly with Neural Networks

One 3D represetation we find particularly interesting is the implicit representation. It turns out that over the last year it happened an explosion of interesting works in this area, leverageing the power of neural networks to represent 3D surfaces implicitly.

This representation has some advantages

* It's the only continuous representation. All other represetations are limited to a fixed resolution due to data discretization. Either you have a limited set of points such as in point clouds and polygonal meshes or you have fixed grid  where your object is represetend such as voxels or image based representations. ... we can represent surfaces as a level set of an continuous function defined implicitly. This allows us to visualize the surface or even extract a polygonal mesh using Marching Cubes in arbitrary resolution - the resolution required for the application.

Thinking about the New Media scenario, arbitrary resolution is extremely powerful as we could have a structure of different level os details and, for instance, send a corse version of the surface through the network while a more refined version can be assembled .... keeping a real time interaction.
  
* Low memory footprint

As we'll see, this area starts with works trying to model the data with a global representation, which is suitable for single objects, but not so good for large scenes. 


Then, we see a second generaton of models which add local information to better represent large scenes and also improve the quality of representation for single objects when 


Third generation models which brings an important XXX to the deep learing scenario. Using radial basis functions such as sinus as the nonlinear steps in neural networks instead of ReLu.

And as a fourth generation model, we see impressive visual results from NeRF - Neural Radiance Fields, which applies the neural networks paradigm to represent light fields(?).

Here, we describe two works 
We do not intend to be exautisve or extensive as a survey, so we'll cite a few works whose key ideas helped us to better understand how this field of research is developing and what could be research directions  over these ideas applied to New Medias.

### Occupancy Networks
"Our key insight
is that we can approximate this 3D function with a neu-ral network that assigns to every location p ∈ R3 an occu-pancy probability between 0 and 1. Note that this network is
equivalent to a neural network for binary classification, ex-cept that we are interested in the decision boundary which
implicitly represents the object’s surface."

We can use the neural network to solve a binary classification problem: **is this 3D point inside or outside the surface?**
So, we use the neural network to model a probability of occupancy in space and we are interested in the decision boundary whic implicitly represents the object's surface.



## Deep Implicits Group
TODO: check name's spelling

#### Professors:
* Luiz velho
* Luiz Henrique de Figueiredo

#### Post-doc researchers
* Guilherme Shardong
* Vinicius Silva
* Thiago Novello

#### PhD students
* Daniel Yukimura
* Caio
* Hallison Paz (me)

#### Msc Students
* Thales
  