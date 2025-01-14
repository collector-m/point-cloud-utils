<p align="center">
  <img src="imgs/logo_solarized_tint.png">
</p>

**Point Cloud Utils** is an _easy-to-use_ Python library for processing 
and manipulating 3D point clouds and meshes.

## Installation
With `pip` (requires git and a compiler supporting C++14 or later):
```shell
pip install git+git://github.com/fwilliams/point-cloud-utils
```

With `conda`:
```shell
conda install -c conda-forge point_cloud_utils
```

## A very simple example
Point Cloud Utils uses numpy arrays as fundamental data structure, making it very easy to integrate with existing numerical code. 
For example, here's how to remove all points in a point cloud which are greater than some distance from a mesh. 

```python
import point_cloud_utils as pcu

# Load a mesh stored in my_mesh.ply:
#   v is a NumPy array of coordinates with shape (V, 3)
#   f is a NumPy array of face indices with shape (F, 3)
v, f = pcu.load_mesh_vf("my_mesh.ply")

# Load a point cloud stored in my_point_cloud.ply:
#   p is a NumPy array of point coordinates with shape (P, 3)
p = pcu.load_mesh_v("my_point_cloud.ply")

# Compute the shortest distance between each point in p and the mesh:
#   dists is a NumPy array of shape (P,) where dists[i] is the 
#   shortest distnace between the point p[i, :] and the mesh (v, f)
dists, _, _ = pcu.closest_points_on_mesh(p, v, f)

# Delete all points which are farther than some distance away from the mesh
dist_thresh = 0.1
keep_points = p[dists < dist_thresh]

# Save the filtered point cloud to my_point_cloud_trimmed.ply
pcu.save_mesh_v("my_point_cloud_trimmed.ply", keep_points)
```



## Core Features
Point Cloud Utils includes utilities to perform the following tasks:

* [Reading and writing meshes and point clouds from disk](sections/mesh_io). Point Cloud Utils can handle any file that can be opened in MeshLab.
* [Resampling point clouds](sections/point_cloud_resampling) to have different distributions.
* [Generating point samples on a mesh](sections/mesh_sampling).
* [Computing metrics between point clouds and meshes](sections/shape_metrics) (e.g. Chamfer Distance, Hausdorff Distance, etc...).
* [Computing signed distances to triangle meshes](sections/mesh_sdf).
* [Estimating normals for point clouds and meshes](sections/normal_estimation).
* [Fast ray/mesh intersection](sections/ray_mesh_intersection).
* [Surface mesh smoothing](sections/mesh_smoothing).
