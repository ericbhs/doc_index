=======
Boucles
=======

.. contents:: :local:

Boucle ``while``
----------------

.. code-block:: python
    
    while i < 10:
        print("i =", i)

Avec ``break`` et ``continue`` :

.. code-block:: python

    while True:
        do_something()
        if condition:  
            break
        else:
            continue
        
Boucle ``for``
--------------

Equivalent to ``foreach`` in C#

.. code-block:: python
    
    myList = [1, 2, 3]
    
    for i in myList:
        print(i)
        
Boucle ``for`` "C-Style"
------------------------

* With ``range()``

.. code-block:: python

    list = [0, 5, 4, 3, 5]
    
    # for (int i=0; i<length(list); i++)
    for i in range(len(list)):
        print("list element", i, "is :", list[i])
        
.. code-block:: python

    list = [0, 5, 4, 3, 5]
    
    # for (int i=a; i>n; i+=s)
    for i in range(a, n, s):
        print("list element", i, "is :", list[i])
        
* With ``Enumerate()`` (returns a list of coupled values containing the list index with its associated element)

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