==================
Configuration File
==================

The BlenderVR XML configuration file is loaded by the console to get the architecture related information to run BlenderVR and send it to each virtual environment rendering node (see `processor file templates <../components/processor-file.html>`_).

.. note::
  For a comprehensive overview of the file specification access its `architecture documentation <../architecture/configuration-file.html>`__.

.. note::
  Example configuration files can be found in the ``$INSTALL_DIR/source/configurations`` directory.

Document Sections
-----------------
  * `Operating System Disclaimer`_
  * `Desktop Basic`_
  * `Desktop Stereo 3D`_
  * `Desktop Networked`_
  * `Desktop Oculus DK2`_
  * `Dual Oculus DK2`_
  * `CAVE`_

..
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

In those examples we assume the BlenderVR files are in ``C:/BlenderVR/``.
So the source is in ``C:/BlenderVR/source/`` and the samples in ``C:/BlenderVR/samples/``.

Change the folders accordingly to your installation.




Mac
===

All samples in this page were written for Windows. There are sections that are not needed for Mac, besides you need to change the corresponding paths of your system.

The first thing that needs to be adapted is the filepaths.
The following are assorted examples of filepaths in Windows and Mac.

**Windows**:

.. code:: xml

  <starter blender='C:/BlenderVR/blender/blender.exe' anchor='C:/BlenderVR/samples'>
  <system root='C:/BlenderVR/source' anchor='C:/BlenderVR/samples'>
  <blenderplayer executable='C:/BlenderVR/blender/blenderplayer.exe' />
  <login remote_command="ssh windows_login@192.168.0.1" python="C:/Python3.4/Python.exe" />
  <library path="C:/BlenderVR/venv/lib/python3.4/site-packages" />

**Mac**:

.. code:: xml

  <starter blender='/Users/MYUSER/BlenderVR/blender/blender.app/Contents/MacOS/blender' anchor='/Users/MYUSER/BlenderVR/samples'>
  <system root='/Users/MYUSER/BlenderVR/source' anchor='/Users/MYUSER/BlenderVR/samples'>
  <blenderplayer executable='/Users/MYUSER/BlenderVR/blender/blenderplayer.app/Contents/MacOS/blenderplayer' />
  <login remote_command="ssh mac_login@192.168.0.1" python="/Users/MYUSER/BlenderVR/venv/bin/python3.4" />
  <library path="/Users/MYUSER/BlenderVR/venv/lib/python3.4/site-packages" />

Notice that in Mac the Blender binary is inside the bundle (blender.app), as well as the Blenderplayer (blenderplayer.app).
Also ``/Users/MYUSER/`` is to be replaced by the location of your BlenderVR installation.

The second thing is the environment XML element which is not required in Mac.
So the lines below are to be suppressed in the Mac configuration files.

.. code:: xml

            <daemon transmit='True'>
              <environment>SystemRoot=C:/Windows</environment>
            </daemon>

Linux
=====

All samples in this page were written for Windows. There are sections that are slightly different for Linux. Besides you need to change the corresponding paths of your system.


The first thing that needs to be adapted is the filepaths.
The following are assorted examples of filepaths in Windows and Linux.

**Windows**:

.. code:: xml

  <starter blender='C:/BlenderVR/blender/blender.exe' anchor='C:/BlenderVR/samples'>
  <system root='C:/BlenderVR/source' anchor='C:/BlenderVR/samples'>
  <blenderplayer executable='C:/BlenderVR/blender/blenderplayer.exe' />
  <login remote_command="ssh windows_login@192.168.0.1" python="C:/Python3.4/Python.exe" />
  <library path="C:/BlenderVR/venv/lib/python3.4/site-packages" />

**Linux**:

.. code:: xml

  <starter blender='/home/MYUSER/BlenderVR/blender/blender' anchor='/home/MYUSER/BlenderVR/samples'>
  <system root='/home/MYUSER/BlenderVR/source' anchor='/home/MYUSER/BlenderVR/samples'>
  <blenderplayer executable='/home/MYUSER/BlenderVR/blender/blenderplayer' />
  <login remote_command="ssh linux_login@192.168.0.1" python="/home/MYUSER/BlenderVR/venv/bin/python3.4"/>
  <library path="/home/MYUSER/BlenderVR/venv/lib/python3.4/site-packages" />

The location ``/home/MYUSER/`` is to be replaced by the location of your BlenderVR installation.

The second thing is the environment XML element which is not required in Linux.
So the lines below are to be suppressed in the Mac configuration files.

.. code:: xml

            <daemon transmit='True'>
              <environment>SystemRoot=C:/Windows</environment>
            </daemon>

Finally, Linux allows you to specify a unique ``<environment>DISPLAY=:0.0</environment>`` element to specify in which display a screen should run. For example:

.. code:: xml

    (...)
    <screen name="console" computer="Any">
      <display options="-w 400 400">
        <environment>DISPLAY=:0.0</environment>
        <graphic_buffer buffer="mono" user='user A' eye="middle"/>
      </display>
    (...)

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

Desktop Stereo 3D
-----------------

This is a very basic configuration file. There is only one computer and one user defined, and there are three screens:

  1. **Fullscreen 2D**: plays the ``.blend`` file in fullscreen without stereo 3d.
  2. **Stereo 3D - Side by Side**: plays the ``.blend`` file in a stereo 3d fullscreen in side by side mode.
  3. **Stereo 3D - Quadbuffer**: plays the ``.blend`` file in a stereo 3d fullscreen with shutter glasses.

The only differences between those three modes are the ``display`` options. A screen need as many ``display_buffer`` items as eyes being rendered.

Simply said, the stereo 3d screens will need the ``left`` and ``right`` buffers, while the 2d screen only needs the ``mono`` buffer.

.. note::
  For more advanced ``display_buffer`` arrangements check the `CAVE`_ example.

Apart from the display_buffers, the display ``options`` are considerably different between the screens.

  * **Fullscreen 2D**: ``<display options="-f 1920 1080">``
  * **Stereo 3D - Side by Side**: ``<display options="-f 1920 1080 -s sidebyside">``
  * **Stereo 3D - Quadbuffer**: ``<display options="-f 1920 1080 24 120 -s hwpageflip">``

Those options are passed straight as command-line arguments to the ``blenderplayer``.
For a comprehensive list of arguments run ``blenderplayer`` with the ``--help`` option.

For *Fullscreen 2D* all you need to do is to specify the fullscreen mode ``-f``, and the screen resolution.

For *Stereo 3D - Side by Side*, besides the above, you need to specify the stereo 3d mode, ``-s sidebyside``.

For *Stereo 3D - Quadbuffer* we specify the stereo 3d mode, ``-s hwpageflip``, and force the screen bits per pixel, ``24``,  and the frequency, ``120``.
This is the shuttering speed of the active shutter glasses.

You can't specify the frequency without defining the bits first.

.. note::
  In order to use the ``hwpageflip`` mode your graphic card must support ``Quadbuffer`` natively.

.. code:: xml

    <?xml version="1.0"?>
    <blendervr>

      <starter blender='C:/BlenderVR/blender/blender.exe'>
        <config name='Fullscreen 2D'>fullscreen</config>
        <config name='Stereo 3D - Side by Side'>sidebyside</config>
        <config name='Stereo 3D - Quadbuffer'>quadbuffer</config>
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
          <display options="-f 1920 1080">
            <graphic_buffer buffer="mono" user='user A' eye="middle"/>
          </display>
          <wall>
            <corner name="topRightCorner">1.0, 1.0, -1.0</corner>
            <corner name="topLeftCorner">-1.0, 1.0, -1.0</corner>
            <corner name="bottomRightCorner">1.0, -1.0, -1.0</corner>
          </wall>
        </screen>

        <screen name="sidebyside" computer="Any">
          <display options="-f 1920 1080 -s sidebyside">
            <graphic_buffer buffer="left" user='user A' eye="left" />
            <graphic_buffer buffer="right" user='user A' eye="right" />
          </display>
          <wall>
            <corner name="topRightCorner">1.0, 1.0, -1.0</corner>
            <corner name="topLeftCorner">-1.0, 1.0, -1.0</corner>
            <corner name="bottomRightCorner">1.0, -1.0, -1.0</corner>
          </wall>
        </screen>

        <screen name="quadbuffer" computer="Any">
          <display options="-f 1920 1080 24 120 -s hwpageflip">
            <graphic_buffer buffer="left" user='user A' eye="left" />
            <graphic_buffer buffer="right" user='user A' eye="right" />
          </display>
          <wall>
            <corner name="topRightCorner">1.0, 1.0, -1.0</corner>
            <corner name="topLeftCorner">-1.0, 1.0, -1.0</corner>
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
          <system root='C:/BlenderVR/source' anchor='C:/BlenderVR/samples'>

            <daemon transmit='True'>
              <environment>SystemRoot=C:/Windows</environment>
            </daemon>

            <blenderplayer executable='C:/BlenderVR/blender/blenderplayer.exe' />
            <login remote_command="ssh master@192.168.0.1" python="C:/Python3.4/Python.exe" />
          </system>
        </computer>

        <computer name='Right' hostname='192.168.0.2'>
          <system root='Z:/BlenderVR/source' anchor='Z:/BlenderVR/samples'>

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

This configuration is composed of three screens: the main one to be used for deployment, and two others used for debugging and testing:

  1. **Oculus DK2 Fullscreen**: plays the ``.blend`` file in fullscreen in Oculus DK2 mode.
  2. **Oculus DK2 Debug**: plays the ``.blend`` file in a small window in Oculus DK2 mode.
  3. **Console**: plays the ``.blend`` file in a small window in the computer.

Besides that, the configuration file example below now defines the Oculus DK2 plugin:

.. code:: xml

    <oculus_dk2>
      <user viewer='user A' computer='Any' processor_method="user_position" />
    </oculus_dk2>


with parameters such as ``viewer`` (which user is concerned) or ``processor_method`` (optional callback that processes oculus tracking data in the processor file, see `sample files <https://github.com/BlenderVR/samples/tree/master/plugin/hmd>`__ for example implementations).

A computer can control only a single Oculus, for a multiple Oculus installation you need networked computers as explained in the `Dual Oculus DK2`_ example.

.. note::

  If you experience a "non full-screen" with the ``fullscreen`` configuration proposed above, or can't drag the blenderplayer window to the Oculus screen, try to replace ``<display options="-f -s sidebyside">`` with ``<display options="-w 1920 1080 0 0 -s sidebyside">``.
  If it works, try changing the two last values (0 0) - corresponding to blenderplayer window left/top coordinate - to values that will position the blenderplayer window on the Oculus screen at BlenderVR start.

.. note::

  On Windows, the shortcut ``Shift + Windows + Left/Right`` enables you to switch the monitor on which is displayed the current window (even a fullscreen one).

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
          <user viewer='user A' computer='Any' processor_method="user_position" />
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
      <starter blender='/Users/MYUSER/BlenderVR/blender/blender.app/Contents/MacOS/blender' hostname='192.168.0.1' anchor='/Users/MYUSER/BlenderVR/samples'>
        <config name='Oculus DK2 Dual1 Dual'>oculus dk2 left, oculus dk2 right</config>
      </starter>

      <users>
        <user name="user A"/>
        <user name="user B"/>
      </users>

      <computers>

        <computer name='Left' hostname='192.168.0.1'>
            <system root='/Users/MYUSER/BlenderVR/source' anchor='/Users/MYUSER/BlenderVR/samples'>
                <blenderplayer executable='/Users/MYUSER/BlenderVR/blender/blenderplayer.app/Contents/MacOS/blenderplayer'/>
                <login remote_command="ssh MYUSER@192.168.0.1" python="/Users/MYUSER/BlenderVR/venv/bin/python3.4"/>
            </system>
        </computer>

        <computer name='Right' hostname='192.168.0.2'>
          <system root='C:/BlenderVR/source' anchor='C:/BlenderVR/samples'>
            <daemon transmit='True'>
              <environment>SystemRoot=C:/Windows</environment>
            </daemon>
            <blenderplayer executable='C:/BlenderVR/blender/blenderplayer.exe' />
            <login remote_command="ssh slave@192.168.0.2" python="C:/Python3.4/Python.exe" />
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
          <user viewer='user A' computer='Left' />
          <user viewer='user B' computer='Right' />
        </oculus_dk2>

      </plugins>
    </blendervr>

CAVE
----
This more advanced configuration has a few screens but two modes:

  1. **Console**: plays the ``.blend`` file in a small window in the current computer (for debugging).
  2. **CAVE**: plays the ``.blend`` file in a CAVE (floor, front, left and right screens).

This `CAVE <http://en.wikipedia.org/wiki/Cave_automatic_virtual_environment>`__ setup is focused on the Linux platform, but it can be adapted for other operating systems as well.
The head-tracking system is using the `VPRN Plugin <vrpn.html>`__ system.

The dimensions of this CAVE is 4.8m (width) x 3.0m (height) x 2.7m (depth) (i.e., x, y, z).

The parameters to define in the screens walls, are all relate to the head reference frame looking forward.
Meaning, the screen walls corners coordinates are as width, height, depth (i.e., x, z, y).
Also the origin of the system is at 0.0 x 0.0 x 1.60 in this particular case.

This also impacts the settings of the head-tracking system (in the plugins vrpn tracker element).
In this example we are converting the data from the VPRN server so that the translation is also in the head reference frame.

Finally, for an ortostereoscopy experience, the ``.blend`` file should mimics this - The scene camera initial position should be at 1.6 height looking forward (rotation: 90, 0, 0).

.. note::

  The head-tracker device expects the processor method ``user_position``.
  Since this is also the name of the fallback routine, it doesn't need to be implemented in the `Processor File <processor-file.html>`__.

.. code:: xml

    <?xml version="1.0"?>
    <blendervr>

      <starter blender="/mnt/softwares/blendervr/blender/blender">
        <config name="Console">console</config>
        <config name="CAVE">floor, front, left, right</config>
      </starter>

      <!-- Users -->
      <users>
        <user name="user A"/>
      </users>

      <!-- System -->
      <system>
        <blenderplayer executable="/mnt/softwares/code/64/tools/blender-git/compile/bin/blenderplayer">
          <environment>PATH=/mnt/softwares/code/64/bin:/mnt/softwares/bin.sh:/usr/bin:/bin</environment>
          <environment>PYTHONPATH=/mnt/softwares/code/64/python3.2mu</environment>
          <environment>HOME=`os.environ["HOME"]`</environment>
        </blenderplayer>
      </system>

      <!-- Computers -->
      <computers>
        <system>
          <login remote_command="ssh `self._attributs_inheritance["hostname"]`"/>
        </system>

        <computer name="Control" hostname="localhost" />
        <computer name="Node 1" hostname="node-`cluster.name`-1" />
        <computer name="Node 2" hostname="node-`cluster.name`-2" />
        <computer name="Node 3" hostname="node-`cluster.name`-3" />
        <computer name="Node 4" hostname="node-`cluster.name`-4" />
      </computers>

      <!-- Screens -->
      <screens>
        <screen name="console" computer="Control">
          <display options="-w 400 400">
            <graphic_buffer buffer="mono" user="user A" eye="middle"/>
          </display>

          <wall>
            <corner name="topRightCorner">    1.0,  1.0, -1.0</corner>
            <corner name="topLeftCorner">    -1.0,  1.0, -1.0</corner>
            <corner name="bottomRightCorner"> 1.0, -1.0, -1.0</corner>
          </wall>
        </screen>

        <display options="-f -s hwpageflip">
          <graphic_buffer buffer="left" user="user A" eye="left"/>
          <graphic_buffer buffer="right" user="user A" eye="right"/>
          <environment>DISPLAY=:0.0</environment>
        </display>

        <screen name="floor" computer="Node 1">
          <wall>
            <corner name="topRightCorner">    2.4, -1.6, -1.35</corner>
            <corner name="topLeftCorner">    -2.4, -1.6, -1.35</corner>
            <corner name="bottomRightCorner"> 2.4, -1.6,  1.35</corner>
          </wall>
        </screen>

        <screen name="front" computer="Node 2">
          <wall>
            <corner name="topRightCorner">    2.4,  1.4, -1.35</corner>
            <corner name="topLeftCorner">    -2.4,  1.4, -1.35</corner>
            <corner name="bottomRightCorner"> 2.4, -1.6, -1.35</corner>
          </wall>
        </screen>

        <screen name="left" computer="Node 3">
          <display><viewport>420, 0, 1500, 1080</viewport></display>
          <wall>
            <corner name="topRightCorner">   -2.4,  1.4, -1.35</corner>
            <corner name="topLeftCorner">    -2.4,  1.4,  1.35</corner>
            <corner name="bottomRightCorner">-2.4, -1.6, -1.35</corner>
          </wall>
        </screen>

        <screen name="right" computer="Node 4">
          <display><viewport>420, 0, 1500, 1080</viewport></display>
          <wall>
            <corner name="topRightCorner">    2.4,  1.4,  1.35</corner>
            <corner name="topLeftCorner">     2.4,  1.4, -1.35</corner>
            <corner name="bottomRightCorner"> 2.4, -1.6,  1.35</corner>
          </wall>
        </screen>

      </screens>

      <!-- Plugins -->
      <plugins>

        <vrpn>
          <tracker device="HeadCap" host="VPRN_SERVER">
            <transformation>
              <post_translation z="-1.6" />
              <pre_rotation x="1.0" y="1.0" z="1.0" angle="`2.0 * math.pi / 3.0`" />
              <post_rotation x="1.0" y="1.0" z="1.0" angle="`-2.0 * math.pi / 3.0`" />
            </transformation>
            <sensor id="0" processor_method="user_position" users="user A" />
          </tracker>
        </vrpn>

      </plugins>

    </blendervr>


..
  Video Wall
  ----------
  .. note::
    Coming Soon

  SMARTI-2 Video Corner
  ---------------------
  .. note::
    Coming Soon
