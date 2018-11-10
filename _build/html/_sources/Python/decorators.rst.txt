==========
Decorators
==========

.. contents:: :local:

Decorator allow to modify the behaviour of a function.

Simple decorator
================

The "prototype" of a decorator is :
    
    * Parameter : the function to be modified
    * Return : another function
    
The returned might be the same function as the function to be modified.

.. code-block:: python
    
    def my_decorator(fonction):
        """This is our decorator : it displays a message before calling the
        decorated function"""
        
        def modified_function():
            """This is the function returned by the decorator.
            
            It is actually a modified version of the original function,
            which displays a message before calling the original function."""
            
            print("Let's call {0}...".format(fonction))
            return fonction()
        return modified_function

    @my_decorator
    def hello():
        print("Hello !")
        
This :

.. code-block:: python

    @decorator
    def fonction(...):
        ...
    
...is the same as this :

.. code-block:: python

    def fonction(...):
        ...

    fonction = decorator(fonction)
    
Using the decorator replaces the function by the function modified by the decorator function.

        
Decorator with parameters
=========================

This :

.. code-block:: python

    @decorator(parameter)
    def fonction(...):
        ...
    
...is the same as this :

.. code-block:: python

    def fonction(...):
        ...

    fonction = decorator(parameter)(fonction)
    
``decorator(parameter)`` is a function, which is applied to ``function``.

Example :

.. code-block:: python

    import time

    def time_control(nb_secs):
        """Controls the time t taken by a function to execute.
        if t > nb_secs => display an alert"""
        
        def decorator(function_to_be_executed):
            """This is our decorator.
            It is called during the definition of the function
            to be decorated"""
            
            def modified_function():
                """Function returned by the decorator.
                Calculates the function execution time if the user
                took more than nb_secs to press enter."""
                
                start_time = time.time() # Before executing the function
                returned_value = function_to_be_executed() # Run the function
                end_time = time.time()
                tps_execution = end_time - start_time   
                if tps_execution >= nb_secs:
                    print("Function {0} took {1} to run.".format( \
                            function_to_be_executed, tps_execution))
                return returned_value
            return modified_function
        return decorator
        
So we have :

``time_control(nb_sec)``
    returns ``decorator(function_to_be_executed)``
        returns ``modified_function()``
        
This could be used like that :

.. code-block:: python

    @controler_temps(4)
    def wait():
        input("Press enter...")

Result : 

.. code-block:: python

    >>> wait() # Pressing enter right now
    Press enter...
    
    >>> wait() # Waiting more than 4s to press enter
    Press enter...
    Function, <function wait at 0x00BA5810> took 4.14100003242 to run

Decorator on functions with parameters
======================================

Taking the previous example, we only have to apply the synthax for functions that take multiple arguments :

* unnamed parameters preceded with ``*``
* named parameters preceded with ``**`` 

That difference is applied to ``modified_function`` :

.. code-block:: python
    
    import time

    def time_control(nb_secs):
        """Controls the time t taken by a function to execute.
        if t > nb_secs => display an alert"""
        
        def decorator(function_to_be_executed):
            """This is our decorator.
            It is called during the definition of the function
            to be decorated"""
            
            def modified_function(*unnamed_parameters, **named_parameters):
                """Function returned by the decorator.
                Calculates the function execution time if the user
                took more than nb_secs to press enter."""
                
                start_time = time.time() # Before executing the function
                # Run the function
                returned_value = function_to_be_executed(*unnamed_parameters,
                                                            **named_parameters)
                end_time = time.time()
                tps_execution = end_time - start_time   
                if tps_execution >= nb_secs:
                    print("Function {0} took {1} to run.".format( \
                            function_to_be_executed, tps_execution))
                return returned_value
            return modified_function
        return decorator
        
Decorators applied to classes definitions
=========================================

.. code-block:: python

    >>> def decorateur(classe):
    ...     print("Définition de la classe {0}".format(classe))
    ...     return classe
    ...
    >>> @decorateur
    ... class Test:
    ...     pass
    ...
    Définition de la classe <class '__main__.Test'>
    >>>
    
Chaining Decorators
===================

.. code-block:: python

    @decorateur1
    @decorateur2
    def fonction():
        ...
        
Example of decorator to check argument types
============================================

.. code-block:: python

    def controler_types(*a_args, **a_kwargs):
        """On attend en paramètres du décorateur les types souhaités. On 
        accepte une liste de paramètres indéterminés, étant donné que notre 
        fonction définie pourra être appelée avec un nombre variable de 
        paramètres et que chacun doit être contrôlé"""
        
        def decorateur(fonction_a_executer):
            """Notre décorateur. Il doit renvoyer fonction_modifiee"""
            def fonction_modifiee(*args, **kwargs):
                """Notre fonction modifiée. Elle se charge de contrôler
                les types qu'on lui passe en paramètres"""
                
                # La liste des paramètres attendus (a_args) doit être de même
                # Longueur que celle reçue (args)
                if len(a_args) != len(args):
                    raise TypeError("le nombre d'arguments attendu n'est " \
                            "pas égal au nombre reçu")
                # On parcourt la liste des arguments reçus et non nommés
                for i, arg in enumerate(args):
                    if a_args[i] is not type(args[i]):
                        raise TypeError("l'argument {0} n'est pas du type " \
                                "{1}".format(i, a_args[i]))
                
                # On parcourt la liste des paramètres reçus et nommés
                for cle in kwargs:
                    if cle not in a_kwargs:
                        raise TypeError("l'argument {0} n'a aucun type " \
                                "précisé".format(repr(cle)))
                    if a_kwargs[cle] is not type(kwargs[cle]):
                        raise TypeError("l'argument {0} n'est pas de type" \
                                "{1}".format(repr(cle), a_kwargs[cle]))
                return fonction_a_executer(*args, **kwargs)
            return fonction_modifiee
        return decorateur
        
Decorators for getters / setters / deleters
===========================================

.. code-block:: python

    class C(object):
        def __init__(self):
            self._x = None

        @property
        def x(self):
            """I'm the 'x' property."""
            return self._x

        @x.setter
        def x(self, value):
            self._x = value

        @x.deleter
        def x(self):
            del self._x
            
The ``@property`` decorator turns the ``x()`` method into a “getter” for a read-only attribute with the same name, and it sets the docstring for voltage to “I'm the 'x' property.”

Once a roperty object has been created with ``@property``, we can redefine its ``getter``, ``setter`` and ``deleter`` methods for accessors to the parameter.

