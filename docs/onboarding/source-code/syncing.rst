Syncing Local and Origin Masters to Upstream
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If you have not forked the liferay-portal repo, navigate to the `Liferay Github repo`_ and do that now. Forking the repo adds liferay-portal to your list of repositories so you can push your changes later on to your origin.

It is important to make sure your local and remote (cloud) files are up to date. Here’s how to sync your local and origin masters to upstream.

1. Brian Chan (or others with system permissions) push changes to Liferay master upstream.
2. To update your local files, run ``git pull upstream {branch}`` in the directory where you have your master-portal files. In this case, ``{branch}`` is master.
3. This pulls down code and merges it in your local master.
4. When that’s done, run ``git push origin {branch}``. This updates your Origin with what you have locally.

Graphically, the process looks something like this:

|image0|

Three things to keep straight in Git
-------------------------------------

**Local master**
This is your copy of the source code, stored locally on your computer. You want to keep this up to date with upstream master.

**Upstream master**
This is all of the source code for portal. Think of this as the Liferay cloud that contains only the reviewed and committed files. Only a select few are allowed to push directly upstream (BChan, Shuyang, etc.).

**Origin master**
This is your copy of the source code, stored in your GitHub cloud. Tt should be identical to Local master. When you want to submit your commits - changes or fixes you make for review (don't worry about this yet), you will need to push them from your local machine to your origin.

If you've noticed, your local and origin master should always be identical to upstream master. In order to keep your local and origin master identical to the upstream master, it is recommended to update your local and origin often (you can use a `script`_).

To avoid conflicts later on, it is not recommended to make changes to any of the master branches. Whenever you need to make a change to the source code it is best practice to create a new branch off of master as your working branch. Run the following command to create a new branch ``git checkout -b {branch.name}``.

⚠️  On the directory where you fetched Source, run ``git log -1``. Ping  your trainers and post what Git ID you are on.

⚠️  Run ``git remote -v`` to verify your configuration and send a screenshot of the outcome to your trainers

.. |image0| image:: ./img/git-upstream-origin-sync.png

.. _Liferay Github repo: http://github.com/liferay/liferay-portal
.. _script: ../portal/shortcut.html
