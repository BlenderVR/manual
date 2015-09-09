=========
First Run
=========


.. note::
  After the `installation <installation/installation-manual.html>`_ you should make sure everything is working before going on your own. For this first run you will need at least the basic sample from the `samples repository <installation/installation-manual.html#download-samples-scenes>`_.

Document Sections
-----------------
  * `Launch BlenderVR`_
  * `Open the Simulation File`_
  * `Edit the Configuration File`_
  * `Run`_

Launch BlenderVR
-----------------

Start by opening the BlenderVR GUI (see `Running BlenderVR <installation/installation-manual.html#running>`_ in the Install section). Although in the future you can launch it via a shortcut, for the first run it's better to do it via command-line, to catch any unexpected error.
It is advised to understand how to manipulate the `User Interface <components/user-interface.html>`_ before going any further.

Open the Simulation File
------------------------

In the `Simulation File <components/user-interface.html#simulation-file>`_ select the ``basic.blend`` file. Mark ``NameLink`` for the ``basic.processor.py`` to be automatically selected as the `Processor File <components/processor-file.html>`_.

Edit the Configuration File
---------------------------

You now need a valid `Configuration File <components/configuration-file.html>`_ to run BlenderVR. Make sure to follow the correct instructions and set a correct ``blender`` and ``blenderplayer`` paths.

Remember to `select and load <components/user-interface.html#configuration-file>`_ the configuration file.

.. note::
  For the initial test it's recommended to create a single screen with a mono buffer setup.

Run
---
If there are no errors in the configuration tab, change to the ``Run`` tab and hit `Start <components/user-interface.html#start-stop>`_ .

Congratulations, you can now try the other sample files, configuration options and finally bring your own ``.blend`` files into BlenderVR.

