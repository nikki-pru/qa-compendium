========================
Guide to Use RCA Tools
========================


What is RCA?
----------------------
RCA stands for Root Cause Analysis. When CI starts failing and we cannot determined the cause of why it is failing, we turn to RCA Tools to help us determine the root cause of failures.
Root cause of failure is most likely cause by a certain commit upstream. This tool basically automates an existing process that Test Engineers have been to executing manually.

This tool will simply run the same test across multiple SHAs that must be manually selected by the user.

We decided against making a git bisect tool for these reasons:

  * Tests can fail due to unrelated issues.  For example:
  
    * A randomly selected SHA could fail to compile.
    * A randomly selected SHA could fail to startup.
    * A randomly selected SHA could fail for another reason unrelated to the target issue.
    * A network resource could fail to respond.
    
  * Compiling portal takes around 30 minutes, so waiting for a result before triggering the next SHA would be too slow.

After the job is complete there should be a report available to view that will help a user analyze where a potential issue was introduced.

Getting Started
----------------

**Steps to Start RCA Tool**

  1. Log in to the `Jenkins Server`_ using your normal Liferay Credentials.
    a. User: [first name].[last name]
    b. Password: [liferay password]

  2. Fill in the following required parameters (See below in “Parameter Descriptions” for more information on each parameter):
    a. PORTAL_BATCH_NAME
    b. PORTAL_BATCH_TEST_SELECTOR
    c. PORTAL_BRANCH_SHAS
    d. PORTAL_GITHUB_URL
    e. PORTAL_UPSTREAM_BRANCH_NAME
    
   3. Click the ‘Build’ button.
   
   4. Wait for the build to be assigned a server.
    a.  While the build is waiting for a server it will look like the Build in queue entry.
    b.  Once the build is assigned a server the build will be given a Build Link as seen below.
    
   5. Click on the Build Link to go to the main build page.
    a. Ensure that you are the Build Owner, if not go back to the previous page and find the correct build.
    b. Click on the Jenkins Report Link to watch as your result begins to form.
    
   6. After all downstream builds have completed the “Jenkins Report” will show

Parameter Descriptions
------------------------

**PORTAL_BATCH_NAME (required):**

This parameter is used to choose which batch to run.  A batch is representative of the type of test that will be executed within CI.

This lists the types of batches currently supported within the RCA Tool:


+-------------------------------+---------------------------------------------+
| **Upstream Branch Name**      | **Supported Batches**                       |
+-------------------------------+---------------------------------------------+
|master, master-private         | integration-mysql57-jdk8                    |
|                               |                                             |
|                               | functional-smoke-jboss71-mysql57-jdk8       |
|                               |                                             |
|                               | functional-smoke-tcserver40-mysql57-jdk8    |
|                               |                                             |
|                               | functional-smoke-tomcat90-db2111-jdk8       |
|                               |                                             |
|                               | functional-smoke-tomcat90-mariadb102-jdk8   |
|                               |                                             |
|                               | functional-smoke-tomcat90-mysql57-jdk8      |
|                               |                                             |
|                               | functional-smoke-tomcat90-oracle122-jdk8    |
|                               |                                             |
|                               | functional-smoke-tomcat90-postgresql10-jdk8 |
|                               |                                             |
|                               | functional-smoke-tomcat90-sybase160-jdk8    |
|                               |                                             |
|                               | functional-smoke-weblogic122-mysql57-jdk8   |
|                               |                                             |
|                               | functional-smoke-websphere90-mysql57-jdk8   |
|                               |                                             |
|                               | functional-smoke-wildfly110-mariadb102-jdk8 |
|                               |                                             |
|                               | modules-integration-mysql57-jdk8            |
|                               |                                             |
|                               | modules-unit-jdk8                           |
|                               |                                             |
|                               | unit-jdk8                                   |
+-------------------------------+---------------------------------------------+
| 7.1.x, 7.1.x-private          | integration-mysql57-jdk8                    |
|                               |                                             |
|                               | functional-smoke-jboss71-mysql57-jdk8       |
|                               |                                             |
|                               | functional-smoke-tcserver40-mysql57-jdk8    |
|                               |                                             |
|                               | functional-smoke-tomcat90-db2111-jdk8       |
|                               |                                             |
|                               | functional-smoke-tomcat90-mariadb102-jdk8   |
|                               |                                             |
|                               | functional-smoke-tomcat90-mysql57-jdk8      |
|                               |                                             |
|                               | functional-smoke-tomcat90-oracle122-jdk8    |
|                               |                                             |
|                               | functional-smoke-tomcat90-postgresql10-jdk8 |
|                               |                                             |
|                               | functional-smoke-tomcat90-sybase160-jdk8    |
|                               |                                             |
|                               | functional-smoke-weblogic122-mysql57-jdk8   |
|                               |                                             |
|                               | functional-smoke-websphere90-mysql57-jdk8   |
|                               |                                             |
|                               | functional-smoke-wildfly110-mariadb102-jdk8 |
|                               |                                             |
|                               | modules-integration-mysql57-jdk8            |
|                               |                                             |
|                               | modules-unit-jdk8                           |
|                               |                                             |
|                               | unit-jdk8                                   |
+-------------------------------+---------------------------------------------+
|7.0.x, 7.0.x-private           | integration-mysql56-jdk8                    |
|                               |                                             |
|                               | functional-smoke-jboss70-mysql56-jdk8       |
|                               |                                             |
|                               | functional-smoke-tcserver32-mysql56-jdk8    |
|                               |                                             |
|                               | functional-smoke-tomcat80-db2111-jdk8       |
|                               |                                             |
|                               | functional-smoke-tomcat80-mariadb102-jdk8   |
|                               |                                             |
|                               | functional-smoke-tomcat80-mysql57-jdk8      |
|                               |                                             |
|                               | functional-smoke-tomcat80-oracle122-jdk8    |
|                               |                                             |
|                               | functional-smoke-tomcat80-postgresql10-jdk8 |
|                               |                                             |
|                               | functional-smoke-tomcat80-sybase160-jdk8    |
|                               |                                             |
|                               | functional-smoke-weblogic121-mysql56-jdk8   |
|                               |                                             |
|                               | functional-smoke-websphere85-mysql56-jdk8   |
|                               |                                             |
|                               | functional-smoke-wildfly100-mariadb102-jdk8 |
|                               |                                             |
|                               | modules-integration-mysql5-jdk8             |
|                               |                                             |
|                               | modules-unit-jdk8                           |
|                               |                                             |
|                               | unit-jdk8                                   |
+-------------------------------+---------------------------------------------+
|ee-6.2.x, ee-6.2.10            | integration-mysql55-jdk7                    |
|                               |                                             |
|                               | functional-glassfish31-postgresql10-jdk7    |
|                               |                                             |
|                               | functional-tomcat70-mysql55-jdk7            |
|                               |                                             |
|                               | functional-wildfly71-oracle122-jdk7         |
|                               |                                             |
|                               | unit-jdk7                                   |
+-------------------------------+---------------------------------------------+
|ee-6.1.x, ee-6.1.30            | integration-mysql55-jdk7                    |
|                               |                                             |
|                               | functional-tomcat70-mysql55-jdk7            |
|                               |                                             |
|                               | unit-jdk7                                   |
+-------------------------------+---------------------------------------------+


*If there is a batches that should be added please contact QA Engineering with your requests.


**PORTAL_BATCH_TEST_SELECTOR (required):**

This parameter is used to choose which test(s) to run with the batch.


**Functional Test Selectors:**

This parameter must be one individual poshi test when referencing a functional batch in the PORTAL_BATCH_NAME parameter.

Examples:

``PortalSmoke#Smoke``

``CPWebcontent#AddWebContent``

``ClusteringCE#AddAndDeleteBlogEntriesOnSeparateNodes``

**Unit/Integration Test Selectors:**


This parameter must be a glob that includes a particular set of tests when referencing a unit or integration batch in the PORTAL_BATCH_NAME parameter.

Examples:

``**/test/unit/**/*Test.java``

``**/test/integration/**/Blogs*Test.java``

``**/src/test/**/JenkinsResultsParserTest.java``

``**/src/testIntegration/**/WikiUserNotificationTest.java``


**PORTAL_BRANCH_SHAS:**

This parameter is used to specify which SHAs to run the test batch & tests selected against.  The SHAs can be selected in 3 ways.


Comma-Delimited List:
********************

The SHAs must be input as a comma-delimited list.  There is a max of 10 SHAs allowed per build.

This is the recommended method for selecting SHAs since it is the most exact.

Examples:

* df1d74ed35dd515a1943205f45dd4adefd52aef1,b492fa4001980c3141723458725f1bb120c99e1f,49f469443df3235f94153c3edf0d9fcfa627b490,362f851fa1f08a28448cbdf520e4dee27ba17de6

* C9dc9b031849ed0f2c4bf54152bdcaca3f53aead,362f851fa1f08a28448cbdf520e4dee27ba17de6


Comparison URL:
********************

This would be using a comparison URL as seen in GitHub.  The RCA Tool will use this URL to create a range of commits to be split up into evenly sized groups.  This input can be used if the user would like to avoid choosing a specific set of commits to run against.

Examples:

* https://github.com/liferay/liferay-portal-ee/compare/8588c543c68589557e18da1f8df5ae5b713e6807...db2ae5737238afc7cdccaa56723515f5e65e2ea9

* https://github.com/liferay/liferay-portal-ee/compare/17973df4764dcc21d51493e5f7c7f7d5ce97f713...b492fa4001980c3141723458725f1bb120c99e1f


Head Commit:
********************

When this parameter is left blank the RCA Tool will simply run the Head Commit of the branch specified within PORTAL_GITHUB_URL.

This can be used if a user has a fix to a specific test, and have that fix in a custom branch that a user would like to test.  This method is favorable to running a full pull request test since it will use a maximum of 2 servers.


**PORTAL_GITHUB_URL (required):**

This parameter is used to select a GitHub branch against which the RCA Tool will run.

Here are some example GitHub URLs:

* https://github.com/liferay/liferay-portal/tree/master

* https://github.com/liferay/liferay-portal-ee/tree/master-private

* https://github.com/pyoo47/liferay-portal/tree/master-qa-12345


**PORTAL_UPSTREAM_BRANCH_NAME (required):**

This parameter is used to tell the RCA Tool which branch the PORTAL_GITHUB_URL branch was based on.

The only valid portal upstream branch names are currently:

* master   /  master-private

* 7.2.x    /  7.2.x-private

* 7.1.x    /  7.1.x-private

* 7.0.x    /  7.0.x-private


**JENKINS_GITHUB_URL:**

This parameter is used to reference a patched version of the RCA Tool.

If someone from QA Engineering has a ‘liferay-jenkins-ee’ branch that has additional features or fixes, this field can be used to reference that branch.

Here are some example inputs for this particular field:

* https://github.com/lesliewong92/liferay-jenkins-ee/tree/master

* https://github.com/michaelhashimoto/liferay-jenkins-ee/tree/master-qa-rca-working-copy








.. _`Jenkins Server`: https://test-1-1.liferay.com/job/root-cause-analysis-tool/build?delay=0sec

