===
JDK
===

Using docker images

Oracle JDK 11
-------------

`Oracle JDK11 Docker File <https://hub.docker.com/r/sgrio/java-oracle/>`_

``docker build -t oraclese11 .``

.. warning::
  Oracle SE JDK cannot be distributed, which is why it may be gone from docker hub.

------------------------------------------------------------

Oracle OpenJDK 8
----------------

`Docker file <https://hub.docker.com/_/openjdk>`_

------------------------------------------------------------

Oracle OpenJDK 11
-----------------

`Oracle OpenJDK 11 <https://hub.docker.com/_/openjdk>`_

------------------------------------------------------------

IBM JDK 8
---------

`IBM JDK 8 Docker file <https://hub.docker.com/_/ibmjava/>`_

------------------------------------------------------------

Adopt JDK 8
-----------

`Adopt JDK 8 Docker <https://hub.docker.com/r/adoptopenjdk/openjdk8>`_

------------------------------------------------------------

Adopt JDK 11
------------

`Adopt JDK11 Docker <https://hub.docker.com/r/adoptopenjdk/openjdk11>`_

------------------------------------------------------------

Red Hat JDK 8
-------------

`Red Hat JDK 8 image <https://drive.google.com/file/d/1vQDgkd_lzlPW4VKcDv9AKdUzxry0x_ij/view?usp=sharing>`_

Import: ``docker load -i redhatjdk8.tar``

Run: ``docker run -it -p 8080:8080 redhatjdk8``

Image is Centos 7

Note: `Manual Installer <https://access.redhat.com/downloads/content/java-1.8.0-openjdk/1.8.0.191.b12-1.el7_6/x86_64/fd431d51/package>`_ requires access to Liferay subscription to Red Hat.

------------------------------------------------------------

Red Hat JDK 11
--------------

`Red Hat JDK 11 image <https://drive.google.com/file/d/1nDucG_IwFwZIHJCfv-Ea1pYoLSsZz6aN/view?usp=sharing>`_

Import: ``docker load -i redhatjdk11.tar``

Run: ``docker run -it -p 8080:8080 redhatjdk11``

`Detailed set up steps <https://github.com/liferay/liferay-qa-ee/blob/liferay-qa-docs/cnqa/fix-pack/manual-environments/RedHatOpenJDK11-CentOS7.markdown>`_


Image is Centos 7

Note: `Manual Installer <https://access.redhat.com/downloads/content/java-11-openjdk/11.0.1.13-3.el7_6/x86_64/fd431d51/package>`_ requires access to Liferay subscription to Red Hat

------------------------------------------------------------

Azul Zulu JDK 8
---------------

* https://hub.docker.com/r/azul/zulu-openjdk/ 
* https://hub.docker.com/_/microsoft-java-jdk (via Microsoft)

------------------------------------------------------------

Azul Zulu JDK 11
----------------

* https://hub.docker.com/r/azul/zulu-openjdk/
* https://hub.docker.com/_/microsoft-java-jdk (via Microsoft)

------------------------------------------------------------

Switching JDKs Windows
----------------------

**Command Prompt**

1. Open command prompt instance
2. Run batch command: ``set JAVA_HOME=C:\path\to\Java\installation`` (e.g., C:\Program Files\Java\jdk-11.0.1)

Note: SET will only change the variable for the current command prompt instance (safer than overriding or changing your system environment variable)

**Git Bash**

https://gist.github.com/anthony-chu/9f1c301ed025dd76d815dbebf3b0b0fd

------------------------------------------------------------

Switching JDKs Linux/MacOS
---------------------------

``export JAVA_HOME=/path/to/jdk/install``
(Only set for current terminal that is running app server)