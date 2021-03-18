
---
layout: default
draft: true
title: Draft - saving ideas
---

### Descriptors and Projections


"they cannot learn the discriminative features from 3D shapes."

[X] describes 


"Sinha et al. in [120] proposed
geometry images where 3D objects were projected into 2D grid so that the classical 2D CNNs can
be employed."

Think about data for computer graphics as 3D data is kind of unfair and doesn't convey the 

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


# Tasks

* 3D Recognition | Classification
* 3D Retrieval
* 3D Correspondence

The goal of3D correspondence is to predict the mapping between a set
ofvertices ofa test mesh and a reference or template mesh. There are two types of correspondences;
sparse and dense correspondence. Sparse correspondence means that only a subset of the vertices
of the test mesh are mapped to the reference mesh. However, in dense correspondence, all the
vertices of the test mesh are mapped to the reference mesh.

> Written with [StackEdit](https://stackedit.io/).
### Multiview Neural Surface Reconstruction by Disentangling Geometry and Appearance

Last, but not least, we have the approach used in [**Multiview Neural Surface Reconstruction by Disentangling Geometry and Appearance**](https://lioryariv.github.io/idr/). 

"Given a set of input masked 2D images, our goal is to infer the following three unknowns: (i) the geometry of the scene, represented as a zero level-set of an MLP f; (ii) the light and reflectance properties of the scene; and (iii) the unknown camera parameters. Toward that goal we simulate the rendering process of an implicit neural geometry inspired by the rendering equation.
The IDR forward model produces differentiable RGB values for a learnable camera position c and some fixed image pixel p as follows: the camera parameters and pixel define a viewing direction v, and we denote by x the intersection of the viewing ray c+tv with the implicit surface.
A Sample Network module represents x, and the normal to the surface n as differentiable functions of the implicit geometry and camera parameters.
The final radiance reflected from the geometry toward the camera c in direction v, i.e., RGB, is approximated by the Neural Renderer M, an MLP that takes as input the surface point x and normal n, the viewing direction v, and a global geometry feature vector z.
In turn, the IDR model is incorporated in a loss comparing it to the ground truth pixel color, that enables learning simultaneously the geometry, its appearance and camera parameters."

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyOTkzNjcxNjRdfQ==
-->