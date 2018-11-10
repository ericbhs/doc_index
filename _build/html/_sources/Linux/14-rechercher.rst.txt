=======================
Rechercher des fichiers
=======================

``locate fichier``
    recherche les fichiers/dossiers qui contiennent "fichier" et qui sont dans la base de données (db)

``sudo updatedb``
    mettre à jour la base de données

``find fichier``
    recherche des fichiers en scannant le disque dur (pas la db base)

``find -name "file.txt"``
    dans le dossier courant

``find /var/log/ -name "syslog"``
    dans un dossier différent du courant

``find -size +10M``
    chercher les fichiers qui font plus de 10Mo

``find -name "*.odt" -atime -6``
    chercher les fichiers .odt auxquels on a accédé depuis 7 jours (numérotation comence à 0)

``find -type d``
    only directories

``find -type f``
    only files

``find -name "*.jpg" -delete``
    supprime tous les fichiers .jpg (dangereux !!!)

``find -name ".jpg" -exec cmd {} \;``
    exécute la commande cmd avec les résultats. La commande doit finir par un ``\;`` obligatoirement