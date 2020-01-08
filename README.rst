West Manifest Import Example
############################

Overview
********

Manifest imports are an in-development west feature which will be released in
version 0.7. You can follow this README to try it out. Please send feedback if you
have any!

This feature lets you import another west manifest file (like
`zephyr/west.yml`_) into your own west.yml file, and get all the imported
Zephyr modules "for free", without having to copy/paste them into your file and
track changes yourself.

.. _zephyr/west.yml:
   https://github.com/zephyrproject-rtos/zephyr/blob/master/west.yml

This repository contains a simple example `west.yml`_ doing just that:

.. code-block:: yaml

   manifest:
     remotes:
       - name: zephyrproject-rtos
         url-base: https://github.com/zephyrproject-rtos
     projects:
       - name: zephyr
         remote: zephyrproject-rtos
         revision: v2.1.0
         import: true

     self:
       path: my-zephyr-app

.. _west.yml:
   https://github.com/mbolivar/my-zephyr-app/blob/master/west.yml

It also contains a Hello World application, so you can see how this feature
lets you combine your own Zephyr application with Zephyr itself.

Getting the west pre-release
****************************

You currently need a pre-release version of west to use this feature.
Install it with pip3::

  pip3 install --user west==0.6.99.dev3   # Linux
  pip3 install west==0.6.99.dev3          # macOS, Windows

**You can always go back to the latest stable release** after you're done.
For example, to go back to 0.6.3::

  pip3 install --user west==0.6.3         # Linux
  pip3 install west==0.6.3                # macOS, Windows

Building and running
********************

First, create your Zephyr downstream using this repository as your manifest
instead of mainline zephyr::

  west init -m https://github.com/mbolivar/my-zephyr-app zephyr-imports
  cd zephyr-imports
  west update

Then you can build and flash this sample application for your favorite board
using ``west`` or any other tools you prefer.

Example build and flash for ``reel_board`` (run this from the
``zephyr-imports`` directory)::

  west build -b reel_board my-zephyr-app
  west flash

Sample Output
*************

If you connect to the board's console, you'll see a hello world message:

.. code-block:: console

    Hello World from my-zephyr-app!

More Examples
*************

We're documenting this feature in Zephyr `pull request 20433`_.

You can read the rendered HTML documentation here:

https://builds.zephyrproject.org/zephyrproject-rtos/zephyr/20433/docs/guides/west/manifest.html#manifest-imports

There are several additional examples along with complete documentation on how
the new feature currently works.

Your feedback is requested! Please let us know if you like it, or if there's
something missing or not quite right. Feel free to comment directly in `pull
request 20433`_ or send email to the Zephyr lists.

.. _pull request 20433:
   https://github.com/zephyrproject-rtos/zephyr/pull/20433

.. _west issue 221:
   https://github.com/zephyrproject-rtos/west/issues/221
