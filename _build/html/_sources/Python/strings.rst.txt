=======
Strings
=======

.. contents:: :local:

**Create** string
=================

.. code-block:: python
    
    s = str()
    
**Concatenate**
===============

.. code-block:: python
    
    s1 = str("hello ")
    s2 = str("world")
    print(s1 + s2)
    
**Format**
==========

.. code-block:: python
    
    my_string = "My name is {0} {1} and I'm {2} years old.".format(first_name, name, age)
    
.. code-block:: python
    
    my_string = "My name is {fn} {n} and I'm {a} years old.".format(fn=first_name, n=name, a=age)

.. code-block:: python
    
    my_string = "My name is %s %s and I'm %i years old." % (first_name, name, age)
    
**Join** strings with a defined separator : ``join()``
======================================================

.. code-block:: python
    
    numList = ['1', '2', '3', '4']
    seperator = ' - '
    print(seperator.join(numList))
    
-> output :

    .. code-block:: none
        
        1 - 2 - 3 - 4
        
With a list of separators :
        
.. code-block:: python

    s1 = 'abc'
    s2 = '123'
    
    #Each character of s2 is concatenated to the front of s1
    print('s1.join(s2):', s1.join(s2))
    
    #Each character of s1 is concatenated to the front of s2
    print('s2.join(s1):', s2.join(s1))  
    
-> output :

    .. code-block:: none
        
        s1.join(s2): 1abc2abc3
        s2.join(s1): a123b123c
        
Create a **list** from a string, split a a sepecific **separator** : ``split()``
================================================================================

.. code-block:: python

    ma_chaine = "Bonjour à tous"
    ma_chaine.split(" ")
    # -> ['Bonjour', 'à', 'tous']
    
**Lower case**
==============

.. code-block:: python
    
    s.lower()
    
**Upper case**
==============

.. code-block:: python
    
    s.upper()
    
**Capitalize** first character
==============================

.. code-block:: python
    
    s.capitalize()

