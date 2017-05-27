# Travail à plusieurs

## Bonnes pratiques
Lorsque l'on travaille à plusieurs, quelques bonnes pratiques de bases sont à suivre :
- La branche `master` contient **UNIQUEMENT** une version du projet parfaitement fonctionnelle.
- Chacun travaille sur une branche personnelle qu'il *merge* dans la branche `master`.
- On effectue **TOUJOURS** un *rebase* sur la branche distante avant de faire un *push*.
- Conserver un historique de *commits* cohérent et lisible pour que les autres comprennent ce qui a été fait. La commande `git add -p` sera votre amie pour découper vos modifications.

## Intégrer son code au projet
On imagine (comme spécifié dans les bonnes pratiques) que l'on a développé, en local, une nouvelle fonctionnalité dans une branche nomée `localbranch`. Le projet est réalisé à plusieurs et on souhaite désormais partager le code que l'on vient de modifier. On va *merger* notre branche `localbranch` dans `master` puis *pusher* les modifications sur le *repository* distant.

On *merge* nos modifications :
```
git checkout master
git merge --no-ff localbranch
```

Une fois le *merge* effectué on *push* la branche `master` locale vers la branche `master` distante.
```
git push origin master
```
Si tout se passe bien, tant mieux. Il ne reste plus qu'à supprimer la branche de travail local devenue inutile `git branch -d localbranch`.  
Par contre si quelqu'un a fait un *push* avant vous, il est possible d'obtenir ceci `! [rejected] master -> master (fetch first)` suivi d'une erreur.

## Gestion d'un *rejected*
Pas de panique ! En effet ceci signifie qu'une autre personne a travaillé sur le projet et a fait des *commits* sur la branche `master`. Git a besoin de récupérer ces modifications en local avant de réaliser un *push* pour pouvoir fusionner vos modifications avec celles faites sur le branche *master* par un autre développeur. Il suffit de récupérer le code mis à jour dans le *repository* distant (avec `git fetch`), l'intégrer à votre historique local (avec `git rebase`), puis de *pusher* à nouveau.
```
git fetch origin master
git rebase -p origin/master
```
Si tout se passe bien vous allez obtenir `Successfully rebased and updated refs/heads/dev`. Il ne vous reste plus qu'à *push* la branche `master` et supprimer celle de travail.
```
git push origin master
git branch -d localbranch
```

Cependant vous pouvez aboutir à un conflit lors du *rebase*, par exemple si le même fichier a été modifié par 2 utilisateurs.

#### Gestion d'un conflit
En cas de conflit, il va falloir le gérer à la main. Ceci arrive lorsque des modifications différentes sur un même fichier sont incompatibles (par exemple deux personnes modifient la même ligne). Le *rebase* en cours se met en pause (visible grâce à `git status`) et les fichiers rencontrant des conflits sont modifiés par Git de manière à rendre visible les conflits (un peu à la manière de la commande `diff` sous Linux). A partir de là, il n'y a pas de miracle, il faut regarder dans les fichiers en question et faire les modifications qui vont bien. Il existe aussi des outils (graphiques ou en CLI) pour gérer les conflits, à vous de voir ce qui vous va.  
En tout cas, lorsque tout est résolu, on ajoute les fichiers modifiés et on les *commit*.
```
git add -A
git commit
```
Si tout est bon (on peut vérifier avec `git status`), alors on continue le *rebase*.
```
git rebase --continue
```
Une fois le *rebase* terminé, on *push* la branche `master` et on supprime celle de travail.
```
git push origin master
git branch -d localbranch
```
