==================
Sending in Commits
==================

Context
-------

When sending in commits for New Automated Tests or Test Fixes, there are guidelines we adhere to. Following these guidelines produce the following result:

* It makes reviewing code easier;
* It keeps source clean; and,
* It makes it easier to track down changes to the tests later on.

Steps
-----

1. On your master directory (or whichever portal version you’re working on), create a branch named LRQA-##### (``git checkout -b LRQA-12345``, which is the ticket you are working on.). See note on branch naming below.

2. Make your changes within that branch

  * For path changes, check the paths folder.
  * Before creating a new macro, check that there is an existing one that can be reused.
  * Check other tests to see how they are  written.
  
3. Run validation and source format on the branch before creating commits.
  a. ``ant -f build-test.xml run-poshi-validation``
  b. On /portal-impl, ``ant format-source-local-changes``
  
4. Create your commits; Reference this PR when reviewing the guidelines below
  * Group your commits in chunks of logic instead of per line changes. 
  * Include the ticket number in the commit name (see Examples below)
  * Make the commit names descriptive, starting with a verb. See examples:
    
    * “LRQA-54166 Change path from div to ul”
    * “LRQA-54166 Add macro to navigate away from page”
    * “LRQA-54166 Create new test for LPS-105474”
    
5. Rebase your branch with the master branch.
  Let’s say you created your branch off of master on git ID ``12345``, made your changes, and then created your commits. You’re ready to send in your changes to your reviewer but now master is at git ID ``98765``. What rebasing does is it updates your base from git ID ``12345`` to git ID ``98765``, and then adds your changes on top of it. To do this:
  
  a. Update master
  b. Checkout your working branch
  c. run ``git rebase master``. See note on rebasing below.
  
6. Submit to your Reviewer

  * Pull request title should be ticket number and branch. See examples:
    
    * LRQA-54166 | master
    * LRQA-1234 | 7.2.x-ee
    
  * Pull request description should be a link to the ticket. See examples:
    
    * http://issues.liferay.com/browse/LRQA-54166
    * http://issues.liferay.com/browse/LRQA-54166

.. note::
  **On branch naming conventions**
  
  An older QA branch naming standard is to name the branches ``master-qa-ticketNumber`` or ``7.2.x-qa-ticketNumber``, depending on the portal version you're working on. This has since been changed to match how the rest of Engineering names their branches using only the ticket number. Both are acceptable since the branch name does not affect the commits. For best practice, coordinate with your reviewer or product team on whether they have a specific convention for branch naming.
  
.. note::
  **On rebasing**
  
  There is a possibility to run into conflicts when creating your code. To resolve these conflicts, consider undoing your commits (not your changes), and fixing the conflicts before recreating your commits. Undoing a commit does not delete your changes.
