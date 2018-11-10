===================
Variables scope
===================

.. contents:: :local:

Local variables
===============

When a variable is defined inside a function, it isn't accessible outside this function.

Example :

.. code-block:: python

    def foo():
        y = "local"

    foo()
    print(y)
    
Returns ``NameError: name 'y' is not defined``

Global variables
================

A global variable is created outside the function and declared as *global* inside the function with the ``global`` keyword :

.. code-block:: python

    x = "global"

    def foo():
        # make 'x' inside the function is the same as 'x' outside the function
        global x
        y = "local"
        x = x * 2
        print(x)
        print(y)
        
    foo()
    
However a variable initialized outside the funtion is accessible in "read" mode inside the function :

.. code-block:: python

    x = "global x"

    def foo():
        y = x
        print(y)
            
    foo()
    
This works as long as we do not write to ``x`` inside the function with ``x = ...``, which would define a new ``x`` local variable. To write, inside an function, to a variable defined outside a function, use the ``global`` keyword.

Objects scope
=============

Inside a function, one can call an object's method to modify it without declaring this object as ``global``.

Attributes changes can also be made without delaring the object ``global``

.. code-block:: python

    def ajouter(liste, valeur_a_ajouter):
        liste.append(valeur_a_ajouter)
        
    ma_liste=['a', 'e', 'i']
    
    ajouter(ma_liste, 'o')
    
    print(ma_liste)
    # returns : ['a', 'e', 'i', 'o']
    
References
==========

References copy
---------------

``object1 = object2`` doesn't create a copy of ``object1`` to a new object ``object2`` but only copies the reference.

Example :

.. code-block:: python

    list1 = [1,2,3]

    list2 = list1

    list1.append(4)

    print(list1)
    print(list2)
    
Returns :

.. code-block:: python
 
    [1, 2, 3, 4]
    [1, 2, 3, 4]
    
Which proves that ``list1`` and ``list2`` point to the same content

Content copy
------------

To make ``list2`` a separate copy of ``list1`` :

.. code-block:: python

    list1 = [1,2,3]

    list2 = list(list1)

    list1.append(4)

    print(list1)
    print(list2)
    
Returns :

.. code-block:: python
 
    [1, 2, 3, 4]
    [1, 2, 3]

``list1`` and ``list2`` point to a separate content.

Content comparison / Reference comparison
=========================================

.. code-block:: python

    ma_liste1 = [1, 2]
    ma_liste2 = [1, 2]

Content comparison :
--------------------

.. code-block:: python

    ma_liste1 == ma_liste2 # On compare le contenu des listes

Returns :

.. code-block:: python

    True

Reference comparison :
----------------------

.. code-block:: python

    ma_liste1 is ma_liste2 # On compare leur référence
    
Returns :

.. code-block:: python

    False
