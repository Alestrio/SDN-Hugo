---
title: "Recherche Hugo"
date: 2021/10/22
tags: ["research","hugo"]
draft: false
---

Dans ce chapitre, nous allons voir le fonctionnement de Hugo afin de générer un site web static


(Attention, la syntax peux varié légerement en fonction des theme utilisé)
## Creation du Site-Web Hugo


Créer un site web hugo est relativement simple, une fois que hugo est installé sur le serveur.
Vous devez entrez la commande suivante dans le dossier désiré:
``` 
hugo new site {site_name} 
```
Vous devriez alors obtenir quelque chose de similaire :
```
3105-alpine-1:/home/hugo/presentation# hugo new site presentation
Congratulations! Your new Hugo site is created in /home/hugo/presentation/presentation.

Just a few more steps and you're ready to go:

1. Download a theme into the same-named folder.
   Choose a theme from https://themes.gohugo.io/ or
   create your own with the "hugo new theme <THEMENAME>" command.
2. Perhaps you want to add some content. You can add single files
   with "hugo new <SECTIONNAME>/<FILENAME>.<FORMAT>".
3. Start the built-in live server via "hugo server".

Visit https://gohugo.io/ for quickstart guide and full documentation.
3105-alpine-1:/home/hugo/presentation# ls
presentation
```
Vous avez donc le nouveau dossier du cite qui est crée, ici ./presentation
## Fichier généraux de Hugo

Hugo va automatiquement générer des fichiers pour vous, nous allons rapidement voir les plus important.
```
3105-alpine-1:/home/hugo/presentation/presentation# ls
archetypes   config.toml  content      data         layouts       static       themes
```

### Le fichier de config


**config.toml** est le fichier de configuration pour votre site. 


### Le dossier **./content**

Le dossier **./content** est l'endroit où vous placerez touse vos contenu
### Le dossier **./themes**

Le dossier **./themes** est l'emplacement ou vous téléchargerez via Github les différents themes que vous utiliserez.
### Le dossier **./public**

Le dossier **./public** sera crée quand vous lancerez votre serveur ou rechargerez les pages grace à la commande ```hugo``. 
Ce dossier contiendra les différent fichier utiliser pour votre site-web.

Ceux-ci sont les principaux fichier et dossier que vous utiliserez. Les autres étant principallement utiliser afin de générer les site ou si vous déssidez de créer vos propre themes.
## Choisir un theme

Pour cette partie j'utiliserai [hugo-learn-theme](https://github.com/matcornic/hugo-theme-learn) pour exemple.
Pour commencer nous nous plaçons dans le dossier **./themes**. Ici vous lancerez la commande git clone courespondante a votre theme [more-theme-there](https://themes.gohugo.io/). Dans notre cas :
```
git clone https://github.com/matcornic/hugo-theme-learn.git
```
Vous avez donc un nouveau theme dans vos dossier.
Pour rendre une theme effectif vous devez ajouter le nom du dossier de votre theme comme suivant : 
```
echo "theme = \"hugo-theme-learn\"" >> config.toml
```
Vous avez maintenant votre theme charger par defaut.
## Crée des nouveau chapitre et des nouveau contenu

Crée des nouveau contenue est simple. Vous avez deux options, une automatic et une manuel.

### Avec des commandes

Les commandes pour crée des chapitre et des contenue sont assés similaire.
```
# Crée un nouveau chapitre
3105-alpine-1:/home/hugo/presentation/presentation# hugo new --kind chapter demo/_index.md
/home/hugo/presentation/presentation/content/demo/_index.md created

# Crée un nouveau contenue
3105-alpine-1:/home/hugo/presentation/presentation# hugo new demo/my-first-content.md
/home/hugo/presentation/presentation/content/demo/my-first-content.md created
```
Comme vous le voyez, vous avez besoins d'ajouter **-- kind chapter** à votre commande afin de crée un chapitre. Il est important de ne pas oubliée le fichier **_index.md** lors de la création d'un chapitre, celui-ci étant utilisé comme référence pour afficher le site dans la navigation.

Une fois la commande utilisé, les fichiers sont générés dans la dossier **./content**.
```
3105-alpine-1:/home/hugo/presentation/presentation# ls content/
demo
3105-alpine-1:/home/hugo/presentation/presentation# ls content/demo/
_index.md            my-first-content.md
```

Les fichiers de chapitres et de contenue seront toujours crée avec un header particulier comme suivant.

**_index.md**
```
+++
title = "Demo" # nom du chapitre
date = 2021-10-22T18:18:48+02:00
weight = 5 # positions dans la bar nav 
chapter = true # defini un chapitre
pre = "<b>X. </b>" # défini le prefix d'affiche
+++
```
**my-first-content.md**
```
---
title: "My First Content" # Titre du contenue
date: 2021-10-22T18:18:48+02:00 # date de création
draft: true # metre à false pour publier le contenue
---
```
 
On peut noter une différence entre les deux puisque le chapitre va utiliser ```+++``` la ou le contenu va utiliser ```---```

Apres ces marques, vous pouvez placer votre contenue en markdown.

### Manuellement 

La methode manuel est aussi facile, vous avez juste besoin de créer vos fichiers et dossier dans le **./content** et d'utiliser les headers vue ci-dessu en fonction du contexte. Une fois de plus, penser à bien metre un fichier **_index.md** afin d'afficher vos chapitre dans la navigation.

## Utiliser plusieurs langue

Avec hugo, vous pouvez facilement gérer plusieur langue. La premiere chose est d'ajouter les lignes suivante dans votre ficher **config.toml** 
```
defaultContentLanguage = "en"
defaultContentLanguageInSubdir= true

[Languages]
[Languages.fr] # Réference du language
title = "Documentation du projet SDN" 
weight = 1 # déclare la positions de la lange dans le button
url ="/fr" # dossier ou vos fichier static sont stoquer dans le /public
landingPageName = "<i class='fas fa-home'></i> Accueil" # acces à la page d'acceuil
languageName = "Français" # nom du language

[Languages.en]
title = "Documentation for the SDN project"
weight = 2
url="/en"
landingPageName = "<i class='fas fa-home'></i> Redirect to Home"
languageName = "English"
```
En ajoutant ces lignes, nous avons maintenant un bouton pour changer de langue dans la bar de navigation. 
Maintenant vous aurez égallement besoins de créer un fichier de contenue par langue comme ci-dessous.
```
_index.en.md              default-zones.en.md       zone-10-59-114.en.md      zone-hr-rtlab1-net.en.md
_index.fr.md              default-zones.fr.md       zone-10-59-114.fr.md      zone-hr-rtlab1-net.fr.md
```

Vous avez maintenant besoins d'un fichier par langue traduite si vous voulez que votre page soit afficher pour les pages traduites.

## Tags

Hugo is also able to manage tags.
To enable the tags, you first need to go in your **config.toml** and add :
Hugo est aussi capable de gérer des tags.
Pour les activers, vous devez en premier lieur ajouter les lignes suivantes dans votre fichier **config.toml**
```
[[menu.shortcuts]]
name = "<i class='fas fa-tags'></i> Tags"
url = "/tags"
weight = 30
```
Ainsi vous pourrez ajouter des tags dans les header de vos contenue comme ci-dessous.
```
---
title: "Default-Zones"
date: 2021-10-21T17:18:05+02:00
draft: false
weight: 5
tags: ["useful","config","dns","alpine1"] # Nouvelle section des tags
---
```

## Commandes utiles

Regénère vos fichier static dans le **./public**
```
hugo
```
Démare le serveur de debugage joignable grace à http://localhost:1313/
```
hugo server -D -v
```
Créer un nouveau chapitre
```
hugo new --kind chapter {new_chapter_name}/_index.md
```
Créer un nouveau contenue
```
hugo new {chapter}/content.md 
#Si dans un sous-chapitre écriver le chemin d'acces complet
hugo new {chapter-1}/{chapter-...}/content.md
```


