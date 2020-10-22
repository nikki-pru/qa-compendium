How to Properly File a JIRA ticket when Analyze Acceptance
===========================================

There are two types of ticket that could be file when Analyze Acceptance

LRQA Type Ticket
----------------
LRQA ticket can only be filed:

1. When testers are unsured what type of bug they found, and failed less than 4 times in History tab. We can categorize this type of ticket as Investigate tickets.
2. When the failure needed a test fix.

When creating a new LRQA Ticket, issue type will need to be set as either ``Test Analysis`` or ``Test Fix`` based on the type of error you found in Acceptance Analysis.

1. Summary will be consist of the description of the failure. (Example: Investigate AssertionError in ``Test Name``)
2. Components will always set to ``Portal``.
3. Project Components is optional, however if you're able to identify which component the error belongs to, then you can set Project Component to an appropriate component
4. Description is where you will write out the appropriate description of the failure with the appropriate format.
5. Labels for Acceptance Analysis is always set to ``qa-a``
6. Affects Version/s will be set to the appropriate version that you're analysing.
7. After you create the ticket, make sure to message the test lead who's in charge of that particular component and ping their name in the comment.

LPS Type Ticket
----------------
LPS ticket can be filed:

1. When tester are able to identify what type of bug they found. (Bug)
2. When tester have seen the bug happened before. (Regression Bug)

When creating a new LPS Ticket, issue type will need to be set as either ``Bug`` or ``Regression Bug`` based on the type of error you found in Acceptance Analysis.

1. Summary will be consist of the description of the failure. (Example: AssertionError in ``Test Name``)
2. Components will be set to the appropriate component that provided in the stacktrace.
3. Affects Version/s will be set to the appropriate version that you're analysing.
4. Description is where you will write out the appropriate description of the failure with the appropriate format.
5. Labels for Acceptance Analysis is always set to ``qa-a``
6. After you create the ticket, make sure to message the test lead who's in charge of that particular component and ping their name in the comment.

Different Failures and How To Analyze Them
===========================================

The following is a list of different types of failures and examples of each.

Compile Failure
----------------
  Scroll to the bottom, then start scrolling up to find the stacktrace. Identify the failing task, then search for when it first fails in the console logs. From there, see why it failed. Keep in mind that the failure may look different from the one in the example. 

  **Example:**
  |image0|

  The failing task is: :apps:portal-vulcan:portal-vulcan-impl:compileJava


Functional Test Failure
-----------------------
  `See this video recording`_.

Semantic Versioning
-------------------
  There are a couple of ways to find semantic versioning issues. The first would to search for “version increase”. Sometimes that won’t work so you’ll need to find the stacktrace, see what task failed, then find where the task first failed.

  **Example 1:**
  |image1|

  **Example 2:**
  |image2|
  The failing task is: :apps:segments:segments-api:baseline

  |image3|

Service Builder
---------------
  Search for “+++”
  **Example:**
  |image4|

Source Format
-------------
  Search for “format-source”. The failures are listed after the line:
  ``java.lang.Exception: Found X formatting issues:``

  **Example:**
  |image5|

  In this example, there are nine total formatting issues. 

Startup
--------
  Start from the bottom and scroll up until you see a stacktrace. A common failure is a dependency issue, so I usually start by searching for “could not resolve module”

  **Example:**
  |image6|

.. |image0| image:: ./img/compile-failure.PNG
.. |image1| image:: ./img/semantic-versioning-1.PNG
.. |image2| image:: ./img/semantic-versioning-2.PNG
.. |image3| image:: ./img/semantic-versioning-3.PNG
.. |image4| image:: ./img/service-builder.PNG
.. |image5| image:: ./img/source-format.PNG
.. |image6| image:: ./img/startup-failure.PNG

.. _See this video recording: https://drive.google.com/file/d/0BySFfOWPyNghWkRzRzNSdEt5ZFE/view
