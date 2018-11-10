==============================
Les utilisateurs et les droits
==============================

``adduser userName``
    ajouter un utilisateur userName

``deluser userName``
    supprimer un utilisateur userName

``deluser --remove-home userName``
    supprime aussi son répertoire personnel

``pswd userName``
    changer le mot de passe de userName

``addgroup groupName``
    crée un groupe d'utilisateurs

``usermod -l userName``
    modifier le nom de l'utilisateur

``usermod -g groupName userName``
    modifier le groupe d'un utilisateur (remplace les précédents groupes)

``usermod -G amis,paris,collegues patrick``
    ajouter l'utilisateur à plusieurs groupes (G majuscule) (remplace les précédents groupes)

``usermod -aG amis,paris,collegues patrick``
    ajoute l'utilisateur aux groupes en gardant ses groupes précédents

``delgroup groupName``
    supprime un groupe

``chown userName fichier``
    rend patrick propriétaire de rapport.txt

``chgrp groupName fichier``
    rend le groupe groupName propriétaire du fichier

``chown userName:groupName fichier``
    Cela affectera le fichier à l'utilisateur userName et au groupe groupName.

``chown -R userName:userName /dossier/``
    modifie tous les sous-dossiers et fichiers contenus dans un dossier pour y affecter un nouvel utilisateur (et un nouveau groupe si on utilise la technique du deux points)

ex : ``drwxr-xr-x 2 mateo21 mateo21 4096 2007-11-13 21:53 Desktop``
    * ``d`` (Directory) : indique si l'élément est un dossier ;
    * ``l`` (Link) : indique si l'élément est un lien (raccourci) ;
    * ``r`` (Read) : indique si on peut lire l'élément ;
    * ``w`` (Write) : indique si on peut modifier l'élément ;
    * ``x`` (eXecute) : si c'est un fichier, « x » indique qu'on peut l'exécuter. Ce n'est utile que pour les fichiers exécutables (programmes et scripts).
    
    Si c'est un dossier, « x » indique qu'on peut le « traverser », c'est-à-dire qu'on peut voir les sous-dossiers qu'il contient si on a le droit de lecture dessus.

    * le premier triplet rwx indique les droits que possède le propriétaire du fichier sur ce dernier ;
    * le second triplet rwx indique les droits que possèdent les autres membres du groupe sur ce fichier ;
    * enfin, le dernier triplet rwx indique les droits que possèdent tous les autres utilisateurs de la machine sur le fichier.

``chmod``
    modifie les droits -> utiliser des numéros :
	* ``r`` = 4
	* ``w`` = 2
	* ``x`` = 1
	
	donc :
    
    * ``---`` = 0+0+0 = 0 
    * ``r--`` = 4+0+0 = 4
    * ``-w-`` = 0+2+0 = 2
    * ``--x`` = 0+0+1 = 1
    * ``rw-`` = 4+2+0 = 6
    * ``-wx`` = 0+2+1 = 3
    * ``r-x`` = 4+0+1 = 5
    * ``rwx`` = 4+2+1 = 7

``chmod 600 rapport.txt``
    ``-rw------- 1 mateo21 mateo21 0 2007-11-15 23:14 rapport.txt``