=========
Iterators
=========

.. contents:: :local:

``__iter__`` , ``__next__`` : inside functionning of iterators
==============================================================

Behind the ``for`` loop is actually a call of the ``__iter__`` special function of the ``list`` object. This functions can be called with ``iter``, and returns an iterator object.

To get the next item from an iterator call the ``next`` function, which actually calls the ``__next__`` special method.

When creating a custom object, we have to create the ``__iter__`` and ``__next__`` functions to make it iterable.

So this :

.. code-block:: python

    list = [12, 5, 6, 87, 9]

    sum = 0
    for i in list:
        sum += i
        
Is equivalent to this :

.. code-block:: python

    list = [12, 5, 6, 87, 9]
    
    list_iter = iter(list)
    while True:
        try:
            sum += next(list_iter)
        except StopIteration:
            break

Create generators with ``yield``
================================

``yield`` must be used exclusively inside a function (or class method). The principle is : each time the interpreter reaches a ``yield`` keyword, it returns the value that follows it and pauses, until another ``next`` function is called.

Here is an example of a generator using ``yield`` :

.. code-block:: python
    
    def interval(lim_low, lim_high):
            """Generator that returns the series of integers
            starting at lim_low and ending at lim_high."""
            
            while lim_low <= lim_high:
                yield lim_low
                lim_low += 1

Use : 

.. code-block:: python

    my_iterator = iter(interval(3, 8))

    i = 3
    while True:
        try:
            print(next(my_iterator))
            i += 1
        except StopIteration:
            break

**TO BE FINISHED**