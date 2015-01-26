========================
Open Sound Control (OSC)
========================

.. note ::

  Document need to be reviewed. The download engine needs to be hosted in the new site.
  Also the documentation need to be tested to see if it is still valid.

OSC is a protocol used to send / receive data through applications. See
http://opensoundcontrol.org.

Blender-VR includes a MaxMSP (http://cycling74.com) Sound Rendering Engine
available at http://blendercave.limsi.fr/doku.php. It is however possible (and advised) to
make it work with any other OSC client and fathom it for other purposes.

While the OSC API allows to easily send OSC (UDP) flags, the MaxMSP associated
Sound Rendering Engine has been design to receive an process these flags.
Once you’ve opened the Blender-VR_Sound_Rendering_Engine_vX.maxpat on the
OSC server as defined in the ``.xml`` configuration file

.. code:: xml

  <processor>
    <osc host='serverName' port='3819'/>
  </processor>

and modified it to fit to your needs (spatializer, speakers mapping, microphone inputs,
etc.), the rest of the sound adding process takes place in Blender-VR.

See ``samples/BlenderCave_OSC.blend`` and ``samples/BlenderCave_OSC_API.blend``
LIMSI members, see http://wikivenise.limsi.fr/index.php/Open_Sound_Control .
