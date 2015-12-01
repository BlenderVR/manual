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

**PySide compilation fails and returns: ``[ 83%] Building CXX object libshiboken/CMakeFiles/libshiboken.dir/shibokenbuffer.cpp.o
Linking CXX shared library libshiboken.cpython-34m.so``**

Python was built without using ./configure option '--enable-shared' and the default is 'disabled'. The PySide build needs a python shared object (``python.X.x.so``) shared library and not a static (``.a``) library.

Error: Python executable not finding libpython shared library
-------------------------------------------------------------

**Python run fails and returns: ``error while loading shared libraries: libpythonX.x.so: cannot open shared object file: No such file or directory``**

See this `thread <http://stackoverflow.com/questions/7880454/python-executable-not-finding-libpython-shared-library>`_.


FAQ - BlenderVR Run
===================

Error: Invalid Blender path
---------------------------

**The main BlenderVR console displays ``Error: invalid blender path (<path-to-blender-binary>) (line 1 of <path-to-.xml-configuration-file>)``**

Check execution permissions on blender and blenderplayer executables (chmod).

Error: Python permission denied
-------------------------------

**PermissionError: [Errno 13] Permission denied: 'path-to-blender-folder/python/lib/python3.4/encodings/__init__.py'**

Check execution permissions on python files (path-to-blender-folder/python and path-to-blender-folder/scripts (chmod).

Error: Using VRPN library crashes Blenderpayer
----------------------------------------------

**No log, the Blenderplayer simply crashes every time BlenderVR starts**

Try to compile Blender setting the ``WITH_PYTHON_FRAMEWORK`` option to ``ON`.


