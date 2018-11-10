======================
Archiver et compresser
======================

fichier ``tar`` : archive permettant de regrouper plusieurs fichiers

``gzip``/``bzip2`` : pour compresser des fichiers (des tar par exemple)
    * ``gzip`` : c'est le plus connu et le plus utilisé ;
    * ``bzip2`` : il est un peu moins fréquemment utilisé. Il compresse mieux mais plus lentement que ``gzip``.

``tar -cvf nom_archive.tar nom_dossier/``
    créer une archive
    
	* ``-c`` : signifie créer une archive tar
	* ``-v`` : signifie afficher le détail des opérations
	* ``-f`` : signifie assembler l'archive dans un fichier.
    
Archiver
--------
	
``tar -tf archive.tar``
    afficher le contenu de l'archive sans l'extraire

``tar -rvf archive.tar fichier_supplementaire``
    ajouter un fichier à l'archive

``tar -xvf archive.tar``
    extraire les fichiers de l'archive
    
Compresser une archive
----------------------

``gzip archive.tar``
    compresse l'archive avec gzip -> ajoute un .gz à la fin (archive.tar.gz)

``gunzip archive.tar.gz``
    décompresse l'archive

``bzip2 archive.tar``
    idem avec ``bzip2``

``bunzip2 archive.tar.bz2``
    idem avec ``bzip2``
    
Archiver et compresser en une commande
--------------------------------------

``tar -zcvf archive.tar.gz tutoriels/``
    archive et compresse en une comande (ici avec ``gzip``)

``tar -zxvf archive.tar.gz``
    décompresse et désarchive en une commande

``tar -jcvf tutoriels.tar.bz2 tutoriels/``
    idem avec ``bzip2``

``tar -jxvf tutoriels.tar.bz2 tutoriels/``
    idem avec ``bzip2``
    
``tar -jxvf tutoriels.tar.bz2 tutoriels/``

    idem avec ``bzip2``
    
Afficher un fichier archivé sans le désarchiver
-----------------------------------------------

``zcat``, ``zmore`` & ``zless``

    afficher directement un fichier compressé (fichier simple, pas archive)

Fichiers ``.zip``
-----------------

``sudo apt-get install unzip``

    installer le décompresseur de zip

``unzip archive.zip``

    décompresser un zip

``unzip -l fichier.zip``

    afficher le contenu du fichier zip sans l'extraire

``sudo apt-get install zip``

    installer le compresseur de zip

``zip -r tutoriels.zip tutoriels/``

    Le -r demande à compresser tous les fichiers contenus dans le dossier tutoriels (sans ce paramètre, seul le dossier, vide, sera compressé !).

Fichiers ``.rar``
-----------------

``sudo apt-get install unrar``

``unrar e tutoriels.rar``
`   Non, vous ne rêvez pas, l'auteur du programme ne veut pas que l'on mette un tiret devant l'option e ! Il faut bien qu'il y ait des exceptions dans la vie. :-)

``unrar l tutoriels.rar``
    Pour lister le contenu avant décompression, utilisez l'option 

	**pas possible de créer des fichiers .rar (format propriétaire)**