# 	Python Framework for data loads

## 	Pre-requisite.
	1. update python to python 3.6
		- yum install -y https://centos7.iuscommunity.org/ius-release.rpm
		- yum install -y python36u python36u-libs python36u-devel python36u-pip

	2. change links from python 2 to python 3
		cd /usr/bin/
		ln -s python3.6 python3
		rm -f python
		ln -s python3 python

	3. Update packages using requirement.txt
		python -m pip install -r requirement.txt
	4. Have oracle client installed. 
		- Set ORACLE_HOME and LD_LIBRARY_PATH
		Ex: ORACLE_HOME=/usr/share/oracle-client/instantclient_18_3
		LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/share/oracle-client/instantclient_18_3
		- Put end system connection in $ORACLE_HOME/network/admin/tnsnames.ora file
		Ex: ppp.prod=
		(DESCRIPTION =
		 (ADDRESS =
		  (PROTOCOL = TCP)(HOST =ne1itcprhdb39.corp.intranet)(PORT = 1645)
		)
		(CONNECT_DATA =
		  (SERVER = DEDICATED)
		  (SERVICE_NAME = instlprd)
		 )
		)
	5. Access to Mysql instance. Please update connection details in Constants.py
	6. Access to Neo4j instance running. Please update connection details in Constants.py
	

## 	Tables in mysql
		1. HYPERLITE_TASK : Keep the Tasks information along with oracle query and Cypher Query.
		2. HYPERLITE_CONNECTION : Keep the connection information of Oracle database.
		3. HYPERLITE_TASK_PARAM : Keep the PARAM_ID information for respective task along with start time and created date.
		4. HYPERLITE_TASK_STATUS : It keeps track of RUN_STATUS for all the tasks.


## 	script name and detail
		1. OracleToNeo4J.py : This script does all the logics of getting the data from Oracle db and writing it to csv file and then loading the data to graph database Neo4J.
		2. Connector.py : This script is for getting the connection from oracle database and my_sql database.
		3. Constants.py : Constants related to Oracle database and Neo4J database are defined in this file.
	
## How to run
		cd {location of python script}
		python OracleToNeo4J.py <TASK_ID>

## enable crons
		Ex: 5,20,35,50 2-22 * * * . $HOME/.bash_profile; cd /var/lib/neo4j/hyperlite_dataloads/python-load/OracleToNeo4J; python OracleToNeo4J.py 2 >> /var/lib/neo4j/hyperlite_dataloads/PPP_Notes.log 2>&1


## How to add new task
		1. create new row in hyperlite_Task table
			- insert sql
			- insert cypher
		Use heidi sql to insert sql and cypher statements [ these have to be in correct format ]
		
		2. create new connection, if not already present for source system, in table hyperlite_conncetion
		3. create new parameter value for start date
	


