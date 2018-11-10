=====
Files
=====

.. contents:: :local:

Change the current directory
============================

* Absolute path :

.. code-block:: python

    import os
    os.chdir("C:/tests python")
    
* Relative path :
    
.. code-block:: python

    import os
    os.chdir("../../relative_dir")

**Open** a file
===============

.. code-block:: python

    mon_fichier = open("fichier.txt", "r")

Modes

======= =========================================================================================
'r'     Read
'w'     Write (file is created if it doesn't exist, **file with the same name is erased**)
'a'     Apend (file is created if it doesn't exist)
't'     Option : open as text. Ex : ``open("file.txt", "rt")``
'b'     Option : open as binary. Ex : ``open("file.txt", "rb")``
======= =========================================================================================

**Close** a file
================

.. code-block:: python

    mon_fichier.close()
    
**Read** the whole content of a file
====================================

.. code-block:: python

    mon_fichier = open("fichier.txt", "r")
    mon_fichier.read()
    
**Write** to a file
===================

* Write a **string**

.. code-block:: python

    mon_fichier = open("fichier.txt", "w")
    mon_fichier.write("Premier test d'écriture dans un fichier via Python")
    
* Write **other data types**

    **TODO** see ``os`` package for more infos
    
**Safer way** to use files with the ``with`` keyword
====================================================

-> automatically closes the file when the operation is finished

.. code-block:: python

    with open('fichier.txt', 'r') as mon_fichier:
        texte = mon_fichier.read()
        
**Save objects** to files with ``pickle``
=========================================

* Use the ``Pickler`` class
* ``dump`` method to save the object
* Write to the file in binary 'b' mode

.. code-block:: python

    import pickle

    score = {
        "joueur 1":    5,
        "joueur 2":   35,
        "joueur 3":   20,
        "joueur 4":    2,
    }

    with open('donnees', 'wb') as fichier:
        mon_pickler = pickle.Pickler(fichier)
        mon_pickler.dump(score)
        
**Retrieve objects** from files with ``pickle``
=============================================== 

* Use the ``Unpickler`` class
* ``load`` method to load the object from the file
* Open the file in binary 'b' mode

.. code-block:: python

    import pickle
    
    with open('donnees', 'rb') as fichier:
        mon_depickler = pickle.Unpickler(fichier)
        score_recupere = mon_depickler.load()

        