---
layout: project
title:  "Daedalus"
pseudo-path: "daedalus"
given-date:  "Oct, 2018"
categories: daedalus rpg games
tag: "daedalus"
tags:  daedalus rpg games
languages:  "C#,dScript"
project-github:  "https://github.com/Buggy-Virus/daedalus-0.1"
private-github:  false
project-page:  false
menu-img:  "/assets/blank.png"
menu-img-alt: "daedalus"
brown: false
---
This project was inspired by me playing Dungeons And Dragons with friends. I really enjoy being the game master, but would end up spending far too much time structuring and illustrating detailed top down maps, then adding complicated mechanics to the combat in an attempt to elevate the game beyond the "you go, they go" of table top games like Dungeon and Dragons and Pathfinder. Of course this made designing and running encounters a hectic headache for myself.

Daedalus is meant to be a utility to help facilitate playing table top rpgs, because the difficult complexity of table top games is the immense amount of simple mathematics. And it happens computers are terrific about doing immense amounts of simple mathematics. This means a table top simulator where the rules of combat are integrated into the system, allowing players to move their tokens and take actions within the rules, while not sacrificing the flexible controls of the game master and allowing them to edit any tokens and the map on the fly.

This meant integrating a custom scripting language into the game itself, which I dubbed dScript. Then allowing dScript to interact with any of the objects in the games, such as characters, items, or the map, thus allowing game masters to write rule sets into dScript to automatically be executed and allow actions for the players, and also allowing them to write scripts to execute on the fly.

For now I've tabled the project, as it's written in Unity, and was my first go at Unity as well as being incredibly ambitious. The moving parts of everything needing to be perfectly flexible and thus able to access anything else in the game made it all a messy web of dependencies that needed to allow for user input at every step. This coupled with the many very good table top simulaters entering the market at the moment made me decide to table the project.
