================================
Surveiller l'activité du système
================================

``w``
    permet de voir qui fait quoi

        ``USER`` : le nom de l'utilisateur (son login) ;

        ``TTY`` : le nom de la console dans laquelle se trouve l'utilisateur. Souvenez-vous que sous Linux il y a en général six consoles (tty1 à tty6) et qu'en plus de ça, on peut en ouvrir une infinité grâce aux consoles graphiques (leur nom commence par pts, en général), comme le propose le programme « Terminal » sous Unity ou « Konsole » sous KDE ;

        ``FROM`` : c'est l'adresse IP (ou le nom d'hôte) depuis laquelle il se connecte. Ici, comme je me suis connecté en local (sur ma propre machine, sans passer par Internet), il n'y a pas vraiment d'IP ;

        ``LOGIN@`` : l'heure à laquelle cet utilisateur s'est connecté ;

        ``IDLE`` : depuis combien de temps cet utilisateur est inactif (depuis combien de temps il n'a pas lancé de commande)

        ``WHAT`` : la commande qu'il est en train d'exécuter en ce moment. En général, si vous voyez bash, cela signifie que l'invite de commandes est ouverte et qu'aucune commande particulière n'est exécutée.

``ps`` : liste statique des processus

``ps -ef``
    lister tous les processus (~ps -A)

``ps -ejH``
    afficher les processus en arbre

``ps -u UTILISATEUR``
    lister les processus lancés par un utilisateur

``top``
    liste dynamique des processus
    
        ``q`` : ferme top ;

        ``h`` : affiche l'aide, et donc la liste des touches utilisables.

        ``B`` : met en gras certains éléments.

        ``f`` : ajoute ou supprime des colonnes dans la liste.

        ``F`` : change la colonne selon laquelle les processus sont triés. En général, laisser le tri par défaut en fonction de %CPU est suffisant.

        ``u`` : filtre en fonction de l'utilisateur que vous voulez.

        ``k`` : tue un processus, c'est-à-dire arrête ce processus. Ne vous inquiétez pas, en général les processus ne souffrent pas. On vous demandera le numéro (PID) du processus que vous voulez tuer. Nous reviendrons sur l'arrêt des processus un peu plus loin.

        ``s`` : change l'intervalle de temps entre chaque rafraîchissement de la liste (par défaut, c'est toutes les trois secondes).
	
``kill processPid``
    tue le processus dont le PID est processPid (proprement)

``kill -9 processPid``
    force l'arrêt immédiat du processus processPid (bourrin)

``killall processName``
    tue plusieurs processus dont le com est processName

``sudo halt/reboot``
    arrête/reboot le PC