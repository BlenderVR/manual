========================
Open Sound Control (OSC)
========================

Routines based on the `OSC protocol <http://opensoundcontrol.org>`_ (based on UDP) have been added to BlenderVR (`dedicated API <http://blender-vr.readthedocs.org/processor-file/osc_api.html>`_) to be able to easily send data to a third party application that would take care of the audio components related to a given VR scene.

You're welcome to use BlenderVR `Sound Rendering Engine <https://blendervr.limsi.fr/doku.php?id=addons>`_ (SRE, open source, developped in `Max/MSP <http://cycling74.com>`_) if you don't want to develop your own sound server.
While the OSC API allows to easily send OSC messages, said SRE has been designed to receive an process these flags.

.. note::

  BlenderVR `OSC API <http://blender-vr.readthedocs.org/processor-file/osc_api.html>`_ can easily be adapted to any other OSC client to fathom your own interactions.

Document Sections
-----------------

  * `Interaction Setup`_

Interaction Setup
-----------------

This section details how to setup BlenderVR `configuration file <configuration-file.html>`_ to work with its Max/MSP `Sound Rendering Engine <https://blendervr.limsi.fr/doku.php?id=addons>`_.

In the ``<osc>`` subsection of the ``<plugins>`` section in the configuration file are defined the parameters related to OSC and sound rendering, typically:

.. code-block:: xml

    <plugins>

      <-- (...) -->

      <-- general parameters -->
      <osc host='localhost' port='3819' configuration='Laptop SPAT' max_audio_objects='8'>
        <-- user parameters -->
        <user listener='Binaural 1' viewer='user A' />
        <user listener='Binaural 2' viewer='user B' />
        <user listener='Ambisonic' />
        <user listener='Stereo' />
      </osc>

    </plugins>

with:

* ``host`` / ``port``: IP adress and port of the OSC server (computer on which the Max/MSP Sound Rendering Engine is opened).

* ``configuration``: flag used to dynamically adapt the Sound Rendering Engine to a given architecture specific (e.g. load the patches adapted to a given speaker configuration, rendering technique, etc.)

* ``max_audio_objects``: flag used to pre-allocate N audio objects in the SRE. BlenderVR will use and reuse (once released) these pre-allocated audio objects to add sound to your scenes. This mecanism allows to limit the maximum DSP usage on the OSC server.

* user ``listener`` / ``viewer``: these flag allow to associate BlenderVR users (viewers) and Max/MSP sound rendering techniques (listeners). Here, ``<user listener='Binaural 1' viewer='user A' />`` associates BlenderVR viewer ``user A`` to Max/MSP listener ``Binaural 1`` (i.e. to a headset in Max/MSP), e.g. for head-tracking automatic update.

Once you've opened the ``BlenderVR_Sound_Rendering_Engine_<version>.maxpat`` on your OSC server, the rest of the sound adding process takes place in BlenderVR `processor file <processor-file.html>`_ through the `OSC API <http://blender-vr.readthedocs.org/processor-file/osc_api.html>`_.

.. tip ::

  If you downloaded BlenderVR `samples <../installation/installation-manual.html#download-samples-scenes>`_, see the scenes in the ``samples/plugin/osc`` folder for a direct insight on how to use the OSC API.

.. LIMSI members, see http://wikivenise.limsi.fr/index.php/Open_Sound_Control.
