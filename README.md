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

- rechercher des fichiers
  - `locate fichier` pour une recherche rapide sur la base de données des fichiers qui est mise à jour toutes les 24 heures. Pour la mettre à jour, lancer la commande `sudo updatedb`
  - `find` pour une recherche approfondie, en parcourant les fichiers sur le disque, ce qui peut être long. La commande s'utilise avec des paramètres `find "où" "quoi" "que faire avec"`. Seul *"quoi"* est obligatoire.
    - *où* est le dossier dans lequel on fait la recherche, ainsi que tous ses sous-dossiers. Si non renseigné, recherche dans le dossier courant
    - *quoi* fichier ou dossier à rechercher, par nom, date de création, taille...
    - *que faire avec* on peut faire un post-traitement. Par défaut, la commande affiche la liste des fichiers trouvés, mais d'autres actions sont possibles
    - exemples :
      - `find -name "README.md"` recherche un fichier dans le répertoire courant qui s'appelle exactement *README.md*. On peut utiliser l'étoile pour rechercher des noms incomplets, par exemple : `find -name "READM*"`
      - `find /var/log/ -name "syslog"`
      - `find -size +10M` permet de rechercher les fichiers de plus de 10Mo. On peut utiliser le **-** au lieu de **+**, et le **k** ou le **G** à la place du **M**
      - `find -name "*.md" -atime 6` recherche les fichiers au format markdown modifié il y a moins de 7 jours (0 pour 1 jour). On peut enlever le *-* pour modifié exactement il y a *x* jours
      - `-type d` et `-type f` permet de limiter la recherche aux répertoires ou au fichier, par exemple `find -name "syslog" -type d`
      - `find -name "README.md" -print` permet d'afficher les résultats, ce qui correspond au résultat par défaut `find -name "README.md"`
      - `-printf` permet de formater le résultat affiché, par exemple `find -name "README.md" -printf "%p - %u\n"`
      - `-delete` permet de supprimer les fichiers trouvés, par exemple `find -name "README.md" -delete`
      - `-exec`, permet d'appeler une commande qui effectuera une action sur chacun des fichiers trouvés


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
