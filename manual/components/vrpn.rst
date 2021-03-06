======================================
Virtual Reality Private Network (VRPN)
======================================

VRPN is a protocol used in Virtual Reality to exchange data with external devices. See http://www.cs.unc.edu/Research/vrpn/.

BlenderVR behaves like a VRPN client. At the other end, a VRPN server will host
different tracker or sensors that would be as many haptic arms, tracked stereoscopic
glasses or Wiimote devices. The server will associate a name to these device, along
with a variable “info” that holds the useful information about the considered device.

In BlenderVR, the receiving of VRPN messages and definition of associated methods
is done in the ``<blender_scene_name>.processor.py`` script attached to a scene (see
examples in the `samples <../installation/installation-manual.html#getting-samples>`_ folder).

Document Sections
-----------------

  * `Interaction Setup`_
  * `Example with a Nintendo Wii Controller`_

Interaction Setup
----------------------

To be able to interact in your BlenderVR scene with a VRPN compatible interface you
will have to:

  1. Define the interface in your ``vprn.cfg`` script
  2. Define the related processor method in the BlenderVR ``.xml`` configuration script
  3. Define the processor method in the ``<blender_scene_name>.processor.py`` script attached to your BlenderVR scene

Example with a Nintendo Wii Controller
--------------------------------------

1. In your ``vrpn.cfg`` file, add:

.. code::

   vrpn_WiiMote WiiMote0 1 0 0 1

2.  In the BlenderVR ``.xml`` configuration script (e.g. single.xml), add:

.. code:: xml

  <processor>
    (...)
    <plugins>
      <vrpn>
        <analog device="WiiMote0" host="localhost" processor_method="wiiAnalog"/>
        <button device="WiiMote0" host="localhost" processor_method="wiiButton"/>
      </vrpn>
    </plugins>
  </processor>

*Analog will receive accelerometer data from the WiiMote, button only the pressed button states.*

.. note::
  You also need to specify the folder containing your vrpn library in the `configuration file <../architecture/configuration-file.html#library-path-sub-section>`_.

3. In the ``<blend_file_name>.processor.py`` script (e.g. BlenderVR_API.processor.py), add:

.. code:: python

  import blendervr

  if blendervr.is_virtual_environment():
    import bge

    class Processor(blendervr.processor.getProcessor()):
      (...)

      def wiiAnalog(self, info):
        self.logger.info("Analog from Wii through VPRN ", info)

      def wiiButton(self, info):
        self.logger.info("Button from Wii through VPRN ", info)

Here, both functions will be executed whenever the VRPN server receives data from the
WiiMote (the wiiButton when your touch a button, the wiiAnalog when you move the
WiiMote).
