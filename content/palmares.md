---
title: Palmarès Projets GL 2022
---


Toutes les équipes du projet GL sont invitées à se comparer les unes aux autres en mesurant **l'efficacité
énergétique** du code produit par leur compilateur sur les 3 fichiers de test fournis dans
`src/test/deca/codegen/perf/provided`.

Le tableau ci-dessous est éditable par les étudiants, ce qui vous permet de noter les performances de chaque équipe.
LORSQUE votre compilateur est prêt à participer, c'est à dire capable de compiler au moins un des
programmes, vous pouvez remplir les cases du tableau avec une ligne pour votre équipe.
Il s'agit d'un palmarès à trier par la colonne "Score", du plus faible (c'est à dire le moins
consommateur) au plus fort (le plus gourmand en cycles, donc en énergie).
Ce score est une pondération des résultats sur les 3 programmes de test.
Vous devez donc honnêtement remplir le tableau avec les performances (actuelles) de votre
compilateur.
Si vous l'améliorez, vous aurez le droit de changer votre ligne et de la remonter plus haut dans le
classement.

Votre objectif est bien sûr de faire mieux que le vieux compilateur des enseignants, conçu il y a
bien longtemps, dans le "monde d'avant", sans souci d'efficacité énergétique.
Il ne devrait donc pas être difficile à battre, et la compétition se jouera entre les meilleures
équipes. Vous pouvez regarder le [Palmarès de l'année précédente](https://projet-gl.pages.ensimag.fr/palmares_2021) pour voir ce à quoi était parvenu vos anciens. 20 équipes de 2021 avaient fait mieux que le vieux compilateur des profs. Nous espérons que la conscience environnementale accrue des étudiants permettra à encore plus d'équipes en 2022 d'améliorer ce score.
Une place dans le _"TOP 10"_ donnera un bonus pour la partie de la note consacrée au développement
durable.

## Consignes

* Pour chaque programme, vous devez donner le nombre de cycles utilisés par le code assembleur
produit par votre compilateur, que vous pouvez obtenir par la commande `ima -s`.
* Chacun de ces programmes a été validé, et ne produira pas d'erreur (débordement arithmétique ou
autre).
Donc vous pouvez (et c'est recommandé) obtenir l'assembleur par la commande `decac -n`.
C'est d'ailleurs ce à quoi sert cette option: gagner du temps d'exécution (et de la consommation de
ressources) sur les programmes validés.
* Si vous n'êtes pas encore capables de compiler un des programmes (par exemple `ln2_fct` qui
utilise l'objet), vous utilisez la valeur indiquée pour _gl00_ pour ce programme (par exemple
50000 pour `ln2_fct`) pour calculer le score.
Donc avant que votre compilateur ne puisse compiler de l'objet et des fonctions, vous avez peu de
chances de battre _VieuxCompDeProf_.
* Bien entendu, vous n'avez le droit d'afficher un nombre de cycles différent de `gl00` que si vous
pouvez compiler ce programme ET si votre assembleur calcule le résultat correct (annoncé dans les
commentaires du fichier source).
* Afin de mieux comparer les équipes, nous vous demandons aussi de préciser l'extension que vous
traitez.
En effet, les équipes ayant choisi l'extension _Optim_ sont favorisées pour traiter spécifiquement
l'efficience de leur compilateur puisque c'est l'objet principal de leur extension.
* Toutes les modifications sur le Wiki sont enregistrées, donc toute malhonnêteté entraînera la
disqualification de l'équipe et bien sûr une incidence sur la note du projet (pour non respect de
l'éthique - sportive).

| Equipe            | Extension | S=Syracuse42 | L0=ln2 | L1=ln2_fct | Score=L0+L1+10*S |
| ---               | ---       | ---          | ---    | ---        | ---              |
| gl29              | OPTIM     |           33 |     85 |         85 |              500 |
| gl54              | OPTIM     |         723  |  8375  |      10798 |            26403 |
| gl38              | HISTOIRE  |         1346 |  8620  |      11402 |            33482 |
| gl28              | BYTE      |         1386 |  9068  |      11397 |            34325 |
| gl07              | TAB       |         1292 |  14986 |      18167 |            46073 |
| gl14              | TAB       |         1286 |  15124 |      18113 |            46097 |
| VieuxCompDeProf   | TRIGO     |         1340 |  15194	|      18102 |            46696 |
| gl13              | BYTE      |         1326 |  15180 |      18379 |            46819 |
| gl20              | TRIGO     |         1288 |  15004 |      19001 |            46885 |
| gl45              | TRIGO     |         1314 |  15672	|      18432 |            47244 |
| gl09              | TAB       |         1392 |  15500 |      18573 |            47993 |
| gl26              | ARM       |         1394 |  15488 |      18971 |            48399 |
| gl36              | TRIGO     |         1438 |  15738	|      19078 |            49196 |
| gl56              | TRIGO     |         1513 |  15831 |      18662 |            49623 |
| gl52              | ARM       |         1663 |  16148 |      17467 |            50245 |   
| gl18              | TAB       |         1708 |  16728 |      18669 |            52377 |
| gl23              | ARM       |         1428 |  18664 |      22263 |            55207 |
| gl49              | ARM       |         1782 |  18322 |      23396 |            59538 |
| gl08              | TAB       |         2428 |  16058 |      22261 |            62599 |
| gl47 (JuNGLE)     | ARM       |         1272 |  13906	|      50000 |            64058 |
| gl34              | ETUD      |         2253 |  23967 |      25903 |            72400 |
| gl04              | TRIGO     |         2430 |  24632 |      26101 |            75033 |
| gl43              | TRIGO     |         1372 |  15510 |      50000 |            79230 |
| gl53              | ARM       |         1838 |  15868 |      50000 |            84248 |
| gl31              | OPTIM     |         1572 |  18738 |      50000 |            84458 |
| gl33              | HISTOIRE  |         1862 |  16857 |      50000 |            85477 |
| gl00              |           |         5000 |  50000 |      50000 |           150000 |

