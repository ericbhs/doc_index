========================================
Compiler un programme depuis les sources
========================================

fichier ``.deb`` : pour installer un programme sur les dérivées de Debian (Red Hat : ``.rpm``)

Convertir un ``.rpm`` en ``.deb`` : utiliser le programme ``alien``

``dpkg -i foo.deb``
    installer un package ``foo.deb``

Pour compiler un programme depuis une source
--------------------------------------------
#. Installer build-ensential (si pas encore installé)
    ``sudo apt-get install build-essential``
    
#. Récupérer l'archive contenant le programme et la décompresse/désarchiver :
    ``tar zxvf htop-0.8.3.tar.gz`` (ici ``htop-0.8.3``)
    
#. Exécuter ``./configure`` pour vérifier les dépendances
    ``./configure``
    
#. Installer ce qui manque au fur et à mesure (chercher sur google pour trouver le nom du paquet à installer pour les headers manquants par exemple) et relancer ``./configure`` jusqu'à ce qu'il n'y ait plus d'erreurs

#. Lancer la compilation
    ``make`` (attention à être dans le répertoire de la source)
    
#. A la fin de la compilation un éxécutable a été créé. Il ne reste plus qu'à l'installer, c'est-à-dire à le copier dans le bon répertoire. Là encore, vous n'avez pas à vous poser beaucoup de questions. Exécutez la commande suivante :
    ``sudo make install``
    
#. Le programme est installé ! Pour le lancer :
    ``htop`` (dans le cas de notre exemple)
    
#. On peut maintenant supprimer le répertoire contenant les fichiers source