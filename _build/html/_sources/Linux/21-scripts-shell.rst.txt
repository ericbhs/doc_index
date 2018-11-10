=============
Scripts Shell
=============

.. contents:: :local:

Remarques générales
-------------------

* ici on utilisera bash
* Extension : ``fichier.sh``
* ajouter ``#!/bin/bash`` au début pour s'assurer qu'il est éxécuté avec bash et pas un autre shell
* comentaires : ``#``
* donner le droit "éxécutable" au script :
    ``chmod +x essai.sh``
* Exécuter le script :
    ``./essai.sh``
* Mode debug : ``bash -x``
    ``bash -x essai.sh``
* Pour éxécuter un script à n'importe quel endroit -> copier le script dans un des répertoires du ``PATH``
    ``echo $PATH`` pour voir où se trouvent les répertoires du PATH

Variables
---------
    **Attention pas d'espaces autour des ``=``**
    
``echo something``
    renvoie le paramètre something
``echo $something``
    pour afficher une variable dans un script (ajouter '$')
``echo -e "test\ntes2\n"``
    tient comptre des retours à la ligne ``\n``

Quotes
------

* **Simple quotes** : bash ne tient pas compte de la variable quand on utilise des simple quotes ``'...'``

.. code-block:: bash

    $ message='Bonjour tout le monde'
    $ echo 'Le message est : $message'
    Le message est : $message``
       
* **Double quotes** : bash tient compte de la variable quand on utilise des double quotes ``"..."``

.. code-block:: bash

    $ message='Bonjour tout le monde'
    $ echo "Le message est : Bonjour tout le monde"
    Le message est : $message

* **Back quotes** : bash éxécute ce qui se trouve dans les back quotes ```...```
    
.. code-block:: bash

    $ message=`pwd`
    $ echo "Vous êtes dans le dossier $message"
    Vous êtes dans le dossier /home/mateo21/bin


``read`` : Demander une saisie
------------------------------

* ``-p`` : demande un message de prompt
    
.. code-block:: bash

    $ read -p 'Entrez votre nom : ' nom prenom    
    $ echo "Bonjour $nom $prenom !"
    Entrez votre nom : Mathieu
    Bonjour Deschamps Mathieu !
    
* ``-n`` : nb max de caractères    

.. code-block:: bash

    $ read -p 'Entrez votre login (5 caractères max) : ' -n 5 nom 
    $ echo "Bonjour $nom !"
    
* ``-t`` : précise un temps max

.. code-block:: bash

    $ read -p 'Entrez le code de désamorçage de la bombe (vous avez 5 secondes) : '  -t 5 code
    $ echo -e "\nBoum !"      
    
* ``-s`` : ne pas afficher les caractères saisis

.. code-block:: bash

    $ read -p 'Entrez votre mot de passe : ' -s pass
    $ echo -e "\nMerci ! Je vais dire à tout le monde que votre mot de passe est $pass ! :)"
    
Opérations mathématiques
------------------------

.. code-block:: bash

    $ let "a = 5"
    $ let "b = 2"
    $ let "c = a + b"
    7
      
Remarque : on peut utiliser : ``let "a += 5"``
    
**Opérations utilisables :**

    * l'addition : ``+``
    * la soustraction : ``-``
    * la multiplication : ``*``
    * la division : ``/``
    * la puissance : ``**``
    * le modulo (renvoie le reste de la division entière) : ``%``
    
**Opérations sur des nombres décimaux** : cf commande ``bc``
    
Les variables d'environnement
-----------------------------

Elles sont disponibles tout le temps pour tous les scripts (variables globales) On les met en majuscules par convention.

Exemples :
    
        * ``SHELL`` : indique quel type de shell est en cours d'utilisation (sh, bash, ksh…) ;
        * ``PATH`` : une liste des répertoires qui contiennent des exécutables que vous souhaitez pouvoir lancer sans indiquer leur répertoire. Nous en avons parlé un peu plus tôt. Si un programme se trouve dans un de ces dossiers, vous pourrez l'invoquer quel que soit le dossier dans lequel vous vous trouvez ;
        * ``EDITOR`` : l'éditeur de texte par défaut qui s'ouvre lorsque cela est nécessaire ;
        * ``HOME`` : la position de votre dossier home ;
        * ``PWD`` : le dossier dans lequel vous vous trouvez ;
        * ``OLDPWD`` : le dossier dans lequel vous vous trouviez auparavant.

Pour en créer de nouvelles : ``export``

Les paramètres
--------------

``./script.sh param1 param2 param3``

Pour récupérer ces paramètres dans le script :
    * ``$#`` : contient le nombre de paramètres 
    * ``$0`` : contient le nom du script exécuté (ici ./variables.sh) 
    * ``$1`` : contient le premier paramètre 
    * ``$2`` : contient le second paramètre 
    * ...
    * ``$9`` : contient le 9e paramètre
            
Si on a plus de 9 variables : décaler l'ordre avec la commande ``shift`` . Exemple :

    Script :

    .. code-block:: bash

        echo "Le paramètre 1 est $1"
        shift
        echo "Le paramètre 1 est maintenant $1"
    
    A l'exécution

    .. code-block:: bash

        $ ./variables.sh param1 param2 param3
        Le paramètre 1 est param1
        Le paramètre 1 est maintenant param2
            
Les Tableaux
------------

    * Définir un tableau :
        ``tableau=('valeur0' 'valeur1' 'valeur2')``
        
    * Accéder à une case particulière :
        ``${tableau[2]}``
        
    * Définir le contenu d'une case :
        ``tableau[2]='valeur2'``
        
    * On peut sauter des cases :
    
    .. code-block:: bash
    
        tableau=('valeur0' 'valeur1' 'valeur2')
        tableau[5]='valeur5'
        echo ${tableau[1]}
        
    * Afficher l'ensemble d'une tableau :
        ``${tableau[*]}``
        
Les conditions
--------------

Synthaxe :
    
.. code-block:: bash

    if [ $1 = "Bruno" ]     # ou if [ $1 = Bruno" ]; then
    then
            echo "Salut Bruno !"
    elif [ $1 = "Michel" ]
    then
            echo "Bien le bonjour Michel"
    elif [ $1 = "Jean" ]
    then
            echo "Hé Jean, ça va ?"
    else
            echo "J'te connais pas, ouste !"
    fi
        
Tests sur les chaines de caractères
"""""""""""""""""""""""""""""""""""

Rappel : toutes les variables sont traitées comme des strings
        
``$chaine1 = $chaine2``
    Vérifie si les deux chaînes sont identiques. Notez que bash est sensible à la casse : « b » est donc différent de « B ».
    
    Il est aussi possible d'écrire ``==`` pour les habitués du langage C.

``$chaine1 != $chaine2``
    Vérifie si les deux chaînes sont différentes.

``-z $chaine``
    Vérifie si la chaîne est vide.

``-n $chaine``
    Vérifie si la chaîne est non vide.
            
            
Tests sur les nombres
"""""""""""""""""""""
        
``$num1 -eq $num2``
    Vérifie si les nombres sont égaux (equal). À ne pas confondre avec le « = » qui, lui, compare deux chaînes de caractères.

``$num1 -ne $num2``
    Vérifie si les nombres sont différents (nonequal).
    
**Encore une fois, ne confondez pas avec ``!=`` qui est censé être utilisé sur des chaînes de caractères.**

``$num1 -lt $num2``
    Vérifie si num1 est inférieur ( < ) à num2 (lowerthan).

``$num1 -le $num2``
    Vérifie si num1 est inférieur ou égal ( <= ) à num2 (lowerorequal).

``$num1 -gt $num2``
    Vérifie si num1 est supérieur ( > ) à num2 (greaterthan).

``$num1 -ge $num2``
    Vérifie si num1 est supérieur ou égal ( >= ) à num2 (greaterorequal).
    
Tests sur les fichiers
""""""""""""""""""""""
    
``-e $nomfichier``
    Vérifie si le fichier existe.

``-d $nomfichier``
    Vérifie si le fichier est un répertoire. N'oubliez pas que sous Linux, tout est considéré comme un fichier, même un répertoire !

``-f $nomfichier``
    Vérifie si le fichier est un… fichier. Un vrai fichier cette fois, pas un dossier.

``-L $nomfichier``
    Vérifie si le fichier est un lien symbolique (raccourci).

``-r $nomfichier``
    Vérifie si le fichier est lisible (r).

``-w $nomfichier``
    Vérifie si le fichier est modifiable (w).

``-x $nomfichier``
    Vérifie si le fichier est exécutable (x).

``$fichier1 -nt $fichier2``
    Vérifie si fichier1 est plus récent que fichier2 (newerthan).

``$fichier1 -ot $fichier2``
    Vérifie si fichier1 est plus vieux que fichier2 (olderthan).
            
Plusieurs tests : ``&&`` et ``||``
""""""""""""""""""""""""""""""""""

Exemple :

.. code-block:: bash

    if [ $# -ge 1 ] && [ $1 = 'koala' ]
    then
            echo "Bravo !"
            echo "Vous connaissez le mot de passe"
    else
            echo "Vous n'avez pas le bon mot de passe"
    fi
        
Test inversé : ``not``
""""""""""""""""""""""

Exemple :

.. code-block:: bash

    if [ ! -e fichier ]
    then
            echo "Le fichier n'existe pas"
    fi
        
Switch case
-----------

Exemple :

.. code-block:: bash

    case $1 in
            "Bruno")
                    echo "Salut Bruno !"
                    echo "tu vas bien ?"
                    ;;
            "Michel")
                    echo "Bien le bonjour Michel"
                    ;;
            "Jean")
                    echo "Hé Jean, ça va ?"
                    ;;
            *)
                    echo "J'te connais pas, ouste !"
                    ;;
    esac
            
Exemple 2 : avec des ou (attention : ``|`` et pas ``||``)
 
.. code-block:: bash

    case $1 in
            "Chien" | "Chat" | "Souris")
                    echo "C'est un mammifère"
                    ;;
            "Moineau" | "Pigeon")
                    echo "C'est un oiseau"
                    ;;
            *)
                    echo "Je ne sais pas ce que c'est"
                    ;;
    esac

Les boucles
-----------

Boucle ``while``
""""""""""""""""

Exemple :

.. code-block:: bash

    # La réponse est vide ? Différente de "oui" ?
    while [ -z $reponse ] || [ $reponse != 'oui' ]
    do
            read -p 'Dites oui : ' reponse
    done
            
Boucle ``until``
""""""""""""""""

``while`` s'exécute tant que la condition est vraie, ``until`` jusqu'à ce qu'elle le soit

Exemple : 

.. code-block:: bash

    # Boucle jusqu'à ce que la réponse soit non vide et qu'elle soit "oui"
    until [ -n $reponse ] && [ $reponse == 'oui' ]  
    do
            read -p 'Dites oui : ' reponse
    done        
    
Boucle ``for``
""""""""""""""

Exemple :

.. code-block:: bash

   for variable in 'valeur1' 'valeur2' 'valeur3'
    do
            echo "La variable vaut $variable"
    done

Exemple 2 :

.. code-block:: bash

    liste_fichiers=`ls`

    for fichier in $liste_fichiers
    do
            echo "Fichier trouvé : $fichier"
    done

Exemple 3 :

.. code-block:: bash

    liste_fichiers=`ls`

    for fichier in $liste_fichiers
    do
            echo "Fichier trouvé : $fichier"
    done

Exemple 4 : renommer chacun des fichiers du répertoire actuel en leur ajoutant un suffixe -old par exemple

.. code-block:: bash

    for fichier in `ls`
    do
            mv $fichier $fichier-old
    done
    
Exemple 5 : pour simuler une boucle for plus classique (seq génère tous les nombres allant du premier paramètre au dernier paramètre)

.. code-block:: bash

    for i in `seq 1 10`;
    do
            echo $i
    done
    
Remarque : pour aller de 2 en 2 : ``seq 1 2 10``
            
Les fonctions
-------------

Déclarer une fonction : 2 possibilités

.. code-block:: bash

    maFonction ()
    {
            bloc d’instructions 
    }
    
ou :

.. code-block:: bash

    function maFonction
    {
            bloc d’instructions 
    }
        
Appeler une fonction :

.. code-block:: bash

    maFonction      # tout simplement ;)
