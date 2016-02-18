===============
Oculus Rift DK2
===============

Setup with one Oculus Rift, without networking
----------------------------------------------

See the `Install Plugin Oculus Section <../installation/plugins.html#oculus-rift-dk2>`_ for installation notes.


Basic setup
~~~~~~~~~~~

.. note ::

  Currently, Blender VR does not support direct mode for the Oculus Rift. To run Oculus Rift with Blender VR, use extended mode (Tools, Rift Display Mode, Extend the HMD to Desktop, Apply in the Windows Oculus Rift Config Utilty).

Select main_dk2.xml as a basic configuration file in BlenderVR, making sure you understand what's new there by taking a look at the `Oculus configuration file section <./configuration-file.html#desktop-oculus-dk2>`_ and select, for example, the basic-dk2.blend in the ``samples/plugin/hmd`` folder.


Additional info relevant for Linux environments
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You need to run ovrd in order to have the Oculus communicating with the applications. ovrd is part of the Oculus SDK.

All this communication is done via the /dev/hidraw2 device. The hidraw driver provides the RAW interface for HID (Human Interface Devices) USB and Bluetooth.

How to install it? All you need is to run make install as indicated in the README.Linux file of the SDK.

Additionally, if you run into problems, you may be required to load the OpenGL library from a recent driver. For example by adding export LD_PRELOAD="/usr/lib/nvidia-346/libGL.so to your .bashrc file (replace-346 by your driver version).
