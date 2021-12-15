---
title: "Research Hugo"
date: 2021/10/22
tags: ["research","hugo"]
draft: false
---

In the folowing part, we will see the test we made on hugo to make it work and create that web-site.

(Warning the syntax might change a bit depending on the theme you use)

## Creating the hugo-web-site

Making an hugo-web-site is quite easy, once you had download hugo on your server.
You need to run :
``` 
hugo new site {site_name} 
```
That should give you something like that :
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
You now got this new folder.

## Hugo basic files

Hugo will generate those files for you and we will quickly go through the most important one.
```
3105-alpine-1:/home/hugo/presentation/presentation# ls
archetypes   config.toml  content      data         layouts       static       themes
```

### Config file


**config.toml** is the config files for your web site. By default it's look like the following.


### **./content** Folder

The **content** folder is the place where you will put all your content.
### **./themes** Folder

The **themes** folder is were you will download trough github the different theme that you may use.

### **./public** Folder

The **public** folder will be generated once you start your server or reload it through the command ```hugo```. The **./public** files will contain the files that you should display on your web-site.

Those are the main files and folder that you will used. The other folder are mostly used to generate the web-site but you don't need to go trough those folder other than for making your own themes.

## Choosing a theme

For that part I will be using [hugo-learn-theme](https://github.com/matcornic/hugo-theme-learn) as an exemple.
To start we need to be in the **./themes** folder. There you will run the git clone command found on your theme page [more-theme-there](https://themes.gohugo.io/). In our case :
```
git clone https://github.com/matcornic/hugo-theme-learn.git
```
You now got a new theme in your files.

To make a theme effectif you need to add your folder name as a variable 
```
echo "theme = \"hugo-theme-learn\"" >> config.toml
```
You now have your theme load as default.

## Making new Chapter and new content

Creating content is quite easy in fact. You got 2 options, one automatic and the other one manual.

### Trough command

The command to make a chapter and a content are quite similar.
```
#Create a new chapter
3105-alpine-1:/home/hugo/presentation/presentation# hugo new --kind chapter demo/_index.md
/home/hugo/presentation/presentation/content/demo/_index.md created

#Create a new posts
3105-alpine-1:/home/hugo/presentation/presentation# hugo new demo/my-first-content.md
/home/hugo/presentation/presentation/content/demo/my-first-content.md created
```
As you can see you need to add **--kind chapter** in your command to create the chapter files. Don't foget to create your **_index.md** for every chapter you made, that will be used as a reference to display.

Once you used those command, a files will be generated in the content folder.
```
3105-alpine-1:/home/hugo/presentation/presentation# ls content/
demo
3105-alpine-1:/home/hugo/presentation/presentation# ls content/demo/
_index.md            my-first-content.md
```
The chapter files and the posts files will always have a specific header like follow.

**_index.md**
```
+++
title = "Demo" # name of the chapter
date = 2021-10-22T18:18:48+02:00
weight = 5 # place in the nav 
chapter = true # defined it as a chapter
pre = "<b>X. </b>" # used to define the 1. in the nav section
+++
```
**my-first-content.md**
```
---
title: "My First Content" # Title of your content
date: 2021-10-22T18:18:48+02:00 # date of creation
draft: true # place to false to display it on the web site
---
```
We can notice a difference beetween both of them  as the chapter will be using ```+++``` and the content will be using ```---``` . 

Following ```---``` you will then place the content you want to display in markdown.

### manually 

The manual way is also quite easy, you just need to create your files and folder in the **./content** and using at the beginning of your files the header we see above acording of your content. Most important, don't forget about the **_index.md** in every folder you want to display on your web-site.

## Multiple language

With hugo you can easly manage multiple language. The first things you need to do is adding a couple of line in your **config.toml** like following.
```
defaultContentLanguage = "en"
defaultContentLanguageInSubdir= true

[Languages]
[Languages.fr] # language reference for the automatic language switch
title = "Documentation du projet SDN" 
weight = 1 # used to defined the order in the switch
url ="/fr" # where your files will be found in your ./public folder
landingPageName = "<i class='fas fa-home'></i> Accueil" # acces to the home page
languageName = "Français" # name of the language

[Languages.en]
title = "Documentation for the SDN project"
weight = 2
url="/en"
landingPageName = "<i class='fas fa-home'></i> Redirect to Home"
languageName = "English"
```
By adding those line we have now a language switch button at the end of our nav section.
There will now be needed for every new content that you create multiple files like :
```
_index.en.md              default-zones.en.md       zone-10-59-114.en.md      zone-hr-rtlab1-net.en.md
_index.fr.md              default-zones.fr.md       zone-10-59-114.fr.md      zone-hr-rtlab1-net.fr.md
```
You now need one files for every language you translate, otherway the content won't be display on your web-site.

## Tags

Hugo is also able to manage tags.
To enable the tags, you first need to go in your **config.toml** and add :
```
[[menu.shortcuts]]
name = "<i class='fas fa-tags'></i> Tags"
url = "/tags"
weight = 30
```
Then you will be able to add the tags section in the header of your different content like :
```
---
title: "Default-Zones"
date: 2021-10-21T17:18:05+02:00
draft: false
weight: 5
tags: ["useful","config","dns","alpine1"] # new tags section
---
```

## Useful command 

Regenerate your static files :
```
hugo
```
Start the debug server of hugo reachable on http://localhost:1313/
```
hugo server -D -v
```
Create new chapter:
```
hugo new --kind chapter {new_chapter_name}/_index.md
```
Create new content:
```
hugo new {chapter}/content.md 
# if in subchapter need to make the complete path
hugo new {chapter-1}/{chapter-...}/content.md
```

