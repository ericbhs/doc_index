======================
Exceptions, assertions
======================

Exceptions
==========

* Try/catch exceptions

.. code-block:: python

    try:
        resultat = numerateur / denominateur
    
    except NameError:
        print("NameError")
    
    except TypeError:
        print("TypeError")
    
    except ZeroDivisionError:
        print("ZeroDivisionError")
    
    # This is done whether there are errors or not
    finally:
        print("At least I've tried")
        
* Raise exceptions

.. code-block:: python

    raise TypeDeLException("message à afficher")
        
Assertions
==========

.. code-block:: python

    def division(x, y):
        assert y != 0, "Can't divide by zero"
        return x / y