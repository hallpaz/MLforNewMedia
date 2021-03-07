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

Another way we can use images to represent 3D data is to work with a set of regular images from different viewpoints of the same object or scene. With a multi-view representation, we don't have any geometric data as we have in RGB-D, but with a sufficient amount of images we might be able to infer it. By working with multiples points of views we are also able to reduce noise, incompleteness, occlusion and illumination problems on data [XX Advances...]

### Voxels

Voxels are a natural extension to 3D of the ideia of a 2D pixel. It's a way to encode volumetric data in a regular grid in the three-dimensional space by describing which cells are occupied and which are not. We can extend this representation to encode, for instance, viewpoint information by classifying the occupied cells into visible, occluded or self-occluded. 

The simplicity of this representation comes at the cost of a high memory footprint as we have to store data for both occupied and unoccupied voxels. By using a hierarchical data structure such as an octree, we can have varying-sized voxels and use less memory to represent unoccupied space or low detailed . 


### Point Clouds

A point cloud is a set of data points in space with no specific order. Point clouds provide us information about a surface geometry, but lack information about its topology.  It's a common output of scanning processes and for that it has a low cost of aqucitions 

The unordered structure of a point cloud is a challenge for learning tasks as we must derive permutation invariant methods. PointNet was the first architecture to make a direct use of point clouds as input and successfully encode this kind of data generating robust features for classification and segmentation tasks. This made PointNet based encoders useful for many other problems of machine learning in computer graphics.

 We can establish a system of reference .... understand 

### Polygonal Mesh

- standard for many applications in computer graphics, specially visual media.
- Graph Neural Networks

### Implicit functions

- continuous
- compact
- huge advances recently 

### These representations are not exhaustive

We presented some common choices for representing 3D data and there are current efforts and advances being made in each of these directions. Some representations are mode related to ours sensors, so they are easier to capture, but on the other hand other representations are more suitable for 3D computer graphics tasks and applications for *new medias* such as real time rendering, artistic modeling or automated assets generation. 

Ideally we want to input the more abundant and easily available data representation such as ordinary 2D images and be able to infer the most scene/object properties as possible – such as it's geometry, topology, appearance and so on – in a useful and standard representation for new media applications. 

In particular, multiview images are here "since forever" and we can avail all the progress that's been done in machine learning for computer vision and image processing




## Change of paradigm: AI Graphics

The convolutional network model 

We have a changed to a data driven paradigm in which our models are estimated from data.

shows 2 things
- change of paradigm
- application of classical ideias still holds

By sampling points over surfaces

output of scanning processes.
3D scanners ...

All of these are representations related to ours sensors (camera, LiDar etc) so it's easier to get the data.

In particular, multiview images are here "since forever" and we can avail all the progress that's been done in machine learning for computer vision and image processing



1. Ahmed, Eman & Saint, Alexandre & Das, Rig & Shabayek, Abdelrahman & Gusev, Gleb & Cherenkova, Kseniya & Aouada, Djamila. (2019). A survey on Deep Learning Advances on Different 3D Data Representations. 10.13140/RG.2.2.32083.02080.

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY3OTgyNDAzMSwtNjgwMDQzNTA2LDczNz
c1MzM3NSw4Mzk0MDMzMCwzNTc5MjcwMDUsLTEzMTQzMDM1MDQs
LTEzMTg0MjIxNyw5MzEwMTkxMDQsNTg4ODYxNDY5LDQzNDMyNT
QzMSwtMTg5OTU4MDI0OSwtNTMyMTcwMTYxLC0xMTk4NzU2MTYx
LDE0Njc5MzM2MzFdfQ==
-->