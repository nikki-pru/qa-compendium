==========
Test Stubs
==========

A test stub is a piece of code used as a stand-in for the actual test. To create this in the poshi ``*.testcase`` files:

1. Add a commented out TODO block.
2. Include the LPS/LRQA reference for the test.
3. Add the test name in the same alphabetical order that our test methods are organized to avoid SF issues later on.
4. Add the test priority and other properties.

For example:
::
  @priority = "5"
  test AddBlogsEntry {
    property testray.component.names = "WYSIWYG";

    Blogs.addEntry(
      entryContent = "Blogs Entry Content",
      entryTitle = "Blogs Entry Title");

    BlogsNavigator.gotoEntryPG(
      entryContent = "Blogs Entry Content",
      entryTitle = "Blogs Entry Title");

    BlogsEntry.viewEntryPG(
      entryContent = "Blogs Entry Content",
      entryTitle = "Blogs Entry Title");
  }

  // TODO | LPS-123456
  // @priority = "4"
  // @ignore = "true"
  // test AddBlogsEntryComment {
  //    WebContentNavigator.openWebContentAdmin(siteURLKey = "test-site-name");
  // }

  @priority = "4"
  	test AddBlogsEntryScheduled {
    ..
    ..
  }

Using test stubs has the following advantages:

* Test Leads or component owners are able to set test name, priority and other test properties prior to handing off the test writing to other teams.
* Avoid conflicts when a large number of tests need to be written; and,
* Create a queriable backlog of tests that need to be written.

.. important::
  
  
.. tip::
  To query a list of test stubs, run ``git grep TODO *.testcase``.
  Or ``git grep LPS-123456 *.testcase`` to query by the ticket number
  


