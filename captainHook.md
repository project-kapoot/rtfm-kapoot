---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
---


# Mise en place du véricateur des message de commit

pour mettre en place le vérificateur de commit en local ( sur le PC du dev). 
nous alons intaller 2 choses: 
- [CaptainHook](https://php.captainhook.info/index.html)
- [ramsey/conventional-commits](ramsey/conventional-commits)


## Installation de ramsey/conventional-commits

ramsey/conventional-commits est une librarie php, qui perme de vérifié les message de commit. 

### procédure install ramsey/convention-commits

pour l'installer, dans votre projet PHP, taper : `composer require --dev ramsey/conventional-commits`

et c'est installé!

## Installation de CaptainHook

CaptainHook est une librarie PHP qui permet de lancer des script et de lancer des action automatique lors divers action git, ex: _git commit_ 

### procédure d'installation de CaptainHook 

pour intaller, taper : `composer require --dev captainhook/captainhook`

### configuration de captainHook

ensuite place à la configuration, on va crée un fichier de configuration _captainhook.json_ à la racine du projet, puis ajouter ceci : 

```json
{
    "commit-msg": {
        "enabled": true,
        "actions": [
            {
                "action": "\\Ramsey\\CaptainHook\\ValidateConventionalCommit"
            }
        ]
    }
}
```

ce code appele la validateur Ramsey et empeche le commit si le message ne respecte pas le conventional commit. 

Ramsey, fournit aussi un assistant pour les message de commit, pour l'activer, rajouter ce code dans le fichier de configuration : 

```json
{
    "_comment": "Le reste du code ( ne pas ajouter ) ",
    "prepare-commit-msg": {
        "enabled": true,
        "actions": [
            {
                "action": "\\Ramsey\\CaptainHook\\PrepareConventionalCommit"
            }
        ]
    }
}
```

### Activivation de Captain hook

pour que CaptainHook, soit fonctionnel, il faut l'activer afin qui intercepte les hook git (_event git_). 

#### Activation manuel

pour l'activer, taper : `vendor/bin/captainhook install`

#### Activiation automatique

pour s'assurer que les dev, n'oublie pas d'activer cette action, on peut lancer cette commande automatiquement après l'installation des dépendance. pour cela dans le _composer.json_ ajouter cette ligne : `vendor/bin/captainhook install -sf` dans le **post-install-cmd**

```json
{
    "_comment": "le reste de la configuration",
    "scripts": {
            "auto-scripts": {
                "cache:clear": "symfony-cmd",
                "assets:install %PUBLIC_DIR%": "symfony-cmd",
                "importmap:install": "symfony-cmd"
            },
            "post-install-cmd": [
                "@auto-scripts", 
                "vendor/bin/captainhook install -sf" ajouter_cette_ligne
            ],

    }
}
```







