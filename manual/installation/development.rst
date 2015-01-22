====================================
Development Environment Installation
====================================

This guide walks you over the basic steps of setting up a development environment for Blender-VR.

Most of the time you won't need to modify and rebuild Blender, so those instructions are specified separately.

Document Sections
-----------------
* `Folders Structure`_
* `Requirements`_
* `Quick Setup`_
* `Getting Samples`_
* `Acquiring Blender`_

Folders Structure
-----------------
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

* `GIT <http://git-scm.com/>`_
* `Python <http://www.python.org/>`_


Required for Interface Development
**********************************

*At this moment those packages are always required, but the plans are to make them optional.*

* `PIP <https://pip.pypa.io/en/latest/installing.html>`_
* `QT 4.8 <https://qt-project.org/downloads#qt-lib/>`_


Required for Blender development
********************************

*Many packages, listed separately.*

Quick Setup
-----------

Type the following commands in your terminal. If you are developing in Windows we recommend you to use Power Shell or similar.

.. code-block:: bash

  $ cd $INSTALL_DIR
  $ pip install virtualenv
  $ virtualenv venv
  $ source venv/bin/activate
  $ pyside_postinstall.py -install
  $ git clone https://github.com/BlenderVR/blender-vr.git
  $ pip requirements -r blender-vr/requirements.txt
  $ deactivate


Getting Samples
---------------

Git is not a good system to work on binary files, so it's recommended to use the SVN protocol to interact with this repository instead.

.. code-block:: bash

  $ cd $INSTALL_DIR
  $ svn checkout https://github.com/BlenderVR/samples


Or for an individual sample folder:

.. code-block:: bash

  $ svn checkout https://github.com/BlenderVR/samples/trunk/simple


Alternatively if you want to access the repository via GIT you can do::

  $ cd $INSTALL_DIR
  $ git clone https://github.com/BlenderVR/samples.git


Acquiring Blender
-----------------

Blender-VR requires a vanilla Blender 2.74 or newer.
If you ever need to modify and rebuild Blender for further customizations, please consult the `Blender's official documentation <http://wiki.blender.org/index.php/Dev:Doc/Building_Blender>`_. 

To download the Blender required to your platform check the `User Installation <installation.html#acquiring-blender>`_ guide.
