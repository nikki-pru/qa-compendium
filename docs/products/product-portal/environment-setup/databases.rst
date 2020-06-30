Databases
=========

MySQL 5.7/8
-----------
**Docker**
  ``docker run -p 3306:3306 --name mysql-docker -e MYSQL_ALLOW_EMPTY_PASSWORD=yes -e MYSQL_DATABASE=lportal -d mysql:5.7 --character-set-server=utf8``

Change tag to switch versions
  * mysql:5.7
  * mysql:8

**References**
  * `MySQL Docker Hub`_

  .. note::
    In order to use MySQL 8.0, we will need to use the new MySQL JDBC Connector/J 8.0 (copy from master/7.2)
    - Updated driver classpath: ``com.mysql.cj.jdbc.Driver``
    - Connector 8.0 also includes the old classpath: ``com.mysql.jdbc.Driver``
  .. note::
    Although backwards compatibility with the previous classpath is present, it is advised to use the updated classpath

------------------------------------------------------------

MariaDB 10.2
------------
**Docker**
  ``docker run -p 3306:3306 --name mariadb-docker -e MYSQL_ALLOW_EMPTY_PASSWORD=yes -e MYSQL_DATABASE=lportal -d mariadb:10.2 --character-set-server=utf8``
**References**
  * `MariaDB Docker Hub`_

------------------------------------------------------------

PostgreSQL 10.6
---------------
**Docker**
  ``docker run -p 5432:5432 --name psql-docker -e POSTGRES_DB=lportal -d postgres:10.6``
**Credentials**  
  Username: postgres
  PW: (blank)
**Portal-ext**
::
  jdbc.default.jndi.name=jdbc.default.driverClassName=org.postgresql.Driver
  jdbc.default.url=jdbc:postgresql://[ipaddress]:5432/[dbname]
  jdbc.default.username=postgres
  jdbc.default.password=

**References**
  * `How to use PostgreSQL`_
  * `PostgreSQL Docker Hub`_

------------------------------------------------------------

DB2 10.5
--------
VM
  * `DB2 10.5 QA Docs`_
  * `DB2 10.5 VM`_
  
------------------------------------------------------------

DB2 11.1
--------
**Docker**
1. Login to Docker hub and follow steps to get access to https://hub.docker.com/_/db2-developer-c-edition 

2. Create a new directory on your machine

3. In that new directory:
  * Add .env_list file
  * Mac users, set IS_OSXFS=true
  * ``docker run --name db2server --restart=always --detach --privileged=true -p 50000:50000 -p 55000:55000 --env-file .env_list store/ibmcorp/db2_developer_c:11.1.4.4-x86_64``
  * ``docker logs -f db2server``
  * ``Wait until "Setup has completed."``

4. Access container to complete setup
::
  docker exec -it db2server bash -c "su - db2inst1"``
  db2 drop database lportal``
  db2 create database lportal pagesize 32768 temporary tablespace managed by automatic storage``

5. Add db2jcc4 driver to bundle (lib/ext)

6. Portal-ext
::
  jdbc.default.driverClassName=com.ibm.db2.jcc.DB2Driver
  jdbc.default.url=jdbc:db2://0.0.0.0:50000/lportal:deferPrepares=false;fullyMaterializeInputStreams=true;fullyMaterializeLobData=true;progresssiveLocators=2;progressiveStreaming=2;
  jdbc.default.username=db2inst1
  jdbc.default.password=password

**VM**
  * `DB2 11 QA Docs`_
  * `DB2 11 VM`_

------------------------------------------------------------

SQL Server 2017
---------------
**VM**
  * `SQL Server 2017 Developer Edition installed against Ubuntu 16.04`_ (configured)
  .. note::
    Currently, SQL Server 2017 for Linux is only compatible with Ubuntu 16.04 (see References)

**Credentials:**
  user/pw: liferay/password

**Docker Linux / MacOSX**
1. Start Linux container for SQL Server 2017 (2019 should also work)
  * ``docker run --name <container-name> -e ACCEPT_EULA=Y -e SA_PASSWORD=<password>  -e MSSQL_PID=Developer -p 1433:1433 -d mcr.microsoft.com/mssql/server:2017-latest-ubuntu``
  .. note::
    Password must be at least 8 characters long and contain characters from three of the following four sets: Uppercase letters, Lowercase letters, Base 10 digits, and Symbols
2. Start a new bash instance for the SQL Server container
  * Wait ~90 seconds for SQL-Server to initialize
  * ``docker exec <container-name> /opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P <password> -Q 'CREATE DATABASE lportal'``
  * ``docker exec <container-name> /opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P <password> -Q 'alter database lportal set allow_snapshot_isolation on;'``
  * ``docker exec <container-name> /opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P <password> -Q 'alter database lportal set read_committed_snapshot on;'``
3. If server is not started in the container:
  ``/opt/mssql/bin/sqlservr &``

**Portal-ext**
::
  jdbc.default.driverClassName=com.microsoft.sqlserver.jdbc.SQLServerDriver
  jdbc.default.url=jdbc:sqlserver://0.0.0.0:1433;databaseName=lportal
  jdbc.default.username=sa
  jdbc.default.password=


**References**
  * `SQLServer Docker Hub`_
  * `SQLServer Linux Setup`_

.. _`How to use PostgreSQL`: https://github.com/liferay/liferay-qa-ee/blob/liferay-qa-docs/tutorials/databases/pages/how-to-use-postgresql.markdown
.. _`DB2 10.5 QA Docs`: https://github.com/liferay/liferay-qa-ee/blob/liferay-qa-docs/tutorials/databases/pages/how-to-use-db2.markdown
.. _`DB2 10.5 VM`: https://files.liferay.com/private/vms/vm-win2012r2/vm-win2012r2.vmdk.x64.db2-10.5.zip
.. _`DB2 11 QA Docs`: https://github.com/liferay/liferay-qa-ee/blob/liferay-qa-docs/tutorials/databases/pages/how-to-use-db2.markdown
.. _`DB2 11 VM`: https://files.liferay.com/private/vms/vm-win2012r2/vm-win2012r2.vmdk.x64.db2-10.5.zip
.. _`SQL Server 2017 Developer Edition installed against Ubuntu 16.04`: https://drive.google.com/open?id=1MTB9kPOwW0BTWe9KyBBFH10Nfpua1Hb6
.. _`MySQL Docker Hub`: https://hub.docker.com/_/mysql
.. _`SQLServer Docker Hub`: https://hub.docker.com/_/microsoft-mssql-server
.. _`SQLServer Linux Setup`: https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-setup?view=sql-server-2017
.. _`PostgreSQL Docker Hub`: https://hub.docker.com/_/postgres 
.. _`MariaDB Docker Hub`: https://hub.docker.com/_/mariadb