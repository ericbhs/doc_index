================
Lists and tuples
================

.. contents:: :local:

**tuple** = list that can't be modified*

**Create** an empty list
========================
    
.. code-block:: python
    
    my_list = []
    
**Create** a populated list
===========================
    
.. code-block:: python
    
    my_list = [1, 3.5, "une chaine", []]

**Access** a list element
=========================
    
.. code-block:: python

    elt = my_list[3]
    
**Insert** an element at the end of the list : ``append``
=========================================================
    
.. code-block:: python

    my_list.append(56)      # Add 56 at the end of the list

**Insert** an element at a specific index : ``insert``
======================================================

.. code-block:: python

    my_list = ['a', 'b', 'd', 'e']
    my_list.insert(2, 'c')         # -> ['a', 'b', 'c', 'd', 'e']
    
**Remove** an element from a list
=================================

    * By **index** : keyword ``del``
    
    .. code-block:: python
    
        my_list = [-5, -2, 1, 4, 7, 10]
        del my_list[0]
        # -> [-2, 1, 4, 7, 10]
        del ma_liste[2]
        # -> [-2, 1, 7, 10]

    * By **content** : method ``remove``

    .. code-block:: python

        my_list = [31, 32, 33, 34, 35]
        my_list.remove(32)
        # -> [31, 33, 34, 35] (removes the element that contains '32')
        
**Clear** list
==============

.. code-block:: python

    my_list.clear()

Returns a list of coupled values containing the list index with its associated element : ``enumerate()``
========================================================================================================

    Example :

    .. code-block:: python

        ma_liste = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h']
        
        for i, elt in enumerate(ma_liste):
            print("À l'indice", i, "se trouve", elt)
            
    -> output :
          
        .. code-block:: none

            À l'indice 0 se trouve a.
            À l'indice 1 se trouve b.
            À l'indice 2 se trouve c.
            À l'indice 3 se trouve d.
            À l'indice 4 se trouve e.
            À l'indice 5 se trouve f.
            À l'indice 6 se trouve g.
            À l'indice 7 se trouve h.

Use lists as **function parameters**
====================================

Place a ``*`` in front of the parameter which takes a list, or use ``...`` :

.. code-block:: python  

    def fonction(*parametres):
        ...
    
    def print(*values, sep=' ', end='\n', file=sys.stdout):
        ...
    # Is equivalent to :
    def print(value, ..., sep=' ', end='\n', file=sys.stdout)
        ...
        
List Comprehensions : a **concise** way to create lists
=======================================================

It's a concise way to create a list. For example :

.. code-block:: python

    new_list = []
    for i in old_list:
        if filter(i):
            new_list.append(expressions(i))
            
... is equivalent to :

.. code-block:: python

    new_list = [expression(i) for i in old_list if filter(i)]
    
    