.. figure:: /images/os-logos.png
  :width: 100px
  :figwidth: 100px
  :align: right

==========================
Install BlenderVR (manual)
==========================

In order to install BlenderVR you need this guide.

.. figure:: /images/windows-logo.png
  :width: 40px
  :figwidth: 40px
  :align: right

.. tip::

  Windows "standard" (non-developpers) users are invited to download the BlenderVR Install Excecutable for Windows 7 *(though you are still advised to read through the following installation and how to use guides)*. See the `Install BlenderVR (automatic) <installation-executable.html>`_ page.

.. note ::

  If you need the full development setup make sure to follow the `Development Environment <development.html>`_ guide.

Document Sections
-----------------
* `Folder Structure`_
* `Acquiring Blender`_
* `Acquiring BlenderVR`_
* `Download Samples Scenes`_
* `Install Dependencies`_
* `Quick Setup`_
* `Running`_


Folder Structure
----------------

After all the downloads and installations you should end up with the following folder structure. This is a recommendation, and it will be used as reference along this manual (the directory holding these files is referred as $INSTALL_DIR in the next sections).

``//source/``
*BlenderVR Source Code*

``//blender/``
*Blender Binaries*

``//samples/``
*BlenderVR Samples*

``//venv/``
*Python Virtual Environment*

Acquiring Blender
-----------------

BlenderVR requires `Blender 2.75 <http://www.blender.org/download>`_ or newer.
Optionally you can use a patched version of Blender 2.74 available here for all the supported platforms.

* `Mac OSX 64 bit: Blender 2.74 Patched <ftp://blendervrdownloads:blendervr@ftp.limsi.fr/compiled/blender-2.74-a8adeeb-OSX-10.6-x86_64.zip>`_. [1]_
* `Windows 32 bit: Blender 2.74 Patched <ftp://blendervrdownloads:blendervr@ftp.limsi.fr/compiled/blender-2.74-a8adeeb-win32.zip>`_. [2]_
* `Windows 64 bit: Blender 2.74 Patched <ftp://blendervrdownloads:blendervr@ftp.limsi.fr/compiled/blender-2.74-a8adeeb-win64.zip>`_. [2]_
* `Linux 32 bit: Blender 2.74 Patched <ftp://blendervrdownloads:blendervr@ftp.limsi.fr/compiled/blender-2.74-a8adeeb-linux-glibc211-i686.tar.bz2>`_. [3]_
* `Linux 64 bit: Blender 2.74 Patched <ftp://blendervrdownloads:blendervr@ftp.limsi.fr/compiled/blender-2.74-a8adeeb-linux-glibc211-x86_64.tar.bz2>`_. [3]_

.. [1] Requires Mac OSX 10.6+
.. [2] Compatible with Windows 8, 7, Vista. If Blender reports an error on startup, please install the `Visual C++ 2013 Redistributable Package <http://www.microsoft.com/en-us/download/details.aspx?id=40784>`_.
.. [3] Requires glibc 2.11. Suits most recent GNU/Linux distributions

Acquiring BlenderVR
-------------------

* `BlenderVR Sources <https://github.com/BlenderVR/source/archive/v1.0.zip>`__ (download and unzip in the top folder, rename it **source**)
* `Oculus Library <https://github.com/BlenderVR/python-ovrsdk/archive/v1.0.zip>`__ (download and unzip it inside the **source/libs** folder, rename it **python-ovrsdk**)

Download Samples Scenes
-----------------------

Before getting started, you'll probably want to take a look at the available BlenderVR ".blend" sample scenes.

* Download `All Samples <https://github.com/BlenderVR/samples/archive/master.zip>`_

You can also download an individual sample folder. For that you will need `SVN <http://subversion.apache.org/>`_ or `SVN Tortoise <http://tortoisesvn.net/>`_ (Windows only).
To check which samples are available visit the `Samples Repository <https://github.com/BlenderVR/samples.git>`_.


.. code-block:: bash

  $ cd $INSTALL_DIR
  $ mkdir -p samples
  $ svn checkout https://github.com/BlenderVR/samples/trunk/basic/basic samples/

(Or simply `svn checkout` the required sample with SVN Tortoise).


Install Dependencies
--------------------

Install those packages or make sure you have them in your system.

All Time Mandatory
******************

* `Python 3.4 <https://www.python.org/downloads/release/python-343/>`_

*Future developments will make the following packages optional:*

* `QT 4.8 <http://download.qt.io/archive/qt/4.8/4.8.6/>`_
* `PIP <https://pip.pypa.io/en/latest/installing.html>`_ (the Python install should have installed pip, try to use it in the next Section before installing)

.. note::
  MacOS: open Qt.mpkg with mouse right click -> Open, to avoid popup window "can't install, non identified developer".


Quick Setup
-----------

Type the following commands in your terminal. If you are in Windows we recommend you to use `Power Shell <https://technet.microsoft.com/en-us/scriptcenter/default>`_ or similar.

On OSX/Linux:

.. code-block:: bash

  $ cd $INSTALL_DIR
  $ pip3 install virtualenv
  $ pyvenv venv
  $ source venv/bin/activate
  $ pip3 install -r source/requirements.txt

At that point, if the console does not show any trace of ``pyside_postinstall.py`` script execution, type in:

.. code-block:: bash

  $ python ./venv/bin/pyside_postinstall.py -install


.. note::
  MacOS: running these lines may popup window "download the command line developer tools", go for it.

  Linux: If the "pyvenv venv" command fails, you can try the command "pyvenv-3.4 venv".

  Linux: If pyvenv command fails due to mising ensurepip module, try `this script <https://gist.github.com/uranusjr/d03a49767c7c307be5ed>`_ .

On Windows:

.. code-block:: bash

  $ cd $INSTALL_DIR
  $ pip3 install virtualenv
  $ virtualenv venv
  $ .\venv\Scripts\activate
  $ pip3 install -r source\requirements.txt
  $ python3 .\venv\Scripts\pyside_postinstall.py -install
  $ python3 .\source\blendervr

You may have to add the path to the python binary, e.g.

.. code-block:: bash

  $ [Environment]::SetEnvironmentVariable("Path", "$env:Path;C:\Python34\;C:\Python34\Scripts\")

*(For PowerShell to automatically add this path at startup, add this line to a file named e.g. profile.ps1 that you'll place in your WindowsPowerShell directory)*

Running
-------

Type the following commands in your terminal. If you are in Windows we recommend you to use `Power Shell <https://technet.microsoft.com/en-us/scriptcenter/default>`_ or similar.

On OSX/Linux:

.. code-block:: bash

  $ cd $INSTALL_DIR
  $ source venv/bin/activate
  $ ./source/blendervr

On Windows:

.. code-block:: bash

  $ cd $INSTALL_DIR
  $ .\venv\Scripts\activate
  $ python3 .\source\blendervr

You should now see the BlenderVR window popping up (see figure below). Congratulations your installation was a success!

.. figure:: /images/user-interface-1.png
  :width: 600px
  :figwidth: 600px
  :align: center

Once you are done running BlenderVR you can end the virtual environment running the command:

.. code-block:: bash

  $ deactivate

For your convenience it is recommended to create a bash script to help re-launching the BlenderVR environment.

