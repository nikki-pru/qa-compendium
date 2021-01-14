======================
Organizing Source Code
======================

In the `Fetch Master`_ section one of the steps was to create a ``master`` folder and then another ``master-portal`` folder inside it. This seems redundant at first glance but becomes very helpful when dealing with multiple portal versions.

Since the bundles folder gets created in the same directory as the ``*-portal`` folder, not having a top-level portal version folder could result in the following file structure:

.. code::
  
  L:\
  ├── 7.0.x-bundles
  ├── 7.0.x-portal
  ├── 7.1.x-bundles
  ├── 7.1.x-portal
  ├── 7.2.x-bundles
  ├── 7.2.x-portal
  ├── 7.3.x-bundles
  ├── 7.3.x-portal
  ├── master-bundles
  └── master-portal  

Whereas creating the top-level portal version folder could result in the following structure:

.. code::
  
  L:\
  ├── 7.0.x
  |   ├── 7.0.x-bundles
  |   └── 7.0.x-portal
  ├── 7.1.x
  |   ├── 7.1.x-bundles
  |   └── 7.1.x-portal
  ├── 7.2.x
  |   ├── 7.2.x-bundles
  |   └── 7.2.x-portal
  ├── 7.3.x
  |   ├── 7.3.x-bundles
  |   └── 7.3.x-portal
  ├── master
  |   ├── master-bundles
  |   └── master-portal
  └── master-snapshot-bundle
  
  .. _Fetch Master: ../fetch-master.rst