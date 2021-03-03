---
layout: default
title: Data Driven Graphics
nav_order: 1
---

# Data Driven Graphics 

Over the last decade, machine learning and specially deep learning promoted a revolution in multiple areas. For instance, in the Visual Computing domain, both image processing and computer vision benefited of this scenario as we saw machine learning models achieving the state of the art performance for tasks such as *object detection and recognition* and impressive results in generation tasks such as *image in-painting*, *image upsampling* and even whole videos of people moving and even talking - raising concerns about what we called *deepfakes*.

This results motivated researches to explore deep learning capabilities in more complex data representations such as graphs,

... algumas técnicas desenvolvidas neste caminho tem nos ajudado a construir pontes entre todas as áreas da computação visual. Então num primeiro momento a gente teve processamento de imagens e visão computacional se aproximando ainda mais com as redes neurais, na medida em que a partir da compreensão do há na imagem a gente pôde ser capaz de realizar transferência de estilo, coloração de imagens em escala de cinza, o vulgo preto e branco e até mesmo geração de novas imagens segundo algum critério baseado em dados.

Agora, a gente tá diante da oportunidade de agregar a computação gráfica e o processamento geométrico neste paradigma, uma vez que estamos aprendendo a lidar com dados mais gerais, fora da estrutura fixa e limitada das imagens. Mais do que isso, a gente está conseguindo inferir a geometria de objetos e cenas a partir de imagens!!!

Now, we are capable of dealing with more complex data, non euclidean data and integrate in this cycle the computer graphics and geometry processing .

But to make data driven graphics, we need to represent 3D data and be able to either apply our known techniques in these data or develop new techiniques to to deal with them. It turns out that research community's been doing both.


## 3D Data Representations

We start briefly describing some 3D data representations from those more related to the techniques and architectures employed in deep learning for computer vision.

### Descriptors and Projections


"they cannot learn the discriminative features from 3D shapes."

[X] describes 


"Sinha et al. in [120] proposed
geometry images where 3D objects were projected into 2D grid so that the classical 2D CNNs can
be employed."

Think about data for computer graphics as 3D data is kind of unfair and doens't convey the 


### RGB-D Images

kinect...

### Multiview images



### Voxels

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


# TOOLs

## Datasets


"We overview below the most recent 3D datasets. There are two main categories of data used by the research community: real-world datasets and synthetic data rendered from CAD models. It is preferable to use the real-world data; however, real data is expensive to collect and usually suffers from noise and occlusion problems. In contrast, synthetic data can produce a huge amount of clean data with limited modelling problems. While this can be seen advantageous, it is quite limiting to the generalization ability of the learned model to real-world test data. It is also important to note that most 3D datasets are smaller than large 2D datasets such as, ImaдeNet [37]. However, there are some recent exceptions as described below. ModelNet [142] is the most commonly used dataset for 3D object recognition and classification. It contains roughly 130k annotated CAD models on 662 distinct categories. This dataset was collected using online search engines by querying for each of the categories. Then, the data were manually annotated. ModelNet provides the 3D geometry of the shape without any information about the texture. ModelNet has two subsets: ModelNet10 and ModelNet40. These subsets are used in most of the recently published work as shown in Table 1 and Table 2 in the supplementary material. In Section 3.2.1, we provide an extensive analysis of the methods employed on the ModelNet dataset for recognition and retrieval tasks highlighting the evolution of DL methods for learning such data. SUNCG [123] contains about 400K of full room models. This dataset is synthetic, however, each
of these models was validated to be realistic and it was processed to be annotated with labelled object models. This dataset is important for learning the “scene-object" relationship and to fine-tune real-world data for scene understanding tasks. SceneNet [56] is also an RGB-D dataset that uses synthetic indoor rooms. This dataset contains about 5M scenes that are randomly sampled from a distribution to reflect the real world. However, not all the generated scenes are realistic and in practice, some of them are highly unrealistic. Still, this dataset can be used for fine-tuning and pre-training. In contrast, ScanNet [34] is a very rich dataset for real-world scenes. It is an annotated dataset which is labelled with some semantic segmentation, camera orientation and the 3D information that is gathered from 3D video sequences of real indoor scenes. It includes 2.5M views, which allows for training directly without pre-training on other datasets, as it is the case with different datasets. 

In addition, datasets for 3D meshes are available for the 3D computer vision community. Most
of the 3D meshes datasets are for 3D objects, body models or face data. The TOSCA [19] dataset provides high-resolution 3D synthetic meshes for non-rigid shapes. It contains a total of 80 objects in various poses. Objects within the same category have the same number of vertices and the same triangulation connectivity. TOSCA [19] provides artistic deformations on the meshes to simulate the real-world deformations of real scans. SHREC [18] adds a variety of artificial noise and artistic deformations on TOSCA scans. However, the artificial noise and deformations are not realistic and can’t generalize to new unseen real-world data which is a requirement for practical solutions. FAUST [13] dataset, however, provides 300 real-scans of 10 people in various poses. The 3DBodyTex dataset [108] is recently proposed with 200 real 3D body scans with high-resolution texture. 3DBodyTex is a registered dataset with the landmarks available for 3D human body models.

The series ofthe BUdatasets is very popular for 3D faces under various expressions. BU-3DFE [151]
is a static dataset which has 100 subjects (56 female and 44 male) of different ages and races. Each subject has in addition to the neutral face, six expressions as (happiness, sadness, anger, disgust, fear and surprise) of different intensities. There is 25 meshes for each subject in total, resulting in 2500 3D facial expressions dataset. Another very popular dataset is BU-4DFE [150], which is a dynamic facial expression dataset that has 101 subjects in total (58 female and 43 male). Similar to the BU-3DFE, each subject has six expressions. Other 3D faces datasets were available as well like the BP4D-Spontanous [156] and BP4D+ [157]

– ShapeNet
– ModelNet40?


## PyTorch3D

We need tools 



# Tasks

* 3D Recognition | Classification
* 3D Retrieval
* 3D Correspondence

The goal of3D correspondence is to predict the mapping between a set
ofvertices ofa test mesh and a reference or template mesh. There are two types of correspondences;
sparse and dense correspondence. Sparse correspondence means that only a subset of the vertices
of the test mesh are mapped to the reference mesh. However, in dense correspondence, all the
vertices of the test mesh are mapped to the reference mesh.

* 


----
DIVULGAR LIVE no LINKEDIN E TWITTER
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0OTcyMjQ5MjUsMTQ2NzkzMzYzMV19
-->