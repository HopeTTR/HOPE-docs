Phy Dept Cluster setup
======================

.. toctree::
   :maxdepth: 2

   runs_pip


You have 3 types of "Machine"

1- login Node(1x)

* editing files, git, compiling, submitting job
* do not run heavy code

2- Computer Node(8X cpu- heavy node)

* each 128 cpu core +512 GB ram 
* 4x NVIDIA A2 GPUs
* for simulations and analysis

3- GPU Node (1x)

* 32 cpu core, 256 GB RAM

**Python via Anaconda (conda)**

Python is managed through conda.

To enable conda:

.. code-block:: bash

 source /home/apps/anaconda3/etc/profile.d/conda.sh
 conda activate
 conda info --envs

**Note-** There too many env already exist on cluster, so should create new one for my work.
	
*Make new env*

.. code-block:: bash

 conda create -n flash_env -y -c conda-forge python=3.11 yt h5py numpy matplotlib ipython jupyterlab ipykernel
 conda activate flash_env

``env_name``=flash_env
 
installed pakages are: yt, h5py, numpy, matplotlib, ipython, jupyterlab, ipykernel

**SLURM scheduler**

mandatory fields in job scripts:

* ``--partition=queue_name``
 
 Which queue of machines you want (CPU vs GPU etc).

* ``--qos=qos_name``

 “Quality of service” = policy limits (max time, priority, etc).

* ``--time=walltime``

Max time your job can run (e.g., 02:00:00).

* ``--account=prof_name``

 The group/allocation you’re charging to (often your PI’s group).

**Note-** All the information are in ``phy_hpc.sh`` file inside the ``site`` dir.

**Things to remember**:

* A node is basically one physical computer inside the cluster.
* A core = one independent processing unit.
* Cluster have 512 GB RAM, sheared by all cores.And 128 CPU cores.
* ``--ntasks=32`` means asking for 32 CPU cores.
* ``--mem-per-cpu=4G`` means 4gb to each core 
* 4x32=128 GB, under 512 GB Ok.
* ``$SLURM_SUBMIT_DIR`` is automatically set by SLURM, not by your script.
* It contains the directory where you ran sbatch.

