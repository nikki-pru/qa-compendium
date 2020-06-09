Starting Up A Portal instance
==============================

1. Go to our `Index of Releases`_ and download 7.2.1 GA2 - Tomcat.
2. Unpack the bundle on your local machine and note the directory.
3. Navigating into the directory, you should see the following files and folders. This directory is your ``liferay.home``.

|image0|

4. On CMD/Terminal, navigate to {liferay.home}/tomcat-9.0.17/bin.
5. Start Tomcat
  * On Windows: ``catalina run``
  * On Linux/Mac: ``./catalina.sh run``
6. Wait for the console log to indicate that the server is up. It should say something like ``Server startup in [_____] milliseconds``. A browser window should pop-up on ``localhost:8080``.
7. Finish Configuration and agree to the Terms of Use. If Portal asks for credentials, use the following:
  * Email address: test@liferay.com
  * Username: Test
  * Password: Test
8. Welcome to Liferay Portal!

⚠️ Show your trainer that Portal is up and running on your machine.

.. _Index of Releases: https://releases.liferay.com/portal/

.. |image0| image:: ./img/liferayhome.PNG
