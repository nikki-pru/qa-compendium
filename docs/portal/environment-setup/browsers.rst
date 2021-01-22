===================
Chrome 65 for Poshi
===================

See this `Loop post`_ for more information.

In order to run tests on Chrome 65 (without using your existing Chrome latest install), you will need to perform this one-time setup.

This second Chrome binary can be used in the poshi tests without interfering with your current Chrome (latest) install.

  1. Download Chrome 65 (Chromium) Binary
    a. `Linux`_
    b. `Mac`_
    c. `Windows`_
  2. Extract to a permanent location
  3. Modify test.USERNAME.properties and add location to Chrome 65 binary
  ::
      browser.chrome.bin.file=C:/chromium/chrome-win32/chrome.exe
      browser.chrome.bin.file=/Users/name/chrome65/Chromium.app/Contents/MacOS/Chromium

.. note::

  Standalone official Chrome 65 binaries can be downloaded and used for Linux and Mac, but they may auto-update after using them for some time, It is recommended to use Chromium instead. Chromium is the only option for Windows.


.. _Loop post: https://loop.liferay.com/web/guest/home/-/loop/feed/16745774
.. _Linux: https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Linux_x64/530372/
.. _Mac: https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Mac/530368/
.. _Windows: https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/530373/