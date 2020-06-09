Starting Fresh
===============

In this section, we will learn some MySQL basics, how the database connects to portal, and at the end of this section, we should have Portal up and running on the Tomcat app server and the MySQL database.

MySQL Basics
-------------
Portal creates the tables needed for the database at startup. All it needs is a bare (empty) database. We will learn how to do that, and other basic MySQL commands, in this section.

Access MySQL Shell
^^^^^^^^^^^^^^^^^^
  ``$ mysql -u root``
*Then enter password if prompted. You may have created this password during install.*

Create a new user
^^^^^^^^^^^^^^^^^
  ``mysql > create user ‘username’@’ipaddress’ identified by ‘password’;``

For  our testing, it easier to create a no-name user at localhost identified by a null password. This reduces issues that relates to incorrect passwords or wrong usernames. To do that, we run this command:

  ``mysql > create user ''@'localhost' identified by '';``

Another option is to create a user at '%'. This allows the no-name user to access the DB from any IP address.

Grant database privileges
^^^^^^^^^^^^^^^^^^^^^^^^^^
  ``mysql > grant all privileges on *.* to ''@'localhost';``
Since Portal creates its own tables, it needs database privileges to do so. In fact, it would need all privileges.
If you created the user at '%'', don’t forget to grant privileges to that user too.

⚠️ On MySQL, run the following commands and show your trainer the results:
  1. ``mysql > select user, host from mysql.user;``
  2. ``mysql > show grants for ‘’@’localhost’;``


Create a bare database
^^^^^^^^^^^^^^^^^^^^^^^
  ``mysql > create database dbname char set utf8;``
You can name the database whatever fits your testing needs. As a standard, we name the liferay database lportal. To create the lportal database, we would run

  ``mysql > create database lportal char set utf8;``
If you are testing multiple portal versions later on, you may change the database name to master, 72x, 71x or whatever fits your needs. The DB name doesn’t matter as long as it’s declared in a properties file that we will discuss in the next section.

Delete a database
^^^^^^^^^^^^^^^^^^
  ``mysql > drop database dbname;``

Show all databases
^^^^^^^^^^^^^^^^^^
  ``mysql > show databases;``

Feel free to test the Delete, Show and Create commands above but make sure that the lportal database is available to use before moving on to the next section. Other useful commands can be found `here`_.

.. _here: https://github.com/liferay/liferay-qa-ee/blob/liferay-qa-docs/tutorials/databases/pages/how-to-use-mysql.markdown#create-a-database
