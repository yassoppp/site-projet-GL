---
title: Accueil
---

## Sommaire du site

- [Actualité du Projet GL 2022](/actualites) **À consulter régulièrement et impérativement**
- [Palmarès Projets GL](/palmares)
- Environnement de travail
    - [Faire le Projet GL sur une machine personnelle](/environnement/machine_perso)
    - [Projet GL sous Mac OS X](/environnement/mac_os)
    - [Vim pour le projet GL](/environnement/vim)
    - [Emacs pour le projet GL](/environnement/emacs)
    - [Questions fréquentes avec Maven pour le projet GL](/environnement/maven)
- Git:
    - [Question fréquentes sur Git pour le Projet GL]()
    - [Amphi Git avancé en projet GL](/git/amphi)
    - [Gérer des branches avec Git](https://bugbusters.pages.ensimag.fr/wiki/linux/git/gerer-des-branches/)
    - [Continuer à travailler avec Git quand le serveur est HS](https://ensiwiki.ensimag.fr/index.php?title=Continuer_%C3%A0_travailler_avec_Git_quand_le_serveur_est_HS)
    - [Écrire de bons messages de commit avec Git](https://bugbusters.pages.ensimag.fr/wiki/linux/git/bons-messages-commits/)
    - [Maintenir un historique propre avec Git](https://bugbusters.pages.ensimag.fr/wiki/git/maintenir-historique/)
- [Organiser des rétrospectives](/retrospectives)
- [Vocabulaire Anglais pour le Projet GL](/vocabulaire_anglais)

## Commandes à utiliser pendant la séance machine

Pour vous gagner un peu de temps pendant la séance machine, voici quelques lignes prêtes à
copier-coller :

* Lire le polycopié:
```Shell
evince /matieres/4MMPGL/GL/global/doc/poly-projet-GL.pdf
```
puis cherchez **[SeanceMachine]** dans le fichier PDF.

Votre numéro d'équipe est le nom du projet gitlab (`gl<nn>`) dont vous faîtes parti.
Vous pouvez également le retrouver ainsi que le numéro de votre groupe par la commande :
```Shell
grep " $LOGNAME " /matieres/4MMPGL/GL/global/doc/liste-equipes.txt
```

* Commande `git clone` (remplacer `NN` par le numéro d'équipe et `GG` par votre numéro de groupe) :
```Shell
git clone git@gitlab.ensimag.fr:gl2022/gGG/glNN Projet_GL
```

* Squelette de fichier <code>~/.gitconfig</code> (à adapter, bien sûr) :
```Shell
[user]
        name = Prénom Nom
        email = Prenom.Nom@grenoble-inp.org
[core]
        editor = votre_editeur_prefere
[diff]
        renames = true
[color]
        ui = auto
[push]
        default = current
```

## Autres documentations utiles

* De quoi écrire des [Script Shell](https://systemes.pages.ensimag.fr/www-unix/avance/),
utile pour automatiser les tests,
* [Git](https://bugbusters.pages.ensimag.fr/wiki/linux/git/), et en particulier les pages
    * [Question fréquentes sur Git pour le Projet GL](/git)
    * [Gérer des branches avec Git](https://bugbusters.pages.ensimag.fr/wiki/linux/git/gerer-des-branches/),
    qui peut servir au moins aux plus curieux d'entre vous en particulier au moment du rendu
    intermédiaire.
    * [Écrire de bons messages de commit avec Git](https://bugbusters.pages.ensimag.fr/wiki/linux/git/bons-messages-commits/)
    et [Maintenir un historique propre avec Git](https://bugbusters.pages.ensimag.fr/wiki/git/maintenir-historique/),
    car maintenant que vous avez un peu d'expérience avec l'outil, c'est peut-être une bonne idée
    d'apprendre vraiment les bonnes pratiques et la puissance de l'outil !
    * [Continuer à travailler avec Git quand le serveur est HS](https://ensiwiki.ensimag.fr/index.php?title=Continuer_%C3%A0_travailler_avec_Git_quand_le_serveur_est_HS)
    qui peut être utile en cas de problème sur les serveurs de l'école.
    * [Créer un dépôt partagé avec Git](https://ensiwiki.ensimag.fr/index.php?title=Cr%C3%A9er_un_d%C3%A9p%C3%B4t_partag%C3%A9_avec_Git)
    qui explique comment mettre en place une archive Git « comme en Projet GL » vous-mêmes (pour
    vos projets à venir).
* [Questions fréquentes avec Maven pour le projet GL](environnement/maven)
* [Exemple d'utilisation de netbeans pour naviguer dans un code source](http://www-prima.inrialpes.fr/reignier/GL/)

## Les enseignants

En 2022 :

- [Akram Idani](mailto:akram.idani@imag.fr)\
enseignant SHEME :  [Valérie Gondre](mailto:valerie.gondre@grenoble-inp.fr)
- [Raquel Oliveira](mailto:Raquel.Araujo-De-Oliveira@grenoble-inp.fr)\
enseignant SHEME :  [Laurent Eyraud](mailto:laurent.eyraud@gmail.com)
- [Dawood Al Chanti](mailto:Dawood.Al-Chanti@grenoble-inp.fr)\
enseignant SHEME : [Bertrand Barnoud](mailto:Bertrand38330@gmail.com)
- [Mathias Ramparison](mailto:mathias.ramparison@univ-grenoble-alpes.fr)\
enseignant SHEME : [Bertrand Barnoud](mailto:Bertrand38330@gmail.com)
- [Patrick Reignier](mailto:Patrick.Reignier@imag.fr)\
enseignant SHEME : [Tarik Larja](mailto:tarik.larja@grenoble-inp.fr)
- [Martin Bodin](mailto:martin.bodin@inria.fr)\
enseignant SHEME : [Tarik Larja](mailto:tarik.larja@grenoble-inp.fr)
- [Roland Groz](mailto:Roland.Groz@univ-grenoble-alpes.fr)\
enseignant SHEME : [Pierre Boccoz](mailto:pierre.boccoz@sogeti.com)
- [Nicolas Jourdan](mailto:nicolas.jourdan@gmail.com)\
enseignant SHEME : [Eric Faugeras](mailto:eric.faugeras@capgemini.com)
- [Jingyan Jourdan](mailto:jingyan.jourdan@gmail.com)\
enseignant SHEME : [Tony Buthod-Garcon](mailto:Tony.Buthod-Garcon@capgemini.com)
- [Wendelin Serwe](mailto:Wendelin.Serwe@inria.fr)\
enseignant SHEME : [Christel Tessier](mailto:christel.tessier@grenoble-inp.fr)
- [Karine Altisen](mailto:Karine.Altisen@imag.fr)\
enseignant SHEME : [Caroline Thomet](mailto:caroline.thomet@capgemini.com)

