---
layout: default
title: Deep Implicits
math: mathjax3
nav_order: 3
---

# Representing the World Implicitly with Neural Networks

Among the multiple 3D data representations, we saw we can model surfaces as a level set of a continuous function defined implicitly. Over the last months, it happened an explosion of interesting works about implicit surfaces representations using neural networks and it's a promising reseach path for new medias. 

Implicit surfaces are the only continuous representation of 3D data. In other representations, either you have a limited set of points such as in point clouds and polygonal meshes or you have fixed grid  where your object is represented such as voxels or image based representations. This approach allows us to visualize or even extract a polygonal mesh from this model in arbitrary resolution which is extremely powerful for new media applications. For instance, thinking about interactive media over a network, we could have a structure of different levels of details in a server and incrementally refine the versions visualized in the clients, keeping a real time interaction. Implicit surfaces also have low memory footprint as their neural networks representations require less parameters and layers.

Here, we describe some very recent works on this topic. We do not intend to be exautisve or extensive as a survey, so we'll citeonly few works whose key ideas helped us to better understand how this field of research is developing and what could be research directions over these ideas applied to new medias.

As we'll see, this area starts with works trying to model the data with a global representation, which is suitable for single objects, but not so good for large scenes. We see a second generaton of models which add local information to better represent large scenes and they also improve the quality of representation for single objects. Then there are a third generation of models which brings an important perspective based on the Eikonal Equation to this deep learning scenario and also proposes periodic activation functions for neural networks. And finally, we have a fourth generation of models which are able to encode both geometry and appearance of objects and scenes, such as NeRF - Neural Radiance Fields – which applies the neural networks paradigm to encode light fields.

## First Generation 

### Occupancy Networks

We are used to apply neural networks to solve binary (and not binary) classification problems in many domains. We can frame the implicit surface representation problem as a binary classification problem by asking the following question: **is this 3D point inside or outside the surface?**

Occupancy Networks [X] builds upon this idea by using a neural network to approximate a continuous scalar field that assigns to every location \(p \in R^3\) an occupancy probability between 0 and 1. This way, the decision boundary of this classificator implicitly represents the object's surface.

To give some generalization abilities to the network, it is condiotioned over a latent code of the shape. For instance, if we have a dataset of point clouds, we can use PointNet to encode the point cloud into a low dimensional latent code and feed it to the network along the 3D space coordinate we want to classify.

### Deep SDF

On the other hand, Deep SDF reframes the implicit surface representation as a regression problem by approximating the Signed Distance Function (SDF). Their ideia is to use a neural network to approximate a continuous scalar field for which the magnitude of a point in the field represents the distance to the surface boundary and the sign indicates whether the region is inside (-) or outside (+) of the shape. This way, the surface is implicitly represented as the zero-level-set of the learned function.

$$ SDF(x) = s : x ∈ R^3, s ∈ R $$


Like Occupancy Networks, if we want to achieve some degree of generalization with this approach, we need to condition the input to the network. However, unlike Occupancy Networks, DeepSDF doesn't use an external encoder as it trains an autodecoder architecture for shape family learning by optimizing the latent code during the network training.


## 2nd Generation

The ideas to represent a global implicit function using a neural network are pretty straightforward and give encoraging results for many objects. However, it's hard to model large scale scenes using only global information. Even highly detailed models might not be represented accurately.

To address these issues, researchers proposed a variety of techiniques here described as local models. We start by looking to the follow up works over Occupancy Networks and DeepSDF, respectively, Convolutional Occupancy Networks and Deep Local Shapes.

### Convolutional Occupancy Network

In **Convolutional Occupancy Network**, motivated by the hypothesis that
"The key limiting factor of most implicit models is their simple fully-connected network architecture which neither allows for integrating local information in the observations, nor for incorporating inductive biases such as translation equivariance into the model” they try to find a new architecture to better represent large scene properties. 

Their strategy consists in projecting features in 2D canonical planes or a 3D canonical volume and generate new features by agreggating neighborhood features using interpolation. This should simulate what the convolutional layers do for images as information is combined and distributed in local neighboorhods. This way, they expect to create features with translation equivariance before running the fully connected model to estimate the occupancy probability.


With this architecture, they are able to reconstruct large scenes by applying it in a “sliding-window” at inference time, such as convolutional operators in images.

### Deep Local Shapes

On the other hand, **Deep Local Shapes** [X] takes the key idea of DeepSDF one step further, by training a neural network to regress the Truncated Signed Distance Function (TSDF) using local latent codes. "The key idea of DeepLS is to compose complex general shapes and scenes from a collection of simple local shapes" it turns out it is more efficient and flexible to encode the space of smaller local shapes and to compose the global shape from an adaptable amount of local codes.

### CvxNet: Learnable Convex Decomposition

CvxNet relies on convex decompositions as universal approximators of 3D geometry. Like Occupancy Networks, they model an object via an indicator function \(O : R^e →[0, 1]\)  with \(∂O = {x ∈ R^3 / O(x) = 0.5}\) representing the surface of the object. However, they decompose the object in \(K\) primitive convexes using a template compositional tree structure.

This convex decomposition is differentiable and it is used to train an end-to-end image encoder. Given an input (e.g. an image, point cloud, or voxel grid) the encoder estimates the parameters \(β_k\) of their template representation $ Ô(·) $ with $K$ primitives (indexed by k). Then, the template is evaluated at random sample points $x$ and a training loss is used to measure the quality of the approximation $Ô(x) ≈ O(x)$. 

### BSP-Net

BSP-Net is a deep generative network which directly outputs compact and watertight polygonal meshes via convex decomposition. Their ideia is to train a neural network to reconstruct a shape using a set of convexes built on a set of planes with learnable parameters and obtained from a BSP-tree (Binary Space Partitioning). BSP-Net targets low-poly reconstruction with sharp features by learning to represent shapes ans planes on leaf nodes and their connections on interior nodes. The explicit polygonal surface is extracted from the BSP-tree by applying classic Constructive Solid Geometry (CSG).

As it outputs polygonal meshes natively based on opertaions on planes, it's able to reconstruct and recover sharp geometric features with low-poly in opposition to meshes extracted using methods like marshing cubes. The learned BSP-tree also allows it to infer both shape segmentation and part correspondence.  

- with arbitrary topology and structure variety.
- The core ingredient of BSP is an operation for recursive subdivision of space to obtain convex sets. 

## 3rd generation models

These models represent implicit surfaces as the solution to the Eikonal equation - the particular case where the gradient is equal to 1 represents a signed distance function.

$$||\nabla f|| = 1||$$ 

Introducing the derivative of a surface as a type of data to the implicit surface representation and reconstruction problem is an interesting addition as it provides information about the normal vector to the surface, allowing us to represent fine and sharp details [Dual Contouring of Hermite Data]. 

SIREN [X] dives into this ideia and proposes periodic activation functions for neural networks as a mean to improve its convergence to high frequency details of signals. By using a basis of sinusoidal functions as activation functions, SIREN proved to be capable of reconstructing functions from its derivatives data. In other words, it's possible to solve a differential equation using a neural network and by solving a particular case of the Eikonal equation, one can implicitly represent a 3D scene. It seems like an interesting progress not only for AI Graphics, but for other problems that could be solved by deep learning.


## 4th generation models

All methods above tackle the problem of surface reconstruction from data, outputting either a polygonal mesh or an isosurface representation from which we could extract a mesh. On the other hand, we could think about a scene representation suitable for direct visualization or, in other words, instead of solving a surface reconstruction problem and render the surface to visualize it, we could solve a novel view synthesis problem and generate a visualization of an unseen viewpoint directly based on the data we have.

### Neural Radiance Fields

NeRF solves the novel view synthesis problem by parameterizing a scene using a neural network. For each 3D point in space and observation direction the neural network outputs an RGB color and a volume density value. With this approach they were able to apply volume rendering techniques to compose the density values along the camera ray direction and generate a novel view. Note that volume rendering is naturally differentiable.

This strategy tackles simultaneously the problem of scene geometry understanding and view synthesis as they demonstrated the capability of render depth frames and use this depth information to address occlusion. Training a neural network using the view direction made it able to represent reflections and specularities when the view direction changes.

It's interesting to notice that at a first moment, they had trouble to represent the fine details of objects. As noted in [X] fully connected neural networks learn low frequencies much faster than high frequencies. This way, they apply a "Fourier feature mapping", a transformation of the inputs from the low dimensional space to a higher dimensional feature space before passing them through the network. 

$$ \gamma(v) = [cos(2\pi Bv), sin(2\pi Bv)]^T $$


As we can imagine, this positional encoding based on Fourier Features transform is related to the SIREN approach which brought a better mathematical formulation to understand this problem and included the sinus function into the neural network representation.

> - Can we use NeRF to solve panorama interpolation problem?
> - Can we make it more general in this case?
> - Can I estimate the distance between two centers of captured panoramas (unknown cameras)?


### Multiview Neural Surface Reconstruction by Disentangling Geometry and Appearance

Last, but not least, we have the approach used in [**Multiview Neural Surface Reconstruction by Disentangling Geometry and Appearance**](https://lioryariv.github.io/idr/). 

*TODO: highlight its key ideas.*


## Remarks

- It seems good works take a key idea, usually inspired by classical results built over the time in the are, and they figure out how to make it work with neural networks.

- It's interesting to note that many of these works can be trained on synthetic data and evaluated on real data, which demonstrates a reasonable degree of generalization.

- Overfitting might be desirable in some cases. An ideia that sounds counter-intuitive for most machine learning scenarios so far.



## Deep Implicits Group

This study was conducted with the Deep Implicity Study Group during the summer at IMPA.

#### Professors:
* Luiz velho (organizer)
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
* Thales Magalhães

## References
=> TODO