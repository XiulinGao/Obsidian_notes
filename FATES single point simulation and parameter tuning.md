1. Clone CESM and environment set up
   a. git clone https://github.com/ESCOMP/CTSM
   b. cd into the CTSM directory : cd CTSM
   c. create python environment for running CLM: ./py_env_create
   d. activate new python env:
   1. module load conda
   2. conda activate ctsm_py
   e. update external modules: ./bin/git-fleximod update
   f. chose the version of FATES you want to use, which also requires switching to the corresponding version of host land model. See https://fates-users-guide.readthedocs.io/en/latest/user/release-tags-compat-table.html for details.
   
   1. 


   
   
    

 