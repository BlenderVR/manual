=======================================
Install for Future blenderVR Developers
=======================================

This guide walks you over the basic steps of setting up a development environment for blenderVR.

.. note ::
  For casual blenderVR users, please refer to the `Install blenderVR <installation.html>`_ page.

The install is the same than described in `Install blenderVR <installation.html>`_ but for:

* git clone of the blenderVR repository, to freely modify and eventually commit your modifications.
* svn/git clone of the blenderVR samples, to eventually add your own demo scenes to the blenderVR samples repository
* manual compilation of Blender, if you need to modify its source code.

Most of the time you won't need to modify and rebuild Blender, so those instructions are specified separately.

Document Sections
-----------------
* `Acquiring Blender`_
* `Acquiring BlenderVR`_
* `Download Samples Scenes`_
* `Requirements`_
* `Quick Setup and Running`_


Acquiring Blender
-----------------

Blender-VR requires a vanilla Blender 2.74 or newer.

If you ever need to modify and rebuild Blender for further customizations, please consult the `Blender's official documentation <http://wiki.blender.org/index.php/Dev:Doc/Building_Blender>`_.

Else, download the sources provided in `Acquiring Blender <installation.html#acquiring-blender>`_.


Acquiring BlenderVR
-------------------

To download the latest blenderVR git version (master HEAD):

.. code-block:: bash

  $ git clone https://github.com/BlenderVR/blender-vr.git

If you do not intend to modify blenderVR source code, simply download the `Blender-VR Sources <https://github.com/BlenderVR/blender-vr/archive/v1.0.zip>`_ zipfile.

Download Samples Scenes
----------------------

Regarding blenderVR samples, Git is not a good system to work on binary files, so it's recommended to use the SVN protocol to interact with the samples repository instead:

.. code-block:: bash

  $ cd $INSTALL_DIR
  $ svn checkout https://github.com/BlenderVR/samples


Or for an individual sample folder:

.. code-block:: bash

  $ svn checkout https://github.com/BlenderVR/samples/trunk/simple


Alternatively if you want to access the repository via GIT you can do::

  $ cd $INSTALL_DIR
  $ git clone https://github.com/BlenderVR/samples.git


Requirements
------------
.. _requirements:

Install those packages or make sure you have them in your system.

All Time Mandatory
******************

* `GIT <http://git-scm.com/>`_
* `Python 3.4 <https://www.python.org/downloads/release/python-343/>`_


Required for Interface Development
**********************************

*At this moment the following packages are always required, but the plans are to make them optional.*

* `PIP <https://pip.pypa.io/en/latest/installing.html>`_
* `QT 4.8 <http://download.qt.io/archive/qt/4.8/4.8.6/>`_

Quick Setup and Running
-----------------------

see `Quick Setup and Running <installation.html#quick-setup>`_ in the Install blenderVR Section.
