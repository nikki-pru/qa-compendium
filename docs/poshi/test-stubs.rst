==========
Test Stubs
==========

A test stub is a piece of code used as a stand-in for the actual test. To create this in the poshi ``*.testcase`` files:

1. Setup a test with descriptions, priority, test name, like you regularly would.
2. Set the test to @ignore = "true".
3. Add a commented out TODO block with the LPS/LRQA ticket

For example:
::
  @description = "This is a test for LPS-125933. Check for possible not covered scenarios for Echo components in Data Engine"
  @ignore = "true"
  @priority = "3"
  test ConvertWidgetPageWithWebContentsToContentPage {
    property portal.acceptance = "false";

    // TODO LPS-125933 ConvertWidgetPageWithWebContentsToContentPage pending implementation

  }

Using test stubs have the following advantages:

* Test Leads or component owners are able to set test name, priority and other test properties prior to handing off the test writing to other teams;
* Avoid conflicts when a large number of tests need to be written; and,
* Create a queryable backlog of tests that need to be written.

.. tip::
  To query a list of test stubs, run ``git grep TODO *.testcase``,
  or ``git grep LPS-123456 *.testcase`` to query by the ticket number
  


