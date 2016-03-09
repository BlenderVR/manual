===============================
Frequently Asked Questions
===============================

.. contents::
  :local:
  :backlinks: none
  :depth: 2

FAQ - BlenderVR Install
=======================

Error: Building PySide
----------------------

| **PySide compilation fails and returns:**
| `[ 83%] Building CXX object libshiboken/CMakeFiles/libshiboken.dir/shibokenbuffer.cpp.o, Linking CXX shared library libshiboken.cpython-34m.so`
|
| Python was built without using ``./configure`` option ``--enable-shared`` and the default is ``disabled``. The PySide build needs a python shared object (``python.X.x.so``) shared library and not a static (``.a``) library.
|
|

Error: Python executable not finding libpython shared library
-------------------------------------------------------------

| **Python run fails and returns:**
| `error while loading shared libraries: libpythonX.x.so: cannot open shared object file: No such file or directory`
|
| See this `thread <http://stackoverflow.com/questions/7880454/python-executable-not-finding-libpython-shared-library>`_.
|
|

FAQ - BlenderVR Run
===================

Error: Invalid Blender path
---------------------------

| **The main BlenderVR console displays:**
| `Error: invalid blender path (<path-to-blender-binary>) (line 1 of <path-to-.xml-configuration-file>)`
|
| Check execution permissions on blender and blenderplayer executables (chmod).
|
|

Error: Python permission denied
-------------------------------

| **The console displays:**
| `PermissionError: [Errno 13] Permission denied: 'path-to-blender-folder/python/lib/python3.4/encodings/__init__.py'`
|
| Check execution permissions on python files (path-to-blender-folder/python and path-to-blender-folder/scripts (chmod).
|
|

Error: Using VRPN library crashes Blenderpayer
----------------------------------------------

| **No log, the Blenderplayer simply crashes every time BlenderVR starts**
|
| Try to compile Blender setting the ``WITH_PYTHON_FRAMEWORK`` option to ``ON``.
|
|

Error: Cannot start daemon for screen <screenName>
--------------------------------------------------

| **One of BlenderVR screen consoles displays:**
| `Cannot start daemon for screen <screenName>`
|
| To run BlenderVR you need a password-less ssh access to all the computers defined in your configuration file, even if the only computer defined there is ``*`` or ``localhost``. See e.g. these threads for `Unix <http://www.thelinuxtips.com/2011/11/step-by-step-password-less-ssh-login/>`_ or `Windows <http://www.servermom.org/passwordless-ssh-login/1608>`_ architectures.
