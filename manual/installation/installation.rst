==================
Installation Guide
==================

In order to install Blender-VR you need this guide.

.. note ::

  If you need the full development setup make sure to follow the `Development Environment <development>`_ guide.


Document Sections
-----------------
* `Folders Structure`_
* `Requirements`_
* `Quick Setup`_
* `Acquiring Blender`_
* `Getting Samples`_
* `Running`_


Folders Structure
-----------------

After all the downloads and installations you should end up with the following folder structure. This is a recommendation, and it will be used as reference along this manual.e

``//blender-vr/``
*Blender-VR Source Code*

``//blender/``
*Blender Binaries*

``//samples/``
*Blender-VR Samples*

``//venv/``
*Python Virtual Environment*


Requirements
------------
.. _requirements:

Install those packages or make sure you have them in your system.

All Time Mandatory
******************

* `Python <http://www.python.org/>`_
* `Blender-VR Sources <http://www.dalaifelinto.com/ftp/blender-vr/blender-vr.zip>`_ (download and unzip in the top folder)
* `Blender Binary <Acquiring Blender>`_ (download and uncompress in the top folder)


Required for Interface Development
**********************************

*At this moment those packages are always required, but the plans are to make them optional.*

* `PIP <https://pip.pypa.io/en/latest/installing.html>`_
* `QT 4.8 <https://qt-project.org/downloads#qt-lib/>`_


Quick Setup
-----------

Type the following commands in your terminal. If you are in Windows we recommend you to use Power Shell or similar.

.. code-block:: bash

  $ cd $INSTALL_DIR
  $ pip install virtualenv
  $ virtualenv venv
  $ source venv/bin/activate
  $ pip requirements -r blender-vr/requirements.txt
  $ pyside_postinstall.py -install


Acquiring Blender
-----------------

*At this moment there is no patched Linux or Windows builds available. In those cases after you download and uncompress Blender you need to rename the folder to* **blender** *for consistency.*

Blender-VR requires a modified version of `Blender <http://www.blender.org>`_. You can download a pre-compiled version of Blender for your system

* `Mac OSX 64 bit: Blender 2.72 Patched <http://www.dalaifelinto.com/ftp/blender-vr/blender/blender-272-patch-osx.zip>`_. [1]_
* `Windows 32 bit: Blender 2.72 Official <http://mirror.cs.umn.edu/blender.org/release/Blender2.72/blender-2.72b-windows32.zip>`_. [2]_
* `Windows 64 bit: Blender 2.72 Official <http://mirror.cs.umn.edu/blender.org/release/Blender2.72/blender-2.72b-windows64.zip>`_. [2]_
* `Linux 32 bit: *Blender 2.72 Official <http://mirror.cs.umn.edu/blender.org/release/Blender2.72/blender-2.72b-linux-glibc211-i686.tar.bz2>`_. [3]_
* `Linux 64 bit: *Blender 2.72 Official <http://mirror.cs.umn.edu/blender.org/release/Blender2.72/blender-2.72b-linux-glibc211-x86_64.tar.bz2>`_. [3]_

.. [1] Requires Mac OSX 10.6+
.. [2] Compatible with Windows 8, 7, Vista. If Blender reports an error on startup, please install the `Visual C++ 2013 Redistributable Package <http://www.microsoft.com/en-us/download/details.aspx?id=40784>`_.
.. [3] Requires glibc 2.11. Suits most recent GNU/Linux distributions


Getting Samples
---------------

Before getting started is recommended to look at the available samples.
The basic sample should help testing if everything was installed correctly, as well as testing the configuration file of your VR lab.
The other samples are to be used as reference to develop other VR projects.

* Download `All Samples <https://github.com/BlenderVR/samples/archive/master.zip>`_

You can also download an individual sample folder. For that you will need `SVN <http://subversion.apache.org/>`_ or `SVN Tortoise <http://tortoisesvn.net/>`_ (Windows only).
To check which samples are available visit the `Samples Repository <https://github.com/BlenderVR/samples.git>`_.


.. code-block:: bash

  $ cd $INSTALL_DIR
  $ mkdir -p samples
  $ svn checkout https://github.com/BlenderVR/samples/trunk/simple samples/

(Or simply `svn checkout` the required sample with SVN Tortoise).


Running
-------

Type the following commands in your terminal. If you are in Windows we recommend you to use Power Shell or similar.

.. code-block:: bash

  $ cd $INSTALL_DIR
  $ source venv/bin/activate
  $ ./blender-vr/blenderVR

You should now see a window popping up. Congratulations your installation was a success. Once you are done running Blender-VR you can end the virtual environment:

.. code-block:: bash

  $ deactivate

For your convenience it is recommended to create a bash script to help re-launching the Blender-VR environment.

