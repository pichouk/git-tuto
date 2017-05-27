# Bases
## Création d'un *repository*

Pour initier un projet avec Git, on va partir d'un dossier qui peut-être vide ou contenir du code déjà existant. On se place dans le dossier en question et on initialise le *repository*.
```
git init
```

Il est désormais possible de suivre l'évolution du contenu du dossier avec Git, c'est un *repository* local. Pour pouvoir partager le code avec d'autres personne, il faut créer un *repository* sur Github (via l'interface Web). Une fois que c'est fait, Github donne une adresse à utiliser (par exemple `git@github.com:pichouk/git-tuto.git`) pour synchroniser le *repository* local avec le *repository* distant (ou *remote*). On configure notre *repository* local pour utiliser le *repository* distant que l'on vient de créer :
```
git remote add origin git@github.com:pichouk/git-tuto.git
```

Un petit point sur cette commande :
- `git remote add` indique que l'on veut ajouter un *repository* distant à notre projet.
- `origin` est le nom que l'on donne à ce *repository* distant. C'est le nom traditionnellement utilisé par défaut.
- `git@github.com:pichouk/git-tuto.git` l'adresse du *repository* distant.

## Versionner son code
On peut ensuite travailler sur le projet. Si c'est un nouveau projet, il est traditionnel d'ajouter un fichier `README.md` décrivant le projet. Une fois le fichier créé, on veut faire en sorte de sauvegarder celui-ci avec Git. On va indexer le fichier avec la commande `add` :
```
git add README.md
```

Après avoir ajouté un fichier à l'index, il est possible de le "sauvegarder" dans Git en faisant un *commit*. Le *commit* est sans doute le concept *le plus important* de Git : c'est une sorte de "sauvegarde" de l'état d'un projet à un instant précis. À chaque modification que l'on souhaite sauvegarder, on fait un *commit* qui ira rejoindre l'historique de tout les *commits* du projet. Il sera par la suite possible de se déplacer dans l'historique pour voir les anciennes versions du code, qui a fait quelles modifications et quand.  
Pour réaliser notre premier commit on utilise la commande suivante :
```
git commit -m "Ajout du fichier README"
```
Comme on peut le voir, l'option `-m` permet d'ajouter un message à son commit, ce qui est obligatoire. Si l'option n'est pas spécifiée, Git demandera automatiquement d'ajouter un message.

Les commandes `git add` et `git commit` sont les commandes de bases les plus utilisées avec Git. Au fur et à mesure du développement d'un projet, le développeur devra *commiter* les différents version de son code, de manière à avoir un suivi du projet et à pouvoir revenir en arrière.

## Partager son code
On a vu comment suivre l'évolution de son projet en réalisant des *commits*. Mais un point important est de partager son travail, pour permettre à d'autre de contribuer à leur tour. Actuellement, le *repository* local contient l'historique de nos *commits* mais pas le *repository* distant. Pour partager le code, on utilise la commande :
```
git push origin master
```

Quelques explications sur la commande :
- `git push` permet de publier (ou parle de *push*) l'état actuel du *repository* local vers un *repository* distant.
- `origin` est le nom du *repository* distant vers lequel on veut *push*.
- `master` est le nom de la *branch* que l'on souhaite *pusher*. Le concept de *branch* sera expliqué plus tard, il faut juste savoir que la *branch* par défaut s'appelle généralement `master`.

Ainsi le code est partagé sur le *repository* distant (on peut le voir dans l'interface de Github). Si on souhaite récupérer la dernière version du code (par exemple si quelqu'un a *push* une modification) on fait :
```
git pull origin master
```

### Les branches
Un concept important de Git est celui de *branch*. Une *branch* est, littéralement, une branche ou ramification dans le code. Par exemple, sur le développement d'un site Web, vous voulez coder un nouveau module (par exemple un système de gestion de commentaires). Le travail est long et conséquent, vous ne pouvez pas le faire en une seule fois. Pendant le temps de développement de ce module, on ne veut aussi pouvoir travailler sur autre chose si besoin (par exemple corriger une erreur). Pour cela, on va créer une *branch* spéciale dans laquelle sera réalisé le développement du module. Le projet aura une *branch* principale (généralement `master`) et une branche spéciale (par exemple *ajout-commentaires*) dans laquelle on pourra coder notre module. Lorsque celui-ci sera terminé, on pourra intégrer le code dans la *branch* principale, ce que l'on appelle un *merge*.

#### Création d'une branche
Imaginons que nous sommes sur un projet avec une *branch* principale nommée `master`. On souhaite développer une fonctionnalité (disons un module de commentaires) sur une *branch* temporaire. On va créer une *branch* que l'on nommera `monmodule` :
```
git branch monmodule
```

La *branch* est créé, on peut vérifier que l'on se trouve bien sur celle ci à l'aide de la commande `git branch` qui liste les *branch* existantes et indique la *branch* courante. On peut ensuite commencer à travailler normalement sur son module et faire des *commits* qui ne seront **que** sur la *branch* `monmodule`. À tout moment, (par exemple pour corriger un bug urgent n'ayant rien à voir avec le module), on peut retourner sur la *branch* `master` avec la commande `git checkout master`.

#### *Merge* d'une branche
Une fois le travail terminé sur notre module, on veut récupérer tout les *commits* qui ont été réalisés dans notre *branch* `monmodule` vers notre *branch* principale (`master`). On va pour cela réaliser une opération de *merge*, c'est à dire intégrer les *commits* d'une *branch* dans une autre. On se positionne dans `master` puis on *merge* :
```
git checkout master
git merge --no-ff monmodule
```
On se trouve dans `master` et on demande un *merge* de `monmodule`, ce qui va fusionner les deux *branch*. (On ne se soucis pas de l'option `--no-ff` ici, elle est simplement utile pour conserver un *repository* propre).
