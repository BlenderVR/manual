=============
Documentation
=============

There are two parts of the project that are covered by this documents:
Source Code API [1]_ and the User Manual [2]_.

Even though those parts are independently hosted and maintained, they
are both built on the same framework.

.. [1] `code <https://github.com/BlenderVR/blender-vr>`__,  `compiled <http://blender-vr.readthedocs.org>`__
.. [2] `code <https://github.com/BlenderVR/manual>`__,  `compiled <http://blender-vr-manual.readthedocs.org>`__

Document Sections:
------------------
  * `Language and Format`_
  * `Requirements`_
  * `Installation`_
  * `How to Build`_
  * `How to Edit`_

Language and Format
-------------------

The documentation is written in `reSt <http://docutils.sourceforge.net/rst.html>`_ (reStructuredText).
This is a markup language that is compiled to generate html (or pdf).

..
  ReST

Requirements
------------

Before working in the documentation you need to install all the requirements and the main repository
from the `installation <../installation/installation.html>`_ guide.

Quick Setup
-----------

Type the following commands in your terminal. If you are developing in Windows we recommend you to use Power Shell or similar.

.. code-block:: bash

  $ cd $INSTALL_DIR
  $ git clone https://github.com/BlenderVR/manual.git
  $ source venv/bin/activate
  $ pip requirements -r blender-vr/docs/requirements.txt
  $ pip requirements -r manual/requirements.txt
  $ deactivate

How to Build
------------

.. note::
  While this generates a local copy of the latest documentation, the Blender-VR project is
  hooked up with the `ReadTheDocs <http://readthedocs.org>`_ system. This auto-compiles the documentation and
  make it available online everytime something is committed in the system.

User Manual
===========

.. code-block:: bash

  $ cd $INSTALL_DIR
  $ source venv/bin/activate
  $ cd manual
  $ make
  $ deactivate

This will output the documentation to ``$INSTALL_DIR/manual/html``.

Souce Code API
==============

.. code-block:: bash

  $ cd $INSTALL_DIR
  $ source venv/bin/activate
  $ cd blender-vr/docs/
  $ make
  $ deactivate

This will output the documentation to ``$INSTALL_DIR/blender-vr/docs/html``.


How to Edit
-----------
The ``.rst`` files are simple plain text files that can be edited with any text editing tool.
Once the file is ready it can be previewed with ``make``, and eventually pushed back to
the repository.

There are tools to preview the ``.rst`` file during the editing, but they are platform specific.
In the Linux and OSX environment one can use `InstantRST <https://github.com/Rykka/InstantRst>`_
with *vim*. Sublime (for OSX) seems to have some tools as well.

* `ReST Quick Reference <http://docutils.sourceforge.net/docs/user/rst/quickref.html>`_
