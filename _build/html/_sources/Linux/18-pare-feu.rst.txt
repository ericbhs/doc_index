========================================================
Analyser le réseau et filtrer le trafic avec un pare-feu
========================================================

``host www.google.com``
    renvoie l'adresse ip du site

pour voir les associations (~DNS) locales :
    -> /etc/hosts
    
``whois google.com``
    obtenir des infos sur un site (installer d'abord le package whois)

``ifconfig``
    liste des interfaces réseau
    ``lo`` : c'est la boucle locale. Tout le monde devrait avoir cette interface. Elle correspond à une connexion à… vous-mêmes. C'est pour cela qu'on l'appelle la boucle locale : tout ce qui est envoyé par là vous revient automatiquement. Cela peut paraître inutile, mais on a parfois besoin de se connecter à soi-même pour des raisons pratiques.
    
``ifconfig eth0 down/up``
    activer/désactiver une interface
    
``netstat``
    statistiques sur le réseau
    
``netstat -i``
    statistiques des interfaces réseau

``netstat -uta``
    lister toutes les connexions ouvertes
    
    Options :
    
    * ``-u`` : afficher les connexions UDP ;
    * ``-t`` : afficher les connexions TCP ;
    * ``-a`` : afficher toutes les connexions quel que soit leur état.
    * ``-n`` : affiche les n° de port plutôt que leur description
    * ``-l`` : affiche les connexions en état d'écoute
    
    Statuts :
    
    * ``ESTABLISHED`` : la connexion a été établie avec l'ordinateur distant 
    * ``TIME_WAIT`` : la connexion attend le traitement de tous les paquets encore sur le réseau avant de commencer la fermeture 
    * ``CLOSE_WAIT`` : le serveur distant a arrêté la connexion de lui-même (peut-être parce que vous êtes restés inactifs trop longtemps ?) 
    * ``CLOSED`` : la connexion n'est pas utilisée 
    * ``CLOSING`` : la fermeture de la connexion est entamée mais toutes les données n'ont pas encore été envoyées 
    * ``LISTEN`` : à l'écoute des connexions entrantes. Les connexions à l'état LISTEN ne sont pas utilisées actuellement mais qu'elles « écoutent » le réseau au cas où quelqu'un veuille se connecter à votre ordinateur

``netstat -s``
    statistiques résumées

``iptables -L``
    afficher les règles
    
    * ``Chain INPUT`` : correspond aux règles manipulant le trafic entrant ;
    * ``Chain FORWARD`` : correspond aux règles manipulant la redirection du trafic ;
    * ``Chain OUTPUT`` : correspond aux règles manipulant le trafic sortant.
    * ``target`` : ce que fait la règle. Ici c'est ACCEPT, c'est-à-dire que cette ligne autorise un port et / ou une IP 
    * ``prot`` : le protocole utilisé (tcp, udp, icmp). Je rappelle que TCP est celui auquel on a le plus recourt. ICMP permet à votre ordinateur de répondre aux requêtes de type « ping » 
    * ``source`` : l'IP de source. Pour INPUT, la source est l'ordinateur distant qui se connecte à vous 
    * ``destination`` : l'IP de destination. Pour OUTPUT, c'est l'ordinateur auquel on se connecte 
    * la dernière colonne : elle indique le port après les deux points « : ». Ce port est affiché en toutes lettres, mais avec -n vous pouvez obtenir le numéro correspondant

``iptables -F``
    réinitialise les règles du pare-feu (attention : efface tout le travail fait auparavant sur le pare-feu...)

Ajouter et supprimer des règles :

    Voici les principales commandes à connaître :

    * ``-A chain`` : ajoute une règle en fin de liste pour la chain indiquée (INPUT ou OUTPUT, par exemple).
    * ``-D chain rulenum`` : supprime la règle n° rulenum pour la chain indiquée.
    * ``-I chain rulenum`` : insère une règle au milieu de la liste à la position indiquée par rulenum. Si vous n'indiquez pas de position rulenum, la règle sera insérée en premier, tout en haut dans la liste.
    * ``-R chain rulenum`` : remplace la règle n° rulenum dans la chain indiquée.
    * ``-L`` : liste les règles (nous l'avons déjà vu).
    * ``-F chain`` : vide toutes les règles de la chain indiquée. Cela revient à supprimer toutes les règles une par une pour cette chain.
    * ``-P chain regle`` : modifie la règle par défaut pour la chain. Cela permet de dire, par exemple, que par défaut tous les ports sont fermés, sauf ceux que l'on a indiqués dans les règles.
    * ``-m (--match)`` : Specifies  a  match  to use, that is, an extension module that tests for a specific property. The set of matches make up the condition under which a target is invoked. Matches are evaluated first to last as specified on the command line and work in short-circuit fashion,  i.e.  if one extension yields false, evaluation will stop.


``iptables -A (chain) -p (protocole) --dport (port) -j (décision)``
    ajouter une règle. Remplacez chain par la section qui vous intéresse (``INPUT`` ou ``OUTPUT``), protocole par le nom du protocole à filtrer (TCP, UDP, ICMP…) et enfin décision par la décision à prendre : ``ACCEPT`` pour accepter le paquet, ``REJECT`` pour le rejeter ou bien ``DROP`` pour l'ignorer complètement.

exemple : ``iptables -A INPUT -p tcp --dport ssh -j ACCEPT``

``iptables -A INPUT -p icmp -j ACCEPT``
    autoriser les pings (protocole ICMP)

``iptables -A INPUT -i lo -j ACCEPT``

``iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT``

    * La première règle autorise tout le trafic sur l'interface de loopback locale grâce à -i lo. Il n'y a pas de risque à autoriser votre ordinateur à communiquer avec lui-même, d’autant plus qu’il en a parfois besoin !
    * La seconde règle autorise toutes les connexions qui sont déjà à l'état ESTABLISHED ou RELATED. En clair, elle autorise toutes les connexions qui ont été demandées par votre PC. Là encore, cela permet d'assouplir le pare-feu et de le rendre fonctionnel pour une utilisation quotidienne.

``iptables -P INPUT DROP``
    on refuse tout ce qui n'est pas aurtorisé (faire de même pour OUTPUT)

ATTENTION : ces règles seront perdues au redémarrage ! pour que ça ne soit pas le cas -> ajouter un script shell