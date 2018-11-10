==========================
Structures conditionnelles
==========================

Exemple :

.. code-block:: python
    
    if annee % 400 == 0:
        bissextile = True
    elif annee % 100 == 0:
        bissextile = False
    elif annee % 4 == 0:
        bissextile = True
    else:
        bissextile = False

=============== ===================================
Opérateur       Signification littérale
=============== ===================================
<               Strictement inférieur à
>               Strictement supérieur à
<=              Inférieur ou égal à
>=              Supérieur ou égal à
==              Égal à
!=              Différent de
True            bool "vrai"
False           bool "faux"
and             bool "et"
or              bool "ou"
not             bool "not"
=============== ===================================