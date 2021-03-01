---
layout: default
title: Deep Implicits
nav_order: 3
---

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
is that we can approximate this 3D function with a neu-ral network that assigns to every location $p \in R^3$ an occupancy probability between 0 and 1. Note that this network is
equivalent to a neural network for binary classification, ex-cept that we are interested in the decision boundary which
implicitly represents the object’s surface."

We can use the neural network to solve a binary classification problem: **is this 3D point inside or outside the surface?**
So, we use the neural network to model a probability of occupancy in space and we are interested in the decision boundary which implicitly represents the object's surface.
LATENT?

### Deep SDF

On the other hand, Deep SDF decides to represent a surface implicitly by it's Signed Distance Function, [another classical and useful representation in implicit functions theory]. This way, they reframe the problem as a regression problem, so 

"DeepSDF, like its classical counterpart, represents a shape’s surface by a continuous volumetric field: the magnitude of a point in the field represents the distance to the surface boundary and the sign indicates whether the region is inside (-) or outside (+) ofthe shape, hence our representation implicitly encodes a shape’s boundary as the zero-level-set of the learned function while explicitly representing the classification ofspace as being part of the shapes interior or not"

"We describe modeling shapes
as the zero iso-surface decision boundaries of feed-forward
networks trained to represent SDFs.
A signed distance func- tion is a continuous function that, for a given spatial point, outputs the point’s distance to the closest surface, whose sign encodes whether the point is inside (negative) or out- side (positive) of the watertight surface:
$$SDF(x) = s : x ∈ R3, s ∈ R$$.

Our key idea is to directly regress the continuous SDF
from point samples using deep neural networks. The re- sulting trained network is able to predict the SDF value of a given query position, from which we can extract the zero level-set surface by evaluating spatial samples. Such surface representation can be intuitively understood as a learned binary classifier for which the decision boundary is the surface of the shape itself as depicted in Fig.
"


## 2nd Generation

The ideas to represent a global implicit function using a neural network are pretty straightforward and give encoraging results for many objects. However, it's hard to model large scale scenes using only global information. Even highly detailed models might not be represented accurately.

To address these issues, researchers proposed a variety of techiniques here described as local models. We start looking to the follow up works over Occupancy Networks and DeepSDF, respectively, Convolutional Occupancy Networks and Deep Local Shapes.

In **Convolutional Occupancy Network**, motivated by the hypothesis that
"The key limiting factor of most implicit models is their simple fully-connected network architecture which neither allows for integrating local information in the observations, nor for incorporating inductive biases such as translation equivariance into the model” they try to find a new architecture to better represent large scene properties. 

They try to derive a strategy that could agreggate neighbhood features such as the convolutional layers do for images. This way, they expect to create features with translation equivariance before running the fully connected model to estimate the occupancy probability.

Nice property; I didn't get the "fully convolutional" meaning though:
"As our model is fully-convolutional, we are able to reconstruct large scenes by applying it in a “sliding-window” fashion at inference time. We exploit this property to obtain reconstructions of entire apartments"

On the other hand, Deep Local Shapes takes the key idea of DeepSDF one step further, by training a neural network to regress the Truncated Signed Distance Function (TSDF) using local latent codes. 




## Remarks

It takes a key idea, usually inspired by classical results built over the time in the area and figuring out how to make it work.

It's interesting to note that many of these works can be trained on synthetic data and evaluated on real data, which demonstrantes a reasonable degree of generalization.

Overfitting might be desirable in some cases.



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
  