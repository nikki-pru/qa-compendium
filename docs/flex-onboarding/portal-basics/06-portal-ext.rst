Portal-ext.properties
======================

Hidden within the source code is a file that controls how Portal can be configured. This is the `portal.properties`_ file. It contains most the default settings that Portal will use at startup. Take a minute to look through the linked properties file to get a glimpse of all that this file controls.

Since portal.properties contains most of the configurations Portal needs, it is not recommended to edit this file (or any *.properties files) directly. Instead, we override these settings using a ``portal-ext.properties`` file that we add to our ``liferay.home`` directory.

Setting up portal-ext.properties
---------------------------------

1. Create a blank portal-ext.properties file in your ``liferay.home``.
2. Because we want to start Portal with MySQL instead of the default HSQL, we need to configure portal-ext to look for MySQL. To do this, copy the MySQL properties from portal.properties into your portal-ext.properties files.
3. Remove the # comment marks to make the properties usable.
4. If you are using a database other than lportal, locate lportal from ``jdbc.default.url=`` and replace it with your database name.
5. If you did not create a no-name user with a null password in the MySQL Basics section, fill in the username and password properties. Else, leave these blank.
6. Save the file.
7. After configuring the portal-ext file, the file should look similar to this `portal-ext.properties`_ file.

Starting up a portal instance with MySQL
-----------------------------------------
Now that you have a portal-ext file, check if you have the following before starting the server:
	* Bare database;
	* Portal-ext pointing to your database; and,
	* Clean environment (no data folder, no logs)
If you’ve checked all of the above, start the server and wait for Portal to load on the browser.

⚠️ Show your trainer that Portal is up and that the database used is MySQL.

.. _portal.properties: https://github.com/liferay/liferay-portal/blob/master/portal-impl/src/portal.properties
.. _portal-ext.properties: https://gist.github.com/calvinctvo/121078d1e4d9c4acf2a5c533bee86f19
