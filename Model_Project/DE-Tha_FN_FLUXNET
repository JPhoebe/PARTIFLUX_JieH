export PROJECT=...
export User=...
export CTSMROOT=...
export CASEROOT=...

Site="DE-Tha"
Site_lat=50.9626
Site_lon=13.5651

let Flux_start=1996
let Flux_end=2014

Surf_path=$(ls ${CASEROOT}/inputdata/surfdata_${Site}_hist_2000_16pfts*.nc | head -n 1)

$CTSMROOT/cime/scripts/create_newcase \
 --case ${CASEROOT}/${Site}_FLUX_FS \
 --compset I2000Clm50BgcCruRs \
 --res CLM_USRDAT \
 --run-unsupported 

cd ${CASEROOT}/${Site}_FLUX_FS
./xmlchange DATM_MODE="1PT"
AD_REST_DIR="/glade/derecho/scratch/${User}/archive/${Site}_FLUX/rest/0201-01-01-00000"
AD_RESTART="${AD_REST_DIR}/${Site}_FLUX.clm2.r.0201-01-01-00000.nc"

./xmlchange DEBUG=FALSE
./xmlchange STOP_OPTION=nyears
./xmlchange STOP_N=100
./xmlchange REST_N=50
./xmlchange REST_OPTION=nyears

./xmlchange RESUBMIT=0
./xmlchange RUN_TYPE=startup
./xmlchange JOB_WALLCLOCK_TIME=06:00:00
./xmlchange walltime=06:00:00
./xmlchange CONTINUE_RUN=FALSE
./xmlchange MAX_TASKS_PER_NODE=1
./xmlchange MAX_MPITASKS_PER_NODE=1
./xmlchange NTASKS=-1

./xmlchange DATM_YR_ALIGN=1
./xmlchange RUN_STARTDATE=0001-01-01

./xmlchange DATM_YR_START=${Flux_start}
./xmlchange DATM_YR_END=${Flux_end}

./xmlchange CLM_FORCE_COLDSTART=off
./xmlchange CLM_ACCELERATED_SPINUP=off

./xmlchange CLM_USRDAT_NAME="1x1pt_${Site}"
./xmlchange PTS_LAT=${Site_lat}
./xmlchange PTS_LON=${Site_lon}
./xmlchange DIN_LOC_ROOT_CLMFORC="${CASEROOT}/inputdata/atm/datm7"

cp ${AD_REST_DIR}/rpointer.atm.0201-01-01-00000 .
cp ${AD_REST_DIR}/rpointer.cpl.0201-01-01-00000 .

echo "fsurdat='${Surf_path}'" >> user_nl_clm
echo "finidat='${AD_RESTART}'" >> user_nl_clm
echo "hist_nhtfrq=0" >> user_nl_clm
echo "hist_mfilt=12" >> user_nl_clm
echo "CLM_USRDAT.1x1pt_${Site}:taxmode=cycle" >> user_nl_datm_streams

./case.setup
./case.build
./case.submit
