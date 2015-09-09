=================================
Install for BlenderVR Development
=================================

This guide walks you over the basic steps of setting up a development environment for BlenderVR.

.. note ::
  For casual BlenderVR users, please refer to the `Install BlenderVR <installation-manual.html>`_ page.

The install is the same as described in `Install BlenderVR <installation-manual.html>`_ but for:

* git clone of the BlenderVR repository, to freely modify and eventually commit your modifications.
* svn/git clone of the BlenderVR samples, to eventually add your own demo scenes to the BlenderVR samples repository
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

BlenderVR requires a vanilla Blender 2.75 or newer.

If you ever need to modify and rebuild Blender for further customizations, please consult the `Blender's official documentation <http://wiki.blender.org/index.php/Dev:Doc/Building_Blender>`_.

Else, download the sources provided in `Acquiring Blender <installation-manual.html#acquiring-blender>`_.


Acquiring BlenderVR
-------------------

To download the latest BlenderVR git version (master HEAD):

.. code-block:: bash

  $ git clone https://github.com/BlenderVR/source.git
  $ cd source
  $ git submodule update --init --recursive --remote

.. note::
  In old versions of git (1.6x, 1.7x) the --remote option doesn't exist and thus should be left out

Download Samples Scenes
-----------------------

Regarding BlenderVR samples, Git is not a good system to work on binary files, so it's recommended to use the SVN protocol to interact with the samples repository instead:

.. code-block:: bash

  $ cd $INSTALL_DIR
  $ svn checkout https://github.com/BlenderVR/samples/trunk samples

where $INSTALL_DIR is the root BlenderVR folder (see the `Install BlenderVR <installation-manual.html#folder-structure>`_ page for more details).

Alternatively, to fetch an individual sample folder, you can use:

.. code-block:: bash

  $ svn checkout https://github.com/BlenderVR/samples/trunk/basic/basic

Alternatively if you want to access the repository via GIT you can do:

.. code-block:: bash

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

see `Quick Setup and Running <installation-manual.html#quick-setup>`_ in the Install BlenderVR Section.
