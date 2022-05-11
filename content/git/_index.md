---
title: Question fréquentes sur Git pour le Projet GL
---

Une liste des quelques erreurs les plus fréquentes avec
[Git](https://bugbusters.pages.ensimag.fr/wiki/linux/git/) pour le Projet GL.
Merci de conserver cette liste courte, pour les détails, il existe déjà une
[FAQ Git](https://git.wiki.kernel.org/index.php/GitFaq) et le
[manuel utilisateur](http://www.kernel.org/pub/software/scm/git/docs/user-manual.html).

{{< toc >}}

## Problèmes après utilisation du mail ou de `scp`
Vous avez échangé des modifications entre membres d'une équipe, en dehors de `git` (par email,
`scp`, clé USB, ...), et vous avez beaucoup de conflits incomprehensible :

-> C'est normal.
`git` ne sait rien sur ce qu'il se passe par email ou `scp`, il croit que plusieurs développeurs ont
fait des modifications similaires (et en general pas tout a fait identiques).
En bref, si vous utilisez autre chose que `git` pour vous échanger du code, attendez-vous a des
problèmes.

## Problème avec `gedit`

Si `EDITOR=gedit`, `git commit` se plaint d'un message de `commit` vide.

-> Le problème se produit lorsqu'un `gedit` est déjà lancé (un nouvel appel à `gedit` demande au
programme existant d'ouvrir le fichier, et termine immédiatement, donc `git` croit que `gedit` a
fini le travail). 3 solutions :
* ne pas utiliser `EDITOR=gedit`
* ou bien, fermer toutes les fenêtres `gedit` avant de faire un `commit`
* ou bien, avec une version récente de `gedit`, utiliser `EDITOR='gedit -s -w'`

## Problème avec `gvim`

Si `EDITOR=gvim`, `git commit` se plaint d'un message de `commit` vide.

-> Même problème qu'avec `gedit` (ci-dessus), mais il y a une solution plus satisfaisante :
utiliser `gvim -f` à la place de `gvim`.

## `git push` échoue avec le message `non-fast-forward`

`git push` échoue avec le message :
```
To ssh://depotglXX@depots.ensimag.fr/~/git/
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'ssh://depotglXX@pcserveur.ensimag.fr/~/git/'
```

La situation classique est qu'il y a des commits envoyés par vos coéquipiers dans l'archive, il faut
les récupérer chez vous avant de pouvoir faire un `push`:

-> il faut faire un `pull` avant le `push`, une nouvelle révision  est disponible dans l'archive
partagée.

Si vous n'êtes pas dans cette situation, voir la question suivante.

## Je voudrais faire un `git push --force`

Une autre raison pour rejeter un push avec l'erreur `non-fast-forward` est que l'historique a été
ré-écrit (avec `git rebase` ou `git commit --amend`).

Par exemple, en partant de cet historique :

```Shell
$ git log --oneline --decorate --graph master origin/master
* 5f08bd8 (HEAD, origin/master, master) troisième commit
* 7fdaada deuxième commit
* cefff88 premier commit
```

et en ré-écrivant les deux premiers commits, on arrive à cet historique :

```Shell
$ git log --oneline --decorate --graph master origin/master
* 4e5d448 (HEAD, master) troisième commit
* 1391552 deuxième commit
| * 5f08bd8 (origin/master) troisième commit
| * 7fdaada deuxième commit
|/
* cefff88 premier commit
```

Le `commit master (5f08bd8)` est une ré-écriture de `origin/master (4e5d448)`.
Techniquement, c'est un nouveau `commit`, même s'il introduit les mêmes changements.
Si on essaye de faire un `push`, `git` refusera (`non-fast-forward`) car `master` n'est pas un
descendant direct de `origin/master`.

Dans certaines situations, il serait pertinent d'écraser l'ancien historique avec
`git push --force`.
C'est interdit en projet GL (via la variable de configuration
[`receive.denyNonFastForwards`](http://git-scm.com/docs/git-config)), à la fois pour vous empêcher
de commettre l'irréparable (effacer votre historique par erreur) et pour vous empêcher de tricher
sur votre historique au moment des rendus.
En dehors du projet, un `git push --force` est une bonne idée sur une branche qui n'a pas été
intégrée (typiquement pour écraser une première version d'une _pull-request_ avec une nouvelle
version qui prend en compte des commentaires de relecteurs), mais pas sur la branche principale, sur
laquelle d'autres développeurs peuvent avoir basé leur travail.

### Comment réparer cette situation ?

La seule solution est donc de créer un `commit` qui soit un descendant de `origin/master` (condition
nécessaire pour pouvoir faire un `push`), et qui contienne la même chose que `origin/master`.
Cette solution suppose que vous vous êtes assurés que tous les changements importants étaient dans
votre branche `master` (tout ce qui est dans `origin/master` sera perdu).
On peut le faire avec les commandes suivantes :

On vérifie que `origin/master` est bien à jour (`fetch`), et on se place sur la branche une nouvelle
branche `new-master`, qui pointe sur le même `commit` que `origin/master` pour l'instant
(`checkout`) :
```Sell
$ git fetch
$ git checkout origin/master -b new-master
```

Le résultat est l'historique suivant :

```Shell
$ git log --oneline --decorate --graph
*   3ef34cf (HEAD, new-master) Merge branch 'master' into new-master
|\
| * 4e5d448 (master) troisième commit
| * 1391552 deuxième commit
* | 5f08bd8 (origin/master) troisième commit
* | 7fdaada deuxième commit
|/
* cefff88 premier commit
```

On peut vérifier qu'on n'a pas fait de bêtise et que new-master pointe bien sur le même arbre que master :

```Shell
git diff new-master master
```

On peut maintenant faire avancer la branche `master` sur notre branche `new-master` :

```
$ git checkout master
$ git merge new-master
Updating 4e5d448..3ef34cf
Fast-forward
 foo.txt | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

Et il nous reste à faire un push :

```Shell
git push
```

### Comment éviter cette situation ?

L'origine du problème est qu'on a ré-écrit une portion d'historique déjà publiée.
La solution est donc de ne pas le faire.

#### Solution 1 : ne ré-écrire que l'historique local

Les commandes `git rebase` (surtout avec l'option `-i`) et `git commit --amend` sont très puissantes
pour ré-écrire son historique local, **avant** un `push`.
Par exemple, sur un historique comme :

```
* 278dbc1 (HEAD, master) Oops, en fait je me suis trompé dans le commit précédent
* d93f772 Ce commit a l'air bon
* 5f08bd8 (origin/master) troisième commit
* 7fdaada deuxième commit
* cefff88 premier commit
```

Il aurait été pertinent d'utiliser `git commit --amend` pour ne pas créer le `commit` `278dbc1`,
mais corriger le `commit` `d93f772`.
Il est encore temps d'utiliser `git rebase -i` et la commande `fixup` pour le faire.
Vos coéquipiers ne sauront pas que vous vous êtes trompés, et ne se rendront même pas compte que
vous avez utilisé ces commandes.

Par contre, les trois premiers `commits` sont "gravés dans le marbre", il est trop tard pour les
ré-écrire.

Bonne nouvelle : la commande `git rebase -i` sans argument fait ce qu'il faut : elle vous propose
de ré-écrire uniquement votre historique local.

#### Solution 2 : utiliser un autre dépôt pour les commits en cours de relecture

Rien ne vous empêche d'avoir du code ailleurs que dans votre dépôt officiel (par exemple un créant
votre propre dépôt à l'Ensimag, ou un utilisant un hébergeur extérieur, pour peut qu'il vous
permette de garder votre projet privé de manière sécurisée bien sûr).
Dans ce cas, l'autre dépôt peut vous permettre de créer des branches temporaires, de faire des
relectures et corrections sur ces branches, puis de les intégrer dans votre dépôt officiel.

Gardez en tête que vos enseignants ne considèrent que la branche master de votre dépôt officiel,
donc tout votre code doit y arriver pour pouvoir être pris en compte dans l'évaluation.

## `fatal: Unable to create '.../index.lock': File exists`

La plupart des opérations échouent avec le message :

```
fatal: Unable to create '/home/ensi2a/bob/Projet_GL/.git/index.lock': File exists.

If no other git process is currently running, this probably means a
git process crashed in this repository earlier. Make sure no other git
process is running and remove the file manually to continue.
```

À moins que vous ne veniez de trouver un bug dans `git`, ce message se produit quand :
* Une autre instance de `git` est en train de s'exécuter dans le même répertoire (typiquement, un
`git commit` qui a lancé un éditeur de texte et qui attend que cet éditeur de texte termine).\
**Solution:** Faire en sorte que cette autre instance termine proprement (typiquement : en fermant
l'éditeur de texte lancé par `git commit`).
* Vous avez tué brutalement un processus `git` (typiquement, `Control-C` dans un terminal).\
**Solution:** supprimer le fichier `index.lock`, et pour la prochaine fois, penser à ne plus tuer
brutalement les processus...

## Plus rien ne marche, et les autres entrées de cette page ne s'appliquent pas

Pas de panique, l'intérêt de `git` est justement que vos données sont à l'abri.
La solution la plus simple (et sans doute la plus brutale) est de refaire un clone depuis l'archive
partagée :

```Shell
cd
mv Projet_GL Projet_GL.casse
git clone ssh://depotglXX@depots.ensimag.fr/~/git/ Projet_GL
```

(On garde une copie de la copie de travail qui pose problème, on ne sait jamais)

Si vous aviez des commits dans votre copie de travail qui n'avaient pas encore été "pushées" vers
l'archive partagée, ils sont récupérables avec

```Shell
cd ~/Projet_GL
git pull ~/Projet_GL.casse
```

Quand la situation est rétablie, on peut faire un `git push` pour envoyer nos modifications vers
l'archive partagée, et continuer à travailler comme avant.
