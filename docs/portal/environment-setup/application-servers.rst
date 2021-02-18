===================
Application Servers
===================

Websphere 9
-----------

1. If using `Windows/MacOS`_: Configure Docker to use 6GB+ of Memory
2. Download `Websphere 9 image`_
3. Import ``docker load -i websphere9docker.tar``
4. Run ``docker run -it -p 8080:8080 -p 9060:9060 websphere9 bash``
5. Build master (head) into websphere ``./build-master.sh`` (inside the container, modify script as needed) **OR** Install Portal WAR manually. See this `example script`_.
6. Start/Stop Server
::
	/source/bundles/websphere-9.0.0.0/profiles/liferay/bin/startServer.sh server1
	/source/bundles/websphere-9.0.0.0/profiles/liferay/bin/stopServer.sh server1
7. Admin Console: ``http://localhost:9060/ibm/console``
  * Blank login

.. note::
  Known issue debugging on Websphere: `LPS-91368`_

**Docker**

* `Websphere 9 Dockerfile`_ (Not recommended to build manually, long build time, high bandwidth usage)

* `Detailed steps for using docker`_

* Another script for fixpack purpose: `setup-websphere.sh`_

* `Walkthrough Websphere docker with portal-ee branch <./websphere-portal-ee.rst>`_

------------------------------------------------------------

Wildfly 11
----------

Build locally with build scripts

------------------------------------------------------------

JBoss EAP 7.1
-------------

Build locally with build scripts

------------------------------------------------------------

Weblogic 12cR2
--------------
Build locally with build scripts

1. Set ``app.server.type=weblogic`` (app.server.USERNAME.properties)
2. ``ant -f build-dist.xml unzip-weblogic-custom``
3. ``ant -f build-test.xml prepare-portal-ext-properties`` (or manually add a portal-ext)
  a. ``liferay.home`` must be set
  b. portal-ext must be  in weblogic-12.2.1/domains/liferay/autodeploy/ROOT/WEB-INF/classes/
4. ``ant all``
5. ``cd LIFERAY_HOME/weblogic-12.2.1/domains/liferay``
6. ``./startWeblogic.sh``

`Installing a release version`_

`Weblogic 12cR2 Docker`_


.. _Windows/MacOS: https://docs.docker.com/docker-for-windows/
.. _Websphere 9 image : https://drive.google.com/file/d/1-eWlIqUXHlv4y15igLsYyqu6rWEvwqYe/view?usp=sharing
.. _example script: https://gist.github.com/vicnate5/89ed11f2d6c15735824e31da324957f0
.. _LPS-91368: https://issues.liferay.com/browse/LPS-91368
.. _Websphere 9 Dockerfile: https://gist.github.com/vicnate5/71ebade2b53fd6c227d4639136e1d567
.. _Detailed steps for using docker: https://github.com/liferay/liferay-qa-ee/blob/liferay-qa-docs/cnqa/fix-pack/manual-environments/debian9-websphere9.markdown
.. _setup-websphere.sh: https://github.com/liferay/liferay-qa-ee/blob/liferay-qa-docs/cnqa/fix-pack/manual-environments/setup-websphere.sh
.. _Installing a release version: https://gist.github.com/anthony-chu/a523114002dbbc14b4b41a0ab20a7760#file-installweblogic-sh
.. _Weblogic 12cR2 Docker: https://github.com/liferay/liferay-qa-ee/blob/liferay-qa-docs/cnqa/new-hire-training/How%20to%20Setup%20WebLogic12.markdown
