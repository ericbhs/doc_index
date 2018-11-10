=====================================
Welcome to Notepad++'s tips & tricks!
=====================================

.. contents:: :local:
   
Npp = Notepad++

Install NppExec to have a console in Notepad++
==============================================

Add Notepad++ Plugin manager
----------------------------

* Download it from https://github.com/bruderstein/nppPluginManager/releases (make sure 32/64bits version is correct compared to Npp installation)

* Copy ``PluginManager.dll`` in ``C:\Program Files\Notepad++\plugins``

* Copy ``gpup.exe`` in ``C:\Program Files\Notepad++\updater`` (updater)

* Restart Npp and run the plugin manager from "Plugin" menu

https://htmlpreview.github.io/?https://github.com/bruderstein/nppPluginManager/blob/master/doc/index.html#install

Add NppExec
-----------

-> get a console in Npp

* Install it from the Plugin Manager (package "NppExec")

* Show Console with menu "Plugin > NppExec > Show Console"

* Change the console font to a constant constant width one like "Courrier news" ("Plugin > NppExec > Change console font")

Create rules to get colors in NppExec console
=============================================

Hit ``Shift + F6`` to see the menu and define rules with wildcards (``*`` and so) :

.. image :: _static/colors.png
    :target: _static/colors.png

Run C/C++ code with NppExec
===========================

Install C/C++ compiler
----------------------

* Install MinGW 

* Run MinGW Installation manager and install "mingw32-gcc-g++" package

* Compiler executable should be located at ``C:\MinGW\bin``

* Add g++ to windows PATH

Launch compiler in NppExec
--------------------------

Hit F6 and add the following script, which compiles and executes the program if compilation succeeded :

.. code-block:: none
    
    npp_save

    cd "$(CURRENT_DIRECTORY)"

    g++ "$(FILE_NAME)" -o $(NAME_PART) -march=native -O3

    if $(EXITCODE) == 0  then
    $(NAME_PART).exe
    endif

Run Python scripts with Notepad++
=================================

Add the following NppExec script :

.. code-block:: none

    npp_save

    cd "$(CURRENT_DIRECTORY)"

    python "$(FULL_CURRENT_PATH)"
    
This only works if Python is in the Windows PATH.

Compile Sphinx documentation
============================

Add the following script in NppExec :

.. code-block:: none
    
    npp_save

    cd "$(CURRENT_DIRECTORY)"

    make html
    
Replace ``html`` by ``latex`` to build to Latex.

To open the generated html file in Firefox, add the followinf line at the end of the script :

.. code-block:: none

    C:\Program Files\Mozilla Firefox\firefox _build\html\$(NAME_PART).html

In case, replace ``C:\Program Files\Mozilla Firefox\firefox`` by the path to firefox.exe.


