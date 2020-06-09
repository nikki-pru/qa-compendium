What just happened? Making Sense of Startup
============================================
As mentioned in the `How does it work?`_ section, a user needs the **code base**, an **application server**, and a **database** to get started.

Code base → Downloaded bundle
------------------------------
The bundle we downloaded has all the code necessary to run Portal. Source code is unusable in its raw form, but what was just downloaded is code that has been precompiled into a bundle that is readily usable. The precompiled code, or jars (java archives), can be found in the {liferay.home}/osgi folder. We will discuss the uncompiled source code at a later time.

Application server → Tomcat
----------------------------
An app server provides an environment where the application (Liferay Portal) will run. For this bundle we used Tomcat. Liferay portal is `not limited`_ to running on the Apache Tomcat server and we do test portal on multiple app servers. For our purposes, we will only be testing on Tomcat unless otherwise asked to do so. Should we come to that, instruction will be provided on how to set up a different app server.

Database → Hypersonic
----------------------
View your console/terminal log and look for something similar to:
``[main][DialectDetector:158] Using dialect com.liferay.portal.dao.orm.hibernate.HSQLDialect for HSQL Database Engine 2.3.``

This line in the console log indicates which database your instance is using. Liferay Portal comes bundled with Hypersonic (HSQL) which is an embedded database useful for development and demonstration purposes. Like with app servers, Portal is not tied solely to HSQL. Our customers can use whichever DB they need for their business, 9 of which `are certified`_ to work with Portal.

For our testing purposes, we can use HSQL for quick checks, but using MySQL 5.7 is highly recommended since this is the database that most of our customers use. Let’s set up MySQL for use with Portal in the next section.

.. _How does it work?: ./portal.html#how-does-it-work
.. _not limited: https://web.liferay.com/documents/14/21598941/Liferay+DXP+7.2+Compatibility+Matrix/b6e0f064-db31-49b4-8317-a29d1d76abf7?
.. _are certified: https://web.liferay.com/documents/14/21598941/Liferay+DXP+7.2+Compatibility+Matrix/b6e0f064-db31-49b4-8317-a29d1d76abf7?
