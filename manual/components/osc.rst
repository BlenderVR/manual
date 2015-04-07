========================
Open Sound Control (OSC)
========================

.. note ::

  Document need to be reviewed. Also the documentation need to be tested to see if it is still valid.

OSC is a protocol used to send / receive data through applications. See
http://opensoundcontrol.org.

BlenderVR includes a MaxMSP (http://cycling74.com) Sound Rendering Engine
available at `Downloads`_. It is however possible (and advised) to
make it work with any other OSC client and fathom it for other purposes.

Document Sections
-----------------

  * `Interaction Setup`_
  * `Downloads`_

Interaction Setup
-----------------

While the OSC API allows to easily send OSC (UDP) flags, the MaxMSP associated
Sound Rendering Engine has been design to receive an process these flags.
Once you’ve opened the ``BlenderVR_Sound_Rendering_Engine_vX.maxpat`` on the
OSC server as defined in the ``.xml`` configuration file:

.. code:: xml

  <processor>
    (...)
    <plugins>
      <osc host='serverName' port='3819'/>
        <user listener='Binaural 1' viewer='user A' />
        <user listener='Ambisonic' />
      </osc>
    </plugins>
  </processor>

And modified it to fit to your needs (spatializer, speakers mapping, microphone inputs,
etc.), the rest of the sound adding process takes place in BlenderVR.

.. note::
  You also need to specify the folder containing your osc library in the `configuration file <configuration-file.html#library-path-sub-section>`__.

See ``samples/BlenderCave_OSC.blend`` and ``samples/BlenderCave_OSC_API.blend``.
LIMSI members, see http://wikivenise.limsi.fr/index.php/Open_Sound_Control .

Downloads
---------

* `BlenderVR Sound Rendering Engine (.zip) <http://dalaifelinto.com/blendervr/ftp/blendervr_sound_rendering_engine_v4.zip>`_ version 4

This is an example of a flexible sound rendering engine developed under MaxMSP which is fully controlled from the OSC messages received from BlenderVR.

One may obviously use it with any other software (it's all about dynamic autonomous instantiations, should be modified to be used as a simple GUI Sound Rendering Engine).
