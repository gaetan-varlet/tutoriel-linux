# Tutoriel Linux

## Raccourcis utiles
- `Tab` permet de faire de l’auto-complétion
- `Ctrl + R` permet de faire une recherche parmi les commandes précédentes
- `Ctrl + C` arrête la commande en cours
- `Ctrl + D` fin de fichier
- `Ctrl + L` efface le contenu de la console
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
- `pwd` *Print Working Directory* c'est-à-dire afficher le dossier courant
- `which` donne l'emplacement d'une commande, par exemple `which pwd`
- `ls` *list* liste les fichiers et dossiers du répertoire courant. `ls /usr` liste les fichiers du répertoire *usr*.
  - `-a` ou `--all` affiche les fichiers et dossiers cachés
  - `-A` affiche tout comme `-a` sauf les dossiers *./* (dossier courant) et *../* (dossier parent)
  - `-F` indique le type d'élément (dossier, fichier, raccourci...)
  - `-l` liste détaillée (droits, nombre de liens physiques, nom du propriétaire, nom du groupe, taille du fichier en octets, date dernière modification, nom du fichier). Avec `lh`, le h pour *Human Readable* permet d'avoir la taille du fichier en Ko, Mo...
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
- `cat` affiche le contenu d'un fichier et peut en concaténer
  - `cat test.txt` affiche le contenu du fichier
  - `cat test.txt test2.txt` affiche le contenu des deux fichiers
  - `cat fichier1 fichier2 fichier3 > grosfichier` enregistre le contenu des trois fichiers dans un seul
  - pour écrire dans un fichier sur plusieurs lignes, par exemple 2 lignes :
    `cat > test.txt << FIN
    ligne1
    ligne2
    FIN`

- `more` et `less` pour afficher les gros fichiers. Ce sont des logiciels de pagination/visualisation de fichiers texte, on ne peut pas modifier les fichiers avec.
  - `more` est plus ancien, `less` plus récent et plus complet
  - `more fichier.txt` affiche le texte en remplissant un écran puis s'arrête. Pour continuer, il faut :
    - `Entrée` pour avancer ligne à ligne
    - `Espace` pour avancer page à page
    - `Q` pour sortir du mode de visualisation
    - `B` pour reculer page par page
    - une fois arrivé au bout du fichier, on sort du mode de visualisation
  - `less` est un autre logiciel de visualisation
    - mêmes commandes avec quelques avantages :
      - ne quitte pas le mode de visualisation à la fin du fichier
      - possibilité de naviguer avec les flèches du clavier
      - fonction de recherche `/maChaine`. Toutes les occurrences sont affichés en surbrillance. Naivguer avec `N` et `Maj + N` pour passer d'occurrence en occurrence.

- `touch monFichier` crée un fichier vide *monFichier* s'il n'existe pas, sinon modifie l'horodatage du fichier si le fichier existe
- `mkdir`, pour *Make Directory*, sert à créer un nouveau répertoire en spécifiant le nom de ce dernier ou en spécifiant le chemin complet
  - `mkdir monDossier` ou `mkdir monDossier monDossier2` pour en créer plusieurs à la fois
  - `mkdir -p monDossier1/monDossier2` avec l'option `-p` pour *parent* pour créer un dossier et un sous-dossier dedans
  - on peut utiliser l'option `-v` ou `--verbose` pour avoir des informations sur la création
  - pour gérer les espaces, 3 possibilités : `mkdir "Mes documents"`, `mkdir 'Mes documents'` ou `mkdir Mes\ documents`
- `tree` permet de voir l'arborescence dans le répertoire courant
  - `tree monDossier` permet de voir l'arborescence d'un sous-dossier du répertoire courant
  - `-d` n'affiche que les dossiers, `-a` affiche les dossiers et fichiers cachés
