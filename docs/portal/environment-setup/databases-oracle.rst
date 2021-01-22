================
Oracle Databases
================

Oracle 12.2
------------

Login to Docker hub and follow steps to get access to `Oracle Database Enterprise`_.

If you haven’t already, log into Docker Hub via your local terminal with your username:
``docker login --username=<username>``

``docker run -d -p 1521:1521 -it --name oracle12 store/oracle/database-enterprise:12.2.0.1``
(wait 2 minutes for full startup)
``docker exec -it oracle12 bash -c "source /home/oracle/.bashrc; sqlplus /nolog;"``

**In sqlplus**

#. ``connect sys/Oradoc_db1 as sysdba;``
#. ``alter session set "_ORACLE_SCRIPT"=true;``
#. ``create user lportal identified by lportal;``
#. ``grant all privileges to lportal;``

Add `driver`_ to bundle (lib/ext)

Alternate one liner to setup database (can be scripted), have script sleep for the startup time if you want to setup oracle in one script:
::
  docker exec oracle /bin/bash -c "source /home/oracle/.bashrc; echo -e 'connect sys/Oradoc_db1 as sysdba; \n alter session set \"_ORACLE_SCRIPT\"=true; \n create user lportal identified by lportal; \n grant all privileges to lportal;' | sqlplus /nolog"

**Portal-ext**
::
  jdbc.default.driverClassName=oracle.jdbc.OracleDriver
  jdbc.default.url=jdbc:oracle:thin:@0.0.0.0:1521:ORCLCDB
  jdbc.default.username=lportal
  jdbc.default.password=lportal

**VM**
  `How to Use Oracle`_
  
------------------------------------------------------------

Oracle 19c
----------

**Docker**

Reference to `Oracle Database Single Instance`_

1. Download Oracle 19c image via ``docker pull yangcao/oracle-19c:19.3.0-ee``
2. Create container by:
::
  docker run --name oracle19c -p 1521:1521 -p 5500:5500 -e ORACLE_SID=ORCLCDB -e ORACLE_PDB=ORCLPDB1 -e ORACLE_PWD=Oracle19 -d yangcao/oracle-19c:19.3.0-ee

3. See logs by ``docker logs -f oracle19c`` look like the following output:

  .. image:: ./img/01-Oracle19c-log.png

  .. image:: ./img/02-Oracle19c-log.png

When the DATABASE IS READY TO USE displays, the oracle container is created successfully.

4. Open a new terminal, access to oracle container by ``docker exec -it oracle19c bash``
5. Access to oracle CMD terminal by ``sqlplus``
6. Login by ``system`` and ``Oracle19``
7. Set session status to read-write by ``alter session set "_ORACLE_SCRIPT"=true;``
8. Create user by ``create user lportal identified by lportal;``
9. Grant privileges to user by ``grant connect,resource,dba to lportal;``
10. Add `driver to bundle` (lib/ext)
11. Edit portal-ext.properties:
::
  jdbc.default.driverClassName=oracle.jdbc.OracleDriver
  jdbc.default.url=jdbc:oracle:thin:@0.0.0.0:1521:ORCLCDB
  jdbc.default.username=lportal
  jdbc.default.password=lportal
  setup.wizard.enabled=false
12. Start bundle

.. _Oracle Database Enterprise: https://hub.docker.com/_/oracle-database-enterprise-edition
.. _driver: https://files.liferay.com/private/jdbc/oracle/12.2.0.1/ojdbc8.jar
.. _How to Use Oracle: https://github.com/liferay/liferay-qa-ee/blob/liferay-qa-docs/tutorials/databases/pages/how-to-use-oracle.markdown
.. _Oracle Database Single Instance: https://github.com/oracle/docker-images/tree/master/OracleDatabase/SingleInstance
.. _drive to bundle: https://files.liferay.com/private/jdbc/oracle/12.2.0.1/ojdbc8.jar
