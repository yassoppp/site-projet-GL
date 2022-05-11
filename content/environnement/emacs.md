---
title: Emacs pour le projet GL
---

## Compiler depuis Emacs

M-x compile RET

## Naviguer dans du code source avec Emacs
{{< hint danger >}}
Cette section date de l'époque où le projet était écrit en Ada, ce n'est pas nécessairement la meilleure manière de faire en Java.
{{< /hint >}}

Pour s'y retrouver plus facilement dans le code fourni, il est utile de disposer d'une fonction de
recherche de définition de fonction, afin de pouvoir vérifier rapidement son prototype par exemple.
Pour faire ceci dans emacs, il faut tout d'abord créer un fichier de tags :

```Shell
find ~/gl /usr/local/GL/Global/Commun/Src/ -name '*.ad[bs]' | xargs etags -o ~/.emacs.d/TAGS
```

(en remplacant les chemins par ceux correspondant à votre configuration).
Cette commande va inspecter vos fichiers `.adb` et `.ads` dans les dossiers fournis en paramètre,
et va produire un fichier TAGS, à stocker dans un répertoire quelconque.
Ensuite, dans emacs, on indique où trouver les tags par :

```lisp
(setq tags-table-list '("~/.emacs.d"))
```

Il suffit ensuite de faire `M-.` dans Emacs avec le curseur sur le nom d'une fonction, ou d'une
variable (et probablement d'autres choses) pour trouver où celle-ci est définie. Et pour revenir où
on en était avant : `M-*`.

On peut automatiser la construction de la table pour éviter d'avoir à répéter la commande à chaque
fois qu'on rajoute une fonction, par exemple avec cron (`crontab -e` pour éditer votre fichier de
configuration `cron`, `man 5 crontab` pour la documentation sur le format).

(Note si un vimiste s'égare sur cette page : il est possible de faire pareil sous Vim avec Ctags.)

## Emacs pour éditer les fichiers `.deca` et `.ass`
Il suffit d'ajouter au `.emacs` :

```lisp
(setq auto-mode-alist (cons '("\\.ass$" . asm-mode) auto-mode-alist))
(setq auto-mode-alist (cons '("\\.deca$" . java-mode) auto-mode-alist))
```

Ceci associera les bons modes pour les fichiers `.deca` et `.ass`, et vous aurez donc la coloration
syntaxique.
