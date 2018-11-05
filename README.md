#######################################
##          FUCLONE 0.1 beta         ##
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
-----
1. Download and unzip fuclone.zip to local drive
2. modify fuclone.ini file 
3. run fuclone.exe -p setup. This will create DB and loads metadata
4. follow on screen instructions
5. wait for completion message

Cloning Tables:
------
1. modify table.txt by adding table names 1 per line
2. run fuclone.exe


Setup:
------
1. Fuclone.ini file: Key file storing connection details to all environments in separate sections which must enclosed between []. ini file is self explanatory for section parameters. 
	a) FUCLONE section stores local database connection info and this is mandatory and 1st section in file. 
	b) You can add any number of Fusion environments as sections, which can be passed on as run time option using switches --env or -e followed by the environment name. 
		If no environment name is passed then, 2nd section is considered for Fusion connection details.

2. tables.txt file: input file with list of table names to clone.

help: fuclone --help or fuclone -h
-----
usage: fuclone [-h] [--env ENV] [--log LOG] [--tables TABLES]
               [--process PROCESS]

Clone Fusion Cloud Database

optional arguments:
  -h, --help            show this help message and exit
  --env ENV, -e ENV     fusion cloud environment name
  --log LOG, -l LOG     log level to generate log file. allowed values: warning, error, info, debug
  --tables TABLES, -t TABLES
                        tables to clone from cloud, ex: T1, T2
  --process PROCESS, -p PROCESS
                        allowed values: clone, metadata, setup
                        clone: clone tables from cloud. default, if not given
                        metadata: reloads FND tables from cloud
                        setup: setup local db and loads FND tables

Examples: 
--------
1. fucone 		: runs with 2nd section details for fusion and table.txt for input list
2. fuclone -e uat	: runs for uat environment with connection details uat section in ini file. 
3. fuconle -e uat -t HZ_PARTIES: runs for uat and clones table HZ_PARTIES, ignoring table.txt file. 
4. fuclone -p metadata 	: reloads metadata 
