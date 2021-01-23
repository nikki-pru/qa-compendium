==============================================
Websphere9 - build from a liferay-portal-ee branch in docker
==============================================

Environment Details
-------------------

.. list-table::
   :header-rows: 1

   * - Product
     - Version
   * - Java
     - OpenJDK JDK 8
   * - Operating System
     - Ubuntu 18.04
   * - Portal
     - EE (ie: 7.3.x)


Prerequisites
-------------


* docker
* `build-portal-ee.sh <build-portal-ee.sh>`_
* `websphere9docker.tar <https://drive.google.com/file/d/1-eWlIqUXHlv4y15igLsYyqu6rWEvwqYe/view?usp=sharing>`_

Setup docker files
------------------


* Clean up any existing websphere9 docker

.. code-block:: bash

  sudo docker ps -a                                   # Lists containers (and tells you which images they are spun from)

  sudo docker images                                  # Lists images

  sudo docker rm :raw-html-m2r:`<container_id>`       # Removes a stopped container

  sudo docker rm -f :raw-html-m2r:`<container_id>`    # Forces the removal of a running container (uses SIGKILL)

  sudo docker rmi :raw-html-m2r:`<image_id>`          # Removes an image
                                                      # Will fail if there is a running instance of that image i.e. container


* Place the following files in same folder:

  * `build-portal-ee.sh <build-portal-ee.sh>`_
  * `websphere9docker.tar <https://drive.google.com/file/d/1-eWlIqUXHlv4y15igLsYyqu6rWEvwqYe/view?usp=sharing>`_

* Navigate to folder with websphere9docker.tar and load the docker image and container

.. code-block:: bash

  sudo docker load -i websphere9docker.tar

  sudo docker run -it -p 8080:8080 -p 9060:9060 --name=websphere9 websphere9 bash

* Login to your container

  * ``sudo docker exec -it websphere9 bash``

Build websphere9 bundle
-----------------------


* Modify build-portal-ee.sh with your github user variables for liferay-portal-ee

  * GITHUB_OAUTH_TOKEN
  * user
  * branch

* Copy build-portal-ee.sh

  * ``sudo docker cp build-portal-ee.sh websphere9:/.``

* In docker websphere terminal:

  * ``sh build-portal-ee.sh``

Setup websphere9 server
-----------------------


* Start Server

  * ``/source/bundles/websphere-9.0.0.0/profiles/liferay/bin/startServer.sh server1``

* Open another terminal and monitor the systemout.log

  * ``sudo docker exec -it websphere9 bash``
  * ``tail -f /source/bundles/websphere-9.0.0.0/profiles/liferay/logs/server1/SystemOut.log``

* Go to admin console after server1 start

  * http://localhost:9060/ibm/console/
  * Click Log in directly

* Add Websphere settings

  * Under Servers > Server Types > WebSphere application servers > server1 > Java and Process Management > process definition > java virtual machine >

    * Set Initial heap: 512
    * Set Max Heap: 2048 (You can also set this to 4096 for a better performance)

  * Click OK > Save

* Stop the server

  * ``/source/bundles/websphere-9.0.0.0/profiles/liferay/bin/stopServer.sh server1``

* Restart the server

  * ``/source/bundles/websphere-9.0.0.0/profiles/liferay/bin/startServer.sh server1``

* Go to Applications > Application Types > Websphere Enterprise Applications

  * check that liferay has started

* login to http://localhost:8080
