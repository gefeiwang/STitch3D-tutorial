Installation 
============

Installation
------------
STitch3D package is publicly available at https://github.com/YangLabHKUST/STitch3D.

STitch3D can be installed from PyPI:

.. code-block:: python

   pip install stitch3d

Alternatively, STitch3D can be downloaded from GitHub:

.. code-block:: python

   git clone https://github.com/YangLabHKUST/STitch3D.git
   cd STitch3D
   conda config --set channel_priority strict
   conda env update --f environment.yml
   conda activate stitch3d

After installation, the package can be imported in Python by:

.. code-block:: python

   import STitch3D

Software dependencies
---------------------
.. code-block:: python

   python>=3.7
   pytorch>=1.6.0, <=1.13.1
   scanpy=1.7.2
   anndata=0.7.6
   pandas=1.1.5
   numpy>=1.19.0
   louvain=0.7.0
   leidenalg>=0.7.0
   umap-learn>=0.4.6
   pot>=0.8.0
   numba>=0.49.1
   matplotlib<3.7