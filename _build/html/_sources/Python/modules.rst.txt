==============
Modules import
==============

With ``import`` we must type the module name before calling one of its function (doesn't import the namespace)

.. code-block:: python

    import my_module
    
    x = my_module.my_function()

    
With ``from ... import ...`` the namespace of my_module has been imported for the function ``my_function()`` : we don't need to type the module name anymore to call this function

.. code-block:: python

    from my_module import my_function()

    x = my_function()
    
With ``from ... import *`` the namespace of my_module has been imported for all its functions : we don't need to type the module name anymore to call any of its functions

.. code-block:: python

    from my_module import *
    
    x = my_function()