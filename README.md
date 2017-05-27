# Tutoriel Git

Ce tutoriel suppose quelques pré-requis :
- avoir un compte sur un sité hébergant des repositories Git (Github, Gitlab, Gogs, etc.)
- avoir accès à un terminal pour utiliser Git en ligne de commandes
- avoir une paire de clef SSH générée et liée à un compte pour utiliser Git via SSH

Git est un logiciel de gestion de version (dit de *versionning*), c'est-à-dire permettant gérer les versions de son code au fur et à mesure que celui-ci évolue. L'utilité étant de pouvoir travailler, seul ou à plusieurs, sur un projet ayant une évolution dans le temps (ajout de fonctionnalités, correction de bug, retour sur une ancienne version, etc.).  
Un projet géré avec Git constitue un *repository* ou *dépôt*, consitant généralement en un dossier contenant plusieurs fichiers (et éventuellement sous-dossiers). Ce *repository* est généralement stocké sur un serveur distant et les développeurs vont déposer leur travail (par exemple l'ajout d'une fonctionnalité) sur ce *repository* distant (on parle de *push*). Il existe plusieurs façon d'héberger son *repository* Git, le site le plus connu permettant de le faire est Github.  

## Basics
Les bases pour commencer avec Git sont dans le fichier [bases.md](bases.md).

## Travail à plusieurs
Les bonnes pratiques à suivre pour le travail à plusieurs sont dans le fichier [collaboration.md](collaboration.md).

## Plus d'infos
Quelques liens pour apprendre à bien utiliser Git.
- https://openclassrooms.com/courses/gerer-son-code-avec-git-et-github
- http://nvie.com/posts/a-successful-git-branching-model/
- http://www.git-attitude.fr/2014/05/04/bien-utiliser-git-merge-et-rebase/#le-pi%C3%A8ge%20de%20git%20pull%20et%20du%20r%C3%A9flexe%20pull%20+%20push
