=================
Operating Systems
=================

Ubuntu 18.04
-------------

`Dockerfile with portal snapshot <https://github.com/anthony-chu/docker/tree/master/operating-systems/ubuntu-1804>`_

------------------------------------------------------------

Windows Server 2016
-------------------

Docker
~~~~~~

.. note::
  See `Warning for Windows Containers <https://docs.google.com/document/d/1gTqqemvzg0ibiAZ7FPe1jPUSML1xWhmdCkkrvLWFKRo/edit#heading=h.lst9bbtb4gwz>`_

**Prerequisites**

* You must be on a Windows machine
* Windows 10 version >= 1709 or build >=16629

**Zulu OpenJDK 8**

* `Base Image <https://hub.docker.com/_/microsoft-java-jdk>`_
* `With Portal (running Tomcat + HSQLDB) <https://github.com/anthony-chu/docker/tree/master/operating-systems/win-server-2016/zulu-openjdk8>`_

**AdoptOpenJDK JDK8**

* `With Portal (running Tomcat + HSQLDB) <https://github.com/anthony-chu/docker/tree/master/operating-systems/win-server-2016/adoptopenjdk8>`_

------------------------------------------------------------

Windows Server 2019
-------------------

Docker
~~~~~~

.. note::
  See `Warning for Windows Containers <https://docs.google.com/document/d/1gTqqemvzg0ibiAZ7FPe1jPUSML1xWhmdCkkrvLWFKRo/edit#heading=h.lst9bbtb4gwz>`_

**Prerequisites**

* You must be on a Windows machine
* Windows 10 version >= 1809 or build >=17763

`Dockerfile <https://github.com/anthony-chu/docker/tree/master/operating-systems/win-server-2019>`_

**Reference**

* `Windows Container Version Compatibility <https://docs.microsoft.com/en-us/virtualization/windowscontainers/deploy-containers/version-compatibility>`_ (Microsoft Docs - Containers on Windows)

VM
~~

* `VMWare <https://drive.google.com/open?id=1bDkM8QkqZQunGgpyg751fvPz1y5QZBXi>`_
* Credentials - user/pw: Administrator / Password1

------------------------------------------------------------

OpenSUSE 12
-----------

VM
~~

* `VMWare <https://drive.google.com/open?id=198SNlAs4UT0OyOBGWDqX145WgecRrO6P>`_
* Credentials are provided in the README file
* License, LCS token are already provided in the ~/Downloads directory

------------------------------------------------------------

OpenSUSE 15
-----------

Docker
~~~~~~

* Start: ``docker run -it -p 8080:8080 opensuse/leap bash``
* Install Java (Oracle openJDK 8): ``zypper install java-1_8_0-openjdk``

------------------------------------------------------------

Debian 9
--------

`Docker <https://hub.docker.com/_/debian/>`_

------------------------------------------------------------

Oracle Linux 7
--------------

`Docker <https://hub.docker.com/_/oraclelinux/>`_

------------------------------------------------------------

Alpine Linux 3.8
----------------

`Docker <https://hub.docker.com/_/alpine>`_

To use same base image as our official docker images, use ``openjdk:8u171-jdk-alpine3.8``

------------------------------------------------------------

Solaris 11
----------

`VM <https://files.liferay.com/private/vms/legacy/vm-sol11/>`_

------------------------------------------------------------

CentOS 7
--------

`Docker <https://hub.docker.com/_/centos>`_

------------------------------------------------------------

(Selling Your Soul to) AIX
--------------------------
`Instructions written for AIX 7.1, please use AIX 7.2 instead <https://github.com/liferay/liferay-qa-ee/blob/liferay-qa-docs/tutorials/operating-systems/pages/how-to-set-up-ibm-aix-7.1.markdown>`_
