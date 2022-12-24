# Implementation of Entrainment Changes

For information, see https://www2.mmm.ucar.edu/wrf/users/docs/user_guide_v4/v4.4/users_guide_chap5.html#runtimeio

Adding the following changes below will produce a `entrain_d0<domain>_<date>` file for each domain and every 5 minutes (`aux_hist7_interval`) containing a range of entrainment-related information:
- REI_KF, rate of environmental inflow (kg s-1)
- UER_KF, net updraft entrainment rate (kg s-1)
- UDR_KF, net updraft detrainment rate (kg s-1)
- DER_KF, net downdraft entrainment rate (kg s-1)
- DDR_KF, net downdraft detrainment rate (kg s-1)
- UMF_KF, updraft mass flux (kg s-1)
- iterf_KF, number of iterations of the LDA scheme.

## Namelist Changes

Add the following to the &time_control and &phys sections of your namelist.input file. 
```
&time_control
iofields_filename = "output_file_d01.txt", "output_file_d02.txt"
ignore_iofields_warning = .false.,
auxhist7_outname = "entrain_d<domain>_<date>"
auxhist7_interval = 5, 5,
frames_per_auxhist7 = 1,1,
io_form_auxhist7 = 2

&phys
kf_edrates = 1, 1 
```
I'm assuming here you are running with 2 domains. If only running with one, only one entry is needed per line.

## output_file_d01.txt
That file should contain the following line, only:
```
+:h:7:UDR_KF,DDR_KF,UER_KF,DER_KF,UMF_KF,REI_KF,ITERF_KF  
```

Repeat that exact line for output_file_d02.txt, or for however many domains you have.




