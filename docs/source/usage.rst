Usage
=====

Preprocessing
----------------


* **Import package**

To use STitch3D, first import the package as 

>>> import STitch3D


* **Alignment of multiple slices**

Before using STitch3D, all spatial transcriptomics tissue slices are required to be provided in a list of AnnData objects, and the single-cell reference dataset should be in another AnnData object.

To align multiple tissue slices,
you can use the ``STitch3D.utils.align_spots()`` function:

>>> adata_st_list = STitch3D.utils.align_spots(adata_st_list_raw, 
...                                            method="icp", 
...                                            data_type="Visium", 
...                                            coor_key="spatial", 
...                                            test_all_angles=True, 
...                                            plot=True)

Aligned slices are stored in ``adata_st_list``. Parameters in ``STitch3D.utils.align_spots()`` include:

``method``: should be either ``"icp"`` (iterative closest point method) or ``"paste"`` (PASTE method).

``data_type``: a parameter that helps to specify the number of neighborhood spots (only for using ``method="icp"``). ``"Visium"`` or ``"ST"``.

``coor_key``: spatial coordinates in ``adata.obsm[coor_key]`` are used for alignment where ``adata`` is an object in list ``adata_st_list_raw``.

``test_all_angles``: parameter for ``method="icp"``; whether to test multiple rotation angles or not.


* **Construction of cell-type-specific expression profile matrix and 3D spatial graph**

After alignment, ``STitch3D.utils.preprocess()`` constructs cell-type-specific expression profile matrix and builds 3D spatial graph:

>>> adata_st, adata_basis = STitch3D.utils.preprocess(adata_st_list,
...                                                   adata_ref,
...                                                   sample_col="sample",
...                                                   slice_dist_micron=slice_dist_micron,
...                                                   c2c_dist=200.,
...                                                   n_hvg_group=500)

Main parameters in ``STitch3D.utils.preprocess()`` include:

``sample_col``: column name in ``adata_ref.obs`` that contains batch information. Ignore if not applicable.

``slice_dist_micron``: a list of distances between pairs of adjecent slices in micrometer. If not specified, all slices are regarded as technical replicates with ignorable distances.

``c2c_dist``: center-to-center distance in micrometer between nearest spots.

``n_hvg_group``: number of highly variable genes for each cell type in the single-cell reference dataset.


Running STitch3D model
----------------

* **Train STitch3D model**

After preprocessing, STitch3D model can be built via

>>> model = STitch3D.model.Model(adata_st, adata_basis)

STitch3D model can be trained by

>>> model.train()

* **Generate outputs from STitch3D model**

After model training, STitch3D provides outputs by

>>> result = model.eval(adata_st_list_raw, save=True, output_path=save_path)

STitch3D's learned representations of spots are saved in ``model.adata_st.obsm["latent"]`` which can be directly used for spatial domain identification. ``result`` is a list of AnnData objects with inferred cell-type proportions stored in ``.obs``, which helps to visualize cell-type proportions in each single slice. STitch3D's results are also saved in ``save_path``.



Visualizing STitch3D's results in 3D
----------------

Here we provide R functions for 3D visualization of STitch3D's results using ``rgl`` package.

* **Visualize 3D spatial regions**

Provided ``save_path`` that contains STitch3D's outputs and clustering result in ``clustering_result.csv``, an integer vector of cluster indices in ``clusters``, and a string vector of colors in ``cluster_colors``, STitch3D's 3D spatial domain detection result can be visualized by

>>> plot3D_clusters(directory = save_path,
...                 clusters = clusters,
...                 cluster_colors = cluster_colors)

* **Visualize 3D cell-type distributions**

With a string vector of cell types in ``celltypes``, and a string vector of colors in ``celltype_colors``, STitch3D's 3D cell-type deconvolution result can be visualized by

>>> plot3D_proportions(directory = save_path,
...                    celltypes = celltypes,
...                    celltype_colors = celltype_colors)