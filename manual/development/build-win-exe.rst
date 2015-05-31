========================
Build Windows Executable
========================

This section is intented for developers willing to create a BlenderVR.exe (Windows executable) based on BlenderVR source code.

.. note::
  For casual users, please download the current `BlenderVR WebInstall Excecutable <ftp://blendervrdownloads:blendervr@echange.limsi.fr/BlenderVR_setup_Win64_Webinstall.exe>`_ or the `BlenderVR Standalone Excecutable <ftp://blendervrdownloads:blendervr@echange.limsi.fr/BlenderVR_setup_Win64.exe>`_ and refer to the `Installation Guide <../installation/installation.html>`_.

This installer was build using `Inno Setup <http://www.jrsoftware.org/>`_ (v5.5.5).
Please download the `BlenderVR Installer source code <ftp://blendervrdownloads:blendervr@echange.limsi.fr/BlenderVR_W7_Installer/Installer_BlenderVR_W7_dev.zip>`_ before reading the next section.

Document Sections:
------------------
  * `Installer Folder Structure`_
  * `Build BlenderVR Windows Installer`_

Installer Folder Structure
--------------------------

+ Installer internal directories

``//deps/``
*BlenderVR dependencies*

``//logo/``
*BlenderVR logos*

``//macros/``
*BlenderVR macros (post install & run)*

``//output/``
*Output directory after installer compilation*

``//doc/``
*Installer documentation*

+ BlenderVR base folders

(copy of the `Folder Structure <installation.html#folder-structure>`_ suggested during BlenderVR `Installation <installation.html>`_)

``//source/``
*BlenderVR Source Code*

``//blender/``
*Blender Binaries*

``//samples/``
*BlenderVR Samples*

``//configuration files/``
*BlenderVR configuration files*


Build BlenderVR Windows Installer
---------------------------------

+ Build

Create .exe based on InnoSetup files:

``//blendervr_online_install.iss/``
*install using the internet*

``//blendervr_offline_install.iss/``
*install without using the internet (packed Qt, git repository, etc.)*

.. warning::
  Do not forget to define the working directory with
  #define MyBaseDir "\\...\sources-of-the-installer-Installer_BlenderVR".


+ Updates

Replace BlenderVR base folders by current `BlenderVR Git <https://github.com/BlenderVR>`_ versions.

.. note::
  To add new folders and files you need to perform specific modifications in the .iss files.
