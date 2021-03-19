---
layout: default
title: Tools for AI Graphics
nav_order: 2
math: mathjax3
highlighter: rouge
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

> **all code examples in this page are from the course "Introduction to PyTorch3D", SIGGRAPH Asia 2020.**

    ``` python
    import torch
    from pytorch3d import Meshes

    verts_list = [torch.tensor([...]), ..., torch.tensor([...])]
    faces_list = [torch.tensor([...]), ..., torch.tensor([...])]

    mesh_batch = Meshes(verts=verts_list, faces=faces_list)
    ```


A challenge when working with meshes is their heterogeneous nature, as the number of vertices and faces can be very different between each element of a batch. PyTorch3D provides control over the memory layout of the tensors, so depending on the operation we need to do, we can alternate between a packed or padded tensor representation. For instance, if we want to work with a packed representation, we have the following functions available:


{% highlight markdown %}
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
{% endhighlight%}

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

### Operations

K-Nearest Neighbors (KNN)

    ```python
    import torch
    from pytorch3d.ops import knn_points

    N, P1, P2, D, K = 32, 128, 256, 3, 1
    pts1 = torch.randn(N, P1, D)
    pts2 = torch.randn(N, P2, D)

    dists, idx, knn = knn_points(pts1, pts2, K=K)
    ```

Graph Convolution

    ```python
    import torch
    from pytorch3d.ops import GraphConv

    conv = GraphConv(input_dim, output_dim, init="normal", directed=False)

    # given a mesh which is a Meshes object
    verts = mesh.verts_packed()
    edges = mesh.edges_packed()
    y = conv(verts, edges)
    ```

### Losses

We can access all regular losses functions such as Mean Squared Error or Cross Entropy already on PyTorch. However, when working with 3D objects we might need new ways to measure apporximation between our target result and our current result. For instance, if we want to deform a template mesh into a target mesh, we need some way to measure the distance between two meshes, two different discrete approximations of a surface in space. One such metric is the **Chamfer distance**. A naive implementation of this metric might use a lot of computational resources and limit the resolution for which we can work [1]. PyTorch3D provides implementation for the most commom losses used in AI Graphics.


```python
from pytorch3d.utils import ico_sphere
from pytorch3d.ops import sample_points_from_meshes
from pytorch3d.loss import chamfer_distance

sphere_mesh1 = ico_sphere(level=3)
sphere_mesh2 = ico_sphere(level=1)

sample_sphere = sample_points_from_meshes(sphre_mesh1, 5000)
sample_test = sample_points_from_meshes(sphre_mesh2, 5000)
loss_chamfer, _ = chamfer_distance(sample_sphere, sample_test)
```

### Renderer

One of the most powerful tools in the context of AI Graphics is differentiable rendering. By using a differentiable renderer, we can do "inverse rendering", that is, we can do backpropagation from images to scene properties, relating 2D and 3D and bridging techniques of computer graphics and vision. This opens new possibilities as self-supervised learning for training models and solving tasks.

PyTorch3D has a modular implementation of a differentiable renderer, which separates the rasterizer and shader modules. It's heavily influenced by Soft Rasterizer [3], but it adds some engineering improvements for efficiency and flexibility.

```python
from pytorch3d.renderer import (
    OpenGLPerspectiveCameras, look_at_view_transform,
    RasterizationSettings, BlendParams,
    MeshRenderer, MeshRasterizer, HardPhongShader
)
R, T = look_at_view_transform(2.7, 10, 20)
cameras = OpenGLPerspectiveCameras(device=device, R=R, T=T)
raster_settings = RasterizationSettings(
    image_size=512,
    blur_radius=0.0,
    faces_per_pixel=1, # sets the value of K
)

renderer = MeshRenderer(
    rasterizer=MeshRasterizer(cameras=cameras, raster_settings=raster_settings),
    shader=HardPhongShader(device=device, cameras=cameras)
)
image = renderer(mesh)
```
This way, we can compute a loss given a ground truth image and update parameters using the gradients.

```python
loss = (gt_image - image).sum()
loss.backward()
```

### Data Loaders

Datasets are an essential part of any machine learning task. PyTorch3D implements Data Loaders to encapsulate operations on the ShapeNetCore and R2N2 datasets. This way, we have a standard interface to access models, labels and operate on batches during a task. Note, however, that the data must be downloaded independently. [This tutorial](https://pytorch3d.org/tutorials/dataloaders_ShapeNetCore_R2N2) shows how it works.



## Datasets

TODO: explain about some datasets and the importance of datasets on AI Graphics research.

## References

1. Nikhila Ravi; Jeremy Reizenstein; David Novotny; Taylor Gordon; Wan-Yen Lo; Justin Johnson; Georgia Gkioxari. **Accelerating 3D Deep Learning with PyTorch3D**. arXiv:2007.08501, 2020.
2. Introduction to PyTorch3D. SIGGRAPH Asia 2020 Course. Available at https://youtu.be/MOBAJb5nJRI
