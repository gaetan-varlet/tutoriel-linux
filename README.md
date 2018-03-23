# Tutoriels Linux

## Raccourcis utiles
- `Tab` permet de faire de l'autocomplétion
- `Ctrl + R` permet de faire une recherche parmi les commandes précédentes
- `Ctrl + C` arrête la commande en cours
- `Ctrl + D` fin de fichier
- `Ctrl + L` efface le contenu de la console
- `Shift + PgUp` et `Shift + PgDown` pour monter et descendre dans la console

- `Ctrl + A` ramène le curseur au début de la commande, `Ctrl + E` ou `Fin` ramène le curseur à la de la commande
- `Ctrl + U` supprime ce qui se trouve à gauche du curseur, `Ctrl + K` ce qui se trouve à droite
- `Ctrl + W` supprime le premier mot à gauche du curseur, utile pour supprimer ke paramètre à gauche du curseyr
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
