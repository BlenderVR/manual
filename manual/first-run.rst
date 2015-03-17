=========
First Run
=========


.. note::
  After the `installation <installation/installation.html>`_ you should make sure everything is working before going on your own. For this first run you will need at least the basic sample from the `samples repository <installation/installation.html#getting-samples>`_.

Document Sections
-----------------
  * `Launch Blender-VR`_
  * `Open the Simulation File`_
  * `Edit the Configuration File`_
  * `Run`_

Launch Blender-VR
-----------------

Start by opening the blenderVR GUI (see `running Blender-VR <installation/installation.html#running>`_). Although in the future you can launch it via a shortcut, for the first run it's better to do it via command-line, to catch any unexpected error.

Open the Simulation File
------------------------

In the `Simulation File <components/user-interface.html#simulation-file>`_ select the ``basic.blend`` file. Mark ``NameLink`` for the ``basic.processor.py`` to be automatically selected as the `processor file <components.html#processor-file>`_.

Edit the Configuration File
---------------------------

You now need a valid `configuration file <components/configuration-file.html>`_ to run Blender-VR. Make sure to follow the correct instructions and set a correct ``blender`` and ``blenderplayer`` paths.

Remember to `select and load <components/user-interface.html#configuration-file>`_ the configuration file.

.. note::
  For the initial test it's recommended to create a single screen with a mono buffer setup.

Run
---
If there are no errors in the configuration tab, change to the ``Run`` tab and hit `Start <components/user-interface.html#start-stop>`_ .

Congratulations, you can now try the other sample files, configuration options and finally bring your own ``.blend`` files into Blender-VR.

