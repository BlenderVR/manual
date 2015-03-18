===============
Install Plugins
===============

blenderVR comes with plugins, e.g. to support the Oculus Rift DK2 or to use VRPN devices.
This page will lead you through their installation, while none of them is mandatory to run blenderVR.


Document Sections
-----------------
* `Folder Structure`_
* `VRPN`_
* `Oculus Rift DK2`_


Folder Structure
----------------

Add a ``plugins`` directory to your $INSTALL_DIR (see `Folder Structure <installation.html#folder-structure>`_, this is once more a recommendation as it will be used as reference along this manual).

.. ``//plugins/``
.. *Blender-VR Plugins*

VRPN
----

This section guides you through `VRPN <http://www.cs.unc.edu/Research/vrpn/index.html>`_,  install.
In a nutshell, you will have to build a VRPN server and blenderVR will act as a VRPN client.
once the VRPN server launched on your machine/network, any device defined in your vrpn.cfg (input of vrpn server) will be handled by the server and its related ``infos`` pulled by the blenderVR VRPn client.
See `Getting started with VRPN <http://www.cs.unc.edu/Research/vrpn/vrpn_getting_started.html>`_ for more information.

Download `VRPN 07.33.zip <http://www.cs.unc.edu/Research/vrpn/downloads/vrpn_07_33.zip>`_ and unzip it into $INSTALL_DIR/plugins/vrpn/.
Create a ``build`` directory to finally have the following tree:

``//plugins/vrpn/vrpn``
``//plugins/vrpn/build``

On OSX:

.. code-block:: bash

  $ cd $INSTALL_DIR/plugins/vrpn/build
  $ cmake -DCMAKE_OSX_ARCHITECTURES=x86_64 ../vrpn
  $ make

Else, follow compilation instructions from `VRPN Compiling <http://www.cs.unc.edu/Research/vrpn/vrpn_standard_stuff.html>`_.

Oculus Rift DK2
---------------

This section guides you through the installation of the dk2-blender-java-web-sockets.
This "java-websocket" is a local server (to be launch on the machine to which the oculus is plugged) that will received the oculus dk2 tracking infos.
In the meantime, blenderVR will pull these data to synchronize the user orientation in the virtual world.

Install `Java <https://www.java.com/fr/download/>`_ on your machine (try to type ``java``in a terminal window to see if it's not already installed).

Download `dk2-blender-java-web-sockets-master.zip <https://github.com/tltmedia/dk2-blender-java-web-sockets/archive/master.zip>`_ rename it ``dk2-blender-java-web-sockets`` and move it to $INSTALL_DIR/plugins.

Install Python dependecies

On OSX/Linux:

.. code-block:: bash

  $ cd $INSTALL_DIR
  $ source venv/bin/activate
  $ pip3 install -r blender-vr/requirements-dk2.txt

.. note::
  MacOS: running these lines may popup window "download the command line developer tools", go for it.

On Windows:

.. code-block:: bash

  $ cd $INSTALL_DIR
  $ .\venv\Scripts\activate
  $ pip3 install -r blender-vr\requirements-dk2.txt

Modify your `configuration file <components/configuration-file.html>`_ to add the path to your newly installed libraries or modify the configuration file ``$INSTALL_DIR/blender-vr/configurations/main-dk2.xml`` to match your architecture.

Once done, launch the basic .blend scene in $INSTALL_DIR/samples/oculus_dk2/
