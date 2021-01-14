Building master
^^^^^^^^^^^^^^^^

The source code we have pulled is still in its raw form at this point. As mentioned previously, code in its raw form is unusable by a machine. This section explains how to build portal into a usable bundle which we can then run on a server and then interact with.

Configuration Files
--------------------
In your master-portal directory, you will find two property files that control how we build/compile bundles. These two files are the build.properties and app.server.properties file. These properties determine the location of the bundle, which app server to build and the version of the app server to be built.

`If you recall`_ we are not to edit *.properties files directly. To override what’s in the properties file so we can make changes specific to our build, we create the following files in the master-portal directory: ``app.server.{computername}.properties`` and ``build.{computername}.properties``.

1. **app.server.{computername}.properties**:

Within this file, you should declare specifically where your Liferay bundle will be located and what application server you want Liferay to be built on. To do so, your app.server.{computername}.properties file should contain these lines
:
::
  app.server.parent.dir={directory}/master-bundles
  app.server.type=tomcat

2. **build.{computername}.properties**:

Within this file, you should declare specifically where the "project" directory is located. This is a similar setting, based on the app server directory. To do this, your build.[computername].properties file should contain this line
:
::
  app.server.dir={directory}/master-bundles/tomcat-9.0.37

.. note::
  ``{directory}`` should be where your master-portal folder is, making the master-bundles folder parallel to master-portal.

Let’s test out our property files. On your master-portal directory, run
	``ant -f build-dist.xml unzip-tomcat``

Check if portal created a master-bundles folder with the app server the same directory as your master-portal folder. If your result is something else, please check with your trainer.

ant all
---------
Now you are ready to build/compile master-portal. Run the following commands
:
::
	ant setup-sdk
	ant setup-profile-dxp
	ant all

When this is done, startup portal from your master-bundles directory.

⚠️  Show your trainer that portal has started up from your master-bundles directory
To stop the server, hit ``Ctrl+C``.

.. _If you recall: ../portal/portal-ext.html
