---
layout: default
title: Data Driven Graphics
nav_order: 1
---

# Data Driven Graphics 

Over the last decade, machine learning and specially deep learning promoted a revolution in multiple areas. For instance, in the Visual Computing domain, both image processing and computer vision benefited of this scenario as we saw machine learning models achieving the state of the art performance for tasks such as *object detection and recognition* and impressive results in generation tasks such as *image in-painting*, *image upsampling* and even whole videos of people moving and even talking - raising concerns about what we called *deepfakes*.

This results motivated researches to explore deep learning capabilities in more complex data representations such as graphs and 3D geometry. Working with more general data, outside of grid or sequential structures as images or audio allows us to derive data driven methods for computer graphics and geometry processing, building bridges to computer vision and image processing though machine learning techniques.

However, to make *data driven graphics*, we need to represent 3D data and be able to either apply our known techniques in these data or develop new methods to to deal with them. It turns out that research community's been doing both and some directions already presented promising results.


## 3D Data Representations

We start briefly describing some 3D data representations. Unlike images, which have a well stablished computational representation in terms of matrices of pixels, tridimensional objects and scenes have many different representation with different trade-offs. We don't intend to make an exhaustive analysis of these representations. For more details, please, refer to [1].

from those more related to the techniques and architectures employed in deep learning for computer vision.

### Descriptors and Projections


"they cannot learn the discriminative features from 3D shapes."

[X] describes 


"Sinha et al. in [120] proposed
geometry images where 3D objects were projected into 2D grid so that the classical 2D CNNs can
be employed."

Think about data for computer graphics as 3D data is kind of unfair and doesn't convey the 


### RGB-D Images

RGB-D data are a natural choice to represent 3D data as it comprises both appearance and geometry of a scene and it has a grid structure as regular images. This way, we can use everything already applied to images, including Convolutional Neural networks (CNNs) and we must only figure out how to make the best use of the depth channel to solve problems in 3D.

SOME WORKS....[X, XX, XXX]

Besides that, depth images and RGB-D data are quite easy to capture nowadays. It's been over a decade since low cost devices as the Kinect are available in the market and today we can even find depth sensors in mobile devices such as the iPad. Due to this scenario, we have a good research literature on how to deal with noise in depth maps and even how to reconstruct surfaces from these kind of data. 

### Multiview images

Another way we can use images to represent 3D data is to work with a set of regular images from different viewpoints of the same object or scene. With a multi-view representation, we don't have any geometric data as we have in RGB-D, but we might be able to infer it. 

### Voxels

Voxels are a natural extension to 3D of the ideia of a 2D pixel. It's a way to encode volumetric data in a regular grid in the three-dimensional space by describing which cells are ccupied .

Volumetric data. 3D data can be characterized as a regular grid in the three-dimensional
space. Voxels are used to model 3D data by describing how the 3D object is distributed through the three-dimensions of the scene. Viewpoint information about the 3D shape can be encoded as well by classifying the occupied voxels into visible, occluded or self-occluded. 

Despite the simplicity of the voxel-based representation and its ability to encode information about the 3D shape, and its viewpoint, it suffers from some constraining limitations [144]. 

Voxel-based representation is not always efficient because it represents both occupied and non-occupied parts of the scene, which establishes an enormous unnecessary need for memory storage. That is why voxel-based representation is not suitable for representing high-resolution data [1, 130]. A more efficient 3D volumetric representation is octree-based [130], which is simply varying-
sized voxels. Octree representation models 3D objects as a hierarchical data structure that models occupancy of the 3D object in the 3D scene [38] as shown in Fig. 1. Octree representation is based on recursive decomposition of the root voxels similar to the quadtree structure [1, 110]. The tree

- natural extension of a pixel to 3D

### Point Clouds

"Point clouds can be seen as a Euclidean-structured data locally when considering a point with respect to its neighborhood (a subset of points) such that the interaction among the points forms a Euclidean space with a distance metric which is invariant to transformations like translation, rotation. However, considering the global structure ofthe point cloud, it is an unordered set of points with no specific order which imposes the irregular non-Euclidean nature on the global structure of the data."


"PointNet [99] is the pioneer in making a direct use ofthe point cloud as an input where each ofits
points is represented using the (x,y, z) coordinates. As a pre-processing step, feature transformation and inputs are feeded into the PointNet architecture. PointNet is composed of three main modules: a “Spatial Transformer Network (STN)" module, an RNN module and a simple symmetric function that aggregates all the information from each point in the point cloud. The STN canonicalizes the data before feeding them to the RNN, i.e., process all the data into one canonical form, and learns the key points of the point cloud which approximately corresponds to the skeleton of the 3D object. Then comes the RNNmodule which learns the point cloud like a sequential signal ofpoints and while training this model with some randomly permuted sequence, this RNN becomes invariant to the sequence ofthe input order ofthe point cloud’s point. Lastly, the network aggregates all the resulted point features using the max-pooling operation which is also permutation invariant. PointNet proved that it is robust against partial data and input perturbation. It was tested on classification and segmentation tasks where it proved to produce results comparable to the state-of-the-art as shown the supplementary material, Table 1."




3D scanners ...

All of these are representations related to ours sensors (camera, LiDar etc) so it's easier to get the data.

In particular, multiview images are here "since forever" and we can avail all the progress that's been done in machine learning for computer vision and image processing

"As noticed in all the previously proposed methods, the main problem in processing point clouds is the un-ordered structure of this representation where researchers are trying to make the learning process invariant to the order of the point cloud. Most of these methods resorted to clustering techniques to opt for similar points and process them together."

### Polygonal Mesh

- standard for many applications in computer graphics, specially visual media.
- Graph Neural Networks

### Implicit functions

- continuous
- compact
- huge advances recently 

### These representations are not exaustive...

Ideally we want to input the more abundant and easily available data representation such as ordinary images and be able to infer/reconstruct the most a maior quantidade possível of scene/object properties such as it's geometry, topology, appearance and so on, in a useful and standard representation for new media applications.


## Change of paradigm: AI Graphics

The convolutional network model 

We have a changed to a data driven paradigm in which our models are estimated from data.

shows 2 things
- change of paradigm
- application of classical ideias still holds






# Tasks

* 3D Recognition | Classification
* 3D Retrieval
* 3D Correspondence

The goal of3D correspondence is to predict the mapping between a set
ofvertices ofa test mesh and a reference or template mesh. There are two types of correspondences;
sparse and dense correspondence. Sparse correspondence means that only a subset of the vertices
of the test mesh are mapped to the reference mesh. However, in dense correspondence, all the
vertices of the test mesh are mapped to the reference mesh.

1. Ahmed, Eman & Saint, Alexandre & Das, Rig & Shabayek, Abdelrahman & Gusev, Gleb & Cherenkova, Kseniya & Aouada, Djamila. (2019). A survey on Deep Learning Advances on Different 3D Data Representations. 10.13140/RG.2.2.32083.02080.

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5MjQ1Njg4NzUsLTE4OTk1ODAyNDksLT
UzMjE3MDE2MSwtMTE5ODc1NjE2MSwxNDY3OTMzNjMxXX0=
-->