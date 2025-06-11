## Clone CESM and environment set up
1.  git clone https://github.com/ESCOMP/CTSM
2. cd into the CTSM directory : cd CTSM
3. create python environment for running CLM: ./py_env_create
4. activate new python env:
   a) module load conda
   b) conda activate ctsm_py
5.  update external modules: ./bin/git-fleximod update
6.  It's fine to use the master version of CLM-FATES, but you can also chose a different version of CLM-FATES you want to use, which also requires switching to the corresponding version of host land model. See https://fates-users-guide.readthedocs.io/en/latest/user/release-tags-compat-table.html for details. If you decide to use a version that is different from the master version:
    a) git checkout -b your_new_branch_name  the_target_ctsm_version_tag
    b) ./bin/git-fleximod update to update FATES or git checkout -b your_new_fates_branch  the_target_fates_varsion; you have to make sure the specific FATES version is compatible with the host land model. 
    
    
    
   
   7. 


   
   
    

 