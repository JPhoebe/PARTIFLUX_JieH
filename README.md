# PARTIFLUX_JieH
Codes and documents generated for the PARTIFLUX model and flux working groups

## For the Model_Project
Code scripts are developed for NCAR's Derecho supercomputer, for CTSM version of `ctsm5.4.021`.

### CTSM code download and check out
- Create new directory for CTSM code  
  `cd /glade/u/home/$User`  
  `mkdir my_codes`  
- Go to the code directory
  `cd /glade/u/home/$User/my_codes`  
- Download the CTSM code to it's specific folder
  `git clone https://github.com/ESCOMP/CTSM.git ctsm_$Version`  
  `cd ctsm_$Version`  
  `git checkout ctsm5.4.021`  
- Update the dependencies
  `./bin/git-fleximod update`  
  The git fleximod script is a git extension that will populate the cesm directory with the relevant versions of each of the components along with the CIME infrastructure code.
- Activate python environment  
  `./py_env_create`  
  `conda activate ctsm_pylib`

## Check the wiki page for step-by-step instructions
Start with Workflow_JieH, while referring to DE-Tha_"AD or FN or Transient"_FLUXNET scripts for bash commands
regarding xmlchange and user namelist edits

Remember to assign your project and directory information at the top of each script
