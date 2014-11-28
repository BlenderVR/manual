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

This quick setup assume you have the requirements installed, and doesn't provide the explanation of what you are doing.

.. code-block:: bash

  $ cd $INSTALL_DIR
  $ pip install virtualenv
  $ virtualenv venv
  $ source venv/bin/activate
  $ pip requirements -r requirements.txt
  $ pyside_postinstall.py -install
  $ git clone https://github.com/BlenderVR/blender-vr.git


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

Blender-VR requires a modified version of `Blender <http://www.blender.org>`_. You can download a pre-compiled version of Blender for your system


Most of the time you won't need to modify and rebuild Blender, so those instructions are specified separately.
