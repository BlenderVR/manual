==================
Notion of  Vehicle
==================

We can see the Virtual Environment as a vehicle: each device is an item of the vehicle (wheel, brake pedal, etc.), the screens are the windows of the vehicle opening on outside (virtual) world, you can "scale" your vehicle to the objects of the scene (microscopes or telescopes are kind of vehicle ...).

In Virtual Environments, each tracker, device, screen, etc. of the real world is defined in its own reference frame. However, everything resides in the same space. So we have to introduce a reference frame change between each device. Instead of device inter-related position, BlenderVR uses a single reference frame in which all device, screen, tracker, etc. will be defined.

This "center" of the real world defines the origin of a vehicle: a bridge between real and virtual worlds.
As such, In the virtual world, the vehicle should be attached to blender virtual camera. Hence, if you move the camera, you move the vehicle inside the virtual world.

From another point of view, you can move yourself inside the vehicle without it moving in the virtual world: if you come back at the same place in the Virtual Environment you will have exactly the same display on the screens.

