=====================================
Installer des programmes avec apt-get
=====================================

``/etc/apt/sources.list`` :

    * adresses des serveurs pour les dépôts
    * pour autoriser le téléchargement de sources
    
ex :
        
.. code-block:: bash
    
    deb-src http://raspbian.raspberrypi.org/raspbian/ stretch main contrib non-free rpi
                                                      ^ OS version

``apt-get update`` (optionnel)
    pour mettre notre cache à jour si ce n'est pas déjà fait 

``apt-cache search monpaquet`` (optionnel)
    pour rechercher le paquet que nous voulons télécharger si nous ne connaissons pas son nom exact 

``apt-get install monpaquet``
    pour télécharger et installer notre paquet

``apt-cache show nomdupaquet``
    pour une plus ample description d'un paquet

``apt-get remove nomdupaquet``
    désinstaller un paquet. Toutefois, cela ne supprime pas les dépendances du paquet devenues inutiles

``apt-get autoremove nomdupaquet``
    Pour demander à ``apt-get`` de supprimer aussi les dépendances inutiles, on utilise ``autoremove``

``apt-get upgrade``
    met à jour tous les paquets du système d'un seul couper (faire un ``apt-get update`` avant)