---
title: Projet GL sous macOS
---

Cette page participative vise à donner quelques informations utiles à la configuration d'un
environnement de développement fonctionnel pour le projet GL sous macOS.
La version de macOS utilisée pour la mise à jour de cette page est macOS
Big Sur 11.6.2, les instructions qui suivent peuvent ne pas s'appliquer de la même manière pour
des versions différentes du système (en particulier les plus anciennes).

La page [Faire le Projet GL sur une machine personnelle](/environnement/machine_perso) reste la
page de référence et sa lecture est indispensable, la présente page vise uniquement à proposer des
informations complémentaires et spécifiques à macOS.

Notez que la façon la plus sûre de garantir que le projet GL fonctionnera de la même façon que sur les machines de l'école, tout en travaillant sur un ordinateur Apple, est d'utiliser docker, avec la configuration qui vous est fournie: de cette façon, vous exécutez dans un environnement virtuel Linux "Ensimag" tout en travaillant sur votre Mac. Mais comme il est parfois plus agréable de travailler en natif, voici les conseils pour avoir l'environnement requis par le projet GL sur macOS.

## Installation des outils développeurs Apple
Les outils de développement Apple peuvent être obtenus en installant **XCode** depuis l'App Store
(attention, fichier volumineux !).

## Installation de `brew`

`Brew` est un gestionnaire de paquets pour macOS, il permet d'installer facilement des outils et
bibliothèques de développement : un must-have pour coder sous Mac.

Pour l'installer, il suffit d'exécuter la ligne suivante dans un terminal :
```Shell
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### Correction des éventuels problèmes gênants

On lit parfois qu'il est recommandé d'exécuter la commande `brew doctor` après installation de brew
et de corriger les problèmes signalés.
C'est vrai, mais tous les "problèmes" ne sont pas bloquants et mieux vaut ne pas faire de
modification hâtive sur le système.
En cas de problème à l'installation d'un logiciel, `brew` signalera l'erreur et il faudra alors en
déterminer la cause à l'aide du message d'erreur et de `brew doctor`.

Par exemple, il peut arriver que le répertoire `/usr/share/man` et ses sous-répertoires ne soient
pas accessibles en écriture et que cela bloque l'installation d'un logiciel.
Dans ce cas, un petit coup de `chmod o+w` règlera le problème.

## Installation d'un JDK

Le projet GL se fait en Java, il est donc nécessaire de disposer d'un _Java Development Kit_ sur sa
machine.

La manière la plus propre d'installer un **JDK** est d'utiliser le package MacOS fourni par Oracle
sur la page http://www.oracle.com/technetwork/java/javase/downloads/index.html.
La version JDK 16 est celle recommandée pour le projet et correspond à ce qui est sur les
ordinateurs de l'école.

### Correction de la variable `JAVA_HOME`

La variable d'environnement `JAVA_HOME` n'est pas correctement initialisée, ce qui entraîne des
problèmes à la compilation des projets Maven comme exposé dans
[la page concernant Maven](/environnement/maven/#mvn-compile-donne-une-erreur-could-not-find-artifact-comsuntoolsjar0).

Dans mon cas avec le **JDK 16.0.2**, faire pointer `JAVA_HOME` au bon endroit a suffit à corriger le
problème sans modification de `pom.xml`.
La ligne suivante est à adapter à votre version du JDK et à mettre dans votre `.bash_profile`:
```Shell
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk-16.0.2.jdk/Contents/Home
```

## Installation de Maven
L'installation de Maven est immédiate avec brew :
```Shell
brew install maven
```

## Mise à jour de git
La version de `git` fournie avec macOS est en retard sur le dépôt officiel et il est conseillé de
la mettre à jour.
`brew` peut s'en occuper avec :
```Shell
brew install git
```

La version de git installée de base sera toujours présente dans `/usr/bin`, et `brew` installera la
dernière version en date dans `/usr/local/bin` (donc sans écraser l'ancienne).
Le répertoire `/usr/local/bin` se trouvant avant les autres dans le `PATH`, la version la plus
récente sera utilisée par défaut. Vous pouvez vérifier la version 
```Shell
$ which git
/usr/local/bin/git
```

## GNAT et GNATMAKE
Installer la version 2020 de gnat, dont `GNATMAKE`.
https://www.adacore.com/download/more

Avec d'anciennes versions,, vous pourriez rencontrer des difficultés avec la version `gcc` de `gnat` pour la
compilation des fichiers
* `flottants_c.c`
* `fma_c.c`
de la machine abstraite, car ceux-ci utilisent des bibliothèques et des prototypes non compatibles avec ceux de MacOS. On pourrait résoudre ceci par une compilation séparée préalable de ces fichiers avec la version standard de `gcc` (typiquement `/usr/bin/gcc`):
* `/usr/bin/gcc flottants_c.c -c -o ../../Obj/flottants_c.o`
* `/usr/bin/gcc fma_c.c -c -o ../../Obj/fma_c.o`

Le reste du `make` utilisera les fichiers `.o` ainsi engendrés.
Mais normalement, avec la version 2020 de gnat, toutes les bibliothèques devraient êêtre compatibles.

## Récupération des fichiers nécessaires
Pour la configuration de l'environnement de travail et la récupération des fichiers nécessaires à la
réalisation du projet, veuillez vous référer à la page
[Faire le Projet GL sur une machine personnelle](/environnement/machine_perso).
