Cleaning up before starting up
===============================

Data Folder
------------
Navigate to your ``liferay.home`` and locate the ``/data`` folder. This data folder is Portal’s default file system storage and is heavily tied to the database. If you navigate through the ``/data`` folder into the ``document_library`` folder, you'll notice that the folders and files are numerically named. The numerical naming is how the database reads what gets displayed on Portal. We don’t necessarily need to understand how the DB reads the data, but it is important to know how closely these two things are related and to understand that whenever we make a change to the database, either by recreating it or replacing the DB completely, we are breaking that DB ↔ data folder link.

Our previous portal instance started up with HSQL and, thus, the data folder is linked to that database. Since the goal of this section is to start a Portal instance on MySQL, go ahead and delete the data folder from ``liferay.home``. This prevents Portal from throwing errors when it can’t find the DB-data folder links.

Log Folder
----------
Locate the /log folder on your ``liferay.home``. Since we’re starting a new instance on a new database, we no longer need these logs. Go ahead and delete that too.

Summary
-------
In summary of this, and the section on `Starting Fresh`_, what we need for a clean startup are the following:

1. Clean database
2. Clean data folder
3. Clean log folder

.. note::
  The ``/osgi/state`` folder in ``liferay.home`` is another directory that needs to be cleaned, but it is not necessary to do so unless you're replacing jar files in the osgi folder.

.. _Starting Fresh: ./starting-fresh.html
