# Tutoriels Linux

## Raccourcis utiles
- `Tab` permet de faire de l'autocomplétion
- `Ctrl + R` permet de faire une recherche parmi les commandes précédentes
- `Ctrl + D` fin de fichier
- `Ctrl + L` efface le contenu de la console
- `Shift + PgUp` et `Shift + PgDown` pour monter et descendre dans la console

- `Ctrl + A` ramène le curseur au début de la commande, `Ctrl + E` ou `Fin` ramène le curseur à la de la commande
- `Ctrl + U` supprime ce qui se trouve à gauche du curseur, `Ctrl + K` ce qui se trouve à droite
- `Ctrl + W` supprime le premier mot à gauche du curseur, utile pour supprimer ke paramètre à gauche du curseyr
- `Ctrl + Y` permet de *coller* le texte *coupé* avec `Ctrl + U`, `Ctrl + K` ou `Ctrl + W`


## Les commandes de base

- `date` donne la date et l'heure
- `pwd` *Print Working Directory* c'est-à-dire afficher le dossier courant
- `which` donne l'emplacement d'une commande, par exemple `which pwd`
- `ls` liste les fichiers et dossiers du répertoire courant
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
