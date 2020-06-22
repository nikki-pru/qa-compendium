===================
7.3 Release Testing
===================

Objective
---------
The objective of this document is to centralize information around the testing process behind 7.3 GA Releases. 

Scope
-----
The scope of this document will cover the minimum guarantees in what will be assured for the release, the communication paths / point of contacts, deliverables, and some risks. Use this document to review what QA Engineering will test during the release process in the fit and finish checks and bring up any concerns with QA Management (kristoffer.onias@liferay.com) What is left out of scope in this document and this stage in testing are the testing procedures that occur during the development phases.

Deliverables
------------
QA will perform quality control testing and report results in the form of a Test Report. This test report will record each of the team's confidence levels for release, test results, blocking / known issues, and an issue count.

Test Schedule
-------------
Generally, publishing will begin on Wednesday to build that same evening. Test results are normally available during the end of China's day and toward the beginning of day for Spain and Hungary. 

Below is a general timeline on each of the main steps of the release testing process. Note that if any blocker is discovered at any of these steps the process restarts. QA is expected to complete testing and analysis within 1 business day. If the build is not completed by 3PM PST, the testing will be completed within 2 business days because a product team will miss their opportunity to test and analyze automated test results.

.. note::
  If the build is not completed by 3PM PST, the testing will be completed within 2 business days because a product team will miss their opportunity to test and analyze automated test results.

+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Estimated Duration | Description                                                                                                                                                        |
+====================+====================================================================================================================================================================+
| Instant            | Release manager notifies QA through Slack #rle-build                                                                                                               |
+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 6-8 Hours          | A Test Lead or Senior Test Engineer will trigger automated tests to run against the builds.                                                                        |
+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Instant            | Once the results are completed a Test Lead, Senior Test Engineer, or above will notify the QA team that the results are available for analysis on Slack            |
+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 1-2 Business Days  | All global teams will complete test analysis and execution and update the Test Report by the end of their business day.                                            |
|                    | If the build is completed after 3PM PST the Test Report will need an additional business day for the team to complete                                              |
+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 1 Hour             | Test Manager will review the Test Report to confirm completion, will notify the Release Manager through Slack #rle-build, and deliver the finalized Test Report    |
+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Test Scope
----------
**Regression Testing**
Below is a high level overview of the scope of testing performed by type. Releasability is determined based on the severity of the issues discovered through these test failures. Generally, release testing relies on automated test analysis where only critical flows that were not automated are executed manually as well as a very basic smoke test.

+-------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Test Type   | Description                                                                                                                                                                                     | 
+=============+=================================================================================================================================================================================================+
| Functional  | All poshi tests are executed and analyzed for issues                                                                                                                                            |
+-------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Unit        | All unit tests are executed and analyzed for issues                                                                                                                                             |
+-------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Integration | All integration tests are executed and analyzed                                                                                                                                                 |
+-------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Environment | Smoke testing is executed and analyzed for every build. With heavier focus on environments factors that are most used by customers and are on application servers that Liferay is bundled with. |
|             | Before the DXP release full environment testing will be performed. Environment specific regression is expected to be low during the stabilization period of development.                        |
+-------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+ 
| Performance | Rough performance testing is done through manual testing and our automated test performance. Many of our tests would fail if there are critical issues with performance.                        |
|             | Performance testing is currently handled by a separate team and will be done before the DXP release.                                                                                            |
+-------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Security    | Security testing is automated and results are analyzed for every release                                                                                                                        |
+-------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Binaries    | QA will validate that the readme and copyright information is correct                                                                                                                           |
+-------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

**Guarantees**
  * QA will complete testing and analysis within 1-2 business days
  * A Test Report will be delivered to the release manager that will summarize release confidence from each team
  
    * The Test Report will contain a summary of known issues that the teams are raising
    * The Test Report will contains a summary of the outstanding issues
    * The Test Report will contains a summary of test results by Product Team
    
  * A green lit release means that all Product Teams validated that there are no show stopping issues

Test Process
------------

#. Release Manager notifies QA that a new build is ready to test via Slack in `#rle-build`_.
#. Test Leads / Senior Test Engineers will trigger automation tests to execute against the build.
#. Once testing is complete the Test Lead / Senior Test Engineer will Autofill the build and assign a `Testray`_ Task to all Test Engineers.
#. The Test Lead / Senior Test Engineer will then provide a link to the team in `#d-quality-assurance`_ which contains a link to the following

    * Bundle
    * Testray Task
    * Jenkins Report
    * Test report
#. Product Teams are given 1 full business day to complete testing, analysis, and completing their section in the Test Report.
#. The Test Lead / Senior Test Engineer will notify the Test Manager when testing and analysis is completed by all teams for final review.
#. The Test Manager will notify the Release Manager immediately if there is a blocker or once the green light report is completed in the #rle-build channel

Expectations
------------
**Blocking issues are acted upon swiftly and with urgency**
  * Raise a possible blocker quickly to the Test Manager and Release Manager
  * Give regular updates to the teams and Release manager
  * Push for a resolution quickly and provide a time estimate into when a resolution can be expected
  * There are many options: Feature flag, disable, revert, fix, etc. Teams should consider the best course of action to make for a quick and low risk release
  * If a blocking issue is discovered outside of one's team, it is expected that they contact the Product Team promptly with urgency
  * All blockers must be Fix Priority 5 and contain the 7.3-blocker label
  
**Set the teams expectations around the release testing phase**
  * Blocking issues should be acted upon with haste and care
  * Be on the lookout for builds to be tested during release testing weeks
  * Be transparent and provide proactive statuses throughout and at the end of the day

**Product teams are taking extra care during the stabilization and release phases**
  * By the time we enter the release phase and the build is to be made the product should already be fit-and-finished
  * Teams should make every effort to not introduce regressions in upstream

**Should a blocker be introduced, Product Teams are expected to perform root cause analysis and work out a prevention plan**
  * Teams are expected to identify the root cause as critical issues should never be discovered during release testing
  * Teams are expected to work out a prevention plan

**All Fix Priority 4 issues must be reviewed and labeled**
  * All Fix Priority 4 issues must be evaluated as a blocker or not and updated accordingly
  * Fix Priority 4 issues that are confirmed not blockers should contain the known-issues label

.. Links:
.. _`#rle-build`: https://liferay.slack.com/archives/CLA7D1CNL
.. _`Testray`: http://testray.liferay.com
.. _`#d-quality-assurance`: https://liferay.slack.com/archives/CL84ZPHAT
