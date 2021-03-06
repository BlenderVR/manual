=================
Master and Slaves
=================

Communications inside BlenderVR are organized through a master/slaves structure.

Although inside `virtual environment <../components/processor-file.html#basic-processor-file>`_, all nodes are equivalent, one node is the master.

The master computer is the `console <../components/processor-file.html#basic-processor-file>`_ from the `configuration file <../components/configuration-file.html>`_.

Document Sections
-----------------

  * `Master`_
  * `Slaves`_

Master
------

The master node is the one that computes all scene interactions, updates the animations and dispatches them to the slaves.

This node have extra possibilities regarding slaves:

* You can access to keyboard and mouse of its graphic window,
* It connects to VRPN to get the information issued by VR devices,
* Dialog from the console are send to it,
* OSC is running on the master,
* . . .


Slaves
------

Playing blender animations on slaves has been reported to conflict with the update
coming from the master and may produces flicking.

To avoid that (and restrict calculation of scene updates), slave nodes are suspended (``bge.logic.getCurrentScene().suspend()``) during BlenderVR runs.

Even if you ``resume()`` the scene, the next execution of BlenderVR will ``suspend()`` it on the slaves.

