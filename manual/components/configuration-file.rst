==================
Configuration File
==================

The BlenderVR XML configuration file is loaded by the `console <../architecture/run-modes.html#console>`_ to get the architecture related information to run BlenderVR and send it to each `virtual environment <../architecture/run-modes.html#virtual-environment>`_ rendering node.

.. note::
  For a comprehensive overview of the file specification access its `architecture documentation <../architecture/configuration-file.html>`__.

Document Sections
-----------------
  * `Operating System Disclaimer`_
  * `Desktop Basic`_
  * `Desktop Networked`_
  * `Desktop Oculus DK2`_
  * `Dual Oculus DK2`_
  * `CAVE`_ (soon)
  * `Video Wall`_ (soon)
  * `SMARTI-2 Video Corner`_ (soon)


Operating System Disclaimer
---------------------------

To avoid redudancy and unsynced and outdated documents the instructions to all supported operating system are condensed together in this page.

In order to use any of the example configuration files in this page you need to first modify it according to the platform of each of your machines.

  * `Windows`_
  * `Mac`_
  * `Linux`_

Windows
=======

All samples in this page were written for Windows. All that is required to change is the corresponding path of blender, your system and the blenderplayer executable.

``TODO`` snippets of a sample, and the changed snippets to adapt for a specific computer.


Mac
===

All samples in this page were written for Windows. There are sections that are not needed for Mac, besides you need to change the corresponding paths of your system.

``TODO`` snippets of a sample, and the changed snippets to adapt for a specific computer.


Linux
=====

All samples in this page were written for Windows. There are sections that are slightly different for Linux. Besides you need to change the corresponding paths of your system.


``TODO`` snippets of a sample, and the changed snippets to adapt for a specific computer.


Desktop Basic
-------------

This is a very basic configuration file. There is only one computer and one user defined, and there are three screens:

  1. **Fullscreen**: plays the ``.blend`` file in fullscreen.
  2. **Console**: plays the ``.blend`` file in a small window.
  3. **Split**: plays the ``.blend`` file in two small windows, side-by-side, completing each other.

.. code:: xml

    <?xml version="1.0"?>
    <blendervr>

      <starter blender='C:/BlenderVR/blender/blender.exe'>
        <config name='Fullscreen'>fullscreen</config>
        <config name='Console'>console</config>
        <config name='Split'>console half left, console half right</config>
      </starter>

      <users>
        <user name="user A"/>
      </users>

      <computers>
        <system>
          <daemon transmit='True'>
            <environment>SystemRoot=C:/Windows</environment>
          </daemon>
          <blenderplayer executable='C:/BlenderVR/blender/blenderplayer.exe' />
        </system>
        <computer name='Any' hostname='*' />
      </computers>

      <screens>
        <screen name="fullscreen" computer="Any">
          <display options="-f">
            <graphic_buffer buffer="mono" user='user A' eye="middle"/>
          </display>
          <wall>
            <corner name="topRightCorner">1.0, 1.0, -1.0</corner>
            <corner name="topLeftCorner">-1.0, 1.0, -1.0</corner>
            <corner name="bottomRightCorner">1.0, -1.0, -1.0</corner>
          </wall>
        </screen>

        <screen name="console" computer="Any">
          <display options="-w 400 400">
            <graphic_buffer buffer="mono" user='user A' eye="middle"/>
          </display>
          <wall>
            <corner name="topRightCorner">1.0, 1.0, -1.0</corner>
            <corner name="topLeftCorner">-1.0, 1.0, -1.0</corner>
            <corner name="bottomRightCorner">1.0, -1.0, -1.0</corner>
          </wall>
        </screen>

        <screen name="console half left" computer="Any">
          <display options="-w 400 400 200 300">
            <graphic_buffer user='user A'/>
          </display>
          <wall>
            <corner name="topRightCorner">0.0, 1.0, -1.0</corner>
            <corner name="topLeftCorner">-1.0, 1.0, -1.0</corner>
            <corner name="bottomRightCorner">0.0, -1.0, -1.0</corner>
          </wall>
        </screen>

        <screen name="console half right" computer="Any">
          <display options="-w 400 400 600 300">
            <graphic_buffer user='user A'/>
          </display>
          <wall>
            <corner name="topRightCorner">1.0, 1.0, -1.0</corner>
            <corner name="topLeftCorner">0.0, 1.0, -1.0</corner>
            <corner name="bottomRightCorner">1.0, -1.0, -1.0</corner>
          </wall>
        </screen>

      </screens>

      <plugins>
      </plugins>

    </blendervr>


Desktop Networked
-----------------

This is an extension of the `Desktop Basic`_ with basic network functionality. There are two computers (the master and the slave) and either is tied to a user.
The screens are analog to the previous ones:

  1. **Fullscreen Dual**: plays the ``.blend`` file in fullscreen in both computers.
  2. **Fullscreen Left / Right**: plays the ``.blend`` file in fullscreen in either computer.
  3. **Console Dual**: plays the ``.blend`` file in a small window in both computers.
  4. **Console Left / Right**: plays the ``.blend`` file in a small window in either computer.

It's important to make sure the master computer can connect to the slave and to itself using the specified ``ssh`` command.
Also, don't understimate the console screens, they are great for debugging.


.. code:: xml

    <?xml version="1.0"?>
    <blendervr>

      <starter blender='C:/BlenderVR/blender/blender.exe' anchor='C:/BlenderVR/samples'>
        <config name='Fullscreen Dual'>full left, full right</config>
        <config name='Fullscreen Left'>full left</config>
        <config name='Fullscreen Right'>full right</config>
        <config name='Console Dual'>console left, console right</config>
        <config name='Console Left'>console left</config>
        <config name='Console Right'>console right</config>
      </starter>

      <users>
        <user name="user A"/>
        <user name="user B"/>
      </users>

      <computers>

        <computer name='Left' hostname='192.168.0.1'>
          <system root='C:/BlenderVR/blender-vr' anchor='C:/BlenderVR/samples'>

            <daemon transmit='True'>
              <environment>SystemRoot=C:/Windows</environment>
            </daemon>

            <blenderplayer executable='C:/BlenderVR/blender/blenderplayer.exe' />
            <login remote_command="ssh master@192.168.0.1" python="C:/Python3.4/Python.exe" />
          </system>
        </computer>

        <computer name='Right' hostname='192.168.0.2'>
          <system root='Z:/BlenderVR/blender-vr' anchor='Z:/BlenderVR/samples'>

            <daemon transmit='True'>
              <environment>SystemRoot=C:/Windows</environment>
            </daemon>

            <blenderplayer executable='Z:/BlenderVR/blender/belnderplayer.exe'/>
            <login remote_command="ssh slave@192.168.0.2" python="D:/MyPython/Python.exe" />
          </system>
        </computer>

      </computers>

      <screens>

        <screen name="console left" computer="Left">
          <display options="-w 720 450 720 450">
            <graphic_buffer buffer="mono" user='user A' eye="middle"/>
          </display>
          <wall>
            <corner name="topRightCorner">2.16, 1.35, -1.0</corner>
            <corner name="topLeftCorner">-2.16, 1.35, -1.0</corner>
            <corner name="bottomRightCorner">2.16, -1.35, -1.0</corner>
          </wall>
        </screen>

        <screen name="console right" computer="Right">
          <display options="-w 720 450 720 450">
            <graphic_buffer buffer="mono" user='user B' eye="middle"/>
          </display>
          <wall>
            <corner name="topRightCorner">2.16, 1.35, -1.0</corner>
            <corner name="topLeftCorner">-2.16, 1.35, -1.0</corner>
            <corner name="bottomRightCorner">2.16, -1.35, -1.0</corner>
          </wall>
        </screen>

        <screen name="full left" computer="Left">
          <display options="-w 720 900 720 900">
            <graphic_buffer user='user A'/>
          </display>
          <wall>
            <corner name="topRightCorner">1.0, 1.0, -1.0</corner>
            <corner name="topLeftCorner">0.0, 1.0, -1.0</corner>
            <corner name="bottomRightCorner">1.0, -1.0, -1.0</corner>
          </wall>
        </screen>

        <screen name="full right" computer="Right">
          <display options="-w 720 900 0 900">
            <graphic_buffer user='user B'/>
          </display>
          <wall>
            <corner name="topRightCorner">0.0, 1.0, -1.0</corner>
            <corner name="topLeftCorner">-1.0, 1.0, -1.0</corner>
            <corner name="bottomRightCorner">0.0, -1.0, -1.0</corner>
          </wall>
        </screen>

      </screens>

      <plugins>
      </plugins>

    </blendervr>

Desktop Oculus DK2
------------------
.. note::

  In order to use the Oculus DK2 you need to run a server separately.
  More on the `sample files <https://github.com/BlenderVR/samples/tree/master/advanced-examples/oculus-rift-dk2>`__


This configuration has three screens - the main one to be used for deployment, and two others used for debugging and testing:

  1. **Oculus DK2 Fullscreen**: plays the ``.blend`` file in fullscreen in Oculus DK2 mode.
  2. **Oculus DK2 Debug**: plays the ``.blend`` file in a small window in Oculus DK2 mode.
  3. **Console**: plays the ``.blend`` file in a small window in the computer.

Besides that we now define the Oculus DK2 library path to be loaded in the system, as well as the plugin users.

A computer can control only a single Oculus, for a multiple Oculus installation you need networked computers as explained in the `Dual Oculus DK2`_ example.


.. code:: xml

    <?xml version="1.0"?>
    <blendervr>

      <starter blender='C:/BlenderVR/blender/blender.exe'>
        <config name='Oculus DK2 Fullscreen'>oculus dk2 full</config>
        <config name='Oculus DK2 Debug'>oculus dk2 debug</config>
        <config name='Console'>console</config>
      </starter>

      <users>
        <user name="user A"/>
      </users>

      <computers>

        <system>
          <daemon transmit='True'>
            <environment>SystemRoot=C:/Windows</environment>
          </daemon>
          <blenderplayer executable='C:/BlenderVR/blender/blenderplayer.exe' />

          <library path="C:/BlenderVR/venv/lib/python3.4/site-packages" />
          <library path="C:/BlenderVR/venv/lib/python3.4/site-packages/websocket_client-0.18.0-py3.4.egg-info" />

        </system>
        <computer name='Any' hostname='*' />

      </computers>

      <screens>

        <screen name="oculus dk2 full" computer="Any">
          <display options="-f -s sidebyside">
            <graphic_buffer buffer="left" user='user A' eye="left"/>
            <graphic_buffer buffer="right" user='user A' eye="right"/>
          </display>
          <hmd model="oculus_dk2">
            <left>
              <corner name="topRightCorner">1.0, 1.0, -1.0</corner>
              <corner name="topLeftCorner">-1.0, 1.0, -1.0</corner>
              <corner name="bottomRightCorner">1.0, -1.0, -1.0</corner>
            </left>
            <right>
              <corner name="topRightCorner">1.0, 1.0, -1.0</corner>
              <corner name="topLeftCorner">-1.0, 1.0, -1.0</corner>
              <corner name="bottomRightCorner">1.0, -1.0, -1.0</corner>
            </right>
          </hmd>
        </screen>

        <screen name="oculus dk2 debug" computer="Any">
            <display options="-w 720 450 720 450 -s sidebyside">
            <graphic_buffer buffer="left" user='user A' eye="left"/>
            <graphic_buffer buffer="right" user='user A' eye="right"/>
          </display>
          <hmd model="oculus_dk2">
            <left>
              <corner name="topRightCorner">1.0, 1.0, -1.0</corner>
              <corner name="topLeftCorner">-1.0, 1.0, -1.0</corner>
              <corner name="bottomRightCorner">1.0, -1.0, -1.0</corner>
            </left>
            <right>
              <corner name="topRightCorner">1.0, 1.0, -1.0</corner>
              <corner name="topLeftCorner">-1.0, 1.0, -1.0</corner>
              <corner name="bottomRightCorner">1.0, -1.0, -1.0</corner>
            </right>
          </hmd>
        </screen>

        <screen name="console" computer="Any">
          <display options="-w 400 400">
            <graphic_buffer buffer="mono" user='user A' eye="middle"/>
          </display>
          <wall>
            <corner name="topRightCorner">1.0, 1.0, -1.0</corner>
            <corner name="topLeftCorner">-1.0, 1.0, -1.0</corner>
            <corner name="bottomRightCorner">1.0, -1.0, -1.0</corner>
          </wall>
        </screen>

      </screens>

      <plugins>

        <oculus_dk2>
          <user host="127.0.0.1" viewer='user A' computer='Any' processor_method="user_position" />
        </oculus_dk2>

      </plugins>
    </blendervr>

Dual Oculus DK2
---------------
This is a mix of the `Desktop Networked`_ with the `Desktop Oculus DK2`_ examples.
We now have a server which is running in Mac, while the client is in Windows.

Each computer has an Oculus DK2 device connected to it. And each device controls a ``user`` point of view. We skipped the debug and console configurations in this example, but they can be copied from the previous ones.

It's important to make sure the master computer can connect to the slave and to itself using the specified ``ssh`` command.

.. note::
  The same configuration file can be used by both computers by changing only the ``starter`` section for each corresponding master station.

.. code:: xml

    <?xml version="1.0"?>
    <blendervr>
      <starter blender='/Users/MYUSER/BlenderVR/blender/blender.app/Contents/MacOS/blender' hostname='192.168.0.1' anchor='/Users/MYUSER/BlenderVR/blender-vr/samples'>
        <config name='Oculus DK2 Dual1 Dual'>oculus dk2 left, oculus dk2 right</config>
      </starter>

      <users>
        <user name="user A"/>
        <user name="user B"/>
      </users>

      <computers>

        <computer name='Left' hostname='192.168.0.1'>
            <system root='/Users/MYUSER/BlenderVR/blender-vr' anchor='/Users/MYUSER/BlenderVR/samples'>
                <blenderplayer executable='/Users/MYUSER/BlenderVR/blender/blenderplayer.app/Contents/MacOS/blenderplayer'/>
                <login remote_command="ssh MYUSER@192.168.0.1" python="/Users/MYUSER/BlenderVR/venv/bin/python3.4"/>
                <library path="/Users/MYUSER/BlenderVR/venv/lib/python3.4/site-packages" />
                <library path="/Users/MYUSER/BlenderVR/venv/lib/python3.4/site-packages/websocket_client-0.18.0-py3.4.egg-info" />
            </system>
        </computer>

        <computer name='Right' hostname='192.168.0.2'>
          <system root='C:/BlenderVR/blender-vr' anchor='C:/BlenderVR/samples'>
            <daemon transmit='True'>
              <environment>SystemRoot=C:/Windows</environment>
            </daemon>
            <blenderplayer executable='C:/BlenderVR/blender/blenderplayer.exe' />
            <login remote_command="ssh slave@192.168.0.2" python="C:/Python3.4/Python.exe" />
            <library path="C:/BlenderVR/venv/lib/python3.4/site-packages" />
            <library path="C:/BlenderVR/venv/lib/python3.4/site-packages/websocket_client-0.18.0-py3.4.egg-info" />

          </system>
        </computer>

      </computers>

      <screens>

        <screen name="oculus dk2 left" computer="Left">
          <display options="-f -s sidebyside">
            <graphic_buffer buffer="left" user='user A' eye="left"/>
            <graphic_buffer buffer="right" user='user A' eye="right"/>
          </display>
          <hmd model="oculus_dk2">
            <left>
              <corner name="topRightCorner">1.0, 1.0, -1.0</corner>
              <corner name="topLeftCorner">-1.0, 1.0, -1.0</corner>
              <corner name="bottomRightCorner">1.0, -1.0, -1.0</corner>
            </left>
            <right>
              <corner name="topRightCorner">1.0, 1.0, -1.0</corner>
              <corner name="topLeftCorner">-1.0, 1.0, -1.0</corner>
              <corner name="bottomRightCorner">1.0, -1.0, -1.0</corner>
            </right>
          </hmd>
        </screen>

        <screen name="oculus dk2 right" computer="Right">
          <display options="-f -s sidebyside">
            <environment>DISPLAY=:0.0</environment>
            <graphic_buffer buffer="left" user='user B' eye="left"/>
            <graphic_buffer buffer="right" user='user B' eye="right"/>
          </display>
          <hmd model="oculus_dk2">
            <left>
              <corner name="topRightCorner">1.0, 1.0, -1.0</corner>
              <corner name="topLeftCorner">-1.0, 1.0, -1.0</corner>
              <corner name="bottomRightCorner">1.0, -1.0, -1.0</corner>
            </left>
            <right>
              <corner name="topRightCorner">1.0, 1.0, -1.0</corner>
              <corner name="topLeftCorner">-1.0, 1.0, -1.0</corner>
              <corner name="bottomRightCorner">1.0, -1.0, -1.0</corner>
            </right>
          </hmd>
        </screen>

      </screens>

      <plugins>

        <oculus_dk2>
          <user host="192.168.0.1" viewer='user A' computer='Left' />
          <user host="192.168.0.2" viewer='user B' computer='Right' />
        </oculus_dk2>

      </plugins>
    </blendervr>

CAVE
----
.. note::
  Coming Soon

Video Wall
----------
.. note::
  Coming Soon

SMARTI-2 Video Corner
---------------------
.. note::
  Coming Soon
