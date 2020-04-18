---
layout: post
title:  "Daedalus And dScript"
date:   2020-04-17 02:00:00 -0000
categories: daedalus games languages
tags: daedalus games languages
---

Daedalus was my initial attempt at making an indie video game in [Unity][unity]. The game was inspired by playing Dungeon and Dragons 3.5 with friends in university, and getting way too into drawing intricate maps, with strange combat mechanics, and custom rules to spice everything up. It was fun, but tedious. So I had the thought, what if there was a table top simulator that didn't just let people see everyone else's tokens, but took the immense amounts of simple mathematics that comes along with table top games, and makes encounters with more than 5 enemies a headache, and used computer to do what they are good at, namely immense amounts of simple mathemetics.

So the goal was, to make a table top simulator with its own rule set. But the best part of table top RPGes is the immense amount of flexibility granted to the game master, so the plaers aren't just playing against a system. So it also needed to be perfectly flexible for the game master. 

Doing all this required a system which had rules baked into it, and yet allowed the game master to break it whenever they wanted. Hey, why stop there, maybe the game master should be able to edit and write the rules however they like as well? So yeah. That was a goal too. So cool, a simulater with a robust map maker and built in rules for the players, where everything can be programmed and changed by the game master, either before the game or on the fly.

This collection of goals motivated the creation of dScript or daedScript.

&nbsp;

## dScript

dScript is a scripting language that I wrote myself in C#. You can find the main logic for it [here][daedscript]. If you clicked on the link you'd saw it's a bit of a monster. But that's what you end up with when you write your own tokenizer, parser, and intepreter. The structure of it is heavily based on projects I did in Brown's [CS1730: Design and Implementation of Programming Languages][langs]. The language is a functional language, with pass by value functions, first class functions, and also extended to support some things like for and while loops. The reason behind making it functional in a system that really likes object oriented programming like a video game is, one, I like functional languages. Having had a great amount of exposure to mathematics before I started studying computer science or learned any coding, the idea that you execute functions and they return results just makes sense to me. Secondly, the idea is that objects, such as characters, rules, and items are instantiated in the game, and scripts are meant to interact with them, not define them. So the language is able to access the variables associated with these objects or add more variables to them, or create no ones, but you can't make your own custom classes.

It was a fun project, and dScript now works. Though it was frustrating debugging the code when I also wrote the error handling myself, so I was unsure as to whether errors were in the scripts I was testing with, the code behind dScript, or my error handler.

Anyways, I've tabled working on Daedalus in general for now. It was too ambitious a first project for working with Unity, and although I was able to get a working system where a player could control various characters beholden to a ruleset written in dScript, the need for customizability and integration with multiplayer meant there was still a ways to go. I hope to return to it eventually when I'm more familiar with Unity and understand the necessary structure for a project of this scope (and more familiar with the system of gameObjects which is relatively unfriendly towards engineers who are interested in coding everything from scratch).

&nbsp;

&nbsp;

&nbsp;

&nbsp;

[unity]: https://unity.com/
[daedscript]: https://github.com/Buggy-Virus/daedalus-0.1/blob/master/Assets/DaedScript/DaedScript.cs
[langs]: http://cs.brown.edu/courses/csci1730/