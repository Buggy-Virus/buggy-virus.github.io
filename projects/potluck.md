---
layout: project
title:  "Potluck"
pseudo-path: "potluck"
given-date:  "Feb, 2020"
categories: algorithms rpg games
tag: "potluck"
tags:  algorithms rpg games
languages:  "C#"
project-github:  "https://github.com/Buggy-Virus/potluck"
private-github:  false
project-page:  false
menu-img:  "/assets/blank.png"
menu-img-alt: "making maps for fun and fights"
brown: false
---
Potluck is an indie video game I'm working on with a close friend. The game is an isometric tactical RPG, similar to other games based on the Dungeon and Dragon formula. The game is centered around procedural generation. The player maintains a roster of classed adventurers and send them into procedurally generated dungeons to progress the story, gain experience and get sweet loot.

The bread and butter of the game is the procedural generation, so I'm working very hard on algorithms to created random dungeons that feel both unique and organic feeling dungeons. This means abandoning a tile or sector system, where predetermined rooms with some random elements are slotted into alignments where they connect. Instead rooms are generated starting from overlapping hyperrectangles, then various features and architecture is added or removed throughout the rooms. Rooms are laid out with randomly according to various random parameters in 3d space. From there various graphing algorithms are used to determine both the connections between accessible areas in rooms as well as their dependencies, such as locked doors and keys, in order to create an interesting gameplay flow through levels which is neither completely random or aggressively contrived.

Currently working diligently and hoping it eventually meets a Steam release at some point in the future.
