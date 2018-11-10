=======================================
Exécuter des programmes en arrière-plan
=======================================

``cmd &``
    démarre la commande cmd en arrière plan

``cmd > /dev/null 2>&1 &``
    démarre le programme en arrière plan sans récupérer sa sortie ni ses erreurs, qui sont "jetées" dans /dev/null

``nohup cmd``
    détacher le processus de la console (ave les autres méthodes le programme se ferme quand on ferme la console, là pas)

``Ctrl + z``
    mettre en pause l'exécution du programme

``bg``
    fait passer en arrière plan le processus que l'on a stoppé avec Ctrl+z

``jobs``
    affiche les processus en arrière plan

``fg``
    reprendre un processus au premier plan (foreground)

``fg %2``
    reprendre le processus n°2 (trouvé avec la commande jobs) en premier plan

``screen``
    permet d'avoir plusieurs consoles en une (installer : sudo apt-get install screen)
    
    ``Ctrl + a puis c`` : créer une nouvelle « fenêtre ».

    ``Ctrl + a puis w`` : afficher la liste des « fenêtres » actuellement ouvertes. En bas de l'écran vous verrez par exemple apparaître : 0-$ bash  1*$ bash. Cela signifie que vous avez deux fenêtres ouvertes, l'une numérotée 0, l'autre 1. Celle sur laquelle vous vous trouvez actuellement contient une étoile * (on se trouve donc ici dans la fenêtre n° 1).
	
    ``Ctrl + a puis A`` : renommer la fenêtre actuelle. Ce nom apparaît lorsque vous affichez la liste des fenêtres avec Ctrl + a puis w.

    ``Ctrl + a puis n`` : passer à la fenêtre suivante (next).

    ``Ctrl + a puis p`` : passer à la fenêtre précédente (previous).

    ``Ctrl + a puis Ctrl + a`` : revenir à la dernière fenêtre utilisée.

    ``Ctrl + a puis un chiffre de 0 à 9`` : passer à la fenêtre n° X.

    ``Ctrl + a puis "`` : choisir la fenêtre dans laquelle on veut aller.

    ``Ctrl + a puis k`` : fermer la fenêtre actuelle (kill).

	``Ctrl + a puis S`` : découper screen en plusieurs parties (split)
	
	``Ctrl + a puis d`` : détache screen et vous permet de retrouver l'invite de commandes « normale » sans arrêter screen. C'est peut-être une des fonctionnalités les plus utiles que nous devons approfondir, et cela nous ramène d'ailleurs à l'exécution de programmes en arrière-plan dont nous avons parlé au début du chapitre.
	
``screen -r``
    récupérer son ancienne session screen (détachée)

``screen -ls``
    affiche la liste des screens actuellement ouverts