---
layout: default
title: Tools for AI Graphics
nav_order: 2
---

# TOOLs and Datasets

We need tools 

To make science.. build on top of others people work. This way, "each researcher puts a step on the stair"$^*$ so we can collectivelly progress to higher grounds.

those foundations we already know 



$^*$ *An usual comparison made by my advisor, professor Luiz Velho. The full statement makes a joke with the music Stairway to Heaven of Led Zeppelin.


Besides the code that researchers usually publish on Github, there are some platforms built to help solving frequent problems on dealing with 3D data. We'll talk more about PyTorch3D.

## PyTorch3D

PyTorch3D is an open source framework built on top of PyTorch to help accelerate research on 3D deep learning. It was created and is mainly maintained by the facebook AI Research team. PyTorch is a well adopted framework for many deep learning use cases as it uses Python, a programming language largely adopted by the AI community, and builds on top of Torch, which was born in the NYU.

It's important to notice that as we are dealing with tasks that demands a lot of computations, we must build and adopt efficient solutions, otherwise it might take too long to obtain a result. PyTorch3D is an effort towards an optimized and efficient resusable components for research. it's divided on seven modules:

1. Operations
2. Loss functions
3. Renderer
4. Data loaders
5. I/O
6. Data Structures
7. Transforms

### Data Structures

The main data structure is called `Meshes` and it's used to represent a batch of 3D meshes - point clouds can be interpreted as a particular case when we have no faces information. A `Meshes` object is composed of a list of tensor of vertices and a list of tensors of faces. 

> all code examples are based on the course "Introduction to PyTorch3D", SIGGRAPH Asia 2020.

    ```python
    import torch
    from pytorch3d import Meshes

    verts_list = [torch.tensor([...]), ..., torch.tensor([...])]
    faces_list = [torch.tensor([...]), ..., torch.tensor([...])]

    mesh_batch = Meshes(verts=verts_list, faces=faces_list)
    ```


A challenge when working with meshes is their heterogeneous nature, as the number of vertices and faces can be very different between each element of a batch. PyTorch3D provides control over the memory layout of the tensors, so depending on the operation we need to do, we can alternate between a packed or padded tensor representation. For instance, if we want to work with a packed representation, we have the following functions available:

    ```python 
    # packed representation
    verts_packed = mesh_batch.verts_packed()

    # auxiliary tensors
    mesh_to_vert_idx = mesh_batch.mesh_to_verts_packed_first_idx()
    vert_to_mesh_idx = mesh_batch.verts_packed_to_mesh_idx()

    # edges
    edges = mesh_batch.edges_packed()

    # face normals
    face_normals = mesh_batch.faces_normals_packed()
    ```

### Input and Output

PyTorch3D has a basic I/O module for reading `obj` files into `Meshes` and writing `Meshes` to `obj`files.

    ```python
    import torch
    from pytorch3d.io import load_obj

    verts, faces, aux = load_obj(obj_file)

    faces = faces.verts_idx
    normals = aux.normals
    textures = aux.verts_uvs
    materials = aux.material_colors
    tex_maps = aux.texture_images
    ```

We read multiple files and load a batch of meshes at once.

    ```python
    import torch
    from pytorch3d.io import load_objs_as_meshes

    batched_mesh = load_objs_as_meshes([obj_file1, obj_file2, obj_file3])
    ```

### 3D Transforms

An usual operation when working with 3D assets is to apply transforms as translation, rotation or scale to objects. Using PyTorch3D, we can compose and apply 3D transforms to meshes. It also has some utilities functions to compute rotation matrices, angles and other useful tasks with rigid transforms.

    ```python
    import torch
    from pytorch3d.transforms import Transform3d, Rotate, Translate

    # example 1
    T = Translate(torch.FloatTensor([[1.0, 2.0, 3.0]]))
    R = Rotate(torch.FloatTensor([[0, 1, 0], [0, 0, 1], [1, 0, 0]]))
    RT = Transform3d().compose(R, T)

    # example 2
    T = Transform3d().scale(2, 1, 3).translate(1, 2, 3)
    ```



## Datasets


"We overview below the most recent 3D datasets. There are two main categories of data used by the research community: real-world datasets and synthetic data rendered from CAD models. It is preferable to use the real-world data; however, real data is expensive to collect and usually suffers from noise and occlusion problems. In contrast, synthetic data can produce a huge amount of clean data with limited modelling problems. While this can be seen advantageous, it is quite limiting to the generalization ability of the learned model to real-world test data. It is also important to note that most 3D datasets are smaller than large 2D datasets such as, ImaдeNet [37]. However, there are some recent exceptions as described below. ModelNet [142] is the most commonly used dataset for 3D object recognition and classification. It contains roughly 130k annotated CAD models on 662 distinct categories. This dataset was collected using online search engines by querying for each of the categories. Then, the data were manually annotated. ModelNet provides the 3D geometry of the shape without any information about the texture. ModelNet has two subsets: ModelNet10 and ModelNet40. These subsets are used in most of the recently published work as shown in Table 1 and Table 2 in the supplementary material. In Section 3.2.1, we provide an extensive analysis of the methods employed on the ModelNet dataset for recognition and retrieval tasks highlighting the evolution of DL methods for learning such data. SUNCG [123] contains about 400K of full room models. This dataset is synthetic, however, each
of these models was validated to be realistic and it was processed to be annotated with labelled object models. This dataset is important for learning the “scene-object" relationship and to fine-tune real-world data for scene understanding tasks. SceneNet [56] is also an RGB-D dataset that uses synthetic indoor rooms. This dataset contains about 5M scenes that are randomly sampled from a distribution to reflect the real world. However, not all the generated scenes are realistic and in practice, some of them are highly unrealistic. Still, this dataset can be used for fine-tuning and pre-training. In contrast, ScanNet [34] is a very rich dataset for real-world scenes. It is an annotated dataset which is labelled with some semantic segmentation, camera orientation and the 3D information that is gathered from 3D video sequences of real indoor scenes. It includes 2.5M views, which allows for training directly without pre-training on other datasets, as it is the case with different datasets. 

In addition, datasets for 3D meshes are available for the 3D computer vision community. Most
of the 3D meshes datasets are for 3D objects, body models or face data. The TOSCA [19] dataset provides high-resolution 3D synthetic meshes for non-rigid shapes. It contains a total of 80 objects in various poses. Objects within the same category have the same number of vertices and the same triangulation connectivity. TOSCA [19] provides artistic deformations on the meshes to simulate the real-world deformations of real scans. SHREC [18] adds a variety of artificial noise and artistic deformations on TOSCA scans. However, the artificial noise and deformations are not realistic and can’t generalize to new unseen real-world data which is a requirement for practical solutions. FAUST [13] dataset, however, provides 300 real-scans of 10 people in various poses. The 3DBodyTex dataset [108] is recently proposed with 200 real 3D body scans with high-resolution texture. 3DBodyTex is a registered dataset with the landmarks available for 3D human body models.

The series ofthe BUdatasets is very popular for 3D faces under various expressions. BU-3DFE [151]
is a static dataset which has 100 subjects (56 female and 44 male) of different ages and races. Each subject has in addition to the neutral face, six expressions as (happiness, sadness, anger, disgust, fear and surprise) of different intensities. There is 25 meshes for each subject in total, resulting in 2500 3D facial expressions dataset. Another very popular dataset is BU-4DFE [150], which is a dynamic facial expression dataset that has 101 subjects in total (58 female and 43 male). Similar to the BU-3DFE, each subject has six expressions. Other 3D faces datasets were available as well like the BP4D-Spontanous [156] and BP4D+ [157]

– ShapeNet
– ModelNet40?


## References

1. Nikhila Ravi; Jeremy Reizenstein; David Novotny; Taylor Gordon; Wan-Yen Lo; Justin Johnson; Georgia Gkioxari. **Accelerating 3D Deep Learning with PyTorch3D**. arXiv:2007.08501, 2020.
2. Introduction to PyTorch3D. SIGGRAPH Asia 2020 Course. Available at https://youtu.be/MOBAJb5nJRI
