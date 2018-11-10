=======
Sorting
=======

.. contents:: :local:

``sort()`` : destructive sort
=============================

Method which sorts the object

.. code-block:: python

    my_list = [2, 6, 3, 12, 0, 44, 51, -6]
    my_list.sort()
    print(my_list)
    # -> [-6, 0, 2, 3, 6, 12, 44, 51]

``sorted()`` : non-destructive sort
===================================

Method which returns a sorted copy of the object

.. code-block:: python

    my_list = [2, 6, 3, 12, 0, 44, 51, -6]
    sorted_list = my_list.sorted()
    print(my_list)
    # -> [2, 6, 3, 12, 0, 44, 51, -6] (my_list isn't affected)
    print(sorted_list)
    # -> [-6, 0, 2, 3, 6, 12, 44, 51]
    
``key`` argument : choose the sorting criterion
===============================================

Use with ``lambda`` functions
-----------------------------

The ``key`` argument is a function, which can be defined as a ``lambda`` function :

.. code-block:: python

    etudiants = [
        Etudiant("Clément", 14, 16),
        Etudiant("Charles", 12, 15),
        Etudiant("Oriane", 14, 18),
        Etudiant("Thomas", 11, 12),
        Etudiant("Damien", 12, 15),
    ]
    
    sorted(etudiants, key=lambda etudiant: etudiant.moyenne)
    
Note : that function means : take ``etudiant`` and returns ``etudiant.moyenne``
    
Output :

.. code-block:: none

    [
        <Étudiant Thomas (âge=11, moyenne=12)>,
        <Étudiant Charles (âge=12, moyenne=15)>,
        <Étudiant Damien (âge=12, moyenne=15)>,
        <Étudiant Clément (âge=14, moyenne=16)>,
        <Étudiant Oriane (âge=14, moyenne=18)>
    ]
    
Use with ``itemgetter``
------------------------

Faster method than the one with lambdas, especially on a large amount of datas.

.. code-block:: python

    from operator import itemgetter
    sorted(etudiants, key=itemgetter(2))
    # is the same as :
    sorted(etudiants, key=lambda etudiant: etudiant[2])
    
Sort a list of objects with ``attrgetter``
==========================================

If we have a list of object as in this example :

.. code-block:: python

    class Etudiant:

        def __init__(self, prenom, age, moyenne):
            self.prenom = prenom
            self.age = age
            self.moyenne = moyenne

        def __repr__(self):
            return "<Étudiant {} (âge={}, moyenne={})>".format(
                    self.prenom, self.age, self.moyenne)

    etudiants = [
        Etudiant("Clément", 14, 16),
        Etudiant("Charles", 12, 15),
        Etudiant("Oriane", 14, 18),
        Etudiant("Thomas", 11, 12),
        Etudiant("Damien", 12, 15),
    ]

We can use ``attrgetter()`` to get a function that returns an attribute for the ``key`` argument of ``sort``/``sorted`` :

.. code-block:: python

    from operator import attrgetter
    sorted(etudiants, key=attrgetter("moyenne"))
    
Stability property
==================

This is the fact that the sorting methods do not modify the order of items which sorting criterion have the same value. This allows the use of chained sortings.

Sort according to multiple parameters
=====================================

Just provide multiple arguments to ``attrgetter``. In the following example, they will be first sorted by ``age``, then if multiple students have the same ``age`` they will be sorted by ``moyenne``.

The **most** important criterion must be called **first**.

.. code-block:: python

    >>> sorted(etudiants, key=attrgetter("age", "moyenne"))
    [
        <Étudiant Thomas (âge=11, moyenne=12)>,
        <Étudiant Charles (âge=12, moyenne=15)>,
        <Étudiant Damien (âge=12, moyenne=15)>,
        <Étudiant Clément (âge=14, moyenne=16)>,
        <Étudiant Oriane (âge=14, moyenne=18)>
    ]
    >>>
    
Chaining sortings
=================

To chain sortings, do multiple calls of ``sort``/``sorted``. The **least** important criterion must be called **first**.