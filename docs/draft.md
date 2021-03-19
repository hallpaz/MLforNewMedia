
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

## DATASETs



"We overview below the most recent 3D datasets. There are two main categories of data used by the research community: real-world datasets and synthetic data rendered from CAD models. It is preferable to use the real-world data; however, real data is expensive to collect and usually suffers from noise and occlusion problems. In contrast, synthetic data can produce a huge amount of clean data with limited modelling problems. While this can be seen advantageous, it is quite limiting to the generalization ability of the learned model to real-world test data. It is also important to note that most 3D datasets are smaller than large 2D datasets such as, ImaдeNet [37]. However, there are some recent exceptions as described below. ModelNet [142] is the most commonly used dataset for 3D object recognition and classification. It contains roughly 130k annotated CAD models on 662 distinct categories. This dataset was collected using online search engines by querying for each of the categories. Then, the data were manually annotated. ModelNet provides the 3D geometry of the shape without any information about the texture. ModelNet has two subsets: ModelNet10 and ModelNet40. These subsets are used in most of the recently published work as shown in Table 1 and Table 2 in the supplementary material. In Section 3.2.1, we provide an extensive analysis of the methods employed on the ModelNet dataset for recognition and retrieval tasks highlighting the evolution of DL methods for learning such data. SUNCG [123] contains about 400K of full room models. This dataset is synthetic, however, each
of these models was validated to be realistic and it was processed to be annotated with labelled object models. This dataset is important for learning the “scene-object" relationship and to fine-tune real-world data for scene understanding tasks. SceneNet [56] is also an RGB-D dataset that uses synthetic indoor rooms. This dataset contains about 5M scenes that are randomly sampled from a distribution to reflect the real world. However, not all the generated scenes are realistic and in practice, some of them are highly unrealistic. Still, this dataset can be used for fine-tuning and pre-training. In contrast, ScanNet [34] is a very rich dataset for real-world scenes. It is an annotated dataset which is labelled with some semantic segmentation, camera orientation and the 3D information that is gathered from 3D video sequences of real indoor scenes. It includes 2.5M views, which allows for training directly without pre-training on other datasets, as it is the case with different datasets. 

In addition, datasets for 3D meshes are available for the 3D computer vision community. Most
of the 3D meshes datasets are for 3D objects, body models or face data. The TOSCA [19] dataset provides high-resolution 3D synthetic meshes for non-rigid shapes. It contains a total of 80 objects in various poses. Objects within the same category have the same number of vertices and the same triangulation connectivity. TOSCA [19] provides artistic deformations on the meshes to simulate the real-world deformations of real scans. SHREC [18] adds a variety of artificial noise and artistic deformations on TOSCA scans. However, the artificial noise and deformations are not realistic and can’t generalize to new unseen real-world data which is a requirement for practical solutions. FAUST [13] dataset, however, provides 300 real-scans of 10 people in various poses. The 3DBodyTex dataset [108] is recently proposed with 200 real 3D body scans with high-resolution texture. 3DBodyTex is a registered dataset with the landmarks available for 3D human body models.

The series ofthe BUdatasets is very popular for 3D faces under various expressions. BU-3DFE [151]
is a static dataset which has 100 subjects (56 female and 44 male) of different ages and races. Each subject has in addition to the neutral face, six expressions as (happiness, sadness, anger, disgust, fear and surprise) of different intensities. There is 25 meshes for each subject in total, resulting in 2500 3D facial expressions dataset. Another very popular dataset is BU-4DFE [150], which is a dynamic facial expression dataset that has 101 subjects in total (58 female and 43 male). Similar to the BU-3DFE, each subject has six expressions. Other 3D faces datasets were available as well like the BP4D-Spontanous [156] and BP4D+ [157]

– ShapeNet
– ModelNet40?
