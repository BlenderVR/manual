==================
Configuration File
==================

The BlenderVR XML configuration file is loaded by the `console <../architecture/run-modes.html#console>`_ to get the architecture related information to run BlenderVR and send it to each `virtual environment <../architecture/run-modes.html#virtual-environment>`_ rendering node.

This file must contain at least four sections, plus the ``plugins`` section.
It also includes a ``BlenderVR`` section which only option is the network port used for the synchronization between the rendering nodes.

.. note::
  Use of space in ``screen`` name should work. Beware still Windows users.

Document Sections
-----------------

  * `Redundant Sections`_
  * `Code Execution`_
  * `Starter Section`_
  * `Anchor`_
  * `Users Section`_
  * `Computers Section`_
  * `Screens Section`_
  * `Sample Configuration File`_

Redundant Sections
------------------

Some elements can be specific to one node, other shared. For instance, the ``blenderplayer`` executable can be the same for all rendering nodes or different on some nodes. In such case, there will be a section called ``system`` that can be inherited by each ``computer`` sub-section:


.. code:: xml

  <computers>
    <system>
      <blenderplayer executable='/usr/local/blender/2.74/bin/blenderplayer' />
    </system>
    <computer name='front computer' hostname='front.fqdn'>
      <system>
        <blenderplayer executable='/usr/bin/blenderplayer' />
      </system>
    </computer>
    <computer name='left computer' hostname='left.fqdn' />
    <computer name='right computer' hostname='right.fqdn'>
      <system>
        <library path='/usr/local/lib/vrpn/' />
      </system>
    </computer>
  </computers>

In this example, ``left computer`` and ``right computer`` nodes will use ``/usr/local/blender/2.74/bin/blenderplayer`` whereas ``front computer`` node will use ``/usr/bin/blenderplayer``.

The ``system`` section is called *redundant* as many entries will use the same information.


Code Execution
--------------

In the XML file, you can use back-quote to execute code. First, the XML parser will try to execute this code as python code in BlenderVR environment system (with all variables and import present in the BlenderVR XML parser). If it fails, then, it tries as bash code and take the stdout result. If none is valid it raises an error.

For instance,

.. code:: xml

  <environment>HOME=`os.environ['HOME']`</environment>

will define an environment variable (passed to the daemon or blenderplayer) called ``HOME`` that contains the current value of ``HOME`` operating system environment variable (with ``os.environ`` python code).


You can even use inherited values from redundant section:

.. code:: xml

  <login remote_command="ssh `self._attributs_inheritance['hostname']`">

used inside the system redundant section will specify that ``remote_command`` will include the hostname as given in the ``computer`` entry.

If uncertain, we suggest you to simply print the ``self._attributs_inheritance`` python dictionary:

.. code:: xml

  <login remote_command="`print(self._attributs_inheritance)`">

that will raise an exception (which is the point, since your purpose here is to create your configuration file, not to run BlenderVR).


Starter Section
---------------
..
  don't forget Blender

This section only concerns the console. It contains all screen sets definitions.

.. code:: xml

  <starter blender='/usr/bin/blender'>
    <config name='console'>console</config>
    <config name='virtual environment'>console, front screen, left screen, right screen</config>
    ...
  </starter>

You can also add a ``hostname`` attribute in case of ``socket.gethostname()`` python function returns wrong hostname. This hostname is used by all *virtual environment* nodes to contact the console for network connection control.

The ``blender`` attribute is required in most of the cases for the `Update Loader <../architecture/run-modes.html#update-loader>`_  process.

Each ``config`` sub-section must list all screens, separated by commas, used by this screen set.

.. note::
  De facto, the first screen listed here is the `master <../architecture/master-slaves.html#master>`_ node.

Anchor
------

On some devices, the paths are not homogeneous: the root path (repository) of ``.blend`` files on the console is not the same than on the master and/or on the slaves.

To fix that, BlenderVR uses the notion of **Anchor**: it is a node specific absolute path on all nodes that prefixes each relative path for blender and processor files.

It is a kind of least common multiple path. For instance, with two computers:

* **console** blender files repository: ``/home/me/blender_files``
* **master node** blender files repository: ``/remote_home/me/blender_files``

This least common path is ``/home`` on the console and ``/remote_home`` on the master node (``me/blender_files`` are common on both systems).

In such case, the starter section (console specific section) will start by:

.. code:: xml

  <starter anchor='/home'>

Whereas system section for the master node will start by:

.. code:: xml

  <system anchor='/remote_home'>

Users Section
-------------

Each ``user`` must be listed here. Several users will e.g. enable you to attach a head tracker to adapt stereoscopic rendering to different points of view inside the virtual environment.

The ``behavior`` `redundant section <#redundant-sections>`_ can define the ``default_position`` (``0.0, 0.0, 0.0`` by default) or the ``eye_separation`` (6 centimeters by default) of the user.

.. code:: xml

  <!-- users section with default values -->
  <users>
    <behavior eye_separation='0.06'>
      <default_position>0.0, 0.0, 0.0</default_position>
    </behavior>
    <user name="user A" />
  </users>


Computers Section
-----------------

We must describe how each rendering node (computer) works: each computer can have a specific configuration to run blenderplayer (paths, environment variables ...).
However, most of the time, all computers are equivalent. Redundant section is useful!

Computer itself must have a ``name`` and a ``hostname``. The name will be used by the screen.

.. code:: xml

  <computers>
    <system>
      . . . <!-- computers global information -->
    </system>
    <computer name='front computer' hostname='front.fqdn'>
      <system>
        . . . <!-- front computer specific information -->
      </system>
    </computer>
    <computer name='left computer' hostname='left.fqdn' />
  </computers>

System Section
==============

The ``system`` redundant section defines many things:

.. code:: xml

  <system root='C:\\program\\BlenderVR' anchor='U:\\blender_files'>
    <login remote_command="ssh `self._attributs_inheritance['hostname']`"/>
      <daemon>
        <environment>SystemRoot=C:\\Windows</environment>
      </daemon>
      <blenderplayer executable='C:\\blenderCave\\blender\\v2.70a\\blenderplayer.exe'>
        <environment>PYTHONPATH=C:\\Python33\\Lib;</environment>
      </blenderplayer>
    </system>

The ``root`` parameter specifies the root path of BlenderVR (where resides the ``BlenderVR`` python script, the ``modules`` folder, etc.). By default, it is set to BlenderVR root path on the console computer.
However, due to `not homogeneous paths between nodes <#anchor>`_, you may have to define it for each system.

See `Anchor <#anchor>`_ to know the purpose of anchor parameter.

Library Path Sub-Section
========================

Plugins often relies on external libraries. If the library is not bundled in the ``blenderplayer`` python folder, the library folder can be specified with the ``library`` element.
If any library is defined in a system section, they all must be defined.

In the example below both OSC and VRPN library folders are specified for the OSX system, while the Linux stations shared the same system as defined in the top of the ``computers`` section.

.. code:: xml

  <computers>
    <system>
      <library path="/usr/local/lib/vrpn/" />
      <library path="/usr/local/lib/osc/" />
    </system>
    <computer name='OSX station' hostname='mac'>
      <system>
        <library path="/User/dev/vrpn/build/python/" />
        <library path="/User/dev/osc/lib/" />
      </system>
    </computer>
    <computer name='Linux station A' hostname='linux_a' />
    <computer name='Linux station B' hostname='linux_b' />
  </computers>

Login Sub-Section
=================

This section explains how to connect console and hosts computers.

.. code:: xml

  <login remote_command="ssh me@host" python="/usr/bin/python3"/>

or

.. code:: xml

  <login remote_command="psexec -d \\host" python="C:\\python33\\python.exe"/>


* **remote_command** specifies the command, from the computer running the console to connect to the remote host.
* **python** contains the path and the name of the python3 executable.

Generally, we use redundant system section with code execution to create this section (see example of the redundant section upper).

Daemon Sub-Section
==================

The daemon sub-section explains how to run the `daemon <#daemon>`_ (now that we know how to connect to the remote computer).

.. code:: xml

  <daemon transmit='True'>
    <environment>SystemRoot=C:\\Windows</environment>
  </daemon>

* **transmit** parameter specifies if the daemon must transmit the environment variables to blenderplayer while it runs it.
* **environment** sub-section adds some specific environment variable to the daemon.


.. note::
  On Windows, you must at least, set the ``SystemRoot`` variable to points towards the path of your Windows installation (generally: ``C:\\Windows``)

Blenderplayer Sub-Section
=========================

This section defines how to run ``blenderplayer``.

.. code:: xml

  <blenderplayer executable='C:\\BlenderVR\\blender\\v2.74\\blenderplayer.exe'>
    <environment>PYTHONPATH=C:\\Python33\\Lib;C:\\Python33\\DLLs;C:\\Python33\\Lib\\site-packages</environment>
  </blenderplayer>

* The **executable** parameter contains the path and the binary name of patched version of blenderplayer.
* The **environment** sub-sections allows you to add specific environment variables for blenderplayer. You can add ``PYTHONPATH`` environment to specify paths for optional modules (such as for VRPN).

Screens Section
---------------

The screen is the unit of rendering: there is a bijection between screen and instance of ``blenderplayer``. Each screen has a ``name`` and a ``computer`` (actually the name of the computer section, above).

.. code:: xml

  <screens>
    <display>
      . . . <!-- screens global information -->
    </display>
    <screen name='front screen' computer='front computer'>
      <display>
        . . . <!-- front screen specific information -->
      </display>
      <wall>
        . . .
      </wall>
    </screen>
    <screen name='left screen' computer='left computer'>
  </screens>

The ``display`` `redundant section <#redundant-sections>`_ defines several things:

* **options** passed as argument to ``blenderplayer`` (for instance, ``-f -s hwpageflip`` to request a stereoscopic full screen ``blenderplayer`` window).
* **environment** to pass specific environment variables to ``blenderplayer``.
* **graphic_buffer** to associate:
* ``buffer`` (``mono`` = no stereo, ``left`` graphic buffer or ``right`` graphic buffer,
* ``user`` (as given inside ``users`` section),
* ``eye`` of the user (``left``, ``middle`` or ``right``).
* **viewport** to reduce the screen (useful if you have occlusion).

.. code:: xml

  <display options='-w 400 400'>
    <viewport>420, 0, 1500, 1080</viewport>
    <environment>DISPLAY=:0.0</environment>
    <graphic_buffer buffer='mono' user='user A' eye='middle'/>
  </display>

Each screen must have one sub-section ``wall`` or ``hmd``.

Wall or HMD differs in the way they manage the projection. Wall screens are fixed in the real world but HMD screen are attached to head of the user, moving along.

Both require a screen definition: three corners (top right, top left and bottom right):

.. code:: xml

  <wall> <!-- or <hmd> -->
    <corner name="topRightCorner">1.0, 1.0, -1.0</corner>
    <corner name="topLeftCorner">-1.0, 1.0, -1.0</corner>
    <corner name="bottomRightCorner">1.0, -1.0, -1.0</corner>
  </wall> <!-- or /<hmd> -->

For Wall, the screens are defined in `vehicle <../architecture/vehicle.html>`_ reference frame. For HMD, the screens are defined in the reference frame of head tracker.

Sample Configuration File
-------------------------

This sample configuration file can be used for a cave with three vertical square (2m x 2m) screens (left, front and right) plus a console computer with a single windowed screen.

.. code:: xml

    <?xml version="1.0"?>
    <BlenderVR>

      <starter anchor='/tmp/console' blender='/usr/local/blender/2.74/bin/blender'>
          <config name='console'>console screen</config>
          <config name='virtual environment'>console screen, front screen, left screen, right screen</config>
      </starter>

      <users>
        <user name='user A' />
      </users>

      <!-- Here, we define the console parameters -->
      <computers>
        <computer name='console computer' hostname='console.fqdn'/>
      </computers>
      <screens>
        <screen name='console screen' computer='console computer'>
          <display options='-w 600 600'>
      <environment>DISPLAY=:0.0</environment>
      <graphic_buffer user='user A'/>
          </display>
          <wall>
      <corner name='topRightCorner'>1.0, 1.0, -1.0</corner>
      <corner name='topLeftCorner'>-1.0, 1.0, -1.0</corner>
      <corner name='bottomRightCorner'>1.0, -1.0, -1.0</corner>
          </wall>
        </screen>
      </screens>

      <computers>
        <system root='/usr/local/blender/vr/1.0' anchor='/tmp/node'>
          <login remote_command="ssh `self._attributs_inheritance['hostname']`" python='/usr/local/blender/2.74/dependencies/bin/python3.3'/>
          <daemon transmit='True'>
      <environment>PATH=/usr/bin:/bin</environment>
          </daemon>
          <blenderplayer executable='/usr/local/blender/2.74/bin/blenderplayer' />
        </system>
        <computer name='front computer' hostname='front.fqdn' />
        <computer name='right computer' hostname='right.fqdn' />
        <computer name='left computer' hostname='left.fqdn' />
      </computers>
      <screens>
        <display options='-f -s hwpageflip'>
          <environment>DISPLAY=:0.0</environment>
          <graphic_buffer buffer='left' user='user A' eye='left'/>
          <graphic_buffer buffer='right' user='user A' eye='right'/>
        </display>
        <screen name='front screen' computer='front computer'>
          <wall>
      <corner name='topRightCorner'>1.0, 1.0, -1.0</corner>
      <corner name='topLeftCorner'>-1.0, 1.0, -1.0</corner>
      <corner name='bottomRightCorner'>1.0, -1.0, -1.0</corner>
          </wall>
        </screen>
        <screen name='left screen' computer='left computer'>
          <wall>
      <corner name='topRightCorner'>-1.0, 1.0, -1.0</corner>
      <corner name='topLeftCorner'>-1.0, 1.0, 1.0</corner>
      <corner name='bottomRightCorner'>-1.0, -1.0, -1.0</corner>
          </wall>
        </screen>
        <screen name='right screen' computer='right computer'>
          <wall>
      <corner name='topRightCorner'>1.0, 1.0, 1.0</corner>
      <corner name='topLeftCorner'>1.0, 1.0, -1.0</corner>
      <corner name='bottomRightCorner'>1.0, -1.0, 1.0</corner>
          </wall>
        </screen>
      </screens>

      <plugins>
        <vrpn>
          <floor x='0.0'/>
          <tracker device='GTK' host='localhost'>
      <transformation>
        <post_translation z='-1.6'/>
        <post_rotation x='1.0' y='1.0' z='1.0' angle="`-2*math.pi/3`"/>
        <pre_rotation x='1.0' y='1.0' z='1.0' angle="`2*math.pi/3`"/>
      </transformation>
      <sensor id='0' processor_method='user_position' users='user A'/>
      <sensor id='1' processor_method='tracker_1'/>
      <sensor id='2' processor_method='tracker_2'/>
      <sensor id='3' processor_method='tracker_3'/>
          </tracker>
          <analog device='GTK' host='localhost' processor_method='movements'/>
          <button device='GTK' host='localhost' processor_method='buttons'/>
        </vrpn>
      </plugins>
    </BlenderVR>

