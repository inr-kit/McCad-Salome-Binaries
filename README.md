
***ATTENTION*** An important bug is fixed on windows version!! 
**************************************************************************************
McCad-Salome: MC geometry conversion tool McCad under Salome platform. 

McCad is a geometry conversion tool developed at KIT to enable the automatic conversions of CAD models into the Monte Carlo (MC) geometries. This version of McCad is integrated into the open-source Salome platform. 

For any questions related to the use of this software/library you may contact Ulrich Fischer(ulrich.fischer@kit.edu) or, for technical assistance, contact Lei Lu (lei.lu@kit.edu) and Yuefeng Qiu (yuefeng.qiu@kit.edu).
**************************************************************************************
********Something to know before going on********

This document describes the procedure of installing McCad binaries. For compiling McCad, please find descriptions on Github repository [McCad-Salome-Source](https://github.com/inr-kit/McCad-Salome-Source). For Using McCad, Please find documents on Github repository [McCad-Salome-Docs](https://github.com/inr-kit/McCad-Salome-Docs).

This release is tested under Salome_7.4.0. Using other Salome version is not guarantee to work, and might cause error during this process. 


**************************************************************************************
********Installation and run McCad on Windows ********

* Download Salome_7.4.0 platform from http://www.salome-platform.org/downloads/previous-versions/salome-v7.4.0 . 

  * The version you need is "binaries self-extracting archive for 64bits Windows". 
	
  * You need to register for downloading Salome. 

* Extract the Package into a folder, here brief as $SALOME (be sure to replace it with actual path during installation). 

* Download the "MCCAD_0.5.0-beta_for_Salome_7.4.0_WIN64.zip", extract it and place it under $SALOME/MODULES. Under $SALOME\MODULES\MCCAD there are three folder: 

  *  bin
  * lib
  * share
	
* We need to add MCCAD into the Salome environment. First make a backup of file $SALOME\env_launch.bat

  * in line 29, add "MCCAD" into the "m_list" (add it anywhere inside the parenthesis, separate with at least one whitespace)
	
  * in line 42, add "GUI GEOM MED SMESH PARAVIS MCCAD" into "env_m_list"(add them inside the parenthesis, separate with at least one whitespace).

* To run McCad, start cmd.exe in the Windows Start menu, and run the following command:

  * $SALOME\run_salome.bat --module=MCCAD
	
  * If you want to start also geometry, meshing and visualization module, using command: $SALOME\run_salome.bat --module=GEOM,SMESH,PARAVIS,MCCAD
	
* One more easy way to run the program is:

  * right-click $SALOME\run_salome.bat and "Send to -> Desktop (short-cut)";
	
  * right-click the short-cut link in the Desktop, choose "properties";
	
  * Behind the value of "Target", add " --module=MCCAD" or "
	--module=GEOM,SMESH,PARAVIS,MCCAD"(with a whitespace in the front). click "OK". Next time you can start McCad with this short-cut link. 


**************************************************************************************
********Installation and run McCad on Linux ********

* Download Salome_7.4.0 platform from http://www.salome-platform.org/downloads/previous-versions/salome-v7.4.0 . 

  * Under the list "Binaries for officially supported Linux platforms", Choose the version which is closest to your OS. 
	
  * You need to register for downloading Salome. 


* Extract the zip file into a folder, then go into this folder and run the script "runInstall". A install wizard window will come out. 

* Click always "Next", and keep the default value if you don't care.

  * If you like, you can change the installation folder;
	
  * It is highly recommended to install all modules except DOCUMENTS, in order to avoid unncessary error.
	
  * There might be warnings on "cppunit" libraries and so on, it won't affect the use of Salome. 
	
* We abbreviate the Salome install folder as $SALOME.

* Download the corresponding McCad binary. Try to choose the version closest to your OS. If it does not work after the following installation, the only solution is to download the McCad source code and compiled the binary by yourself. 

* Extract the zip file and place it under $SALOME. Be sure that your $SALOME/MCCAD_0.5.0 folder have following folders:

  * bin
  * lib
  * share
  * adm_local
  * idl
  * include

* Open $SALOME/KERNEL_7.4.0/salome.sh, add the following environment variables into this file.
```
	#------ MCCAD ------
	export MCCAD_ROOT_DIR=${INST_ROOT}/MCCAD_0.5.0
	if [ -n "${ENV_FOR_LAUNCH}" ] ; then
	  if [ "${ENV_FOR_LAUNCH}" = "1" ] ; then
		exportp PATH ${MCCAD_ROOT_DIR}/bin/salome
		exportp LD_LIBRARY_PATH ${MCCAD_ROOT_DIR}/lib/salome
		exportp PYTHONPATH ${MCCAD_ROOT_DIR}/bin/salome:${MCCAD_ROOT_DIR}/lib/python${PYTHON_VERSION}/site-packages/salome
	  fi
	fi
	##
	#------ MCCAD_src ------
	export MCCAD_SRC_DIR=${INST_ROOT}/MCCAD_SRC_0.5.0
```
* In your desktop, create a new file "runSalome.sh" and put following text into this file(replacing $SALOME with actual path!!): 
```
	#!/bin/bash
	source $SALOME/KERNEL_7.4.0/salome.sh
	$SALOME/salome_appli_7.4.0/salome --module=GEOM,SMESH,PARAVIS,MCCAD
```
* Under Desktop, make this file as executable script using this command:

	chmod +x ./runSalome.sh

* You can run McCad-Salome with running this script now. 


**************************************************************************************
For more information, you can find in our publications.

* Yuefeng Qiu, Lei Lu, Ulrich Fischer, Integrated approach for fusion multi-physics coupled analyses based on hybrid CAD and mesh geometries, Fusion Engineering and Design, Available online 4 July 2015, ISSN 0920-3796, http://dx.doi.org/10.1016/j.fusengdes.2015.06.118.

* L. Lu, U. Fischer, P. Pereslavtsev, Improved algorithms and advanced features of the CAD to MC conversion tool McCad, Fusion Engineering and Design, Volume 89, Issues 9–10, October 2014, Pages 1885-1888, ISSN 0920-3796, http://dx.doi.org/10.1016/j.fusengdes.2014.05.015.

Have fun!
