=======
Github
=======

Github Workflow
------------------

It is important to understand Github commit workflow when writing a Poshi test.
Following these steps will help both test lead and flex tester to keep in sync when it comes to committing and pushing up codes to Github:

1. Before writing any tests, you need to make sure your master branch is up to date by using ``git pull upstream master``, then push your master origin to Github with ``git push origin master``.
2. When master is up to date, you need to create your own local branch with ``git checkout -b {yourBranchName}``. Most of the time your branch name will be the LRQA ticket number that you are assigned to. (Example: ``git checkout -b LRQA-123412``)
3. Now you're on your local branch, you can make changes to the files without affecting master branch. Time to start writing your automation test.
4. After completing your Poshi test. Time to dive in committing workflow.
  a. Run ``git status`` on your local terminal to see which files you make changes
  b. When writing poshi, the only changes you should make is files end with ``.testcase``, ``.macro``, and ``.path``.
  c. Test leads prefer the commits to only contain changes make to each file separately and come in the order of 
  ``.path`` > ``.macro`` > ``.testcase``
      Example: After adding ``.path`` file, you need to commit right away, make sure to include the ticket number at the beginning of the message ``git commit -m`` "LRQA-123412 Add path file" 
  d. Continue the previous step for ``.macro`` and ``.testcase`` files.
  e. Finally, you will need to push your local branch to Github with ``git push origin {yourBranchName}``.

Merge your remote branch to test lead's branch
----------------------

After you have finished pushing your code to your remote branch on Github, you need to send a `Pull Request`_ to your test lead.
On the comment section, comment ``ci:test:sf`` and ``ci:test:relevant`` for the test to run on CI.

Congratulations! You have finished your Poshi test




.. _`Pull Request`: https://docs.github.com/en/free-pro-team@latest/github/collaborating-with-issues-and-pull-requests/about-pull-requests
