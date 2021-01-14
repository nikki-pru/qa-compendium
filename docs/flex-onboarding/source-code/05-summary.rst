Summary
^^^^^^^^

There are two main ways we work with an updated master portal.
1. Using a snapshot bundle as described in `this section of Training`_.

These snapshots are built every few hours. If it is not critical to use code that has been updated in the last few hours, it is perfectly acceptable to use these bundles instead of building from ant all.

2. Building from Source
Building from source is recommended if the code you need was merged very recently, after the latest snapshot bundle was created.

If I only need snapshot bundles, do I need to update master?
-------------------------------------------------------------
If you are working with Poshi, yes. This is because updated Poshi files are housed in master and you would need to pull in changes to be able to work on updated files. Running ``ant all``  is not needed to use Poshi files, but it is recommended to run ``ant setup-sdk`` after pulling upstream.

To summarize that, your setup could be:

1. Run a snapshot bundle
2. Update your master-portal directory and run ``ant setup-sdk``
3. Proceed with Tests workflow

.. _this section of Training: ../portal/starting-portal.html#starting-up-a-portal-instance
