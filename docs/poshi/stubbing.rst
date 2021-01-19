==========
Test Stubs
==========

A test stub is a piece of code used as a stand-in for the actual test. To create this in the poshi ``*.testcase`` files, add a TODO comment and include the LPS/LRQA reference for the test. For example:
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

  // TODO AddBlogsEntryComment | LPS-123456

  @priority = "4"
  	test AddBlogsEntryScheduled {
    ..
    ..
  }

Using test stubs has the following advantages:

* Avoid conflicts when a large number of tests need to be written; and,
* Create a queriable backlog of tests that need to be written.

.. note::
  To query a list of test stubs, run ``git grep TODO *.testcase``.

