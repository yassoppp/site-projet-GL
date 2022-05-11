---
title: Faire le Projet GL sur une machine personnelle
---

Cette page a pour but de vous aider à installer un environnement de développement, sous Linux, pour
le Projet GL de l'Ensimag, 2ème année.
Le projet devrait marcher sans trop d'effort sous macOS (n'hésitez pas à remonter les problèmes
que vous rencontrez à vos enseignants et/ou à mettre à jour cette page).
Faire marcher le projet sous Windows serait bien plus compliqué en revanche (le projet utilise des
scripts shell en plus de Java, ils marcheraient peut-être avec Mingw), il est sans doute plus
simple d'installer Linux que de faire le portage.

Pour le projet _Projet GL Apprentissage_, les instructions s'appliquent en adaptant l'arborescence
globale : `/matieres/4MMPGL/GL/global` en 2A étudiant, `/matieres/3MM1PGL/global` en 1A
apprentissage.

{{< toc >}}

## Installation des outils (Java, Git, ...)

Nous allons tout d'abord installer les outils nécessaires au projet.
Si ces outils sont déjà installés sur votre machine, vous n'avez rien à faire.

### Sous macOS : Outils pour développeurs Apple
Si vous travaillez sous Mac pensez à installer les outils pour développeur Apple.

Il faut notamment modifier le fichier `pom.xml` comme indiqué sur cette page
[Questions fréquentes avec Maven pour le projet GL](/environnement/maven#tools-jar), afin de faire
pointer correctement maven vers le fichier `tools.jar`.

Quelques conseils spécifiques pour macOS sont disponibles sur la page [Projet GL sous macOS](/environnement/mac_os).

### Installation de Java

Une installation de Java quelconque récente (au delà de java 8) fera l'affaire.
La version installée actuellement en salle sur les PC est la 16.

1. Vérifiez la version java utilisée actuellement sur votre machine avec: `javac -version`

2. Si java 16 n'est pas installé sur votre machine: selon la distribution, un
`apt-get install openjdk-16-jdk` ou un `yum install openjdk-16-jdk` devrait installer tout cela.
Sinon, on peut télécharger Java sur [le site d'OpenJDK](http://openjdk.java.net/install/) ou bien
sur [le site d'Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).

3. Si plusieurs versions de Java sont installées sur votre machine, positionnez la variable
d'environnement `JAVA_HOME` sur le JDK 16 dans votre `.bash_rc` avec une ligne comme:
`export JAVA_HOME=/usr/lib/jvm/java-16-openjdk-amd64` (en adaptant avec le nom du répertoire
d'installation de JDK sur votre machine, que vous pouvez trouver par exemple à l'aide de
`dpkg-query -L openjdk-16-jdk` sous debian/ubuntu).\
Positionner `JAVA_HOME` ne change pas la version de Java sur votre machine (`java -version` reste
inchangé), ça change juste la version de Java utilisée dans maven (et netbeans).

4. Si la méthode du point 3 ne permet pas de faire fonctionner maven correctement, vous pouvez
essayer `sudo update-alternatives --config javac` pour imposer le choix de java 16 à votre système
(mais ça ne devrait pas être nécessaire).

### Installation de Maven

Maven est disponible dans Debian et Ubuntu : `sudo apt install maven`

Installer Maven manuellement est très facile : il suffit de télécharger une archive _Binary_ depuis
[cette page](http://maven.apache.org/download.cgi), d'extraire l'archive et de placer le répertoire
`bin/` au début de votre `$PATH`.
Pour plus de détails, voir par exemple [cette page](http://johnathanmarksmith.com/linux/java/maven/programming/project%20management/2013/04/18/how-to-install-maven-on-fedora-centos-red-hat-and-scientific-linux/)
si nécessaire.

Une autre option est d'utiliser le Maven distribué avec Netbeans (`netbeans/java/maven/bin/mvn`):
dans ce cas, voir l'installation de netbeans ci-dessous.

Vérifiez que maven fonctionne avec Java version 1.8 en lançant `mvn -version`.
Si ce n'est pas le cas, consultez le paragraphe [Installation de Java](#installation-de-java)
ci-dessus.

Vérifiez aussi que vous avez installé la version 3.8.4 de maven `mvn -version`. D'autres versions de Maven peuvent causer le problème "Error executing Maven. Unable to load cache item". Vous pouvez installer maven 3.8.4 à partir du tar.gz en suivant [ce lien](https://www.javahelps.com/2017/10/install-apache-maven-on-linux.html) .


### Installation de Git

Votre distribution contient probablement [Git](https://bugbusters.pages.ensimag.fr/wiki/linux/git/),
et il suffira probablement d'un `sudo apt install git-core gitk`, `sudo yum install git`, ...

Sous Mac téléchargez la dernière version de Git depuis https://git-scm.com/download/mac puis suivez
les indications de l'utilitaire.

### Installation de Netbeans (optionnelle pour ceux qui veulent travailler avec cet IDE)

Les versions packagées pour Ubuntu et Debian sont en général cassées (le gestionnaire de plugins ne
marche pas).
Il est fortement recommandé d'installer une version récente d'**Apache Netbeans** (version 12 par
exemple).

Suivre les instructions de téléchargement et d'installation de netbeans depuis cette page :
https://netbeans.apache.org/download/index.html

Pour plus de confort, sous Linux, n'hésitez pas à ajouter le chemin vers les binaires netbeans à
votre `PATH`.
Il suffit d'ajouter `export export PATH="/chemin/vers/dossier/netbeans-12.0-bin/bin:$PATH"`.

### Installation du plugin ANTLRWorks pour Netbeans (optionnelle, mais conseillée si votre IDE est netbeans)

Pour avoir la coloration syntaxique dans les fichiers `.g4` (grammaires ANTLRv4), installez le
plugin **ANTLRWorks** disponible au téléchargement ici :
http://plugins.netbeans.org/plugin/73187/netbeans-antlr

* Lancer netbeans
* Dans le menu `Tools`, choisir `Plugins`
* Onglet `Downloaded plugins`, choisir `Add plugin`, puis bouton `install` et se laisser guider.

## Installation de l'environnement du projet

### Installation de l'arborescence globale du projet (ima)

Récupérez l'arborescence `GL/global/` de l'Ensimag sur votre machine.
Dans l'exemple, on installe l'arborescence dans `~/ensimag`, mais vous pouvez bien sûr adapter (dans
ce cas, il faudra remplacer dans les commandes ultérieures `$HOME/ensimag` par le répertoire
choisi) :

```Shell
laptop:~$ mkdir -p ensimag/GL; cd ensimag/GL
```

Puis, pour les 2A:
```Shell
laptop:~/ensimag/GL$ git clone ssh://votrelogin@pcserveur.ensimag.fr/matieres/4MMPGL/GL/global/ global
```

Ou, pour les apprentis 1A:

```Shell
laptop:~/ensimag/GL$ git clone ssh://votrelogin@pcserveur.ensimag.fr/matieres/3MM1PGL/global/ global
```

Vérifiez que la commande `ima` fonctionne :

```Shell
laptop:~/ensimag/GL$ ./global/bin/ima -v
```

Si ce n'est pas le cas, vous pouvez recompiler `ima` sur votre machine comme ceci (la version
fournie devrait fonctionner sur architecture 64 bits sous Linux) :

```
laptop:~/ensimag/GL$ cd global/sources
laptop:~/ensimag/GL/global/sources$ make
```

Si après avoir exécuter `make`, la commande `gnatmake` n'est pas reconnue, c'est que vous devez
récupérer la package ADA pour GCC (`gcc-ada` ou `gnat` selon la distribution Linux).
{{< hint warning >}}
**ATTENTION (mai 2020):**\
Il semble que les Makefiles d'`ima` ne sont pas robustes aux caractères spéciaux (espaces,
apostrophes, accents, etc) dans les noms de répertoire.\
En attendant, un patch des enseignants, il vaut mieux éviter ce type de caractères dans les noms de
répertoire (utiliser juste un mélange de lettres, chiffres, points, soulignés).
{{< /hint >}}

La dernière commande devrait compiler `aflex`, `ayacc` (qui sont nécessaires pour compiler `ima`),
et `ima` sur votre machine.

Si des bugs sont trouvés et corrigés dans l'arborescence globale en cours de projet, il faudra
simplement faire :

```Shell
laptop:~$ cd ~/ensimag/GL/global
laptop:~/ensimag/GL/global$ git pull
```

pour récupérer ces corrections (et si vous aviez eu besoin de recompiler `ima`, vous devrez
recompiler à nouveau).

### Configuration de votre compte

Dans le fichier d'initialisation de votre shell :
* si vous ne savez pas comment il s'appelle ou ce qu'il est, il s'agit sans doute de `~/.bashrc`
* sous Mac il s'agit de `~/.bash_profile`


* Modifier la variable `PATH` (à la FIN du fichier `.bashrc`) :
```Shell
export PATH=$HOME/ensimag/GL/global/bin:$PATH
```

Vous aurez bien sûr besoin d'appliquer les autre consignes données dans **[SeanceMachine]** pour
avoir les répertoires de votre projet dans le `$PATH`.
`$HOME/ensimag/GL/global/bin` remplace simplement `~moy/GL/global/bin/`.

Une fois ces opérations effectuées, il faut demander à votre shell de relire le fichier `.bashrc`
(sinon, les modifications ne seront effectives qu'au prochain démarrage du shell) :

```Shell
. ~/.bashrc
```

* Récupérer le `~/.gitconfig` créé pendant la séance machine si vous n'en avez pas déjà un sur
votre machine.
Par exemple :

```Shell
rsync -v pcserveur.ensimag.fr:.gitconfig ~/.gitconfig
```

Il est recommandé de refaire les vérifications indiquées dans **[SeanceMachine]**

Les résultats peuvent être légèrement différents : sur Debian, on obtient, par exemple :

 ```Shell
$ which mvn
/usr/bin/mvn
```

Vérifiez aussi que `mvn -version` utilise bien la version Java 1.8.

La commande `which ima` doit renvoyer quelque chose comme `$HOME/ensimag/GL/global/bin/ima` selon
l'endroit où vous avez installé `ima`.

### Création du répertoire Projet_GL par rapatriement depuis l'archive

Pour les 2A: commande `git clone` (remplacer `NN` par le numéro d'équipe et `GG` par votre numéro
de groupe) :

```Shell
git clone git@gitlab.ensimag.fr:gl2022/gGG/glNN Projet_GL
```

Pour les apprentis: (remplacer N par le numéro d'équipe entre 1 et 6)
```Shell
git clone git@gitlab.ensimag.fr:glapp2022/glN Projet_GL
```

<div id="debug">

## Image Docker (expérimental)

Si vous souhaitez vous retrouver dans un environnement identique à celui des PC de l'école, il est
possible de télécharger l'image pour machine virtuelle depuis le site intranet de l'école.
Attention : cette image est très lourde.
Une autre solution consiste à utiliser Docker qui peut être vu comme une solution de virtualisation
légère.
Docker est disponible sous Linux (son environnement de prédilection) mais également sous Windows et
MacOsX.
Vous trouverez [https://docs.docker.com/get-started/overview/ ici] une présentation des principes de
cette approche.

### Installation de Docker

Les instructions principales d'installation sont disponibles
[ici](https://docs.docker.com/engine/install/).

* **sous Linux :** La plupart des distributions proposent des packages standards.
Une installation docker consiste en la mise en place d'un démon devant être lancé au démarrage ainsi
que des outils clients en ligne de commande.
Il est également nécessaire d'ajouter votre compte utilisateur comme membre du groupe créé par
docker afin de pouvoir l'utiliser dans être root.
Le [wiki d'Arch Linux](https://wiki.archlinux.org/index.php/Docker) est une source précieuse
d'information, y compris pour les autres distributions.
* **sous Windows :** Cela dépend de la version que vous utilisez.
Pour une version Windows home, les instructions sont
[ici](https://docs.docker.com/docker-for-windows/install/).
Pour une version Windows pro ou Windows Education, les instructions sont
[ici](https://docs.docker.com/docker-for-windows/install/).
* **sous MacOs :** [ici](https://docs.docker.com/docker-for-mac/install/).

### Mise en place de l'image Docker

L'image Docker proposant un environnement minimal identique à celui disponible en salle peut être
soit reconstruite localement depuis votre machine personnelle, soit téléchargée directement sur le
gitlab de l'école.
Les instructions correspondantes pour ces deux possibilités sont dans le fichier `README.md` du
répertoire docker à la racine de votre dépôt du projet.

Trois modes de fonctionnement nous semblent envisageables (nous sommes ouverts à toutes autres
suggestions ou améliorations...).

#### Chaîne de compilation externe à l'IDE

L'image Docker proposée n'embarque pas en interne le répertoire projet (vous pouvez néanmoins le
faire si vous le souhaitez) mais accède par montage au répertoire du projet présent sur votre
machine sur votre OS hôte (Windows, MacOs, Linux).
Vous pouvez donc éditer votre projet avec votre environnement de développement préféré installé sur
votre machine et bénéficier des aides au développement qu'il apporte.
Le lancement de la chaîne de compilation et des tests (`mvn` ..., ... pouvant être par exemple
`clean`, `compile`, `verify`, `install` etc.) ou le lancement de tests manuels (`decac` ... etc.)
se fera en ligne de commande depuis le shell lancé dans le container.

#### Couplage de la chaîne de compilation et de l'IDE

Afin de pouvoir compiler, naviguer en hypertexte des erreurs de compilation vers le code source etc,
depuis l'IDE, il faut que celui gère le lancement et les sorties de cette chaîne de compilation.
On peut envisager à priori trois configurations :
* l'IDE est installé à l'intérieur du container : on se retrouve dans le cadre du développement sur
une seule machine mais cette machine est distante (le container)
* l'IDE est installé sur l'OS hôte mais pilote via ssh la compilation sur la machine distance
(le container).
* la solution hybride : l'IDE est partiellement sur l'OS hôte et partiellement sur la machine
distance (le container).


#### IDE installé dans le container

Si vous souhaitez bénéficier d'un environnement de développement totalement intégré et lancer en particulier la compilation et les tests depuis votre IDE, vous pouvez installer cet IDE à l'intérieur du container (la version CentOS de cet IDE donc). L'IDE sera alors lancé depuis la ligne de commande du shell du container.

Exécuter votre IDE depuis votre container nécessite que votre OS hôte soit capable d'afficher les fenêtres X-Windows et que votre container soit paramétré pour envoyer les instructions X-Windows vers votre OS hôte.

##### Serveur X-Window

Sous **Windows**, vous pouvez installer le serveur _X-Windows_ open-source `VcXsrv` :\
https://sourceforge.net/projects/vcxsrv/

Sous **macOS**, vous pouvez utiliser par exemple le serveur _X-windows_ open-source `XQuartz` :
https://www.xquartz.org/

Sous Windows et macOS, il faudra également autoriser l'affichage de fenêtres venant d'une machine
extérieur (le container docker est vu comme une autre machine).
C'est l'équivalent du `xhost +` sous Linux.

Sous **Linux**, _X-Windows_ étant le système graphique par défaut, il n'y a pas d’installation
supplémentaire à prévoir.
Le `xhost +` n'est pas nécessaire également, le container étant lancé en "re-mappant" le répertoire
contenant les socket du serveur X de l'hôte sur le répertoire équivalent du container.
Le container voit le serveur X de l'hôte comme si c'était son propre serveur.

##### Envoi des instructions X-Windows vers l'OS hôte

###### Linux

Comme cela a été expliqué dans la section précédente, le principe sous Linux consiste à _"mapper"_
le serveur X de l'hôte dans le container (en montant le répertoire `/tmp/.X11-unix` de l'hôte sur le
répertoire `/tmp/.X11-unix` du container).
Il faut ensuite positionner la variable d'environnement `DISPLAY` à la même valeur que celle
utilisée dans votre session.
La création du container devient donc (dans le cas du téléchargement de l'image):

```Shell
$ docker create --interactive --tty -v /home/reignier/Documents/Cours/ENSIMAG/Compil:/home/gl/Compil   -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$DISPLAY --name projetgl projetgl
```

Sous macOS et Windows, le principe est de considérer le container l'OS hôte comme deux systèmes
distincts et de positionner la variable `DISPLAY` à l'adresse IP à laquelle le container voit le
système hôte.

###### macOS

Pas testé faute de machine à disposition

###### Windows

Pas testé faute de machine à disposition

#### IDE installé dans l'OS hôte

Cette solution nécessite deux points différents : ajouter un accès ssh au container et choisir un IDE capable de piloter par ssh une chaîne de compilation.

##### Accès ssh au container

L'image proposée par défaut dans le répertoire Docker (pour reconstruction ou récupération sur gitlab) offre un accès bash mais pas ssh. Vous trouverez également dans ce répertoire le fichier fichier Dockerfile.ssh permettant de reconstruire une image avec accès ssh. Au delà de l'IDE, ce scénario permet via ssh d'avoir un container où vous pouvez vous connecter par ssh depuis plusieurs terminaux différents et donc bénéficier de plusieurs accès simultané au même container). Pour utiliser ce fichier pour la construction, il faut utiliser l'option "-f".

* Reconstruction de l'image :
 ```Shell
 docker build -f Dockerfile.ssh -t projetgl_ssh .
```

* Création du container (il n'y a pas plus paramètres liés à l'interaction, ce container ne faisant que démarrer un serveur ssh et pas un shell interactif) :
 ```Shell
 docker create -v <your GL home dir absolute path>:/home/gl/Projet_GL --name projetgl_ssh projetgl_ssh
 ```

* Lancement
```Shell
docker start projetgl_ssh
```

* Arrêt
```Shell
docker stop projetgl_ssh
```

* Détermination de l'adresse IP du container pour se connecter en ssh :
```Shell
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' projetgl_ssh
```

`projetgl_ssh` est le nom du container.
Pour voir l'ensemble des containers présents sur votre machine (lancés ou arrêtés) :
```Shell
docker ps -a
```

* Connexion :
```Shell
ssh gl@<ip address>
```

**Netbeans** permet de piloter par ssh le compilateur java (utilisé par exemple pour le
développement sur raspberry depuis son PC) mais à ma connaissance pas **Maven**.
Eclipse est un candidat potentiel avec en particulier le plugin Remote System Explorer
(pas testé... merci de nous prévenir si vous le testez et pour quel résultat).


#### Installation hybride

Les environnements de développement "classiques" comme **Netbeans**, **Eclipse** ou **Idea** sont
des environnement monolithiques s'installant donc naturellement sur l'OS hôte ou dans le container.
Il existe également des environnements reposant nativement sur une architecture client - serveur
même si cela n'est pas apparent en tant qu'utilisateur.
C'est le cas en particulier de [Visual Studio Code](https://code.visualstudio.com/) qui est un
projet opensource de Microsoft disponible sur Windows, Linux et MacOS.
Cette architecture permet en particulier plus facilement de déployer une partie serveur sur le
container et le client sur l'OS hôte.
Cette approche est expliquée [ici](https://code.visualstudio.com/docs/remote/containers) et
illustrée par le schéma d'architecture présent sur cette page.

Pour mettre en oeuvre cette approche, il faut dans un premier temps installer le plugin Docker
fournit par Microsoft au sein de votre Visual Studio Code
([vscode-docker](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker)).
Le lien entre **Code** et le container est ensuite décrit par un fichier `.devcontainer.json` qui
doit se trouver dans le répertoire où vous lancez l'éditeur.
Pour des raisons de facilitée, nous vous en fournissons un dans le répertoire docker de votre
projet.
C'est donc depuis ce répertoire que vous devez lancer **Visual Studio Code** si vous voulez utiliser
cette solution.
Le contenu de ce fichier est le suivant :
```Json
{
    "image" : "gitlab.ensimag.fr:5050/reigniep/dockergl",
    "extensions": [
    	"ms-azuretools.vscode-docker",
   	    "redhat.java",
   	    "VisualStudioExptTeam.vscodeintellicode",
   	    "vscjava.vscode-java-debug",
   	    "vscjava.vscode-java-dependency",
   	    "vscjava.vscode-java-pack",
   	    "vscjava.vscode-java-test",
   	    "vscjava.vscode-maven",
   	    "mike-lischke.vscode-antlr4"
    ],
    "workspaceMount": [
        "source=${localWorkspaceFolder}/..,target=/home/gl/Projet_GL,type=bind,consistency=cached"
    ],
    "workspaceFolder" : "/home/gl/Projet_GL"
}
```

Cette configuration spécifie où **Code** doit télécharger l'image Docker si elle n'est pas présente
sur votre système, quels plugins y ajouter (complétion `java`, `antlr`, etc.) et quelle
configuration pour la création du container (montage des répertoires pour vous retrouver en
particulier à la racine de votre projet).
Il n'est donc pas nécessaire dans ce cadre de réaliser les différentes opérations docker de
construction / pull, de création de container etc.
Le lancement de **Code** depuis le répertoire docker réalisera tout ceci automatiquement.
À la première ouverture, un _popup_ en bas à droite doit vous proposer "Reopen in container" qu'il
faudra sélectionner pour que **Code** utilise le fichier `.devcontainer.json` et se déploie dans le
container.

**Remarque :** Lorsque Code est connecté au container, le menu Terminal -> New Terminal permet d'ouvrir un nouveau shell à l'intérieur du container

## Problèmes et solutions

« S'il n'y a pas de solution, c'est qu'il n'y a pas de problème »

## Historique

- Fichier initial écrit par Matthieu MOY en janvier 2001 (ouch, ça fait un coup de vieux de relire
ça maintenant ;-) ), puis amende par Xavier NICOLLIN, destiné à aider les étudiants à installer un
environnement de développement chez eux sous Linux pour le projet GL.\
Nous (les enseignants) ne pouvons pas tester toutes les distributions et configurations, mais les
corrections pour votre distribution préférée sont les bienvenues !
- Modification pour CygWin par Laurent Belcour (2008)
- Modification pour Mac OS X par Amaury Balliet (2010)
