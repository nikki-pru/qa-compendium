Test Fix Exercise
=================

Now that you've written your first Poshi test, ``HelloPoshi#ViewHelloWorld``, let's practice debugging and fixing tests using a real world example. For this exercise, we will be fixing the failing ``PGBlogs#AddBlogsEntryComment`` test.

The first step in test writing/fixing is to understand what we're trying to test. In this case, we would like to verify that a user is able to add a comment to a blog entry, ``AddBlogsEntryComment``, via the Blogs portlet which is on a page, ``PGBlogs``. Start up a portal instance and manually test the feature to get an idea how you, as a user, would do that task. 

If the feature fails during manual testing and the user is not able to add a comment, consider if there is an actual bug in Portal. Perhaps the test is not failing after all, but it caught a bug instead. If this happens, rejoice! The test is doing what it's supposed to do. Report the bug through JIRA, or ping the product team on Slack.

If there is no bug, the feature passes and the user is able to add a comment, then you have verified that the test is indeed broken and needs to be fixed. Proceed with the following steps:
  
  1. Fetch this `FlexTraining branch`_ where the test is failing.
  2. Run the test using steps in previous sections to get an idea of where the test is failing.
  3. Debug and fix the test as discussed in the previous sections. The index.html file in the ``/portal-web/test-results/LocalfileFile.{testName}/`` directory is a helpful resource. This file gets generated after every run.
  
.. hint::
  For this exercise, the `tearDown block`_ is not needed and may be commented out. Teardown may also be skipped through the test.{computerName}.properties file. For more information, see the section on **Timesavers**.
  
  
.. links::
.. _`FlexTraining branch`: https://github.com/nikki-pru/liferay-portal/tree/FlexTraining
.. _`tearDown block`: https://github.com/nikki-pru/liferay-portal/blob/FlexTraining/portal-web/test/functional/com/liferay/portalweb/tests/enduser/collaboration/blogs/PGBlogs.testcase#L28-L55