=======================
Les flux de redirection
=======================

``cmd > fichier.txt``
    redirige la sortie standard de la commande cmd vers le fichier fichier.txt

``cmd >> fichier.txt``
    redirige la sortie standard de la commande cmd vers la fin du fichier fichier.txt

``cmd > fichier.txt 2> erreurs.txt``
    redirige la sortie standard de la commande cmd vers le fichier fichier.txt et la sortie des erreurs vers le fichier erreurs.txt (fin du fichier : 2>>)

``cmd > fichier.txt 2>$1``
    redirige la sortie standard ET celle des erreurs de la commande cmd vers le fichier fichier.txt

``cmd < fichier.txt``
    envoie le contenu de fichier.txt à la commande cmd

``cmd << motDeFin``
    passe la console en mode saisie au clavier, ligne par ligne. Toutes ces lignes seront envoyées à la commande lorsque le mot-clé de fin "motDeFin" aura été écrit.

``cmd1 | cmd2``
    exécute cmd1 et envoie sa sortie en entrée de cmd2 ("pipe")

``cmd > /dev/null 2>&1``
    démarre le programme sans récupérer sa sortie ni ses erreurs, qui sont "jetées" dans /dev/null
