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

* install java
* install dk2-blender-java-web-sockets
* install python dependencies
* install the oculus rift dk2 runtime
* modify BlenderVR configuration file for dk2 support

The dk2 support in BlenderVR relies on the `dk2-blender-java-web-sockets <https://github.com/tltmedia/dk2-blender-java-web-sockets>`_.
This java-websocket is a local server (to be launched on the machine to which the oculus is plugged) that will receive the data from the oculus dk2 and let BlenderVR pull them to synchronize the user orientation in the virtual world.

Install `Java <https://www.java.com/fr/download/>`_ on your machine (try to type ``java`` in a terminal window to see if it's not already installed).

Download `dk2-blender-java-web-sockets-master.zip <https://github.com/tltmedia/dk2-blender-java-web-sockets/archive/master.zip>`_ or clone the `Git repository <https://github.com/tltmedia/dk2-blender-java-web-sockets>`_, rename it ``dk2-blender-java-web-sockets`` and move it to $INSTALL_DIR/plugins.

Install Python dependencies

On OSX/Linux:

.. code-block:: bash

  $ cd $INSTALL_DIR
  $ source venv/bin/activate
  $ pip3 install -r source/requirements-dk2.txt

On Windows:

.. code-block:: bash

  $ cd $INSTALL_DIR
  $ .\venv\Scripts\activate
  $ pip3 install -r source\requirements-dk2.txt

Download and install the `Oculus Runtime <https://developer.oculus.com/downloads/>`_ for your architecture.

.. note ::

  OSX: check on the web to setup your screen configuration for the rift (mirrored display, 90 rotation, etc.), e.g. `here <http://www.reddit.com/r/oculus/comments/2dbxve/041_with_dk2_on_a_mac_incompatible_resolution/>`_


Modify your `configuration file <components/configuration-file.html>`_ to add the path to your newly installed libraries. Check the configuration file ``$INSTALL_DIR/source/configurations/main-dk2.xml`` for guideline.

Once done, launch the ``basic-dk2.blend`` scene in ``$INSTALL_DIR/samples/plugin/hmd/``.
