# Site web projet GL Ensimag

[projet-gl.pages.ensimag.fr](https://projet-gl.pages.ensimag.fr/)

## Fonctionnement
Le générateur de sites statiques [Hugo](https://gohugo.io/) permet de générer ce site à partir de
sources markdown.
Le site est régénéré et redeployé à chaque _push_ grâce à une _pipeline_ d'intégration continue (CI)
GitLab.
Cette dernière est configurée dans le fichier [`.gitlab-ci.yaml`](https://gitlab.ensimag.fr/projet-gl/projet-gl.pages.ensimag.fr/-/blob/master/.gitlab-ci.yml).

### Thème
Le thème utilisé est un [_fork_](https://gitlab.ensimag.fr/proba/hugo-geekdoc) du thème
[geekdoc](https://geekdocs.de/).
Par rapport à la version originale:
- Une [modification](https://gitlab.ensimag.fr/proba/hugo-geekdoc/-/commit/82cd81c6d67032cb40b8422ed5f1c258309cb30b)
  permet le fonctionnement des liens _Modifier la page_ qui se trouve en haut de
  chaque page.
- Le support de [MathJax](https://www.mathjax.org/) (pour les équations) a été
  [ajouté](https://gitlab.ensimag.fr/proba/hugo-geekdoc/-/commit/141647fe5ffb243e89731d3d27eb4ea0a19762d0).

### Hébergement
L'hébergement est assuré par [GitLab Pages](https://docs.gitlab.com/ee/user/project/pages/).
