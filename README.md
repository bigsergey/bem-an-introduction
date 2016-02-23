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

## Naming Conventions

The idea behind various BEM naming conventions is to make them as informative and easy to understand as possible. We’ll take a look at several sets of naming rules:

### Yandex style

* **Block**
```html
<div class="block-name"></div>
```
The block name consists of lowercase Latin characters, separate words are divided with hyphens:
```
<!-- html -->
<div class="menu">...</div>
 
/* css styles */
.menu { color: red }
```

* **Element**
```html
<div class="block-name__element-name"></div>
```
The name of the element should be preceded by a double underscore.
```
<!-- html -->
<div class="menu">
    ...
    <span class="menu__item"></span>
</div>
 
/* css styles */
.menu__item { color: red; }
```
**REMEMBER!** It is not recommended to create elements within elements like: block_element1__element2, the structure of a block should be flat. The DOM’s block, however, can be nested.
CSS:
```css
.block {}
.block__element1 {}
.block__element2 {}
```
HTML:
```html
<div class="block">
  <div class="block__element1">
    <div class="block__element2"></div>
  </div>
</div>
```

*  **Modifier**
```html
<div class="block-name__element-name_mod-name_mod-val"></div>
```
Modifiers are preceded by single underscores. Yandex provides us with two schemes:
* for Boolean modifiers (these are actually just the name modifiers that could be described with a single word),
* for key-value type modifiers (e.g. for seasonal themes).
```
<!-- html -->
<div class="menu menu_hidden">...</div>
<div class="menu menu_theme_xmas">...</div>
 
/* css styles */
.menu_hidden { display: none }
.menu_theme_xmas { color: green; }
```

### Harry Roberts’ Style
Harry Roberts thought that marking the modifer with a single underscore can be difficult to distinguish from the elements with double underscore. In his convention, modifier is preceded by a double hyphen which makes it more readable:
```html
<div class="block-name__element-name--state_active"><div>
```

### CamelCase Style
You can use CamelCase spelling instead of hyphens for Blocks and Elements:
```html
<div class="blockName__elementName--state_active"></div>
```

### 'Sans underscore' Style
Here, not only is CamelCase used, but you also separate blocks from elements using single hyphens (modifiers are separated by double hyphens).
```html
<div class="blockName-elementName--modName--modVal"></div>
```

### Prefixes
You can use prefixes in your block names:
* b – common blocks (b-menu, b-message), name of the block is preceded by “b”
* l – layouts (grid)
* js – javascript prefix (I personally use it to mark the fact that a given element uses javascript, so its removal may cause incorrect behavior.)
* qa – used sometimes for testing the views
* This list can be expanded, of course, depending on the project.

### Naming Conventions in Practice
Below you will see a simple implementation of user list with three users. Each block consists of user’s name and age, additionally, there are three types of users (inactive, regular, premium). These types are changed using modifiers:

```html
<div class="user user--inactive">
  <div class="user__name">Inactive user</div>
  <div class="user__age">16 years old</div>
</div>
<div class="user">
  <div class="user__name">Normal user</div>
  <div class="user__age">18 years old</div>
</div>
<div class="user user--premium">
  <div class="user__name">Premium user</div>
  <div class="user__age">18 years old</div>
</div>
```

```css
.user {
  font-size: 25px;
  width: 200px; 
  margin:0px auto;
}

.user--inactive {
  opacity: 0.5;
}
.user--premium {
  color: red;
}

.user__name {
  font-weight: bold;
}
.user__age {
 font-style: italic; 
}
```

CodePen [Demo](http://codepen.io/bigsergey/pen/vLWxaJ).