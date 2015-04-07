============================
UI - Daemon Network Protocol
============================

.. DPQ removed, failed latex compilation
.. ============================
.. UI ↔ Daemon Network Protocol
.. ============================

First of all, to avoid problem of paths resolutions, the UI must run in the same context (computer and user), than the daemon.

Document Sections
-----------------

  * `Base Protocol`_
  * `Get/Set Settings`_
  * `Simulation`_

Base Protocol
-------------

The communication relies on encapsulation of (command, argument) messages. Each stage of encapsulation is responsible to compose/decompose its information and parse the provided commands. In charge of the central stage to use blendervr.tools.connector.Client class to interact with the daemon and use its send(command, argument = '') method.

The method blendervr.tools.connector.Common.composeMessage(command, argument) must be use to compose a message sent to the peer.
On the other side, the method blendervr.tools.connector.Common.decomposeMessage(message) must be use to decompose a message and analyze its content.

For instance, if the UI request the blender file name, it should send (supposing client is a blendervr.tools.connector.Client object and composer is an import of blendervr.tools.connector.Common): client.send('get', composer.composeMessage('simulation', 'blender file name'))
For commodity, in the remaining specs, we will write: ('get', ('simulation', 'blender file name'))

Unless specified, the daemon will reply to request with the same keywords to acknowledge the value. Thus, if the UI request for the current blender file name, the dialog will be (supposing the current blender file is /home/blender/samples/mountain/mountain.blend):

* **UI**: ('get', ('simulation', ('blender file name')))
* **Daemon**: ('get', ('simulation', ('blender file name', '/home/blender/samples/mountain/mountain.blend')))


Get/Set Settings
----------------

The simulation can request/set many information from the daemon. For instance, to define the processor file, it must use ('set', ('simulation',('blender processor name', '/home/blender/samples/spider/spider.blend'))) (and the daemon will answer : ('set', ('simulation', ('blender processor name')))).


Simulation
----------

* blender file name [string]: name of the .blend file
* processor file name [string]: name of the processor file.
* link processor to blender [boolean]: do we have to link the processor file name to the blender file name ?

