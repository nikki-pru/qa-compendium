========================
Guide to Disabling Tests
========================

.. note::
  Please use caution when disabling tests. Disabled tests should always be properly documented so we don’t lose track of them. If you have questions about this, work with your Test Lead or Lead Developer on figuring out the best solution for your team.

Runner vs Test Levels
----------------------
The following are differences between excluding a test at the Runner level versus at the Test level

  * Runner Level 
  
    * Example: batch patterns in our Ant builds or the `--tests` parameter in `gw test`
    * The decision is per location. You can suppress a unit test for Liferay CI, while still running it on a component team CI and most importantly on local developers’ machines.
    
  * Test level
  
    * Example: `@Ignore` in Java code itself.
    * The test stops running everywhere at once.

Functional Tests
----------------
.. note::
  Disclaimer: Please make sure to run ant -f build-test.xml run-poshi-validation after making functional test changes to check that changes are valid.

**How do I find a functional test?**

  One way is to use the find command in your terminal to locate the testcase file. Most testcase files reside in portal-web, but others exist in modules.
  
  .. code::
  
    >find portal-web -name "ContentPageConverter*"
    >portal-web/test/functional/com/liferay/portalweb/tests/enduser/wem/layout/pagesadmin/ContentPageConverter.testcase

**How do I quarantine functional tests from relevant?**

  Add ``property portal.upstream = "quarantine";`` to the functional test. This will be true as long as we’re `globally excluding the quarantine value`_ from relevant. 

  `Example: Elasticsearch7EE.testcase`_
  
  .. code::
  
    test XPackSmokeTest {
    	property elastic.xpack.enabled = "true";
    	property osgi.app.includes = "portal-search-elasticsearch6-xpack-monitoring,portal-search-elasticsearch7";
    	property portal.upstream = "quarantine";
    	property remote.elasticsearch.enabled = "true";
    	property test.name.skip.portal.instance = "Elasticsearch7EE#XPackSmokeTest";

**How do I ignore functional tests?**

  Add ``@ignore = "true"`` to the top of your functional test.

  `Example: Elasticsearch6.testcase`_
  
  .. code::
  
    @ignore = "true"
    @priority = "3"
    test AssertSystemSettingsPropogateToModule {

**How do I ignore failures due to console errors that happen on functional tests?**

  Add a `regex ignore in test-ignorable-error-lines.xml`_

  .. code::
  
    <ignore-error description="">
    <contains>Do NOT use embedded Elasticsearch in production</contains>
    <matches></matches>
    </ignore-error>

    This is specifically used for functional tests that have the `test.assert.warning.exceptions`_ property enabled. This does NOT ignore errors for the PortalLogAssertorTest.

Backend Tests
-------------

**How do I disable specific js-unit tests?**

  If the test is written in `mocha`_ or `jest`_ (easy way to tell is if it uses ``describe`` and ``it`` syntax), you can tack on ``.skip()`` at the end of the ``describe`` keyword for the test case that is failing.

  Example: `Liferay.Search.SearchBar.updateQueryString`_

  An alternative and functionally equivalent method is to use the ``xit`` alias, i.e. putting an ``x`` in front of the ``it`` keyword `as in this example`_.

  .. warning:: 
    For jest tests, there is a bug where the disabled tests will look as if they are running and passing within the Jenkins test report. To verify that the tests were really skipped, look for the test run within the console log underneath the module’s npmRunTest command.

**How do I disable all js-unit tests in a module?**

  The following examples are useful if the suite fails prior to running the actual test.

  Change the test script from ``test`` to ``test_DISABLED`` in the corresponding ``package.json`` file.

  Example: `Quarantine search_bar_test.js js-unit test`_

  .. code:: 
  
    {
    	"name": "portal-search-web",
    	"scripts": {
    		"checkFormat": "liferay-npm-scripts check",
    		"format": "liferay-npm-scripts fix",
    		"test": "karma start"
    		"test_DISABLED": "karma start"
    	},
    	"version": "4.0.19"
    }

  Another way to disable specific module patterns is through ``testPathIgnorePatterns`` in corresponding ``package.json`` file as long as disabling is documented to a fix later:

  Example: `Ignore specific ddm js-unit tests`_

  .. code::
  
  	"jest": {
  		"testPathIgnorePatterns": [
  			"AutoSave",
  			"ShareFormPopover"
  		]
  	},

**How do I disable individual unit or integration tests?**

  Import the ``org.junit.ignore`` package to the class if it's not already there. Then add the ``@Ignore`` annotation to the start of a test method.

  Be careful of where you put the import if you are not familiar with the sf standards in integration/unit tests, a quick way to check SF (faster than CI) is to just run ``gradlew formatSource`` in the test-module

  `Example import: DLAppServiceWhenSearchingFileEntriesTest.java`_
  `Example ignore: DLAppServiceWhenSearchingFileEntriesTest.java`_

**How do I disable an entire unit or integration test class?**

  Import the org.junit.Ignore package to the class if it's not already there.
  Add the @Ignore annotation to the start of a test class

  `Example import: Cluster1InstanceTest.java`_

  .. code::
  
    import org.junit.Rule;

  `Example ignore: Cluster1InstanceTest.java`_

  .. code::
  
    @Ignore
    public class Cluster1InstanceTest {

**How do I ignore an integration test method in a specific subclass that is implemented in a superclass?**

  ``@Override`` the ``@Test`` with a no-op method at the subclass, then ``@Ignore`` that

  Example: `DLFileEntrySearchTest.java`_

  .. code::
  
    @Ignore
    @Override
    @Test
    public void testLocalizedSearch() throws Exception {
    }

    Example superclass test method being overridden: `BaseSearchTestCase.java`_

Test Batches
------------

**How do I disable portal log assertor for a specific batch?**

  Change the value of ``test.portal.log.assert`` to **false**. Use this sparingly!

  Example: `build-test-batch.xml`_

  .. code::
  
    <target name="functional-smoke-tcserver32-mysql56-jdk8">
    	<run-functional-test app.server.type="tcserver" database.type="mysql" test.portal.log.assert="false" />
    </target>

**How do I disable test classes for all batches?**

  Add them to either ``test.batch.class.names.excludes.permanent`` or ``test.batch.class.names.excludes.temporary`` in `test.properties`_

  .. code::
  
    test.batch.class.names.excludes.permanent=\
            modules/apps/static/portal-lpkg-deployer/**,\
            modules/test/external-data-source-test/**,\
            modules/private/apps/osb-asah/**,\
            modules/private/apps/osb-cerebro/**,\
            modules/private/apps/osb-common/osb-common-remote-company/**,\
            modules/private/apps/osb-faro/**,\
            modules/private/apps/osb-lcs/**,\
            modules/private/apps/osb-training/**


**How do I disable test classes for a specific batch?**

  Add them to ``test.batch.class.names.excludes[batch-name-here]``.

  `Example disabled test for a specific batch`_.

  .. code::
  
    test.batch.class.names.excludes[modules-unit-jdk8]=\
         ${test.batch.class.names.excludes},\
         **/project-templates/**/src/test/**/*Test.java

Test Suites
------------

**How do I disable test classes for a specific test suite?**

  Add them to ``test.batch.class.names.excludes[suite-name-here]``.

  `Example disabled test in a specific suite`_.

  .. code::
  
    test.batch.class.names.excludes[search]=\
         ${test.batch.class.names.excludes},\
         **/portal-search-solr/**/*Test.java,\
         **/portal-search-solr7/**/*Test.java

.. _`globally excluding the quarantine value`: https://github.com/brianchandotcom/liferay-portal/pull/86785/commits/496332ea3113e380e6a5f328aa1554f108686dbb
.. _`Example: Elasticsearch7EE.testcase`: https://github.com/brianchandotcom/liferay-portal/pull/86773/commits/c50dc63be8b3214f2cbac5c8d157b8c4027e0991
.. _`Example: Elasticsearch6.testcase`: https://github.com/liferay/liferay-portal/blob/9cc5c9e823ccf5c834d5bbfc2e3b37cdd6aabc0d/portal-web/test/functional/com/liferay/portalweb/tests/coreinfrastructure/search/elasticsearch/Elasticsearch6.testcase#L62
.. _`regex ignore in test-ignorable-error-lines.xml`: https://github.com/liferay/liferay-portal/blob/master/portal-web/test-ignorable-error-lines.xml
.. _`test.assert.warning.exceptions`: https://github.com/liferay/liferay-portal/blob/9cc5c9e823ccf5c834d5bbfc2e3b37cdd6aabc0d/portal-web/test/functional/com/liferay/portalweb/tests/portalsmoke/PortalSmoke.testcase#L8
.. _`mocha`: https://mochajs.org/
.. _`jest`: https://jestjs.io/
.. _`Liferay.Search.SearchBar.updateQueryString`: https://github.com/liferay/liferay-portal/commit/8e389d0db4c22a6fe5fcf953f229e438f2c93c02
.. _`as in this example`: https://stackoverflow.com/a/32724129
.. _`Quarantine search_bar_test.js js-unit test`: https://github.com/liferay/liferay-portal/commit/312753264dc6ade37b1419abd78b72e76e9b473c
.. _`Ignore specific ddm js-unit tests`: https://github.com/4lejandrito/liferay-portal/pull/431/commits/32fb68761231e4a4d518ebd4bd575d1298eebded
.. _`Example import: DLAppServiceWhenSearchingFileEntriesTest.java`: https://github.com/liferay/liferay-portal/blob/master/modules/apps/document-library/document-library-test/src/testIntegration/java/com/liferay/document/library/app/service/test/DLAppServiceWhenSearchingFileEntriesTest.java#L32
.. _`Example ignore: DLAppServiceWhenSearchingFileEntriesTest.java`: https://github.com/liferay/liferay-portal/blob/master/modules/apps/document-library/document-library-test/src/testIntegration/java/com/liferay/document/library/app/service/test/DLAppServiceWhenSearchingFileEntriesTest.java#L64
.. _`Example import: Cluster1InstanceTest.java`: https://github.com/liferay/liferay-portal/blob/master/modules/apps/portal-search-elasticsearch6/portal-search-elasticsearch6-impl/src/test/java/com/liferay/portal/search/elasticsearch6/internal/cluster/Cluster1InstanceTest.java#L24
.. _`Example ignore: Cluster1InstanceTest.java`: https://github.com/liferay/liferay-portal/blob/46913cbf90966249ac353adeb872321b52e2f2d3/modules/apps/portal-search-elasticsearch6/portal-search-elasticsearch6-impl/src/test/java/com/liferay/portal/search/elasticsearch6/internal/cluster/Cluster1InstanceTest.java#L32
.. _`DLFileEntrySearchTest.java`: https://github.com/liferay/liferay-portal/blob/d44b9282f6bd4fceb317cd2a8692d76ebb1ebc6e/modules/apps/document-library/document-library-test/src/testIntegration/java/com/liferay/document/library/search/test/DLFileEntrySearchTest.java#L91-L95
.. _`BaseSearchTestCase.java`: https://github.com/liferay/liferay-portal/blob/d44b9282f6bd4fceb317cd2a8692d76ebb1ebc6e/portal-test-integration/src/com/liferay/portal/search/test/BaseSearchTestCase.java#L75
.. _`build-test-batch.xml`: https://github.com/liferay/liferay-portal/commit/da4e460840afd3cce2fee3902e9ab59a63953b05#diff-6af2cc91305312749b4870d62f84b38c
.. _`test.properties`: https://github.com/liferay/liferay-portal/blob/3b9c1103206d96c0b3f24fc08d6343412b84730e/test.properties#L1006-L1019
.. _`Example disabled test for a specific batch`: https://github.com/liferay/liferay-portal/blob/3b9c1103206d96c0b3f24fc08d6343412b84730e/test.properties#L1029-L1031
.. _`Example disabled test in a specific suite`: https://github.com/liferay/liferay-portal/blob/3b9c1103206d96c0b3f24fc08d6343412b84730e/test.properties#L1921-L1924
