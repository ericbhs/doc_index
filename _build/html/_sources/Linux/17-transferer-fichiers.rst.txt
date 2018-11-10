=======================
Transférer des fichiers
=======================

``wget`` : télécharger un fichier sur le web
--------------------------------------------

``wget http://website.com/file``
    télécharger un fichier distant

``scp`` : copier/coller un fichier par SSH
------------------------------------------

``scp fichier_origine copie_destination``
    permet de copier des fichiers distants de manière sécurisée (cryptage ssh)

``scp fichier remoteLogin@85.123.10.201:/home/remoteLogin/dossier/``
    copier un fichier de l'ordi local vers le distant

``scp remoteLogin@85.123.10.201:fichier copie_fichier``
    pas nécessaire de préciser le nom -> gardera le même nom que le fichier d'origine

``scp -P 16296 mateo21@85.123.10.201:image.png``
    en précisant le port (attention MAJUSCULE)

Protocole ftp non sécurisé
--------------------------

``ftp://ftp.debian.org``
    connection au serveur ftp de debian (login : anonymous mpd : any)
    
    * on a ensuite un prompt qui nous permet de naviguer sur le serveur (``ls``, ``cd``, ``pwd``...)
    * ``put`` : ajouter un fichier sur le serveur (verouillé dans le cas de celui de debian)
    * ``get`` : récupérer un fichier depuis le serveur (sera mis dans le dossier courant du pc local)
    * pour se déplacer dans le pc local : ``!cd``, ``!ls``, ``!pwd``... (ajouter un ! avant la commande)
    * attention : protocole ftp pas sécurisée

Protocole ftp sécurisé
----------------------
    
``sftp mateo21@lisa.simple-it.fr``
    ftp sécurisée avec ssh (port par défaut : 22)

``rsync`` : sauvegardes sur un serveur distant    
----------------------------------------------

``rsync``
    permet de créer des sauvegardes sur un serveur distant (incrémentielles, etc...)

``rsync -arv Images/ backups/``
    analyse les différences entre /Images et /backup et fait une sauvegarde
    
    * ``-a`` : conserve toutes les informations sur les fichiers, comme les droits (chmod), la date de modification, etc. ;
    * ``-r`` : sauvegarde aussi tous les sous-dossiers qui se trouvent dans le dossier à sauvegarder ;
    * ``-v`` : mode verbeux, affiche des informations détaillées sur la copie en cours.
   
``rsync -arv --delete Images/ backups/``
    analyse les différences entre /Images et /backup et efface les fichiers de backups qui ne sont plus dans /Images

``rsync -arv --delete --backup Images/ backups/``
    garde les fichiers suprimés en leur ajoutant un suffixe dans le dossier de sauvegarde

``rsync -arv --delete --backup --backup-dir=/home/mateo21/backups_supprimes Images/ backups/``
    les fichiers suprimés vont dans le dossier /home/mateo21/backups_supprimes

``rsync -arv --delete --backup --backup-dir=/home/mateo21/fichiers_supprimes Images/ mateo21@IP_du_serveur:mes_backups/``
    fait le backup sur un ordinateur distant via ssh

``rsync -arv --delete --backup --backup-dir=/home/mateo21/fichiers_supprimes Images/ mateo21@IP_du_serveur:mes_backups/ -e "ssh -p 12473"``
    avec un n° de port custom