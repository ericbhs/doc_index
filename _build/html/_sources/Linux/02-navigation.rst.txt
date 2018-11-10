============================
Navigation dans les dossiers
============================

``pwd``
    savoir où je suis

``which cmd``
    permet de localiser l'emplacement d'une commande cmd

``ls -F``
    rajoute à la fin des éléments un symbole pour qu'on puise faire la distinction entre les dossiers, fichiers, raccourcis...

``ls -lh``
    afficher la taille des éléments (-h : "for humans")

``cd``
    sans arguments, ramène dans home/currentUser/

``du``
    pour Disk Usage (utilisation du disque) vous donne des informations sur la taille qu'occupent les dossiers sur votre disque

``du -c``
    produces a grand total

``du -hsc *``
    This finds the size recursively and puts it next to each folder name, along with total size at the bottom, all in the human format.
	
``du -hs * | sort -h``
    same as previous but sort by size
    
**Note** : on the ``du`` results, ``/dev/root`` is the disk on which the system is installed