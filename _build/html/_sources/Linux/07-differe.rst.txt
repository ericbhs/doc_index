==========================================
Exécuter un programme à une heure différée
==========================================

``date``
    afficher / régler l'heure

``at HH:MM``
    donne la possibilité de démarrer un programme à HH:MM. Un promppt aparait pour demander lequel.

``at HH:MM tomorrow``

``at HH:MM 11/15/10``
    attention date au format américain

``at now +5 minutes``

``atq``
    afficher les jobs en attente -> donne un n°

``atrm x``
    supprimer un job en attente dont le numéro est x

``sleep x``
    attend x secondes (minute : xm, heure : xh, jour : xd)

``echo "export EDITOR=nano" >>  ~/.bashrc``
    faire de Nano l'éditeur par défaut

``crontab -e``
    modifier la crontab

``crontab -l``
    afficher la crontab

``crontab -r``
    supprimer la crontab (immédiate et sans confirmation)

``m	h	dom	mon	dow	command``
	* ``m`` : minutes (0 - 59)
	* ``h`` : heures (0 - 23) 
	* ``dom`` (day of month) : jour du mois (1 - 31) 
	* ``mon`` (month) : mois (1 - 12) ;
	* ``dow`` (day of week) : jour de la semaine (0 - 6, 0 étant le dimanche) ;
	* ``command`` : c'est la commande à exécuter.

	ex : ``47 15 * * * touch /home/mateo21/fichier.txt`` -> tous les jours à 15h47
	
	Pour chaque champ, on a le droit à différentes notations :
		* ``5`` (un nombre) : exécuté lorsque le champ prend la valeur 5
		* ``*`` : exécuté tout le temps (toutes les valeurs sont bonnes) ;
		* ``3,5,10`` : exécuté lorsque le champ prend la valeur 3, 5 ou 10. Ne pas mettre d'espace après la virgule ;
		* ``3-7`` : exécuté pour les valeurs 3 à 7 ;
		* ``*/3`` : exécuté tous les multiples de 3 (par exemple à 0 h, 3 h, 6 h, 9 h…).