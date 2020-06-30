General Docker
===============

`Using Docker for QA Databases`_

`QA Presentation on using Docker`_ (Slides and recording included)

Container + Host Communication
-------------------------------
* IP of your local machine (as seen by the inside of a docker container)
  ``host.docker.internal``

  .. note::
    If a container is port-forwarded to your local machine (e.g. -p 8080:8080), use localhost:8080 to access from your local machine

Container + Container Communication
------------------------------------
1. Create a network
  ``docker network create mynetwork``

2. Add flag when starting new containers
  ``--network mynetwork``

3. Connecting existing container to network
  ``docker network connect <network> <container>``

4. Use container ``name`` for the IP address between containers on the same network
	 Example:
   
	 * Container 1: Portal
	 * Container 2: MySQL

  Container 1 portal-ext:
    ``jdbc.default.url=jdbc:mysql://mysql-docker:3306/lportal?characterEncoding=UTF-8&dontTrackOpenResources=true&holdResultsOpenOverStatementClose=true&useFastDateParsing=false&useUnicode=true``

5. Enter Command Line for a running container
  ``docker exec -it CONTAINER_NAME bash``

-----------------------------------------------------

Docker for Windows
------------------

**Networking Containers**

To create a network in which Windows containers can communicate with one another, the driver type must be specified as *transparent* (different from Linux containers, where default driver type is *bridge*):

  ``docker network create -d transparent my_network``

In order to communicate between the container and the host, use the host's IP address as opposed to *host.docker.internal*.

Windows containers on Windows currently have some limitations and are not recommended for environment cert testing as they cannot communicate with your local machine or other containers.

**Known issues on Windows containers:**

* `Cannot use networking`_ (container to container communication)
* `Cannot resolve host.docker.internal` (container to host communication)

.. _`Using Docker for QA Databases`: https://github.com/liferay/liferay-qa-ee/tree/liferay-qa-docs/tutorials/databases/pages/docker
.. _`QA Presentation on using Docker`: https://docs.google.com/document/d/1UZiqttTDTTPBzHLq_0XMesOM4zuz2A3FeH9GWMaARRM/edit?usp=sharing
.. _`Cannot use networking`: https://github.com/docker/for-win/issues/1960
.. _`Cannot resolve host.docker.internal`: https://github.com/docker/for-win/issues/1976