# NEMO-docs
NEMO workflow and instruction documentation

This documentation is to briefly introduce NEMO3.6 OGCM and to run the noCC / CC experiments via the model. 

NEMO file folders: ../
- ARCH      (set computing center: e.g., HPC)
- CONFIG    (set configuration)
- EXTERNAL
- fcm-make
- NEMO      (original code; should not be changed; copy it)
- SETTE
- TOOLS
- License_CeCILL.txt

Main floders: ../
- CONFIG
-     /ORCA1_PISCES_FLX  (PISCES flux-based experiments)
-       /MY_SRC  (fortran code for parameters???)
-       /BLD/bin/nemo.exe  (executable)
-       /PARAM   (can be identified)
-           /NAMELIST  
-               /namelist_ref  (default file; should not be changed)
-               /namelist_pisces_cfg  (your configuration file)
-           /XML  (output set-up: e.g., 'yearly' / 'monthly')
-               /file_def_nemo-opa.xml  (???)
-               /field_def_nemo-opa.xml  (variables)
-       /SCRIPTS   (can be identified? job computing)

- NEMO  (never be changed)
-     /OPA_SRC
-       /SBC  (surface boundary conditions)
-       /LBC  (lateral boudary conditions)
-       /TRA  (tracers: e.g., T/S)
-       /ZDF  (mixing schemes)
