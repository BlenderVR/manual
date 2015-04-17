===============
Install Plugins
===============

BlenderVR comes with plugins, e.g. to support the Oculus Rift DK2 or to use VRPN devices.
This page will lead you through their installation, while none of them is mandatory to run BlenderVR.


Document Sections
-----------------
* `Folder Structure`_
* `VRPN`_
* `Oculus Rift DK2`_


Folder Structure
----------------

Add a ``plugins`` directory to your $INSTALL_DIR (see `Folder Structure <installation.html#folder-structure>`_, this is once more a recommendation as it will be used as reference along this manual).

.. ``//plugins/``
.. *BlenderVR Plugins*

VRPN
----

This section briefly exposes the `VRPN <http://www.cs.unc.edu/Research/vrpn/index.html>`__, install.
In a nutshell, you will have to build VRPN, launch a VRPN server and BlenderVR then will act as a VRPN client to fetch the data from your VRPN devices.
once the VRPN server launched on your machine/network, any device defined in your vrpn.cfg (input of vrpn server) will be handled by the server and its related ``infos`` pulled by the BlenderVR VRPN client.
See `Getting started with VRPN <http://www.cs.unc.edu/Research/vrpn/vrpn_getting_started.html>`_ for more information.

Download `VRPN 07.33.zip <http://www.cs.unc.edu/Research/vrpn/downloads/vrpn_07_33.zip>`__ and unzip it into $INSTALL_DIR/plugins/vrpn/.
.. Create a ``build`` directory to finally have the following tree:

.. ``//plugins/vrpn/vrpn``
.. ``//plugins/vrpn/build``

.. On OSX:

.. .. code-block bash

..   $ cd $INSTALL_DIR/plugins/vrpn/build
..   $ cmake -DCMAKE_OSX_ARCHITECTURES=x86_64 ../vrpn
..   $ make

then follow compilation instructions from `VRPN Compiling <http://www.cs.unc.edu/Research/vrpn/vrpn_standard_stuff.html>`__.

Add the path of the vrpn python directory (e.g. `$INSTALL_DIR/plugins/vrpn/build/python`) to your `configuration file <components/configuration-file.html>`_ libraries.

Once done, launch the ``basic-vrpn.blend`` scene in ``$INSTALL_DIR/samples/plugin/vrpn/basic-vrpn/``.

Oculus Rift DK2
---------------

This section guides you through the installation required to run the `Oculus Rift DK2 <http://oculus.com/>`__ with BlenderVR.
The install procedure involves:

* install the oculus rift dk2 runtime
* modify BlenderVR configuration file for dk2 support

Download and install the `Oculus Runtime <https://developer.oculus.com/downloads/>`_ for your architecture.

.. note ::

  OSX: check on the web to setup your screen configuration for the rift (mirrored display, 90 rotation, etc.). For example: [`here <http://www.reddit.com/r/oculus/comments/2dbxve/041_with_dk2_on_a_mac_incompatible_resolution/>`__]


Modify your `configuration file <components/configuration-file.html>`_ to add the plugin users.
Check the Oculus configuration examples for `Desktop Oculus DK2 <../components/configuration-file.html#desktop-oculus-dk2>`_ and `Dual Oculus DK2 <../components/configuration-file.html#dual-oculus-dk2>`_ setups.

Once done, launch the ``basic-dk2.blend`` scene in ``$INSTALL_DIR/samples/plugin/hmd/``.
