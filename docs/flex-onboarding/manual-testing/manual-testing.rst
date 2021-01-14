Manual Testing
===============

We rely a lot on automation to test our products. Automated tests improve the efficiency of testing a large system like Liferay Portal. However, unless specified to do so, automation does not check every single thing related to the product or feature. Automated tests also take time to write and for a fast-paced environment, like during a product version release, it could be faster for someone to manually test a feature rather than scripting out the test. Because of these, manual testing is still a very important activity when testing the product.

Some manual testing tasks come with detailed instructions called `Test Plans`_. Test Plans organizes the who, what, when, where, how of testing.

1. Who will execute the tests
2. What test cases will be executed
3. When will the tests be executed and in what order
4. Where the tests will be executed
5. How we will be measuring, documenting the results

In other cases, manual testing tasks come with minimal instruction, like `this ticket`_. In cases where you are not given steps to test, use your best judgment and consider the following:

1. Deduct what is being asked for in the ticket through the summary or description;
2. If the ticket has a video or gif attached, figure out the steps from there;
3. Put yourself in the shoes of a customer/user - how will this feature be used, how can this feature break;
4. Never base on uncertainty - reach out to a team member, your lead or another QA member, or the developer to clarify what needs to be tested.

If something breaks or you find a bug while testing, don’t sweep it under the rug. These issues could potentially be blockers for an upcoming release or could cause more issues down the line if not properly looked into. If something breaks in-house it will also most likely break when it gets to the customer. If something is inconsistent, you can take note of the issue or ask a friend to do a sanity check on what you're seeing. You can also add a comment to the ticket being tested, or file a bug ticket on JIRA.  We will learn how to do that in the next section.

.. _Test Plans: https://docs.google.com/spreadsheets/d/15clEKFeLYoDPyqRHqZbjBTGpAwSMdqqM6Fhgr3gK1Ug/edit?usp=sharing
.. _this ticket: https://issues.liferay.com/browse/COMMERCE-2410
