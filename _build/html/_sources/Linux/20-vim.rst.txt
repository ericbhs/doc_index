=============================
VIM : éditeur de texte avancé
=============================

``vim``
    lancer vim

``vimtutor``
    lancer le tutoriel vim

Modes de VIM
------------

    * **Mode interactif** : par défaut. Permet de se déplacer dans le texte, de supprimer une ligne, copier-coller du texte, rejoindre une ligne précise, annuler ses actions, etc
    * **Mode insertion** : appuyer sur ``i`` pour y entrer
    * **Mode commande** : l'activer en tapant ``:``

============ ===========================    
Racourcis    
========================================
``i``        | insérer du texte
``ESC``      | sortir du mode insertion
============ ===========================

|

============ ================================  
Commandes
=============================================
``:w``       | enregistrer le fichier (write)
``:q``       | quitter
``:wq``      | enregistrer puis quitter
============ ================================    

|

============ ================================    
Déplacements
=============================================  
``h``        | gauche
``j``        | bas
``k``        | haut
``l``        | droite
``0``        | aller en début de ligne (origin)
``$``        | aller en fin de ligne
``w``        | se déplacer de mot en mot (word)
============ ================================    

.. code-block:: bash

          ^
          k
    < h       l >
          j
          v

|

============ ================================    
Opérations standards
=============================================  
``x``        | effacer des lettres en mode interactif
``(nb)x``    | effacer nb lettres
``dw``       | effacer un mot
``dd``       | effacer une ligne
``d0``       | supprimer du curseur au début de la ligne
``d$``       | supprimer du curseur à la fin de la ligne
``yy``       | copier une ligne en mémoire
``p``        | coller (coller plusieurs fois : ex : 8p -> 8x)
``r``        | remplacer une lettre
``u``        | annuler des modifications
``G``        | aller à la ligne x (Go)
============ ================================    

|

=================================== ================================
Opérations avancées
====================================================================
``/``                               | passer en mode recherche (pour chercher un mot par ex)
                                    | ``n``   aller à la prochaine occurence
                                    | ``N``   aller à la précédente occurence
``:s/ancien/nouveau``               | remplacer le mot "ancien" par le mot "nouveau" :
``:s/ancien/nouveau``               | remplace la première occurrence de la ligne où se trouve le curseur ;
``:s/ancien/nouveau/g``             | remplace toutes les occurrences de la ligne où se trouve le curseur ;
``:#,#s/ancien/nouveau/g``          | remplace toutes les occurrences dans les lignes n° # à # du fichier ;
``:%s/ancien/nouveau/g``            | remplace toutes les occurrences dans tout le fichier. C'est peut-être ce que vous utiliserez le plus fréquemment.
``:r``                              | fusion de fichiers : insérer le contenu d'un fichier au curseur
=================================== ================================    

|

=================================== ================================      
Splitter écrans (viewports)
====================================================================
``:sp``                             | découper l'écran horizontalement
``:sp autrefichier``                | ouvrir autrefichier dans la seconde moitié de l'écran
``:vsp``                            | découper l'écran verticalement
``Ctrl + w`` puis ``Ctrl + ``w``    | navigue de viewport en viewport. Répétez l'opération plusieurs fois pour accéder au viewport désiré.
``Ctrl + w`` puis ``j``             | déplace le curseur pour aller au viewport juste en dessous. La même chose fonctionne avec les touches ``h``, ``k``, ``j`` et ``l`` que l'on utilise traditionnellement pour se déplacer dans Vim.
``Ctrl + w`` puis ``+``             | agrandit le viewport actuel.
``Ctrl + w`` puis ``-``             | réduit le viewport actuel.
``Ctrl + w`` puis ``=``             | égalise à nouveau la taille des viewports.
``Ctrl + w`` puis ``r``             | échange la position des viewports. Fonctionne aussi avec « R » majuscule pour échanger en sens inverse.
``Ctrl + w`` puis ``q``             | ferme le viewport actuel.
=================================== ================================  

|

=================================== ================================      
Zoom
====================================================================
``Ctrl + Shift`` + ``+``            | zoom
``Ctrl + Shift`` + ``-``            | dezoom
=================================== ================================
        

Options de vim
--------------

Rem : pour qu'elles soient retenues, créer un fichier .vimrc dans le répertoire personnel (un exemple de fichier se trouve dans /etc/vim -> vimrc)

=========================== ======================================================
``:set option``             | activer l'option en mode commande
``:set nooption``           | désactiver l'option en mode commande
``:set option?``            | connaitre l'état d'une option
``:set option=valeur``      | donner une valeur à une option
``:set syntax=ON``          | coloration synthaxique
``:set background=dark``    | coloration adaptée pour les fonds noirs
``:set number``             | affiche les n° de lignes
``:set showcmd``            | afficher la commande en cours
``:set ignorecase``         | ignorer la casse lors des recherches
``:set mouse=a``            | activer la souris
=========================== ======================================================

Gérer les plugins
-----------------

https://artisan.karma-lab.net/configurer-vim

* Création d'une arborescence pour les fichiers de config :

.. code-block:: bash

    $ cd
    $ mkdir -p .vim/{autoload,colors,syntax,plugin,spell,config}
    $ mv .vimrc .vim/vimrc
    $ ln -s .vim/vimrc .vimrc

(on crée un lien vers ``.vim/vimrc```)

* Installation de ``pathogen`` :

.. code-block:: bash

    $ cd ~/.vim
    $ git clone https://github.com/tpope/vim-pathogen.git pathogen
    $ cd autoload
    $ ln -s ../pathogen/autoload/pathogen.vim 
    
* Pour mettre à jour ``pathogen`` :

.. code-block:: bash

    $ cd ~/.vim/pathogen
    $ git pull

* Installer un plugin : exemple avec ``NERDTree``

.. code-block:: bash

    $ cd ~/.vim
    $ mkdir -p bundle
    $ cd bundle
    $ git clone https://github.com/scrooloose/nerdtree.git nerdtree
    
* Allure finale du dossier ``.vim`` (situé dans ``~/``)

.. code-block:: bash

    .vim
    ├── autoload
    │   └── pathogen.vim -> ../pathogen/autoload/pathogen.vim
    ├── bundle
    │   └── nerdtree
    │       ├──.......
    ├── colors
    ├── config
    ├── pathogen
    │   ├── autoload
    │   │   └── pathogen.vim
    │   ├── CONTRIBUTING.markdown
    │   └── README.markdown
    ├── plugin
    ├── spell
    ├── syntax
    └── vimrc (fichier)

* Allure du fichier ``vimrc`` :

.. code-block:: none

    1 set nocompatible
    2 
    3 runtime! config/**/*.vim
    4 
    5 set number
    6 
    7 " Initialisation de pathogen
    8 call pathogen#infect()
    9 call pathogen#helptags()
    10 

* Pour démarrer NerdTree : taper ``:NERDTree`` en mode interactif