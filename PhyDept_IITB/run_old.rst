Validating the run pipline
==========================


Steps to run full simulation. Here is the steps for check the run pipline from the existed data (sph) the old run, without any changes in Simulationinit_Block.F90 file

1- Clean login without any conda initialisation
2- source ``profile_flash.sh`` 
3- The setup the problem by running this:

.. code-block:: bash

 ./setup magnetoHD/magbwd -3d +cube32 -maxblocks=20 -auto +usm +newMpole --with-unit=Particles -site=PhyDept_IITB

4- Then after SUCCESSFULLY setting the problem go to the new generated dir ``object``. Now do compilation, linking and runtime by running this:

.. code-block:: bash

 cd object
 make -j32

5- After get ``SUCCESS, just check for doble confirmation that flash.4 and flash.par files has written.

.. code-block:: bash

 vi flash.par
 vi flash4

6- Now to run the simulation first make new dir outside the main flash repo.

.. code-block:: bash

 mkdir flash_runs
 cd flash_runs

7- As this is only for test run using the external sph data let's make another folder inside this called ``chk_run``, but usually make folders like run01, run02...

.. code-block:: bash

 mkdir chk_run
 cd chk_run

8- Now we have to copy some files from different folders of flash repo.
 It's also depends on the setup problem as we are focusing on magwd problem so the files are ``flash4``, ``flash.par``, ``SpeciesList.txt``, ``helm_table.dat`` from object dir 
and ``Makefile.h`` , ``submit.sh`` from ``sites/PhyDept_IITB`` dir.
 After copy all these file change the ``submit.sh`` to ``job.sh``.
 And the spd data ``1011_5050.comp``, ``1011_5050.sph`` from ``source/Simulation/SimulationMain/magnetoHD/magbwd/`` 

.. code-block:: bash

 cp <path_to_source_file> <path_where_u_want_it>
 mv old_name new_name

9- Now the the job submition part comes, for this first run these commonda to get info about the slurm basics so that we can edit out ``job.sh`` file.

.. code-block:: bash

 sinfo
 sacctmgr show assoc where user=$USER format=Account,User,Partition,QOS -n

10- Now edit the ``job.sh`` and submit the job. the final working job script is already on the cluster.

.. code-block:: bash

 sbatch job.sh
 squeue -u 23n0315
 scancel <job_id>


