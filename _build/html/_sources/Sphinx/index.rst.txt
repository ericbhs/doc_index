Welcome to Sphinx Cheat Sheet
=============================

Add code extract :
==================

.. code-block:: none

    .. code-block:: <language>
        
        Code must be one indent more that the code-block tag, and
        separated by a blank line.
        
        This very text is an example. Replace <language> by "none"
        to avoid color highlighting.

.. _my-reference-label:
        
Add in-line code extract
========================
    .. code-block:: none
    
        ``this will show as an in-line code extract``
        This won't.
        
Add a local content table of content
====================================

.. code-block:: none

    .. contents:: :local:
        
Add an image
============

.. code-block:: none
    
    .. image:: image.png
    
Add an image with link to see it full size
==========================================

.. code-block:: none

    .. image:: _static/image.png
        :target: _static/image.png
        
Add a simple table
==================

.. code-block:: none

    =========================== ===========================
    Test title 1                Test Title 2    
    =========================== ===========================
    Row 1 Col 1                 Row 1 Col 2
    Row 2 Col 1                 Row 2 Col 2
    Row 3 Col 1                 Row 3 Col 2
    =========================== ===========================
    
Add a numbered list
===================

.. code-block:: none

    #. Something
    #. Something else
    #. Another thing
    #. etc...
    

Add a bullet list
=================

.. code-block:: none

    * Something
    * Something else
    * Another thing
    * etc...
    
External link
=============


.. code-block:: none
    
    `Link text <link URL>`_
    
example : `CNN <http://cnn.com>`_

Cross-referencing arbitrary locations inside the document
==========================================================

Place the following code on top of the target :

.. code-block:: none

    .. _my-reference-label:

The use ``:ref:`` like this :

.. code-block:: none

    ...bla bla bla, see :ref:`my-reference-label`.
    
Example : ...bla bla bla, see :ref:`my-reference-label`.