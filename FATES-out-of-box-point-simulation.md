## Clone CTSM and environment set up
### Author: Xiulin Gao
### Date: 2025-06-11

1. clone CTSM 

		git clone https://github.com/ESCOMP/CTSM
		
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
Before you start, make sure following files are ready.

1. A surface data file for your site. You can create a site-specific surface data file using the subset_data script under CTSM/tools/site\_and\_regional

	~~~bash
	cd CTSM/tools/site_and_regional
	./subset_data point --lat site_lat --lon site_lon --site site_name --create-surface --surf-year 2000
	~~~
Once you have the subset surface data file, you can modify some of the variables based on site observations. Usually, the important variables to change are site soil texture for PCT\_CLAY, PCT_SAND. But you can always change other varibales too if you have better data for them. 
	
2. Climate drivers. You can also create climate drivers using the same script if you don't have a site-specific

	~~~bash
	./subset_data point --lat site_lat --lon site_lon --site site_name --create-datm --datm-syr start-year --datm-eyr end-year
	~~~
	*you can combine the two line of code into one to create DATM and Surfdate simutaneously*
	
	~~~bash
	./subset_data point --lat site_lat --lon site_lon --site site_name --create-surface --surf-year 2000 --create-datm --datm-syr start-year --datm-eyr end-year
	~~~
	
	if you want to create you own climate drivers with flux-tower data, please see [Marcos Longo's script](https://github.com/mpaiao/FATES_Utils/blob/master/make_fates_met_driver.Rmd) and his in-code documentation for how to creare monthly forcing data. 
	
3. A parameter file with targeted PFT. To create a parameter file for selected PFTs, you can use the FatesPFTIndexSwapper.py script under CTSM/src/fates/tools

	~~~bash
	cd CTSM/src/fates/tools
	./FatesPFTIndexSwapper.py  --pft-indices 5, 12 --fin input-file-name --fout output-file-name
	~~~
	
	This will create a parameter file that only includes a tropical drought-deciduous broadleaf tree and a C4 grass. FATES has 12 PFTs, checkout FATES parameter file to see what they are. 
	You can then manually edit the parameter file to change parameters you have site-specific measurements for. For instance, change the Vcmax value for the two PFTs. 
	

Of course, you might also need a bash script to build the model. See [Adam Hanbury-Brown's single instant run script for example](https://github.com/adamhb/california-fates/blob/main/run_scripts/build_single_point_case_single_inst.sh); for more complicated run script, see [Xiulin Gao's script](https://github.com/XiulinGao/Sierra-mixedConifer-project/blob/main/scripts/ctrl-resprt.sh)

Once your case is sucessfully built, you can go to the case directory to submit your case.

  ~~~bash
  cd case_dir
 ./case.submit
  ~~~

## Useful resources

The [CESM forum](https://bb.cgd.ucar.edu/cesm/) is a great place for posting questions about model bugs that you run into if it's more a land surface model issue.
[FATES GitHub](https://github.com/NGEET/fates) is where you probably should go for most of the FATES related questions or model bugs. 
	
	
	
	





    



   
   
    

 