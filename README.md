# LPJ-GUESS_nightmare
Scripts
To run LPJ-GUESS:

1. Build LPJ-GUESS
    cd lpj_guess/src/guess_4.0.1/
    ./build_lpj_guess.sh

On gadi, LPJ-GUESS doesn't find a necessary library
```
NETCDF_CXX_LIBRARY               NETCDF_CXX_LIBRARY-NOTFOUND
```
This has to be edited by hand, i.e. change NETCDF_CXX_LIBRARY-NOTFOUND to libnetcdf_c++4.so:
1. press c
2. press t
3. press enter and change NETCDF_CXX_LIBRARY-NOTFOUND to /apps/netcdf/4.7.1/lib/libnetcdf_c++4.so
4. press enter to confirm
5. press t to end writing
6. press c 
6. press g to generate

In addition, a file needs to be adjusted before the utilities are compiled:
```
cd utils/guess_utilities_1.3/gmap/libproj4/misc/
vim PJ_ob_tran.c
```
Change line 45
```
// change by Martin to compile, 20/01/2020
if (xy.x != HUGE_VAL && P->rot) {
//if (xy.x != HUGE && P->rot) {
```
3. Compile utilities (ask Martin but n.e.v.e.r. touch again)
```
make 
```
4. Start run
```
cd ../../runs/global_annual_CRUNCEP/
./clean_up.sh
./initial_setup.sh
./submit_to_raijin.sh
```
LPJ-GUESS produces ASCII output for landpoints only, ```convert_annual_ascii_to_netcdf_only_landpoints.py``` converts all land points that are in the annual output to netCDF (278x701 grid points); ```convert_annual_ascii_to_netcdf.py``` fills the gaps, i.e. the ocean points, with NaN and converts the annual output to netCDF (320x720 grid points).
