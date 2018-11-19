#######################################
##             FUCLONE 1.0           ##
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

Setup:
------
1. Fuclone.ini file: Key file storing connection details to all environments in separate sections which must enclosed between []. ini file is self explanatory for section parameters. 

	1.1. FUCLONE section stores local database connection info and this is mandatory and 1st section in file. 
	
	1.1. You can add any number of Fusion environments as sections, which can be passed on as run time option using switches --env or -e followed by the environment name. If no environment name is passed then, 2nd section is considered for Fusion connection details.

2. tables.txt file: input file with list of table names to clone. wildcard % use is allowed to specify a table name pattern.

Cloning Tables:
------
1. modify table.txt by adding table names 1 per line
2. run fuclone.exe

help: fuclone --help or fuclone -h
-----
usage: fuclone [-h] [--env ENV] [--log LOG] [--tables TABLES]
               [--process PROCESS]

usage: fuclone [-h] [--env ENV] [--log LOG] [--tables TABLES] [--file FILE]
               [--process PROCESS]

Clone Fusion Cloud Database

optional arguments:
  -h, --help            show this help message and exit
  
  --env ENV, -e ENV     fusion cloud environment name
  
  --log LOG, -l LOG     log level to generate log file. allowed values: warning, error, info, debug
  
  --tables TABLES, -t TABLES
                        table(s) to clone from cloud. use with clone or fileload options
			
  --views VIEWS, -v VIEWS
                        view(s) to create. use with views process
			
  --file FILE, -f FILE  pipe seperated file path. use with fileload option
  
  --process PROCESS, -p PROCESS
  
                        clone: clone tables from cloud. default, if not given
			
                        metadata: reloads FND tables from cloud
			
                        setup: setup local db and loads FND tables
			
                        tables: creates all Fusion tables
			
                        views: creates fusion views
			
                        fileload: loads table from file., ex: fuclone -p fileload -t TBL -f filepath

Examples: 
--------
* fucone 			: clones tables listed in table.txt
* fuclone -e uat		: runs for uat environment with connection details uat section in ini file. 
* fuconle -e uat -t HZ_PARTIES	: runs for uat and clones table HZ_PARTIES, ignoring table.txt file. 
* fuclone -p metadata 		: reloads metadata 
* fuclone -p tables		: creates all tables from metadata
* fuclone -p tables -t a, b	: creates tables a and b from metadata
* fuclone -p tables -t HZ%	: creates tables with name starting 'HZ' from metadata
* fuclone -p views     	: creates all views from metadata
* fuclone -p views -v DOO_LINES_ALL_V: creates DOO_LINES_ALL_V views from metadata
* fuclone -p views -v doo%	: creates all views with name starting 'DOO' from metadata
* fuclone -p fileload -t hz_parties -f c:\hz_parties.txt: loads hz_parties table from psv file hz_parties.txt 

fileload: 
--------
Clone process may fail for a very large table (size in gigs) with timeout error to avoid server crashes. In such cases locate the job, download the file and run fuclone with fileload switch to load table.

Known Issues:
------------
If the tool fails with error 'ORA-12899: value too large for column', it means table definition is not matching with its  metadata. It is observed that metadta is not 100% accurate. In suchcase, find the actual length, update respective row in FND_COLUMNS table and run the tool again.

Release History:
----------------
1.0      15/11/18: Fuclone 1.0 released.

0.3 beta 14/11/18: New process switch Views added. Bug fixes and performance fixes.

0.2 beta 08/11/18: 2 new process switches tables and fileload are added to support tables creation and populating tables from a file.

0.1 beta 01/11/18: Initial beta version released. 
