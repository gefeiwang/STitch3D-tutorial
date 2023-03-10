STitch3D
=========================================================
We developed STitch3D, a deep learning-based method for 3D reconstruction of tissues or whole organisms. Briefly, STitch3D characterizes complex tissue architectures by borrowing information across multiple 2D tissue slices and integrates them with a paired single-cell RNA-sequencing atlas. 

STitch3D enables two critical 3D analyses: First, STitch3D detects 3D spatial tissue regions which are related to biological functions, for example cortex layer structures in brain; Second, STitch3D infers 3D spatial distributions of fine-grained cell types in tissues, substantially improving the spatial resolution of seq-based ST approaches. 

The output of STitch3D can be further used for various downstream tasks like inference of spatial trajectories, denoising of spatial gene expression patterns, identification of genes enriched in specific biologically meaningful regions and detection of cell type gradients in newly generated virtual slices.

.. image:: images/Overview.jpg
   :width: 600

STitch3D Tutorials and Interactive 3D Results
==================
.. toctree::
   :maxdepth: 3
   
   tutorials/index.rst

STitch3D Installation
==================
.. toctree::
   :maxdepth: 2

   installation.rst

STitch3D Usage
==================
.. toctree::
   :maxdepth: 2
   
   usage.rst