=========================
JIRA Commenting Standards
=========================

.. meta::
  :keywords: jira, standards, comments
  
Since JIRA is used by most business functions in Liferay, it is good to have some standards when interacting with others over tickets. These are not arbitrary standards but are best practices we’ve developed over the years to efficiently get information across to a developer, another viewer, or for reporting purposes. We work with developers and team members across different time zones and languages and the more efficiently we get our point across the first time, the faster we get results.

Filing a bug ticket
--------------------
When filing bug tickets it is important to inform others on how the issue was reproduced and on what GIT IDs it was reproduced on. Attached GIFs or images are also helpful. Example, `LPS-103947`_.
::
  *Steps to Reproduce:*
  # Step 1
  # Step 2
    a. Step 2.1
    b. Step 2.2
  # Step 3

  *Expected Result:*
    What the expected behavior should be.

  *Actual Result:*
    What actually happened.

  *Reproduced on:*
    {appserver.version} + {db.version}
    Portal {version} GIT ID: #######################

.. note::
  Before filing a bug ticket, search through JIRA to find out if the issue you are seeing has already been reported. This reduces the number of duplicate tickets that need to be worked on and closed.

Verifying a bug ticket
-----------------------
Once a bug ticket has been created, it is set to Open status. These tickets need to be verified and given a fix priority before the developers start fixing the bug. Use the following steps to verify and assign a fix priority to tickets:

1. Determine the `likelihood`_ of the bug occurring (L#);
2. Determine the `severity`_ of the bug (S#);
3. Given the likelihood and severity, determine the Fix Priority (FP) using the `Risk Assessment Matrix`_;
4. Set the ticket status to Verified;
5. Comment ``L# + S# = FP#``, and set the comment privacy to "liferay-staff."

Closing bug tickets
--------------------
There are multiple scenarios that can happen when closing a bug ticket. As in Filing a Bug Ticket, steps and GIT ID are important to document how or when the bug was closed in case the ticket needs to be referenced later on. The first thing to do is to Manually test the ticket to see if the issue is no longer reproducible

GIT ID can be found in hidden file inside of your bundle folder called ``.githash``

Fixed
^^^^^^
A bug ticket should be closed as fixed when there is a linked pull request. Example: `LPS-103737`_

*When steps are included in the description*
::
  *PASSED* Manual Testing following the steps in the description

  Fixed on:
  {appserver.version} + {db.version}
  Portal {version} GIT ID: #######################

  A short summary of observed behavior.
  
``{appserver.version}`` is essentially Tomcat version in your bundle folder

``Portal {version}`` depends on which bundle you use. If you start your bundle on your ``master-bundle``, then it should be ``master``. Otherwise it'll be bundle specific.

*When steps are not included in the description*
::
  *PASSED* Manual Testing using the following steps:

  #. Step 1
  #. Step 2
  #. Step 3

  Fixed on:
  {appserver.version} + {db.version}
  Portal {version} GIT ID: #######################

  A short summary of observed behavior.

No Longer Reproducible
^^^^^^^^^^^^^^^^^^^^^^^
A ticket is no longer reproducible when there is no linked pull request. The issue may have been fixed together with a fix for a different ticket. Example, `LPS-103861`_.

*When steps are included in the description*
::
  *No longer reproducible** following the steps in the description

  No longer reproducible on:
  {appserver.version} + {db.version}
  Portal {version} GIT ID: #######################

  A short summary of observed behavior.

*When steps are not included in the description*
::
  **No longer reproducible** using the following steps:
  # Step 1
  # Step 2
  # Step 3

  No longer reproducible on:
  {appserver.version} + {db.version}
  Portal {version} GIT ID: #######################

  A short summary of observed behavior.


.. _LPS-103947: https://issues.liferay.com/browse/LPS-103947
.. _LPS-103737: https://issues.liferay.com/browse/LPS-103737
.. _LPS-103861: https://issues.liferay.com/browse/LPS-103861
.. _likelihood: https://docs.google.com/spreadsheets/d/1AEKD3C7WhkwWffJiCdNul5MBt-9Rl_fa0WPQVSkYptY/edit#gid=5&range=B4:C8
.. _severity: https://docs.google.com/spreadsheets/d/1AEKD3C7WhkwWffJiCdNul5MBt-9Rl_fa0WPQVSkYptY/edit#gid=5&range=D2:H3
.. _Risk Assessment Matrix: https://docs.google.com/spreadsheets/d/1AEKD3C7WhkwWffJiCdNul5MBt-9Rl_fa0WPQVSkYptY/edit#gid=5
