==============
User Interface
==============

We dissociate the *controlling interface* from the *virtual environment*.

The *controlling interface* (here called ``console``) is the graphical user interface (GUI) that controls BlenderVR. The *virtual environment* is the part of the simulation that runs on each node inside ``blenderplayer``.

To simplify, the ``console`` is run by the user, use PySide but cannot import ``bge`` python module whereas the *virtual environment* is run by ``blenderplayer``, don't have any GUI and can import ``bge`` python module.

From the `processor file <processor-file.html>`_ perspective there is even a third mode, the ``update loader``. This mode is a glue between the previous ones. In the ``update loader`` the ``.blend`` file is changed on-the-fly so when it runs into the ``virtual environment`` it interacts with the ``console`` and with eventual interaction devices.

Document Sections
-----------------

* `Console`_

  * `Configuration File`_
  * `Active Screen Set`_
  * `Simulation File`_
  * `Start/Stop`_
  * `Debug Window per Screen`_
  * `Standard/Error Outputs`_
  * `Log Level`_

* `Daemons`_

Console
-------


The so called ``console`` is the GUI of BlenderVR. It allows you to choose the configuration file, the screen set to use, the simulation file (.blend) or to run blenderVR.

.. You can load the ``console`` by invoking ``./blenderVR path/blenderVR`` (clicking on it or running from a ``console``). You can also add ``blenderVR`` inside a ``bin`` folder that is included inside your ``PATH`` environment variable.

.. figure:: /images/user-interface-1and2.png
  :width: 700px
  :figwidth: 700px
  :align: center

  Console Graphical User Interface (left: ``Configuration`` tab, right: ``Run`` tab)


By default, the ``console`` does not "know" anything. You have to manually set configuration file, active screen-set, simulation file ... However, it stores these relevant information in its internal data store path (see above). So you have to set these information the first time you run BlenderVR and they remain active (across different running) until you change it with the GUI.

Configuration File
==================

You can specify the ``XML`` file inside the ``configuration`` tab (A-1). Don't forget to click on ``> Load configuration`` (A-2) to ask BlenderVR to read the configuration file (and store it inside its internal data file) ! You should go to ``run`` tab (B) and select ``debug`` (3b) inside the log window (3) to see if there is bug inside your configuration file.

Active Screen Set
=================

You can choose any screen set (4) that is defined inside your ``XML`` configuration file. You also must click on ``> Load screen set`` (5) to make it active (and register it for further BlenderVR usage). The current active screen set is displayed on the right.

Simulation File
===============

Here, you must select the ``.blend`` file you want to load (6). For the beginning, you should try the ``basic.blend``, that you can get from the `samples repository <../installation/installation.html#getting-samples>`_. You can manually select a processor file (7) or activate the ``NameLink`` (8) for blenderVR to automatically look for a <name_of_blender_scene>.processor.py file in the directory of the .blend  file. You will learn to create your own .blend scenes and processor files via the samples and going though the `blenderVR API <http://blender-vr.readthedocs.org>`_.

Start/Stop
==========

When everything is defined you can try to start/stop (9) by going to the ``Run`` tab. Have a look at the main log window below the Start and the Stop buttons.

Debug Window per Screen
=======================

Once the configuration file and the screen set are loaded, you can also have a look at the per screen log window : top screen menu ``Windows`` > ``Screens`` and select the screen that you want to debug. We suggest, at the beginning, to debug your XML `configuration file <configuration-file.html>`_, to set it to debug mode and activate ``Standard output`` and ``Error output``.

.. figure:: /images/select-screen.png
  :width: 400px
  :figwidth: 400px
  :align: center

  Top screen ``Windows`` menu.

.. figure:: /images/screen-window.png
  :width: 700px
  :figwidth: 700px
  :align: center

  Screen window for screen named ``full left`` in the configuration file.

Standard/Error Outputs
======================

They will display ``stdout`` and ``stderr`` of the instance of blenderplayer. Thus, you will see if there is a bug while running it. When blenderplayer runs correctly, you should disable these options.

Log Level
=========

The log level (3b) is useful when blenderplayer runs properly. It can display errors of your `processor file <processor-file.html>`_ in the log window (3).

Daemons
-------

The ``console`` use one daemon per screen. The daemon is a python script that:

  * Connects by network to the ``console`` and interact with it.
  * Start the instance of blenderplayer (for the "virtual environment") when required.
  * Catch blenderplayer's ``stdout`` and ``stderr`` to address them to the ``console`` if requested.
  * Kill blenderplayer if the "virtual environment" don't gently stop on ``console`` request.
  * . . .

In other words, the daemon manages blenderplayer. It runs on the computer that will run the blenderplayer instance.

Under Linux, this daemon becomes a real UNIX daemon (fork, close input and output ...).

.. note::
  The daemon script is included inside BlenderVR - you don't have to tweak it.

