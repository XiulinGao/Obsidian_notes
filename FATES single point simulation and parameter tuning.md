## Clone CTSM and environment set up
1. git clone https://github.com/ESCOMP/CTSM
2. cd into the CTSM directory : 

		cd CTSM
 
3. create python environment for running CLM: 

		./py\_env\_create


4. activate new python env:

	~~~bash
	module load conda
	conda activate py_env_name
	~~~

5.  update external modules: ./bin/git-fleximod update
6.  It's fine to use the master version of CLM-FATES, but you can also chose a different version of CLM-FATES you want to use, which also requires switching to the corresponding version of host land model. See [FATES-WIKI](https://fates-users-guide.readthedocs.io/en/latest/user/release-tags-compat-table.html) for details. If you decide to use a version that is different from the master version:

	~~~bash
	# checkout a different version of CTSM and update FATES
	cd CTSM
	git checkout -b your-new-branch-name  the-target-ctsm-version-tag
	./bin/git-fleximod update 	
		
	# checkout a different version of CTSM for a desired version of FATES
	cd CTSM/src/fates
	git checkcout -b your-new-fates-branch tag-of-desired-version-of-FATES
	cd ../../
	git checkout -b new-ctsm-tag tag-of-corresponding-CTSM-for-current-FATES
		
	~~~

**Note: you have to make sure the specific FATES version you chose is compatible with the host land model.** 
    

## Singel point simulation



    



   
   
    

 