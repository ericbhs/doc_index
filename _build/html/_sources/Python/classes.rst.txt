=======
Classes
=======

.. contents:: :local:

Simple class with methods 
=========================

Class declaration
-----------------

.. code-block:: python

    class Parrot:

        # class attribute
        species = "bird"

        # instance attribute
        def __init__(self, name, age):
            self.name = name
            self.age = age
            
        # instance method
        def sing(self, song):
            return "%s sings %s" % (self.name, song)
        
        # instance method
        def dance(self):
            return "%s is now dancing" % (self.name)

Object use
----------
     
.. code-block:: python
     
    # instantiate the Parrot class
    blu = Parrot("Blu", 10)
    woo = Parrot("Woo", 15)

    # access the class attributes (same for any instance)
    print("Blu is a", blu.__class__.species)
    print("Woo is also a", woo.__class__.species)

    # access the instance attributes (different for every instance)
    print(blu.name, "is", blu.age, "years old")
    print(woo.name, "is", woo.age, "years old")
    
    # call our instance methods
    print(blu.sing("'Happy'"))
    print(blu.dance())
    
Output : 

.. code-block:: none

    Blu is a bird
    Woo is also a bird
    Blu is 10 years old
    Woo is 15 years old
    Blu sings 'Happy'
    Blu is now dancing

Inheritance
===========

.. code-block:: python

    # parent class
    class Bird:
        
        def __init__(self):
            print("Bird is ready")

        def whoisThis(self):
            print("Bird")

        def swim(self):
            print("Swim faster")

    # child class
    class Penguin(Bird):

        def __init__(self):
            # call super() function
            super().__init__()
            print("Penguin is ready")

        def whoisThis(self):
            print("Penguin")

        def run(self):
            print("Run faster")

    peggy = Penguin()
    peggy.whoisThis()
    peggy.swim()
    peggy.run()
    
Output :

.. code-block:: none

    Bird is ready
    Penguin is ready
    Penguin
    Swim faster
    Run faster
    
Encapsulation
=============

Private variables
-----------------

-> add double underscore prefix ``__``

.. code-block:: python

    class Computer:

        def __init__(self):
            self.__maxprice = 900

        def sell(self):
            print("Selling Price: {}".format(self.__maxprice))

        def setMaxPrice(self, price):
            self.__maxprice = price

    c = Computer()
    c.sell()

    # change the price
    c.__maxprice = 1000
    c.sell()    # direct change of __maxprice has no effect

    # using setter function
    c.setMaxPrice(1000)
    c.sell()    # change through the setter has an effect
    
Output :

.. code-block:: none

    Selling Price: 900
    Selling Price: 900
    Selling Price: 1000
    
**Note** : when a name has two leading underscores (``__``), Python interpreter actually changes its name. For example, the name of the method ``__method`` from the ``ClassName`` class will be changed to ``_ClassName__method``.

Therefore : use ``classInstance._className__privateVariable`` to access the private variable anyway

With previous example : ``c._Computer__maxprice``

Protected variables
-------------------

-> add a simple underscore prefix ``_``

Those are accessible from the outside of the class, so there's no "real" protection to prevent the user from    accessing them

Special methods
===============

``__init__`` : constructor
--------------------------

.. code-block:: python

    class Exemple:
        """Un petit exemple de classe"""
        def __init__(self, nom):
            """Exemple de constructeur"""
            self.nom = nom
            self.autre_attribut = "une valeur"
            
``__del__`` : object destructor
-------------------------------

Defines what happends when the object is destructed with the ``del`` keyword

**Could lead to memory leakages : potentially messes up the garbage collection**

.. code-block:: python

    def __del__(self):
            """Méthode appelée quand l'objet est supprimé"""
            print("C'est la fin ! On me supprime !")

``__repr__`` : object representation
------------------------------------

Defines what is returned when we simply call the object. Example :

.. code-block:: python

    class Personne:
        """Classe représentant une personne"""
        def __init__(self, nom, prenom):
            """Constructeur de notre classe"""
            self.nom = nom
            self.prenom = prenom
            self.age = 33
        def __repr__(self):
            """Quand on entre notre objet dans l'interpréteur"""
            return "Personne: nom({}), prénom({}), âge({})".format(
                    self.nom, self.prenom, self.age)

.. code-block:: python

    >>> p1 = Personne("Micado", "Jean")
    >>> p1
    Personne: nom(Micado), prénom(Jean), âge(33)
    >>>

``__getattr__`` : called when an non-existent attribute is set
--------------------------------------------------------------

.. code-block:: python

    class Protege:
        """Classe possédant une méthode particulière d'accès à ses attributs :
        Si l'attribut n'est pas trouvé, on affiche une alerte et renvoie None"""
        
        def __init__(self):
            """On crée quelques attributs par défaut"""
            self.a = 1
            self.b = 2
            self.c = 3
        def __getattr__(self, nom):
            """Si Python ne trouve pas l'attribut nommé nom, il appelle
            cette méthode. On affiche une alerte"""
            print("Alerte ! Il n'y a pas d'attribut {} ici !".format(nom))
            
.. code-block:: python

    >>> pro = Protege()
    >>> pro.a
    1
    >>> pro.c
    3
    >>> pro.e
    Alerte ! Il n'y a pas d'attribut e ici !
    >>>
    
``__setattr__`` : redefines the way an attribute is set
-------------------------------------------------------

.. code-block:: python

    class MyClass:

        def __init__(self):
            self.foo = 0

        def __setattr__(self, attr_name, attr_value):
            if attr_value < 0:
                print("wrong value")
            else:
                object.__setattr__(self, attr_name, attr_value)
                
Note : it is necessary to specify ``object.__setattr__`` to avoid creatung an infinite loop (``__setattr__`` -> ``__setattr__`` -> ``__setattr__``...)

.. code-block:: python

    >>> c = MyClass()
    >>> c.foo = -5
    wrong value
    >>> print(c.foo)
    0
    >>> c.foo = 65
    >>> print(c.foo)
    65
    >>>

``__delattr__`` : delete an attribute
---------------------------------------

``del objet.attribut`` doesn't work -> use ``object.__delattr__`` instead

.. code-block:: python

    def __delattr__(self, nom_attr):
        """On ne peut supprimer d'attribut : on lève l'exception AttributeError"""
        raise AttributeError("Vous ne pouvez supprimer aucun attribut de cette classe")

Container (lists, dictionaries, strings...) methods
===================================================

``__getitem__``
---------------

Called to get container[i]

.. code-block:: python

    class ZDict:

        """Classe enveloppe d'un dictionnaire"""

        def __init__(self):
            """Notre classe n'accepte aucun paramètre"""
            self._dictionnaire = {}

        def __getitem__(self, index):
            """Cette méthode spéciale est appelée quand on fait objet[index]
            Elle redirige vers self._dictionnaire[index]"""
            return self._dictionnaire[index]

``__setitem__``
---------------

Called to set ``container[i]``

.. code-block:: python

    class ZDict:
    
    """Classe enveloppe d'un dictionnaire"""
    
        def __init__(self):
            """Notre classe n'accepte aucun paramètre"""
            self._dictionnaire = {}
            
        def __setitem__(self, index, valeur):
        """Cette méthode est appelée quand on écrit objet[index] = valeur
        On redirige vers self._dictionnaire[index] = valeur"""
        self._dictionnaire[index] = valeur

``__delitem__``
---------------

Called to delete ``container[i]``

.. code-block:: python

    class ZDict:
    
    """Classe enveloppe d'un dictionnaire"""
    
        def __init__(self):
            """Notre classe n'accepte aucun paramètre"""
            self._dictionnaire = {}
            
        def __delitem__(self):
            """Cette méthode est appelée quand on écrit del objet[index]"""
            print("Item deleted !")

``__contains__``
----------------

Called when using ``in`` keyword

.. code-block:: python

    ma_liste = [1, 2, 3, 4, 5]
    # This :
    8 in ma_liste
    # ...is the same as :
    ma_liste.__contains__(8)

Overloading mathematical operators
==================================

Classic operators
------------------

=========================== =========================== ===========================
Operation 	                Syntax 	                    Function
=========================== =========================== ===========================
Addition 	                ``a + b``	                ``add(a, b)``
Concatenation 	            ``seq1 + seq2`` 	        ``concat(seq1, seq2)``
Containment Test 	        ``obj in seq`` 	            ``contains(seq, obj)``
Division 	                ``a / b`` 	                ``truediv(a, b)``
Division 	                ``a // b`` 	                ``floordiv(a, b)``
Bitwise And 	            ``a & b`` 	                ``and_(a, b)``
Bitwise Exclusive Or 	    ``a ^ b`` 	                ``xor(a, b)``
Bitwise Inversion 	        ``~ a`` 	                ``invert(a)``
Bitwise Or 	                ``a | b`` 	                ``or_(a, b)``
Exponentiation 	            ``a ** b`` 	                ``pow(a, b)``
Identity 	                ``a is b`` 	                ``is_(a, b)``
Identity 	                ``a is not b`` 	            ``is_not(a, b)``
Indexed Assignment 	        ``obj[k] = v`` 	            ``setitem(obj, k, v)``
Indexed Deletion 	        ``del obj[k]`` 	            ``delitem(obj, k)``
Indexing 	                ``obj[k]`` 	                ``getitem(obj, k)``
Left Shift 	                ``a << b`` 	                ``lshift(a, b)``
Modulo 	                    ``a % b`` 	                ``mod(a, b)``
Multiplication 	            ``a * b`` 	                ``mul(a, b)``
Matrix Multiplication 	    ``a @ b`` 	                ``matmul(a, b)``
Negation (Arithmetic) 	    ``- a`` 	                ``neg(a)``
Negation (Logical) 	        ``not a`` 	                ``not_(a)``
Positive 	                ``+ a`` 	                ``pos(a)``
Right Shift 	            ``a >> b`` 	                ``rshift(a, b)``
Slice Assignment 	        ``seq[i:j] = values`` 	    ``setitem(seq, slice(i, j), values)``
Slice Deletion 	            ``del seq[i:j]`` 	        ``delitem(seq, slice(i, j))``
Slicing 	                ``seq[i:j]`` 	            ``getitem(seq, slice(i, j))``
String Formatting 	        ``s % obj`` 	            ``mod(s, obj)``
Subtraction 	            ``a - b`` 	                ``sub(a, b)``
Truth Test 	                ``obj`` 	                ``truth(obj)``
Ordering 	                ``a < b`` 	                ``lt(a, b)``
Ordering 	                ``a <= b`` 	                ``le(a, b)``
Equality 	                ``a == b`` 	                ``eq(a, b)``
Difference 	                ``a != b`` 	                ``ne(a, b)``
Ordering 	                ``a >= b`` 	                ``ge(a, b)``
Ordering 	                ``a > b`` 	                ``gt(a, b)``
=========================== =========================== ===========================

Inplace Operators
-----------------

=============================== ===================================
Function 	                    Equivalent
=============================== ===================================
``a = iadd(a, b)``              ``a += b``
``a = iand(a, b)``              ``a &= b``
``a = iconcat(a, b)``           ``a += b`` for a and b sequences
``a = ifloordiv(a, b)``         ``a //= b``
``a = ilshift(a, b)``           ``a <<= b``
``a = imod(a, b)``              ``a %= b``
``a = imul(a, b)``              ``a *= b``
``a = imatmul(a, b)``           ``a @= b``
``a = ior(a, b)``               ``a |= b``
``a = ipow(a, b)``              ``a **= b``
``a = irshift(a, b)``           ``a >>= b``
``a = isub(a, b)``              ``a -= b``
``a = itruediv(a, b)``          ``a /= b``
``a = ixor(a, b)``              ``a ^= b``
=============================== ===================================

Pickles specific methods
========================

``__getstate__``
----------------

Returns the object to be serialized by pickle. If it's not defined, the object is serialized as is. ``__getstate__`` allows to modify it before serializing it:

.. code-block:: python

    class Temp:
        """Classe contenant plusieurs attributs, dont un temporaire"""
        
        def __init__(self):
            """Constructeur de notre objet"""
            self.attribut_1 = "une valeur"
            self.attribut_2 = "une autre valeur"
            self.attribut_temporaire = 5
       
        def __getstate__(self):
            """Renvoie le dictionnaire d'attributs à sérialiser"""
            dict_attr = dict(self.__dict__)
            dict_attr["attribut_temporaire"] = 0
            return dict_attr
            
Here the ``attribut_temporaire`` attribute is set to zero beforethe object is serialized.

``__setstate__``
----------------

Called when the object is deserialized by pickle

.. code-block:: python

    ...
        def __setstate__(self, dict_attr):
            """Méthode appelée lors de la désérialisation de l'objet"""
            dict_attr["attribut_temporaire"] = 0
            self.__dict__ = dict_attr
            
**see POP307 for more serialization linked methods**

Summary on how special methods are called
=========================================

.. image:: _static/special_methods_calls.png
    :target: _static/special_methods_calls.png
