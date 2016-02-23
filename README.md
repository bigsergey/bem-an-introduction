# BEM: An Introduction
**BEM is a methodology that helps you create reusable and maintainable code. Do you want to start following BEM? This text will cover the basics for you.**
Dividing a project into smaller parts is a natural thing you want to do when creating an app or a website. You want to be able to reuse some sequences, and similarly to Angular’s directives or React’s components, BEM is the way to make sure your CSS code is easier to develop & maintain.

For Javascript and HTML we have no problem to sensibly divide our app, but CSS is a different story. Usually, the bigger the project, the more complicated the CSS – the app becomes more difficult to develop and maintain. You can see an example of code that is hard to maintain below:

```html
<div class="message user banned">
  <img  class="image photo" src=""/>
  <p class="body info"></p>
</div>
```
It’s hard to tell what is the relation between the classes – is '.banned' related to the user or to the message? Does '.info' concern the message or the user?

This code snippet is more readable:
```html
<div class="message message--banned user">
  <img class="message__image user__photo" src=""/>
  <p class="message__body user__info"></p>
</div>
```

As you can see, it’s clear where the classes belong to and what are the relations between them. This particular code piece is in line with **BEM – a methodology for achieving reusable components in CSS**. This article will teach you more about its origins, naming conventions and writing CSS styles according to its rules.

Before we jump into details, let’s start with a brief background of this methodology.

## Why BEM?

BEM was actually created quite a while ago, in 2005 at Yandex. Yandex is a leading Russian Internet company and, while running multiple projects, they needed to standarise their code. The visual interface of Yandex’s products was similar, but the code, created in separate teams, was not reusable. Teams used different naming conventions and different methodologies. Small changes, like introducing a new team member, were time-consuming, since getting familiar with the code was a lengthy process. These issues were adressed when BEM started to be used across the company. At the beginning it was just a set of rules which then evolved into a whole methodology.

You don’t necessarily encounter similar issues at work, especially when you work for a startup or a software house, not a multiteam corporation. Be that as it may, there are still ways in which BEM could prove effective.

Let’s analyze this situation – your project manager comes to your desk and asks you to move one element of the page you’re currently working on. The HTML portion of the code is easy to transfer, the CSS styles, however, can end up being broken. In order not to cause any mistakes, we add more styles or increase the specificity of classes and selectors. At the end of the day, this code becomes difficult to maintain and hardly reusable. BEM is able to solve these problems.

## The essentials

BEM stands for **Block**, **Element**, **Modifier** which are the BEM entities:

### BLOCK

Block is a logically independent component that encapsulates styles, behavior or implementation technologies. The fact that blocks are indepentent allows us to easily reuse them.

Other features of blocks:
* nested structure (blocks can consist of other blocks),
* arbitrary placement (blocks will work properly even when you change their position on the page or move them to another project).

### ELEMENT

Element is a part of a block that can’t be used outside of it (e.g. items within the menu block).

### MODIFIER

Modifier is a BEM entity that defines the state, appearance and behavior of blocks or elements – identical blocks can look different because of a modifier. The use of this entity is optional.

### MIX

Mix is a way of hosting different BEM sequences on a single DOM node. Owing to that you can:
* combine styles and behavior of different BEM entities (no code duplication),
* create new components based on the existing entities.
