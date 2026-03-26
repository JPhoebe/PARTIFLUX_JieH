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

## Spin up evaluation
After AD and final spin ups, remember to check whether soil carbon and nitrogen pools have reached equilibrium.
  Stability is confirmed when net ecosystem carbon storage changes by less than a specified threshold over a defined period (e.g., < 1.0 g C m-2 year-1). 
  `spinupStability.`
- One way to do the evaluation is by using the
  `$CTSMROOT/clm5.0/tools/contrib/SpinupStabilityXXX.ncl` script to calculate the annual change in total ecosystem carbon against a default tolerance. Note: copy the .ncl script to your histfile directory and then make necessary changes in the copied script.
- Another way to quickly evaluate is by opening your histfile in ncview
  to visually check if the long-term trend (slope) of carbon pools is sufficiently small.
  Ensure you have X11 forwarding enabled, then
  `module load ncview`
  `ncview *clm2.h0a.*.nc`
