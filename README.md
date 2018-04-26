# Tutoriel Linux

## Raccourcis utiles
- `Alt + Ctrl + T` permet d'ouvrir un terminal
- `Ctrl + D` fin de fichier, ou `exit`. ferme le terminal
- `Tab` permet de faire de l’auto-complétion
- `Ctrl + R` permet de faire une recherche parmi les commandes précédentes
- `Ctrl + C` arrête la commande en cours
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
- `gucharmap` affiche la table de caractères
- `history` affiche la liste des commandes que l'on a saisi
  - `!num` permet de répéter une commande déjà effectuée, par exemple `!245`
- `pwd` pour *Print Working Directory* affiche le dossier courant
- `ls` pour *list*, liste les fichiers et dossiers du répertoire courant. `ls /usr` liste les fichiers du répertoire *usr*.
  - `-a` ou `--all` affiche les fichiers et dossiers cachés
  - `-A` affiche tout comme `-a` sauf les dossiers *./* (dossier courant) et *../* (dossier parent)
  - `-F` indique le type d'élément (dossier, fichier, raccourci...)
  - `-l` liste détaillée (droits, nombre de liens physiques, nom du propriétaire, nom du groupe, taille du fichier en octets, date dernière modification, nom du fichier). Avec `lh`, le h pour *Human Readable* permet d'avoir la taille du fichier en Ko, Mo...
  - `ls -l prefixe*` permet de lister seulement les fichiers commençant par *prefixe*
  - `-d` pour *Directory* qui affiche le répertoire au lieu d'afficher le contenu. Pour afficher les informations détailles du répertoire sans son contenu : `ls -ld`
  - `-t` trie par date de dernière modification. On voit en premier le dernier fichier modifié.
  - `-r` renverse l'ordre d'affichage des fichiers
  - `-R` pour *recursive*, affiche les sous-dossiers et leur contenu
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
    - **liens physiques** : `ln fichier1 fichier2` crée *fichier2* qui partage le même inode (contenu du fichier) que *fichier1*
      - `ls -i` permet d'afficher le numéro d'inode pour vérifier si les fichiers sont associés au même inode
      - Une modification dans l'un entraîne une modification dans l'autre. Si on supprime l'un des 2 fichiers, l'autre reste en place et le contenu est toujours le même. Il faut supprimer les 2 pour supprimer le contenu.
    - **liens symboliques** : `ln -s fichier1 fichier2` pour *symbolique*. Crée *fichier2* qui pointe sur **fichier1**.
      - ressemble davantage au "raccourci" sous Windows, c'est-à-dire qu'on crée un lien vers un autre fichier
      - on édite le même contenu dans *fichier1* et *fichier2*
      - fonctionnent sur des répertoires contrairement aux liens physiques qui ne fonctionnent que sur les fichiers
      - si on supprime *fichier2*, rien de mal. Si on supprime *fichier1*, *fichier2* pointe vers un fichier qui n'existe plus, on parle de *lien mort*

- `alias` concerne les alias de commande, qui sont des raccourcis
  - `alias` permet de voir les alias existants
  - `alias rm='rm -i'` permet de créer un alias. Cette création n'est pas persistante, elle disparaît en fermant la console

- la documentation
  - `man` pour *manual* affiche le manuel d'une commande comme avec la commande *less* : `man mkdir`. `/test` pour rechercher *test* dans la documentation. La documentation *man* est aussi disponible sur internet
  - `apropos` permet de chercher les commandes en rapport à un terme, par exemple `apropos sound`
  - `--help` donne une information proche de celle de *man*, par exemple `mkdir --help`
  - `whatis` donne juste le nom de la commande pour comprendre ce qu'elle fait, par exemple `whatis mkdir`
  - `info` affiche un manuel en ligne encore plus complet que *man*, par exemple `info mkdir`

- rechercher des fichiers
  - `locate fichier` pour une recherche rapide sur la base de données des fichiers qui est mise à jour toutes les 24 heures. Pour la mettre à jour, lancer la commande `sudo updatedb`
  - `find` pour une recherche approfondie, en parcourant les fichiers sur le disque, ce qui peut être long. La commande s'utilise avec des paramètres `find "où" "quoi" "que faire avec"`. Seul *"quoi"* est obligatoire.
    - *où* est le dossier dans lequel on fait la recherche, ainsi que tous ses sous-dossiers. Si non renseigné, recherche dans le dossier courant
    - *quoi* fichier ou dossier à rechercher, par nom, date de création, taille...
    - *que faire avec* on peut faire un post-traitement. Par défaut, la commande affiche la liste des fichiers trouvés, mais d'autres actions sont possibles
    - `-iname` option qui permet d'ignorer la casse pour faire la recherche, par exemple `find /etc/ -iname 'readme'`
    - exemples :
      - `find -name "README.md"` recherche un fichier dans le répertoire courant qui s'appelle exactement *README.md*. On peut utiliser l'étoile pour rechercher des noms incomplets, par exemple : `find -name "READM*"`
      - `find /var/log/ -name "syslog"`
      - `find /etc -type d` permet d'afficher tous les répertoires et sous-répertoires du dossier
      - `find -size +10M` permet de rechercher les fichiers de plus de 10Mo. On peut utiliser le **-** au lieu de **+**, et le **k** ou le **G** à la place du **M**
      - `find -name "*.md" -atime 6` recherche les fichiers au format markdown modifié il y a moins de 7 jours (0 pour 1 jour). On peut enlever le *-* pour modifié exactement il y a *x* jours
      - `-type d` et `-type f` permet de limiter la recherche aux répertoires ou aux fichiers, par exemple `find -name "syslog" -type d`
      - `find -name "README.md" -print` permet d'afficher les résultats, ce qui correspond au résultat par défaut `find -name "README.md"`
      - `-printf` permet de formater le résultat affiché, par exemple `find -name "README.md" -printf "%p - %u\n"`
      - `-delete` permet de supprimer les fichiers trouvés, par exemple `find -name "README.md" -delete`
      - `-exec`, permet d'appeler une commande qui effectuera une action sur chacun des fichiers trouvés
        - `find /bin -size +200k -exec ls -l \{} \;` permet d'effectuer un `ls -l` sur les résultats de la recherche. {} symbolise le résultat de la recherche
        - `find /bin -size +200k | xargs ls -l`. `xargs` sert à construire et exécuter des lignes de commande à partir de l’entrée standard

- manipulations dans les fichiers
  - `awk` est un langage de traitement de lignes qui sert à manipuler des fichiers textes

  - `grep` permet de filtrer des données
    - `grep texte fichier` permet de chercher *texte* dans *fichier*, par exemple `grep alias .bashrc` permet de chercher le mot *alias* dans le fichier *.bashrc* et affiche toutes les lignes du fichier comportant ce mot
    - `-i` pour ne pas tenir compte de la casse, `grep -i texte fichier`
    - `-n` pour afficher les numéros de lignes
    - `-v` permet d'inverser la recherche et d'afficher uniquement les lignes qui ne contiennent pas le mot recherché
    - `-c` permet de compter le nombre de lignes au lieu de les afficher
    - `-r` permet de faire une recherche récursive dans tous les sous-dossiers et fichiers, par exemple `grep -r machaine dossier/`. Le nom du fichier où la chaîne a été trouvé s'affiche au début de la ligne
    - `-E` permet d'utiliser des expressions régulières
      - on peut utiliser `egrep` à la place de `grep -E`
      - `-E` n'est pas obligatoire car les expressions régulières sont activées de base sur Linux. C'est utile sur les autres systèmes Unix
      - `.` caractère quelconque, `^` début de ligne, `$`fin de ligne, `[]` un des caractères entre les crochets, `?` l'élément précédent est optionnel (peut être présent 0 ou 1 fois), `*` l'élément précédent peut être présent 0, 1 ou plusieurs fois, `+` l²'élément précédent doit être présent 1 ou plusieurs fois, `|` ou, `()` groupement d'expressions
      - par exemple `grep -E ^alias .bashrc` pour rechercher le mot alias uniquement en début de ligne
      - `grep -E [Aa]lias .bashrc` renvoie les lignes qui contiennent *alias* ou *Alias*
      - `grep -E [0-4] .bashrc` renvoie les lignes qui contiennent un chiffre entre 0 et 4

  - `sort` permet de trier les lignes
    - `sort fichier` trie les lignes du fichier par ordre alphabétique et affiche le résultat dans la console, en ignorant la casse
    - `-o` permet d'écrire le résultat dans un fichier : `sort -o resultatTrié fichierATrier`
    - `-r` permet de trier en ordre inverse, `sort -r fichier`
    - `-R` permet de trier aléatoirement
    - `-n` permet de trier des nombres. Sans cette option, ils sont triés alphabétiquement donc par exemple 150 serait avant 18

   - `wc` pour *word count* permet de compter le nombre de lignes, de mots, de caractères, d'octets
    - `wc fichier` retourne le nombre de lignes, de mots et d'octets
    - `-l` retourne le nombre de lignes, `wc -l fichiers`
    - `-w` retourne le nombre de mots
    - `-c` retourne le nombre d'octets
    - `-m` retourne le nombre de caractères

  - `uniq` permet de supprimer les doublons (lignes identiques) seulement si elles se suivent, il faut donc travailler sur un fichier trié
    - `uniq fichier` affiche dans la console la liste des lignes sans doublons
    - `uniq fichierATraiter fichierSansDoublons` enregistre le résultat dans un fichier
    - `-c` compte le nombre d'occurence, affiche devant chaque ligne le nombre de fois qu'elle est présente dans le fichier, par exemple `uniq -c fichier`
    - `-d` affiche uniquement les lignes présentes plusieurs fois

  - `cut` permet de couper les lignes d'un fichier afin de conserver uniquement une partie de chaque ligne
    - `-c` pour couper selon le nombre de caractères. `cut -c 2-5 noms.txt` affiche les caractères 2 à 5 de chaque ligne, `cut -c -3` du 1er au 3 et `cut -c 3-` du 3e au dernier
    - couper selon un délimiteur, `-d` pour préciser le délimiteur, `-f` pour indiquer le numéro du ou des champs à couper. `cut -d , -f 1 fichier` conserve le 1er champ de chaque ligne, `-f 2-4` conserve les champs 2, 3 et 4, `-f 1,3` les champs 1 et 3


## Les éditeurs de texte
Il en existe plusieurs. Les plus connus sont Nano, Vim et Emacs.
- Nano
  - éditeur de texte simple comparé à Vim et Emacs
  - `nano` pour lancer l'éditeur vide
  - `nano fichier` lance l'éditeur en ouvrant le fichier
  - `-m` pour autoriser l'utilisation de la souris
  - `-i` pour l'indentation automatique, c'est-à-dire que la tabulation de la ligne précédente sera respecté lorsqu'on va à la ligne
  - Nano se configure dans le fichier *.nanorc*, situé à la racine du home pour son propre fichier de configuration (*/home/user/.nanorc*), où dans le fichier *nanorc* situé dans le dossier etc (*/etc/nanorc*). Ce dernier nécessite d'être en root pour le modifier. Il contient déjà plusieurs options mises en commentaires pour l'exemple

- Emacs : puissant éditeur de texte développé par Richard Stallman, le fondateur du projet GNU

- Vim : autre puissant éditeur de texte généralement disponible par défaut sur Linux
  - Vi existe en plusieurs versions : *vi* , le clone *elvis*, *vim* (VI iMproved, version améliorée de Vi),ou encore *gvim* dotée d'une interface graphique
  - Vimtutor pour apprendre à s'en servir


## Configuration de la console

Il faut modifier le fichier *.bashrc* personnel situé dans le répertoire personnel, ou le fichier *bashrc* global situé dans le répertoire */etc/bash.bashrc*. On peut par exemple personnaliser l'invite de commande, ou aussi y créer des alias qui sont persistants.

Il existe également un fichier *~/.profile* et un fichier */etc/profile* qui est lu dans les consoles où on se logue (les consoles Alt+Ctrl+F1 à F6), alors que le *.bashrc* est lu dans les consoles où on ne se logue pas, comme les consoles en mode graphique.
Le *.profile* fait appel au *.bashrc* par défaut, donc faire des modifications dans le *.bashrc* modifiera les options pour les consoles avec et sans login.


## Les utilisateurs et les droits

Chaque personne à son propre compte utilisateur avec des droits limités. Il existe un super-utilisateur appelé *root* qui a tous les droits, qui ne doit servir que rarement, lorsque c'est nécessaire.

- `sudo` pour *Substitute User DO* ou encore faire en se substituant à l'utilisateur, permet de devenir *root temporairement* le temps d'exécuter une commande en faisant `sudo commande`
- `sudo su` pour *switch user*, permet de devenir root et de le rester dans Ubuntu
  - `su -` est suffisant dans les autres distributions, le tiret rend accessible certains programmes destinés seulement à root, et nous place dans le dossier personnel de root (*/root*)
  - le symbole `#` à la fin de l'invite de commandes indique que l'on est devenu super-utilisateur
  - `exit` permet de quitter le *mode root*, permet aussi de fermer la console dans une session normale
  - `su - test` permet de se connecter avec le compte utilisateur *test*, le tiret indique que l'on souhaite utiliser ses variables d'environnement
- `whoami` permet de savoir avec quel utilisateur on est connecté
- `id` permet d'afficher l'UID (User Identification), le GID (Group Identification) et la liste de groupe secondaires de l'utilisateur connecté, par exemple affiche `uid=1000(gaetan) gid=1000(gaetan) groupes=1000(gaetan),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),113(lpadmin),130(sambashare)`
  - `id user` affiche les mêmes informations pour l'utilisateur *user*
  - `id -u` affiche uniquement le numéro uid
  - `id -g` affiche uniquement le numéro gid
  - `id -gn` affiche uniquement le nom du groupe
  - `id -Gn` ou `groups` affiche les noms des groupes dont l'utilisateur est membre
- `finger user` affiche les données GECOS de *user*, c'est-à-dire son login, son nom, son home, son shell, etc...
- le fichier **/etc/passwd** contient les informations des utilisateurs concernant leur connexion, par exemple : `gaetan:x:1000:1000:Gaëtan Varlet,,,:/home/gaetan:/bin/bash`.
  - utilisateur root, uid=0
  - utilisateurs système, uid compris entre 1 et 99
  - utilisateurs normaux avec uid supérieur ou égal à 1000
- les mdp sont dans le fichier **/etc/shadow**, uniquement accessible par root

### Gestion des utilisateurs
- commandes réservés à root
- `adduser` permet d'ajouter un utilisateur, avec au minimum le nom d'utisateur à créer, par exemple `adduser louis`
  - répertoire personnel est créé
  - on doit choisir un mot de passe
- `passwd` permet de changer le mot de passe du compte en paramètre, par exemple `passwd louis`
  - sans paramètre, c'est le mdp de l'utilisateur connecté que l'on modifie
- `deluser` permet de supprimer un compte, par exemple `deluser louis`
  - ne supprime pas le répertoire personnel. Si on souhaite le faire, ajouter l'option `--remove-home`, par exemple `deluser --remove-home louis` ou encore `userdel -r louis`
- `adduser` et `deluser` n'existent que sous Debian et ses descendants dont Ubuntu. Ailleurs, il faut utiliser les commandes Unix traditionnelles `useradd` et `userdel` qui font la même chose de manière plus basique, par exemple il faut appeler `passwd` pour définir un mdp et activer le compte

### Gestion des groupes
- chaque utilisateur appartient à un groupe. Par défaut, un groupe du même nom que l'utilisateur est créé
- `addgroup` permet de créer un groupe, par exemple `addgroup famille`
- `delgroup` permet de supprimer un groupe, par exemple `delgroup famille`
- `usermod` permet de modifier un utilisateur
   - `-l` renomme l'utilisateur sans renommer son répertoire personnel
   - `-g` change de groupe, par exemple `usermod -g famille louis` pour mettre Louis dans le groupe famille et `usermod -g louis louis` pour le remettre dans le groupe louis
   - `-G` permet à un utilisateur d'avoir plusieurs groupes, par exemple `usermod -G famille,amis louis`. L'utilisateur ne sera plus dans les groupes dans lesquels il était avant.
   - `-a` permet d'ajouter des groupes à un utilisateur sans perdre les groupes auxquels il appartient, par exemple `usermod -aG famille louis`
- `gpasswd -d` permet de supprimer l'appartenance d'un utilisateur à un groupe, par exemple `gpasswd -d louis audio`
- le fichier **/etc/group** contient la liste des groupes avec leur GID et la liste de des membres des groupes
- `addgroup` et `delgroup` n'existent que sous Debian et ses dérivés. Les commandes traditionnelles sont `groupadd` et `groupdel` qui offrent moins d'options

### Gestion des propriétaires d'un fichier
- seul l'utilisateur root peut changer le propriétaire d'un fichier
- `chown` pour *change owner*, permet de changer le propriétaire d'un fichier, en renseignant le nom du nouveau propriétaire et le nom du fichier, par exemple `chown louis fichier`. Cela ne change pas le groupe du fichier
  - `chown louis:famille fichier` permet de changer le propriétaire et le groupe en même temps
  - `-R` pour *recursive* permet d'affecter tous les sous-dossiers et fichiers contenu dans le dossier, par exemple `chown -R louis:louis /home/gaetan/dossier/`
- `chgrp` permet de changer le groupe propriétaire du fichier, par exemple `chgrp famille fichier`

### Modifier les droits d'accès
- chaque fichier et dossier possède des droits : voir, modifier et exécuter
- la commande `ls -l` permet de voir les droits, il s'agit des 10 premiers caractères
  - le 1er **d** pour *directory* si c'est un dossier, **l** pour *link* ou **-** si c'est un fichier
  - 3 triplets qui correspondent aux droits de l'utilisateur, du groupe et des autres. Un triplet correspond à **rwx** pour *read*, *write* et *execute* Ce dernier n'est utile que pour les fichiers exécutables (programmes et scripts).
  - si la lettre apparaît, c'est que le droit existe. S'il y a un tiret à la place, c'est qu'il n'y a aucun droit.
  - si c'est un dossier, *x* indique qu'on peut se placer dans le répertoire avec la commande `cd`, et voir son contenu si on a les droits en lecture dessus *r*.
- les droits de modification donnent aussi les droits de suppression
- root à tous les droits
- `chmod` permet de modifier les droits d'accès. Pas besoin d'être root, il suffit d'être propriétaire du fichier pour modifier les droits d'accès
- plusieurs méthodes d'attribution des droits
  - avec des chiffres : r=4, w=2, x=1. On les combine en additionnant, par exemple 6 donne les droits en lecture et écriture. ça va de 0 à 7. `chmod 777 fichier` donne tous les droits à tout le monde, `chmod 000 fichier` ne donne aucun droit à personne, sauf à root
  - avec des lettres : u=user, g=group, o=other. `+`=ajouter, `-`=supprimer et `=`=affecter. Par exemple `chmod g+w fichier` ajoute le droit en écriture au groupe
  - `-R` pour affecter récursivement tous les sous-dossiers et fichiers, par exemple `chmod -R 700 /home/louis`
- `umask` permet de voir les permissions par défaut. Un fichier créé ne peut avoir de base les droits d'exécution.


## Installer des programmes

- **paquet** : c'est un programme « prêt à l'emploi », l'équivalent des programmes d'installation sous Windows en quelque sorte. C'est une sorte de dossier zippé qui contient tous les fichiers du programme. Il se présente sous la forme d'un fichier *.deb* et contient toutes les instructions nécessaires pour installer le programme
- **dépendance** : un paquet peut avoir besoin de plusieurs autres paquets pour fonctionner, on dit qu'il a des dépendances
- **dépôt** : c'est le serveur sur lequel on va télécharger nos paquets

- programme graphique qui gère les paquets ou utiliser un programme en ligne de commande comme **apt-get** ou **aptitude**

- `apt-get update` met à jour le cache (liste des paquets existant proposé par le dépôt)
- `apt-cache search paquetRecherché` recherche le paquet que l'on veut télécharger si on ne connait pas le nom exact
- `apt-get install monPaquet` télécharge et installe le paquet
- `apt-get upgrade` met à jour tous les paquets installés, après avoir fait un `apt-get update` car *apt-get* comapre la version des paquets installés avec ceux présents dans le cache
- `apt-get autoremove monPaquet` permet de désinstaller un paquet et les dépendances devenues inutiles alors `apt-get remove monPaquet`ne supprime que le paquet en paramètre

**Programmes absents des dépôts officiels**
Si un programme est absent des dépôts officiels, on peut parfois trouver sur le site web du logiciel un paquetage **.deb**, spécifique à Debian et ses distributions dérivées. Par exemple, Red Hat utilise des **.rpm**.
- télécharger le *.deb* et double-cliquer dessus.
  - s'il n'y a pas d'erreurs, on peut installer le programme
  - sinon, le programme ne correspond pas à notre machine (32 bits au lieu de 64 bits par exemple) ou alors qu'il manque des dépendances qu'il faut installer manuellement

Si le *.deb* n'est pas disponible, il faut alors récupérer le code source du programme et le compiler pour avoir un exécutable pour sa machine
- le programme **build-essential** est nécessaire pour compiler le code source d'un programme
- trouver le code source sur le site du programme et le télécharger, et éventuellement le décompresser
  - exécuter le programme *configure* avec la commande `./configure`. Cela analyse notre ordinateur et vérifie si tous les outils nécessaires à la compilation du logiciel que l'on souhaite installer sont bien présents
  - s'il y a une erreur, il y a sûrement des paquets manquants. Il faut le trouver, l'installer puis relancer `./configure` jusqu'à qu'il n'y ait plus d'erreurs
  - une fois qu'il n'y a plus d'erreur, lancer la compilation avec la commande `make` qui crée l'exécutable
  - installer le programme avec la commande `sudo make install`. Une fois terminé, le programme est installé et on peut le lancer en écrivant son nom dans la ligne de commande
  - pour le désinstaller, exécuter la commande `sudo make uninstall` depuis le répertoire où il a été compilé. Si on supprime le répertoire avec le code source, on ne pourra plus lancer la commande de désinstallation


## Les flux de redirection

Au lieu d'afficher le résultat d'une commande dans la console (comportement par défaut), on peut le rediriger
- dans un fichier
- en entrée d'une autre commande pour effectuer des chaînes de commandes
- dans la "corbeille", `commande > /dev/null`, tout est supprimé immédiatement, si on ne veut ni l'afficher dans la console ni dans un fichier

- `> et >>` permettent de rediriger le résultat dans un nouveau fichier pour `>` et à la fin d'un fichier pour `>>`
  - `echo Bonjour` affiche *Bonjour* dans la console
  - `echo Bonjour > test.txt` enregistre *Bonjour* dans un fichier *test.txt*. Si le fichier existe déjà, il est écrasé
  - `echo Bonjour >> test.txt` ajoute une ligne au fichier *test.txt*.Si le fichier n'existe pas, il sera créé

- `2>, 2>> et 2>&1` permettent de rediriger les erreurs
  - toutes les commandes produisent deux flux de données : la **sortie standard** et la **sortie d'erreur**. Par défaut, les deux s'affichent dans la console
  - avec `> et >>`, seule la sortie standard est redirigée vers le fichier, les erreurs continuent à être affiché dans la console
  - `2>` permet de rediriger les erreurs dans un fichier à part, par exemple `ls -l /root/ > test 2> erreur` redirige la sortie standard dans le fichier *test* et la sortie d'erreur dans le fichier *erreur*
  - `2>>` permet d'ajouter les erreurs à la fin du fichier
  - `2>&1` permet de fusionner les sorties dans un seul fichier, par exemple `ls -l / > testFusion 2>&1`

- `< et <<` permet de lire depuis un fichier pour `<`, et de lire progressivement depuis le clavier pour `<<`
  - l'entrée d'une commande vient des paramètres de la commande, mais elle peut aussi venir d'un fichier ou d'une saisie au clavier
  - `cat < fichier` affiche le contenu de *fichier*. La commande *cat* reçoit le contenu du fichier qu'elle affiche, alors que la commande `cat fichier` reçoit le nom du fichier qu'elle doit d'abord ouvrir pour ensuite afficher son contenu. Le résultat est le même mais ce qui se passe derrière est différent
  - `<<` passe la console en mode saisie au clavier ligne par ligne. Toutes ces lignes seront envoyées à la commande lorsque le mot-clé de fin aura été écrit. Par exemple :
  `wc -m << FIN
  Combien de caractères dans cette phrase ?
  FIN`

- `|` permet de chaîner les commandes
  - connecter la sortie d'une commande à l'entrée d'une autre commande
  - exemple : `du | sort -nr | head` permet d'afficher les 10 dossiers les plus lourds triés par taille


## Surveiller l'activité du système

- `w` permet de voir qui est connecté et ce qu'ils font
  - l'heure, aussi accessible via `date`
  - l'uptime, aussi accessible via `uptime`, qui indique depuis combien de temps l'ordinateur n'a pas été redémarré
  - la charge, aussi accessible via `uptime` et `tload`. Il s'agit de la charge moyenne depuis 1, 5 et 15 minutes, plus précisément le nombre de processus qui réclament le processeur. La charge maximale correspond au nombre de processeur, au delà, il y a surcharge
  - la liste des personnes connectés sur la machine, accessible aussi via `who`

- `ps` et `top` pour lister les processus
  - un processus est un programme qui tourne en mémoire. Certains programmes ne font tourner qu'un processus, d'autres plusieurs comme Chrome qui crée un processus par onglet
  - `ps` permet d'avoir la liste statique des processus en cours
    - *PID* est l'identifiant du processus
    - par défaut, seul les processus lancés par l'utilisateur dans la console sont affichés
    - `ps -x` affiche l'ensemble des processus de l'utilisateur
      - `-a` ajoute ceux de tous les utilisateurs
      - `-u` donne des informations supplémentaires comme le propriétaire du processus, l'utilisation du processus et de la mémoire
    - `ps -ef` permet d'afficher tous les processus et `ps -ejH` de les afficher en arbre
  - `pstree`, ou `pstree | less` affiche l’organisation hiérarchique de tous les processus en cours du système
  - `top` permet d'avoir la liste dynamique des processus et permet de mesurer la consommation en ressources de chaque processus
    - affiche les processus trié sur le taux d'utilisation du processeur
    - `h` permet d'afficher l'aide

- `Ctrl + C` ou `kill` pour arrêter un processus
  - `Ctrl + C` permet d'arrêter un processus lancé en console
  - `kill` permet d'arrêter proprement un processus lancé en arrière-plan en indiquant son *PID*, par exemple `kill 12345`
    - `kill -9` permet de tuer un processus sans lui laisser le temps de s'arrêter proprement, s'il refuse de se fermer normalement. Par exemple `kill -9 12345`
    - `killall` permet de tuer tous les processus d'un même programme, par exemple `killall find`

- éteindre l'ordinateur
  - `halt`, `poweroff` et `reboot -p` arrêtent le système en tuant tous les processus sans prévenir personne
  - `reboot` redeméarre le système de la même manière
  - `shutdown` arrête ou redémarre le système proprement : `shutdown -h now` et `shutdown -r now`


## Exécuter des programmes en arrière-plan
- un **service**, ou **demon** est un processus qui s'exécute en arrière-plan plutôt que sous le contrôle direct d'un utilisateur
- `&` permet de lancer un processus en arrière-plan, par exemple `cp fichier copie &`
  - les messages renvoyés par les commandes s'affichent toujours dans la console. On peut donc les envoyer dans un fichier, par exemple `find / -name "*log" > sortiefind &`
- `nohup` permet de détacher le processus de la console. Si l'utilisateur se déconnecte ou si la console est fermée, le processus continuera. Exemple : `nohup fichier copie`
- `Ctrl+Z` met en pause un processus exécuté au premier plan, sans `&` donc
- `bg` pour *background*, passe le processus en pause en arrière-plan
- `jobs` permet de connaître les processus qui tournent en arrière-plan
- `fg` pour *foreground*, permet de reprendre un processus au premier plan
  - `fg` s'il y a un seul processus en arrière-plan listé dans *jobs*
  - `fg %x` s'il y a plusieurs processus en arrière-plan pour reprendre le processus *x*
- `screen` est un programme qui permet d'ouvrir plusieurs consoles virtuelles au sein d'une seule et même console, et d'exécuter facilement plusieurs processus en parallèle


## Exécuter des programmes à une heure différée

- `date` permet d'afficher la date
  - `date "+%H:%M:%S"` permet de personnaliser l'affichage
  - `sudo date MMDDhhmmYYYY` permet de modifier la date système
- `at` permet d'exécuter une commande plus tard une seule fois
  - 1) on indique quand on veut exécuter la commande, par exemple `at 18:17` ou `at 18:17 tomorrow` ou `at 18:17 04/12/18` (12 avril, attention à l'ordre MM/DD/YY) ou encore `at now +5 minutes` (minutes, hours, days, weeks, months, years)
  - 2) taper la ou les commandes que l'on veut exécuter à cette heure là
  - 3) faire `Ctrl + D`. Le symbole `<EOT>` s'affiche et nous donne le numéro de la tâche (job en anglais)
- `atq` permet d'avoir la liste des jobs en attente
- `atrm` permet de supprimer un job en attente, par exemple `atrm 5` pour supprimer le job n°5
- il est possible d'enchaîner des commandes :
  - avec le point-virgule, par exemple `touch fichier; rm fichier`
  - avec les `&&`, par exemple `touch fichier && sleep 10 && rm fichier`. Les instructions ne s'enchaîneront que si elles se sont correctement exécutées
- `sleep` permet de faire une pause, par exemple `touch fichier; sleep 10; rm fichier` ou une pause de 10 secondes aura lieu
  - on peut régler l'unité de sleep qui est par défaut la seconde : `m` pour minute, `h` pour heure et `d` pour jour. Exemple : `sleep 1m`
- `crontab` permet exécuter une commande régulièrement
  - `crontab` permet de lire et modifier un fichier appelé la **crontab**, qui contient la liste des programmes à exécuter régulièrement, et l'heure à laquelle ils soient exécutés
  - `-l` permet d'afficher la crontab, `-e` la modifier, `-r` la supprimer sans confirmation
  - syntaxe : `m h dom mon dow   command` pour minute (0-59), hour (0-23), day of month (1-31), month (1-12), day of week (0-6, 0=dimanche)
    - on peut mettre une étoile à la place d'un chiffre pour dire tous les chiffres
    - `3,5,10` pour les 3 valeurs, `3-7` pour les valeurs 3 à 7, `*/3` pour les multiples de 3, par exemple 0, 3, 6, 9...
  - le résultat de la commande n'apparaît pas dans la console, il est normalement envoyé par mail
    - le rediriger dans un fichier : `45 18 * * * touch /home/louis/fichier >> /home/louis/cron.log 2>&1`
    - le rediriger dans le trou noir pour suppression immédiate : `* * * * * commande > /dev/null 2>&1`
  - exemples :
    - `45 18 * * * commande` est exécuté tous les jours à 18h45
    - `0 0 * * 1 commande` tous les lundis à minuit (nuit de dimanche à lundi)
    - `0 4 1 * * commande` tous les premiers du mois à 4h
    - `0 4 * 12 * commande` tous les jours du mois de décembre
    - `* * * * *` toutes les minutes, c'est la fréquence minimale


## Archiver et compresser

- `tar` est un programme d'archivage. Il permet :
  - d'assembler des fichiers dans une archive
    - regroupement des fichiers dans un même dossier
    - création de l'archive tar : `tar -cvf nomArchive.tar nomDossier/`. `-c` pour la création de l'archive, `-v` pour l'affichage des détails de l'opération et `-f` pour assembler l'archive dans un fichier
  - d'afficher le contenu d'une archive sans l'extraire, par exemple `tar -tf archive.tar`
  - d'ajouter un fichier à une archive existante, par exemple `tar -rvf archive.tar nouveauFichier`
  - d'extraire les fichiers d'une archive, par exemple `tar -xvf archive.tar` avec `-x` pour *extract*. Le contenu de l'archive est extrait dans le répertoire courant

Les différents programmes de compression d'une archive
- **gzip** est le plus connu et le plus utilisé
  - `gzip archive.tar` compresse l'archive qui devient *archive.tar.gz*
  - `gunzip archive.tar.gz` décompresse l'archive qui redevient *archive.tar*
- **bzip2** compresse mieux mais plus lentement
  - `bzip2 archive.tar` compresse l'archive qui devient *archive.tar.bz2*
  - `bunzip2 archive.tar.bz2` décompresse l'archive qui redevient *archive.tar*
- **compress** n'est plus utilisé car moins performant que *gzip* et *bzip2*
- contrairement à *zip* et *rar*, *gzip* et *bzip2* ne peuvent compresser qu'un seul fichier à la fois, c'est pour cela qu'il faut créer une archive *tar* auparavant

Archiver et compresser en même temps avec *tar*
- avec *gzip*
  - `-zcvf` permet d'archiver et compresser, par exemple `tar -zcvf nomArchive.tar.gz nomDossier/`
  - `-zxvf` permet de décompresser, par exemple `tar -zxvf nomArchive.tar.gz`
- avec *bzip2*
  - `-jcvf` permet d'archiver et compresser, par exemple `tar -zcvf nomArchive.tar.bz2 nomDossier/`
  - `-jxvf` permet de décompresser, par exemple `tar -zxvf nomArchive.tar.bz2`

Lecture d'un fichier compressé
- on peut compresser directement un fichier en faisant `gzip fichier`
- si on veut le lire, par exemple en faisant `cat fichier`, des caractères bizarres s'affichent à cause de la compression. A la place, on peut utiliser *zcat*, *zmore* ou *zless* qui permettent de lire un fichier compressé. Exemple `zmore fichier`

Décompresser les *zip* et les *rar*
- `unzip` permet de décompresser un *.zip*
  - exemple `unzip archive.zip`
  - `-l` permet d'afficher le contenu sans l'extraire, par exemple `unzip -l archive.zip`
- `zip` permet de créer un *zip*, par exemple `zip -r dossier.zip dossier/`
- `unrar` permet de décompresser un *rar*
   - exemple `unrar e toto.rar` sans tiret devant le *e*
   - `unrar l toto.rar` permet d'afficher le contenu sans l'extraire
- il n'est pas possible gratuitement de créer des *rar* car c'est un format propriétaire. Le paquet *rar* est payant


## Les connexions à distance

### Les protocoles

- on peut configurer une machine Linux pour s'y connecter à distance à condition qu'elle reste allumée
- pour communiquer entre eux, deux ordinateurs doivent utiliser le même **protocole**
  - il en existe plein, par exemple *HTTP* pour s'échanger des pages web, *FTP* protocole de transfert de fichier, *IMAP* protocole pour s'échanger des emails...
  - **Telnet** est un protocole simple créé dans les années 80 pour échanger des messages en clair d'une machine à une autre, qui peuvent donc être interceptés et lus par n'importe qui
  - **SSH** est un protocole qui permet de chiffrer les échanges
    - création d'un tunnel sécurisé avec SSH (tout ce fait automatiquement) :
      - utilisation du chiffrement asymétrique pour s'échanger une clé de chiffrement symétrique :
        - le serveur envoie la clé publique en clair au client pour qu'il puisse chiffrer
        - le client génère une clé de chiffrement symétrique qu'il chiffre grâce à la clé publique qu'il a reçue, et l'envoi au serveur, qui déchiffre la clé reçue grâce à sa clé privée
        - ensuite, utilisation du chiffrement symétrique pour chiffrer tous les échanges car le chiffrement asymétrique est beaucoup plus lent que le chiffrement symétrique.
        - une fois le tunnel mis en place, le client peut se connecter au serveur avec son login et son mot de passe

### Transformer sa machine en serveur et s'y connecter en SSH²

- transformer son pc en serveur : il faut installer le paquet *openssh-server* `sudo apt-get install openssh-server`
  - normalement, le serveur SSH sera lancé à chaque démarrage
  - `sudo /etc/init.d/ssh start` permet de le lancer à tout moment
  - `sudo /etc/init.d/ssh stop` permet de l'arrêter à tout moment
  - au besoin, le fichier de configuration se trouve dans */etc/ssh/ssh_config*. Il faut ensuite recharger SSH avec la commande `sudo /etc/init.d/ssh reload` pour que les changements soient pris en compte

- se connecter via SSH à partir d'une machine Linux
  - `ssh login@ip` en remplaçant *login* par notre login et *ip* par l'adresse IP de notre ordinateur que l'on peut obtenir par exemple via le site *www.whatismyip.com* ou l'IP locale si on se connecte depuis un autre ordinateur sur le même reseau local
  - `ssh login@localhost` ou `ssh login@127.0.0.1` permet de se connecter depuis son propre PC
  - `exit` ou `logout` permet de se déconnecter
  - le port 22 est le port utilisé par défaut par SSH. Si le serveur tourne sur un autre port, il faut le préciser comme ceci : `ssh login@ip -p 12345` si le serveur  fonctionne sur le port 12345
  - le *fingerprint* du serveur, ou empreinte, est un numéro unique qui permet d'identifier le serveur. Si quelqu'un essaie de se faire passer pour le serveur, le fingerprint changera et on sera averti

- se connecter via SSH à partir d'une machine Windows
  - renseigner l'adresse IP dans *Host Name* et le port (22 par défaut)
  - lors de la première connexion, Putty nous demande une confirmation en nous donnant l'empreinte du serveur
  - le serveur demande le login et le mot de passe. La connexion est maintenant établie

### L'identification automatique par clé

- Les méthodes les plus utilisées pour s'authentifier auprès du serveur sont
  - l'authentification par mot de passe
  - l'authentification par clés publique et privée du **client**.
    - cette méthode évite de renseigner son mot de passe à chaque fois
    - la clé publique ainsi générée doit être envoyée sur le serveur, la clé privée reste sur le PC du client. La connexion se fait alors sans mot de passe et reste sécurisée

- Authentification par clé depuis Linux
  - générer une paire de clés publique/privée avec la commande `ssh-keygen -t rsa` sur le client
    - *rsa* étant un algorithme de chiffrement asymétrique, on peut aussi utiliser *dsa* qui est un autre algorithme de chiffrement
    - les clés sont enregistrées dans des fichiers. Laisser les valeurs par défaut, *~/.ssh/id_rsa.pub* pour la clé publique et *~/.ssh/id_rsa* pour la clé privée. Le dossier *.ssh/* contient aussi un fichier *known_hosts* qui est la liste des fingerprint que votre PC de client tient à jour
    - on nous demande une **passphrase** qui sert à chiffrer la clé privée pour plus de sécurité. On peut ne pas la renseigner si personne d'autre n'utilise le PC ou ne peut lire le fichier contenant la clé privée.
  - envoyer la clé publique au serveur, pour qu'il puisse chiffrer les messages qu'il nous envoi
    - `ssh-copy-id -i id_rsa.pub login@ip` avec le login et l'ip du serveur
    - on envoie la clé publique *id_rsa.pub* sur le serveur dans son fichier *authorized_keys*
    - on peut maintenant se connecter avec la commande `ssh login@ip`. Si on n'a pas mis de passphrase on est directement connecté, sinon il faut renseigner la passphrase
    - pour éviter de renseigner la passphrase à chaque fois, on peut utiliser **l'agent SSH** qui permet de la renseigner une seule fois. C'est un programme qui tourne en mémoire qui retient les clés privées pendant toute la durée de la session. Lancer le programme avec `ssh-add` sur le client, qui va lire notre clé privée et va nous demander notre passphrase pour la déchiffrer. On peut maintenant se connecter plusieurs fois sur le même serveur ou sur différents serveurs sans retaper le passphrase

- Authentification par clé depuis Windows avec Putty
  - même principe : générer une paire de clés publique/privée sur le client et envoyer la clé publique au serveur
  - générer la paire de clé avec *Puttygen* en laissant les valeurs par défaut.
    - on peut éventuellement renseigner une passphrase
    - enregistrer les clés dans des fichiers, par exemple *cle.pub* et *cle.ppk*
    - se connecter au serveur avec son login/mdp et ajouter la clé publique dans les clé autorisées à la fin du fichier : `cd .ssh` pour aller dans le dossier *.ssh* de notre dossier personnel puis `echo "cle_publique" >> authorized_keys`
    - se déconnecter pour configurer Putty pour se connecter avec la clé. Dans *Connection → SSH → Auth*, indiquer le chemin du fichier contenant la clé privée,  et dans *Connection → Data* renseigner le login dans *Auto-login username*
    - se connecter en cliquant sur Open, le login est déjà renseigné, il faut renseigner la passphrase
    - pour éviter de renseigner la passphrase à chaque fois, on peut utiliser **l'agent SSH Pageant** , installé avec Putty. Il est possible de le lancer automatiquement au démarrage. Cliquer sur *addkey*, préciser l'emplacement du fichier et renseigner la passphrase. Se connecter à un serveur en sélectionnant *Saved Sessions*


## Le transfert de fichiers

- `wget` permet de télécharger des fichiers en indiquant l'adresse HTTP ou FTP
  - exemple `wget https://thumbs.dreamstime.com/z/chat-mignon-2507126.jpg`
  - `-c` permet de reprendre un téléchargement arrêté si le bout de fichier téléchargé est toujours là : `wget -c adresseHttp`
  - `--background` permet de laner un téléchargement en tâche de fond (tout comme la commande *nohup*)

- `scp` pour *secure copy*, permet de copier des fichiers sur le réseau d'un ordinateur à un autre de manière sécurisée
    - `rcp` pour *remote copy* fait la même chose sans cryptage
    - syntaxe : `scp origine destination`, sous la forme `login@ip:nom_fichier`. Le login et l'IP sont facultatifs. S'ils sont absents, la commande considère que le fichier est sur notre ordinateur
    - exemple :
      - `scp louis@12.345.67.890:image.png copie.png` copie l'image sur l'ordinateur distant sur mon ordinateur sous le nom *copie.png*
      - `scp louis@12.345.67.890:image.png .` fait la même copie sans changer le nom du fichier, le `.` signifie répertoire courant
    - si le serveur SSH sur lequel on se connecte n'est pas sur le port par défaut (22), il faut indiquer le numéro de port avec `-P`. Par exemple `scp -P 12345 louis@12.345.67.890:image.png .` avec un P majuscule contrairement à la commande `ssh` qui utilise le p minuscule pour le port

- `ftp` et `sftp` permettent de transférer des fichiers
  - Le FTP pour *File Transfer Protocol* est un protocole permettant d'échanger des fichiers sur le réseau. Il est assez ancien (1985) et toujours utilisé à l'heure actuelle pour transférer des fichiers
  - On l'utilise pour télécharger depuis un serveur FTP public, notamment lorsqu'on clique sur un lien de téléchargement via un navigateur. La connexion se fait alors en **mode anonyme**. On l'utilise aussi pour transférer des fichiers vers un serveur FTP privé (et aussi télécharger). La connexion se fait donc en **mode authentifié**
  - **FileZilla** est un logiciel graphique qui permet de faire des transferts de fichiers via FTP
  - `ftp adresseServeurFtp` permet de se connecter à un serveur FTP
    - exemple : `ftp speedtest.tele2.net` ou via un navigateur web `ftp://speedtest.tele2.net/`
    - sur les serveur public, le login est toujours **anonymous** et pour le mot de passe, tout fonctionne. On fait ensuite face à un prompt `ftp>`
  - les commandes sont pour la plupart les mêmes que celles qu'on connait : `ls` liste les fichiers du répertoire courant, `pwd` affiche le chemin du répertoire actuel, `cd` change de répertoire...
  - pour utiliser les commandes sur son poste, il faut ajouter un point d'exclamation au début, par exemple `!pwd` pour savoir dans quel répertoire on est sur notre ordinateur
  - `put` et `get` permettent d'envoyer un fichier vers le serveur et de télécharger un fichier depuis le serveur
    - exemple : `get fichier.zip` pour télécharger *fichier.zip*
  - `delete` permet de supprimer un fichier et non `rm`
  - `bye`, `exit`, `quit` et `Ctrl+D` permet de fermer la session
  - `sftp` est un FTP sécurisé contrairement à FTP ou les données circulent en clair
    -  repose sur SSH pour sécuriser la connexion : `sftp login@ip` et on nous demande ensuite notre mot de passe (ou connexion via clé publique/privée)
    - les commandes sont globalement les mêmes qu'avec `ftp`, sauf pour supprimer un fichier, il faut utiliser `rm` et non plus `delete`
    - par défaut, on utilise le port 22 comme pour SSH. Si le port est différent, il faut le préciser comme ceci : `sftp -oPort=27401 login@ip`

- `rsync` permet de synchroniser des fichiers pour une sauvegarde
   - permet d'effectuer une synchronisation entre deux répertoires, que ce soit sur le même PC ou entre deux ordinateurs reliés en réseau
   - utilisé pour effectuer des sauvegardes incrémentielles : *rsync* compare et analyse les différences entre deux dossiers puis copie uniquement les changements
   - `rsync -arv dossierASauvegarder/ backup/` fait une sauvegarde dans un autre dossier du même ordinateur
    - `-a` conserve les infos sur les fichiers (droits, date de modification...)
    - `-r` pour sauvegarder tous les sous-dossiers
    - `-v` mode verbeux pour afficher les détails
  - par défaut,`rsync` ne supprime pas les fichiers dans le répertoire de copie. Il faut ajouter l'option `--delete`. Exemple : `rsync -arv --delete dossierASauvegarder/ backup/`
  - sauvegarder les fichiers supprimés
    - `--backup` garde de côté les fichiers supprimés qui prennent un suffixe dans le répertoire de sauvegarde
    - `--backup-dir=/chemin` déplace les fichiers supprimés dans un dossier dédié. Exemple : `rsync -arv --delete --backup --backup-dir=/home/louis/backups_supprimes Images/ backups/`
  - `--exclude` permet d'exclure un dossier de la sauvegarde
  - `rsync` permet de sauvegarder sur un autre ordinateur, le plus couramment en utilisant SSH
    - `rsync -arv --delete --backup --backup-dir=/home/louis/fichiersSupprimes Images/ louis@ip:backup/`
    - `rsync -arv --delete --backup --backup-dir=/home/louis/fichiersSupprimes Images/ louis@ip:backup/ -e "ssh -p 12345"` si le serveur SSH écoute sur un autre port que celui par défaut


## Le réseau


- **adresse IP** : chaque ordinateur relié à Internet est identifié par une adresse IP
  - format **IPv4** : 86.172.120.28
  - format **IPv6** : fe80::209:62fa:fb80:29f2
  - nom d'hôte, **hostname** en anglais, équivalent à l'IP mais plus simple à retenir
  - `host` donne le nom d'hôte à partir de l'adresse IP et inversement. Exemple : `host siteduzero.com` et `host 92.243.25.239`
  - les **serveurs DNS** fournissent la liste des correspondances IP <-> noms d'hôte
  - le fichier */etc/hosts* permet de modifier la liste de correspondance personnalisée de notre ordinateur, par exemple ajouter un nom d'hôte à chaque PC pour s'y connecter sans retenir l'IP
  -  `whois` donne des renseignements sur un nom de domaine. Exemple : `whois siteduzero.com`

- `ifconfig` liste les interfaces réseau et permet aussi de faire des réglages réseau
  - exemple : **eth0** pour une connexion par câble réseau, **lo** pour la boucle locale, c'est-à-dire une connexion à soi-même, **wlan0** pour une connexion sans-fil Wi-Fi
  - `ifconfig interface etat` permet d'activer/désactiver une interface réseau, par exemple `ifconfig eth0 down` ou `ifconfig eth0 up`
- `netstat` permet d'avoir des statistiques sur le réseau
  - `netstat -i` donnent des stats par interface réseau
  - `netstat -uta` liste toutes les connexions ouvertes
    - `-u` pour les connexions UDP, `-t` pour les connexions TCP, `-a` pour afficher toutes les connexions quelque soit leur état
    - permet de voir les **ports** sur lequels se sont les connexions. `-n` permet d'avoir les numéros des ports plutot qu'une description en toutes lettres
    - `-l` permet de filter uniquement les connexions à l'état *LISTEN*
    - `netstat -s` permet d'avoir des statistiques résumées

- `iptables` est un pare-feu Linux.
  - Il permet d'établir des règles
    - à quels ports on peut se connecter à votre ordinateur
    - à quels ports vous avez le droit de vous connecter
    - filtrer par IP
  - `iptables -L` affiche les règles actuellement en place
    - *Chain INPUT* correspond aux règles manipulant le trafic entrant, *Chain FORWARD* correspond aux règles manipulant la redirection du trafic, *Chain OUTPUT* correspond aux règles manipulant le trafic sortant
    - *policy ACCEPT* signifie que par défaut, tout le trafic est accepté, alors que *policy DROP* permet de resufer toutes les connexions que nous n'avons pas autorisé
    - *iptables -F* permet de réinitialiser toutes les règles iptables
  - l'ajout et la suppression de règles
