===============================
Frequently Asked Questions
===============================

FAQ - BlenderVR Install
=======================

FAQ - BlenderVR Run
===================

.. contents::
  :local:
  :backlinks: none
  :depth: 1

Error: Invalid Blender path
---------------------------

**The main BlenderVR console displays ``Error: invalid blender path (<path-to-blender-binary>) (line 1 of <path-to-.xml-configuration-file>)``**

check permissions of blender and blenderplayer executables (chmod).

Error: Python permission denied
-------------------------------

**PermissionError: [Errno 13] Permission denied: 'path-to-blender-folder/python/lib/python3.4/encodings/__init__.py'**

check permissions of python files (path-to-blender-folder/python and path-to-blender-folder/scripts (chmod).
