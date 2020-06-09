New Properties for Modules' test.properties for ci:test:relevant
=================================================================

New properties have been introduced that can be used in each module’s test.properties with completion of `Explore adding backend test batches into test.properties files within a module`_. 

Currently allowed properties
-----------------------------

``modules.includes.required``
  All PQLs and backend tests from the modules specified will be included when change has been detected in this module 
  
  .. warning::
    There are plans to deprecate this property in the future, if possible please refrain from using this property and switch to using a combination of the new properties instead. See the `Example section`_ at the bottom of this document to see how this can be achieved.

``test.batch.run.property.query``
  Specifies the PQL for functional tests to run when this module has been modified.

New additional properties
--------------------------
Support has been added for these new properties in order to make test selection more granular:

``modules.includes.required.functional``
  This property functions exactly the same as the already allowed ``modules.includes.required`` property, except that it will only apply to functional batches in order to include PQLs from another module.

``modules.includes.required.test.batch.class.names.includes``
  This property allows a list of globs relative to the `liferay-portal/modules` directory in order to include *additional* tests in other modules.
  
  This works just like the `test.batch.class.names.includes property in liferay-portal/test.properties`_
  
  Globs  **DO NOT** need to be specified for tests within your own module, all backend tests within modified modules will be included by default.

``modules.includes.required.test.batch.class.names.excludes``
  This property allows a list of globs relative to the ‘liferay-portal/modules’ directory in order to exclude tests matching the globs.
  
  This property **CAN** be used to exclude any tests including the tests in your own module.

How to use
----------
Specified properties will take effect during a `ci:test:relevant` run whenever change has been detected in that module, see `Example`_.

Specifically, globs can be specified for each batch (or use a wild card to match multiple batches):
::

  modules.includes.required.test.batch.class.names.includes[modules-unit-jdk8][relevant]
  modules.includes.required.test.batch.class.names.includes[modules-integration-*-jdk8][relevant]

Things to keep in mind when using globs
----------------------------------------
* modules-unit tests all follow this glob pattern:     ``**/src/test/**/*Test.java``
* modules-integration tests all follow this pattern:  ``**/src/testIntegration/**/*Test.java``

How properties are read
------------------------
There are multiple ways to specify a property with batch name, wild card, test suite. 
Please refer to the “How Test Properties are Read” section in this `Grow Article`_.

Example
--------
The same set of tests can be ran using the new properties, the two pull requests below run the exact same set of functional/backend tests using old vs new properties. 

* `Using currently available properties`_ : https://github.com/yichenroy/liferay-portal/pull/376
* `Using new properties`_ : https://github.com/yichenroy/liferay-portal/pull/377

.. _Explore adding backend test batches into test.properties files within a module: https://issues.liferay.com/browse/LRCI-1036
.. _Example Section: ./modules-test-properties.html#example
.. _test.batch.class.names.includes property in liferay-portal/test.properties: https://github.com/liferay/liferay-portal/blob/dabc30e52619a902550aacc0fc690d25bad0121d/test.properties#L1098-L1128
.. _`Example`: https://github.com/yichenroy/liferay-portal/blob/e22127c7add30148f87019a33ca5aafb44be6a9f/modules/apps/portal-search/test.properties
.. _`Grow Article`: https://grow.liferay.com/people?p_p_id=com_liferay_wiki_web_portlet_WikiPortlet&p_p_lifecycle=0&p_p_state=normal&p_p_mode=view&_com_liferay_wiki_web_portlet_WikiPortlet_struts_action=%2Fwiki%2Fview&_com_liferay_wiki_web_portlet_WikiPortlet_pageResourcePrimKey=815070&p_r_p_http%3A%2F%2Fwww.liferay.com%2Fpublic-render-parameters%2Fwiki_nodeName=Grow&p_r_p_http%3A%2F%2Fwww.liferay.com%2Fpublic-render-parameters%2Fwiki_title=Pull+Request+Tester+CI+Test+Suites
.. _`Using currently available properties`: https://github.com/yichenroy/liferay-portal/blob/0085e794eb832bbd8f98dd11e8aa1a01c9b1de4f/modules/apps/portal-search/test.properties
.. _`Using new properties`: https://github.com/yichenroy/liferay-portal/blob/e22127c7add30148f87019a33ca5aafb44be6a9f/modules/apps/portal-search/test.properties