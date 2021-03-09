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

$$ SDF(x) = s : x ∈ R3, s ∈ R $$

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



**CvxNet: Learnable Convex Decomposition** convex decompositions as universal approximators of 3D geometry.

"Our object is represented via an indicator O : R3 →[0, 1], and with ∂O = {x ∈ R3 | O(x) = 0.5} we indicate the surface of the object. The indicator function is defined such that {x ∈ R3 | O(x) = 0} defines the outside of the object and {x ∈ R3 | O(x) = 1} the inside. Given an input (e.g. an image, point cloud, or voxel grid) an encoder estimates the parameters {βk} of our template representation
Oˆ(·)
with K primitives (indexed by k). We then evaluate the template at random sample points x, and our training loss ensures
Oˆ(x) ≈ O(x). In the discussion below, without
loss of generality, we use 2D illustrative examples where O : R2 →[0, 1]. Our representation is a differentiable con- vex decomposition, which is used to train an image encoder in an end-to-end fashion."

**BSP-Net**

"In this paper, we develop a generative neural network
which outputs polygonal meshes natively."

"BSP-Net is the first deep generative network which di-
rectly outputs compact and watertight polygonal meshes with arbitrary topology and structure variety.
• The learned BSP-tree allows us to infer both shape seg- mentation and part correspondence.
• By adjusting the encoder of our network, BSP-Net can also be adapted for shape auto-encoding and single-view 3D reconstruction (SVR).
• To the best of our knowledge, BSP-Net is among the first to achieve structured SVR, reconstructing a segmented 3D shape from a single unstructured object image.
• Last but not the least, our network is also the first which can reconstruct and recover sharp geometric features."

"At inference time, we feed the input to the network to ob-tain components of the BSP-tree, i.e., leaf nodes (planes P)
and connections (binary weights T). We then apply classic Constructive Solid Geometry (CSG) to extract the ex-plicit polygonal surfaces of the shapes."

decompose em planos, learnable plane parameters, learn how to combine (CSG) them and also the union

"Another similar work is CvxNet [8], which decomposes
shapes as a collection of convex primitives. However, BSP-Net differs from CvxNet in several significant ways: 1? we
target low-poly reconstruction with sharp features, while
they target smooth reconstruction; 2? their network always
outputs K convexes, while the “right” number of primitives
is learnt automatically in our method; 3? our optimization
routine is completely different from theirs, as their compositional tree structure is hard-coded."

On the other hand, Deep Local **Shapes** takes the key idea of DeepSDF one step further, by training a neural network to regress the Truncated Signed Distance Function (TSDF) using local latent codes. "The key idea of DeepLS is to compose complex general shapes and scenes from a collection of simple local shapes" it turns ou it is more efficient and flexible to encode the space of smaller local shapes and to compose the global shape from an adaptable amount of local codes.

### 3rd generation models

These models represent implicit surfaces as the solution to the Eikonal equation - the particular case where the gradient is equal ot 1 represents a signed distance function.

$$||\nabla f|| = 1||$$ 

- reconstruct from it's derivative
- an interesting point to note is that this approach (SIREN) is an improvement to deep learning solutions in general - another useful activation function


### 4th generation models

All methods above tackle the problem of surface reconstruction from data, outputting either a polygonal mesh or an isosurface representation from which we could extract a mesh. On the other hand, we could think about a scene representation suitable for direct visualization or, in other words, instead of solving a surface reconstruction problem and render the surface to visualize it, we could solve a novel view synthesis problem and generate a visualization of an unseen viewpoint directly based on the data we have.

NeRF solves the novel view synthesis problem by parameterizing a scene using a neural network. For each 3D point in space and observation direction the neural network outputs an RGB color and a volume density value. With this approach they were able to apply volume rendering techniques to compose the density values along the camera ray direction and generate a novel view. 

"Because volume rendering is naturally differentiable, the only input required to optimize our representation is a set of images with known camera poses."

This strategy tackles simultaneously the problem of scene geometry understanding and view synthesis as they demonstrated the capability of render depth frames and use this depth information to address occlusion. Training a neural network using the view direction made it able to represent reflections and specularities when the view direction changes.

It's interesting to notice that at a first moment, they had trouble to represent the fine details of objects. As noted XXXX fully connected neural networks learn low frequencies much faster than high frequencies. This way, they apply

n this paper, we train MLP networks to learn low dimensional functions, such as the function defined by an image that maps each (x, y) pixel coordinate to an output (r, g, b) color. A standard MLP is not able to learn such functions (blue border image). Simply applying a Fourier feature mapping to the input (x, y) points before passing them to the network allows for rapid convergence (orange border image).

This Fourier feature mapping is very simple. For an input point v (for the example above, (x, y) pixel coordinates) and a random Gaussian matrix B, where each entry is drawn independently from a normal distribution N(0, σ2), we use

$$ \gamma(v) = [cos(2\pi Bv), sin(2\pi Bv)]^T$$

to map input coordinates into a higher dimensional feature space before passing them through the network."

As we can imagine, this positional enconding based on Fourier Features transform is related to the SIREN approach wich formulated the problem mathematically and included the sinus function into the neural network representation.

**Can we use NeRF to solve panorama interpolation problem?**
**Can we make it more general in this case?**
**Can I estimate the distance between two centers of captured panoramas (unknow cameras)?**


Last, but not least, we have the approach used in [**Multiview Neural Surface Reconstruction by Disentangling Geometry and Appearance**](https://lioryariv.github.io/idr/). 

"Given a set of input masked 2D images, our goal is to infer the following three unknowns: (i) the geometry of the scene, represented as a zero level-set of an MLP f; (ii) the light and reflectance properties of the scene; and (iii) the unknown camera parameters. Toward that goal we simulate the rendering process of an implicit neural geometry inspired by the rendering equation.
The IDR forward model produces differentiable RGB values for a learnable camera position c and some fixed image pixel p as follows: the camera parameters and pixel define a viewing direction v, and we denote by x the intersection of the viewing ray c+tv with the implicit surface.
A Sample Network module represents x, and the normal to the surface n as differentiable functions of the implicit geometry and camera parameters.
The final radiance reflected from the geometry toward the camera c in direction v, i.e., RGB, is approximated by the Neural Renderer M, an MLP that takes as input the surface point x and normal n, the viewing direction v, and a global geometry feature vector z.
In turn, the IDR model is incorporated in a loss comparing it to the ground truth pixel color, that enables learning simultaneously the geometry, its appearance and camera parameters."


## Remarks

It takes a key idea, usually inspired by classical results built over the time in the area and figuring out how to make it work.

It's interesting to note that many of these works can be trained on synthetic data and evaluated on real data, which demonstrantes a reasonable degree of generalization.

Overfitting might be desirable in some cases. An ideia that sounds counter-intuitive for most machine learning scenarios so far.



## Deep Implicits Group
TODO: check name's spelling

#### Professors:
* Luiz velho
* Luiz Henrique de Figueiredo

#### Post-doc researchers
* Guilherme Shardong
* Vinicius Silva
* Tiago Novello

#### PhD students
* Daniel Yukimura
* Caio Souza
* Hallison Paz (me)

#### Msc Students
* Thales
  
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkxOTAwMDkwLC0xNTI4MjU5NTc2XX0=
-->