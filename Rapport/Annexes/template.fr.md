---
title: "Exemple de template Flask"
date: 2021-10-21T17:35:34+02:00
draft: false
tags: ["rapport", "Annexes"]
weight: 3
---

```html
<header class=" header flex w-full h-14 md:h-20  items-center text-2xl font-extrabold text-white space-x-5">
    <div>
        <button class="px-5 grow hidden md:block"><a href="/">SDN-Cloudstack</a></button>
    </div>
    <!---- Menu fold button ---->
    <div class="flex-1 flex justify-end items-center align-middle">
        <button class="block md:hidden" onclick="toggleMenu()">
            <svg class="h-6 w-6 fill-current text-white" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20">
                <path d="M0 3h20v2H0V3zm0 6h20v2H0V9zm0 6h20v2H0v-2z"/>
            </svg>
        </button>
    <div>
        <select class="header text-white text-sm md:text-xl align-middle" onchange="if (this.value) window.location.href=this.value">
            {%for room in api%}
                {% if selected == room %}
                    <option value="./{{room}}" selected>{{room}}</option>
                {%else%}
                    <option value="./{{room}}">{{room}}</option>
                {%endif%}
            {%endfor%}
        </select>
    </div>
    <div class="flex-auto text-center">
        <p class="text-sm md:text-xl align-middle">{{title}}</p>
    </div>
    {% if user %}
        <div class="flex-auto text-center">
            <button class="px-5 text-sm md:text-xl align-middle"><a href="/logout">{{ user }}</a></button>
        </div>
    {%else%}
        <div class="flex-auto text-center">
            <button class="px-5 text-sm md:text-xl align-middle"><a href="/login">Login</a></button>
        </div>
    {%endif%}
</header>
```

Les blocs entre crochets sont des blocs de pseudo-python intégrés dans le template.