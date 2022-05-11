---
title: Vim pour le projet GL
---

(un Vimiste volontaire pour développer un peu ?)

## Pour les débutants

<!-- Pour ceux qui sont pas encore à l'aise avec Vim, regardez Vim. -->

## Vim pour éditer les fichiers `.deca` et `.ass`

Il faut pour cela créer sa propre coloration syntaxique.

Si cela n'est déjà fait, créez un dossier `.vim` à la racine de votre compte.
Ensuite, créez-y un fichier `filetype.vim`, que vous remplirez comme suit:

```Vim
"mon fichier de types
if exists("did_load_filetypes")
   finish
endif
augroup filetypedetect
   au! BufRead,BufNewFile *.deca       setfiletype java
   au! BufRead,BufNewFile *.decah      setfiletype java
   au! BufRead,BufNewFile *.ass        setfiletype asm
augroup END
```

Vous aurez enfin de jolies couleurs à vos fichiers `.deca` et `.ass` !
