# Tutoriel Linux

## Raccourcis utiles
- `Tab` permet de faire de l’auto-complétion
- `Ctrl + R` permet de faire une recherche parmi les commandes précédentes
- `Ctrl + C` arrête la commande en cours
- `Ctrl + D` fin de fichier
- `Ctrl + L` ou `clear` efface le contenu de la console
- `Shift + PgUp` et `Shift + PgDown` pour monter et descendre dans la console

- `Ctrl + A` ramène le curseur au début de la commande, `Ctrl + E` ou `Fin` ramène le curseur à la de la commande
- `Ctrl + U` supprime ce qui se trouve à gauche du curseur, `Ctrl + K` ce qui se trouve à droite
- `Ctrl + W` supprime le premier mot à gauche du curseur, utile pour supprimer ke paramètre à gauche du curseur
- `Ctrl + Y` permet de *coller* le texte *coupé* avec `Ctrl + U`, `Ctrl + K` ou `Ctrl + W`

## Les répertoires
- **/bin** pour *binaires* contient les commandes dont le système à besoin pour démarrer
- **/boot** est le répertoire où Linux range ce qu'il faut pour démarrer. Les fichiers *vmlinuz* sont les différents noyaux, on en utilise un seul à la fois
- **/dev** pour *device* ou *périphérique* en français, contient un fichier pour chaque périphérique
- **/etc** pour *Editable Text Configuration* ou *configuration éditable par texte*
- **/lib** pour *libraries* ou *bibliothèqes* contient les bibliothèques partagées par */bin* et */sbin*
- **/media** et **/mnt** sont les points de montage du système. **/run** est un ajout réent qui doit prendre la relève de **/media**. Les périphériques amovibles doivent être montés lors de leur insertion et démonter lorsqu'on l'enlève
- **/proc** et **/sys** contiennent un sytème de fichiers "volatile" qui fournit des infos sur le système
- **/root** est le répertoire de l'utilisateur *root*
- **/sbin** pour *system binaries* ou *binaires système* contient des exécutables pour l'administrateur comme partitionner ou formation des disques, configurer le réseau...
- **/usr** pour *Unix System Resources* contient tout ce qui n'est pas utile au fonctionnement minimal du système. Les applications se trouvent pour la plupart ici. */usr/bin* est équivalent à *C:\Program Files* de Windows.
- **/tmp** est le répertoire temporaire du système
- **/var** contient des fichiers variables, crées par des serivces, c'est-à-dire des logiciels qui tournent en tâche de fond

## Les types de fichier
- **répertoire** avec une barre oblique à la fin (couleur par défaut : bleu)
- **fichier régulier non exécutable** sans suffixe (couleur par défaut : noir ou blanc)
- **lien symbolique** avec un @ à la fin, équivalent du raccourci sous Windows  (couleur par défaut : turquoise)
- **fichier régulier exécutable** avec un * à la fin (couleur par défaut : vert)


## Les commandes de base

- `date` donne la date et l'heure
- `history` affiche la liste des commandes que l'on a saisi
  - `!num` permet de répéter une commande déjà effectuée, par exemple `!245`
- `pwd` pour *Print Working Directory* affiche le dossier courant
- `ls` pour *list*, liste les fichiers et dossiers du répertoire courant. `ls /usr` liste les fichiers du répertoire *usr*.
  - `-a` ou `--all` affiche les fichiers et dossiers cachés
  - `-A` affiche tout comme `-a` sauf les dossiers *./* (dossier courant) et *../* (dossier parent)
  - `-F` indique le type d'élément (dossier, fichier, raccourci...)
  - `-l` liste détaillée (droits, nombre de liens physiques, nom du propriétaire, nom du groupe, taille du fichier en octets, date dernière modification, nom du fichier). Avec `lh`, le h pour *Human Readable* permet d'avoir la taille du fichier en Ko, Mo...
  - `ls -l prefixe*` permet de lister seulement les fichiers commençant par *prefixe*
    - `-d` pour *Directory* qui affiche le répertoire au lieu d'afficher le contenu
  - `-t` trie par date de dernière modification. On voit en premier le dernier fichier modifié.
  - `-r` renverse l'ordre d'affichage des fichiers
  - exemple de combinaison des commandes : `ls -larth`
- `cd` *Change Directory*, c'est-à-dire changer de dossier. Sans paramètre, ramène dans le home personnel
  - chemin absolu : on part de la racine : `cd /home/gaetan/documents`
  - chemin relatif : on part du dossier courant. Exemple si on est dans */home/gaetan* : `cd documents`
  - `cd ..` pour remonter dans le dossier parent
- `du` *Disk Usage* informe sur la taille que les dossiers occupent.
  - à combiner avec `-h` : `du -h`
  - `-a` pour avoir la taille des dossiers ET des fichiers `du -ah`
  - `-s` pour avoir juste le total : `du -sh`

- `echo` affiche une ligne de texte et peut l'enregistrer dans un fichier
  - `echo Bonjour` affiche *Bonjour* dans la console
  - `echo Bonjour > test.txt` enregistre *Bonjour* dans un fichier *test.txt*. Si le fichier existe déjà, il est écrasé.
  - `echo Bonjour >> test.txt` ajoute une ligne au fichier *test.txt*
- `cat` affiche tout le contenu d'un fichier, et peut en concaténer
  - `cat test.txt` affiche le contenu du fichier
  - `cat -n test.txt` affiche le contenu du fichier avec les numéros de ligne
  - `cat test.txt test2.txt` affiche le contenu des deux fichiers
  - `cat fichier1 fichier2 fichier3 > grosfichier` enregistre le contenu des trois fichiers dans un seul
  - pour écrire dans un fichier sur plusieurs lignes, par exemple 2 lignes :
    `cat > test.txt << FIN
    ligne1
    ligne2
    FIN`

- `more` et `less` pour afficher les gros fichiers, page par page. Ce sont des logiciels de pagination/visualisation de fichiers texte, on ne peut pas modifier les fichiers avec.
  - `more` est plus ancien, `less` plus récent et plus complet
  - `more fichier.txt` affiche le texte en remplissant un écran puis s'arrête. Pour continuer, il faut :
    - `Entrée` pour avancer ligne à ligne
    - `Espace` pour avancer page à page
    - `Q` pour sortir du mode de visualisation
    - `B` pour reculer page par page
    - une fois arrivé au bout du fichier, on sort du mode de visualisation
  - `less` est un autre logiciel de visualisation
    - `=` permet de savoir à quelle ligne on est et à quel pourcentage du fichier
    - mêmes commandes avec quelques avantages :
      - ne quitte pas le mode de visualisation à la fin du fichier
      - possibilité de naviguer avec les flèches du clavier
      - fonction de recherche `/maChaine`. Toutes les occurrences sont affichés en surbrillance. Naivguer avec `n` et `N` pour passer d'occurrence en occurrence.

- `head` et `tail` permettent d'afficher le début et la fin d'un fichier, par défaut 10 lignes. On peut spéficier le nombre de lignes que l'on veut afficher.
  - `head -n 4 fichier` affiche les 4 premières lignes de *fichier*
  - `tail fichier` affiche les 10 dernières lignes du fichier
  - `tail -f fichier` pour *follow* permet d'afficher la fin du fichier au fur et à mesure de son évolution

- `touch monFichier` crée un fichier vide *monFichier* s'il n'existe pas, sinon modifie l'horodatage du fichier si le fichier existe
- `mkdir`, pour *Make Directory*, sert à créer un nouveau répertoire en spécifiant le nom de ce dernier ou en spécifiant le chemin complet
  - `mkdir monDossier` ou `mkdir monDossier monDossier2` pour en créer plusieurs à la fois
  - `mkdir -p monDossier1/monDossier2` avec l'option `-p` pour *parent* pour créer un dossier et un sous-dossier dedans
  - on peut utiliser l'option `-v` ou `--verbose` pour avoir des informations sur la création
  - pour gérer les espaces, 3 possibilités : `mkdir "Mes documents"`, `mkdir 'Mes documents'` ou `mkdir Mes\ documents`
- `tree` permet de voir l'arborescence dans le répertoire courant
  - `tree monDossier` permet de voir l'arborescence d'un sous-dossier du répertoire courant
  - `-d` n'affiche que les dossiers, `-a` affiche les dossiers et fichiers cachés

- `cp` pour *copy* permet de copier des fichiers et des répertoires
  - `cp fichier fichier2` copie le fichier dans le même répertoire
  - `cp fichier.txt /cheminDestination` copie le fichier dans un autre répertoire
  - `cp fichier.txt /dossier/fichier2.txt` copie le fichier dans un autre répertoire en le renommant
  - `cp -R Fichiers/ /tmp/` ou `cp -r Fichiers/ /tmp/` permet de copier un répertoire entier avec tout son contenu (`-R` pour *recursive*) dans le répertoire spécifié
  - `cp -R dossier/ copieDossier` permet de copier l'intégralité du répertoire dans un répertoire d'un autre nom
  - `cp -R dossier/ ../copieDossier` permet de copier l'intégralité du répertoire dans un répertoire d'un autre nom dans un autre endroit du système
- `mv` pour *move* permet de déplacer et renommer des fichiers et des répertoires
  - `mv fichier dossier/` déplace *fichier* dans *dossier*
  - `mv dossier1 dossier2/` déplace *dossier1* et son contenu dans *dossier2*
  - `mv dossier/fichier ./` déplace *fichier* qui est dans *dossier* dans le répertoire courant
  - `mv fichier fichierRenommé` renomme *fichier* en *fichierRenommé*, fonctionne aussi pour les dossiers
  - `mv fichier dossier/fichierRenommé` déplace et renomme le fichier en une seule commande

- `rm` et `rmdir` pour *remove* et *remove directory* permettent de supprimer des fichiers et des dossiers
  - `rm fichier` supprime *fichier* sans demande de confirmation, le fichier est perdu à jamais
  - `rm -i fichier` pour *interactive* demande une confirmation avant la suppression
  - `rm -f fichier` pour *force* force la suppression si la demande de confirmation est systématique, par exemple avec l'ajout d'un alias sur la commande `rm`
  - `rmdir dossier` supprime *dossier* seulement s'il est vide
  - `rm -r dossier` pour *recursive*, supprime *dossier* et tout son contenu

- `ln` permet de créer des liens (raccourcis) entre fichiers. Il existe 2 types de liens :
    - **liens physiques** : `ln fichier1 fichier2` crée *fichier2* qui partage le même inode que *fichier1*
      - `ls -i` permet d'afficher le numéro d'inode pour vérifier si les fichiers sont associés au même inode
      - Une modification dans l'un entraîne une modification dans l'autre. Si on supprime l'un des 2 fichiers, l'autre reste en place et le contenu est touhours le même. Il faut supprimer les 2 pour supprimer le contenu.
    - **liens symboliques** : `ln -s fichier1 fichier2` pour *symbolique*. Crée *fichier2* qui pointe sur **fichier1**.
      - ressemble davantage au "raccourci" sous Windows, c'est-à-dire qu'on crée un lien vers un autre fichier
      - on édite le même contenu dans *fichier1* et *fichier2*
      - fonctionnent sur des répertoires contrairement aux liens physiques qui ne fonctionnent que sur les fichiers
      - si on supprime *fichier2*, rien de mal. Si on supprime *fichier1*, *fichier2* pointe vers un fichier qui n'existe plus, on parle de *lien mort*.

- `alias` concerne les alias de commande, qui sont des raccourcis
  - `alias` permet de voir les alias existants
  - `alias rm='rm -i'` permet de créer un alias. Cette création n'est pas persistante, elle disparaît en fermant la console

- la documentation
  - `man` pour *manual* affiche le manuel d'une commande comme avec la commande *less* : `man mkdir`. `/test` pour rechercher *test* dans la documentation. La documentation *man* est aussi disponible sur internet
  - `apropos` permet de chercher les commandes en rapport à un terme, par exemple `apropos sound`
  - `--help` donne une information proche de celle de *man*, par exemple `mkdir --help`
  - `whatis` donne juste le nom de la commande pour comprendre ce qu'elle fait, par exemple `whatis mkdir`
  - `info` affiche un manuel en ligne encore plus complet que *man*, par exemple `info mkdir`

- les éditeurs de texte
  - Nano
  - Vim (vimtutor)
  - Emacs
