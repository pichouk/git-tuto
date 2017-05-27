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
- `master` est le nom de la *branch* que l'on souhaite *pusher*. Le concept de *branch* sera expliqué plus tard, il faut juste savoir que la *branch* par défaut s'appelle généralement *master*.

Ainsi le code est partagé sur le *repository* distant (on peut le voir dans l'interface de Github). Si on souhaite récupérer la dernière version du code (par exemple si quelqu'un a *push* une modification) on fait :
```
git pull origin master
```
