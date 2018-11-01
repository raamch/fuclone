#######################################
##          FUCLONE 1.0 beta         ##
#######################################

Fuclone application clones tables from Fusion cloud to local database.

Fuclone package files:
----------------------
1. fuclone.exe
2. fuclone.ini
3. tables.txt
4. Extract_Report.xdoz
5. Readme.txt

Installation: 
1. Download and unzip fuclone.zip to local drive.
2. run fuclone.exe file


Setup:
------
1. Fuclone.ini file: Key file storing connection details to all environments in separate sections which must enclosed between []. ini file is self explanatory for section parameters. 
	a) FUCLONE section stores local database connection info and this is mandatory and 1st section in file. 
	b) You can add any number of Fusion environments as sections, which can be passed on as run time option using switches --env or -e followed by the environment name. 
		If no environment name is passed then, 2nd section is considered for Fusion connection details.

2. tables.txt file: input file with list of table names to clone.


Usage: various examples given below. Also, fuclone -h or fuclone --help shows different options to run.
------
1. fucone 			: runs with 2nd section details for fusion and table.txt for input list
2. fuclone -e uat	: runs for uat environment with connection details uat section in ini file. 
3. fuconle -e uat -t HZ_PARTIES: runs for uat and clones table HZ_PARTIES, ignoring table.txt file. 

