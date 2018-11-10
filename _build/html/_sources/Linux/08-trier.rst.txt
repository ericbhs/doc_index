======================================
Extraire, trier et filtrer des données
======================================

``grep -i mot fichier``
    affiches les occurences de "mot" dans fichier sans faire attention à la casse.

``grep -n mot fichier``
    affiche les n° de ligne

``grep -v mot fichier``
    inversion de la recherche : "tout ce qui ne contient PAS mot"

``grep -r mot répertoire``
    rechercher dans tous les fichiers et sous-dossiers (équivalent à rgrep)

``grep "ma phrase contient des espaces" monFichier``

``grep -E mot fichier``
    grep avec expression régulière

    Expressions régulières :
        * ``.`` : Caractère quelconque
        * ``^`` : Début de ligne (cherche un mot placé en début de ligne)
        * ``$`` : Fin de ligne (cherche un mot placé en fin de ligne)
        * ``[]`` : Un des caractères entre les crochets
        * ``?`` : L'élément précédent est optionnel (peut être présent 0 ou 1 fois)
        * ``*`` : L'élément précédent peut être présent 0, 1 ou plusieurs fois
        * ``+`` : L'élément précédent doit être présent 1 ou plusieurs fois
        * ``|`` : Ou
        * ``()`` : Groupement d'expressions

``sort fichier``
    trier le contenu d'un fichier

``sort -o noms_tries.txt noms.txt``
    avec sortie vers noms_tries.txt

``sort -R fichier``
    trier aléatoirement

``sort -n fichier``
    trier des nombres (ne se bas pas sur l'alphabet, sinon : 1 123 23 ...)

``wc fichier.txt``
    renvoie un résultat type "a b c fichier.txt" où :
	* ``a`` : nb de lignes (``-l``)
	* ``b`` : nb de mots (``-w``)
	* ``c`` : nb d'octets (``-c``)
	
``wc -m fichier.txt``
    nb de caractères dans le fichier

``uniq fichier.txt``
    supprime les doublons

``uniq doublons.txt sans_doublons.txt``
    sort ça dans sans_doublons.txt

``uniq -c``
    compte le nb d'occurences
    
    ex :
        ``uniq -c doublons.txt``
    
    résultats :
    
    .. code-block:: bash
    
        1 Albert
        3 François
        1 Jean
        2 Marcel

``uniq -d fichier``
    uniquement les lignes en double

``cut -c 2-5 noms.txt``
    conserve uniquement les caractères 2 à 5 de chaque ligne

``cut -c -3 noms.txt``
    conserve uniquement les caractères 1 à 3 de chaque ligne

``cut -c 3- noms.txt``
    du n°3 au dernier de chaque ligne

``cut -d , -f 1 notes.csv``
    * ``-d`` : indique quel est le délimiteur dans le fichier (ici ',')
    * ``-f`` : indique le numéro du ou des champs à couper, cad que l'on garde (ici le 1er)
    
``cut -d , -f 1,3 notes.csv``
    garde les champs 1 ET 3

``cut -d , -f 1-3 notes.csv``
    garde les champs 1 à 3