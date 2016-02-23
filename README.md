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
* b – common blocks (b-menu, b-message), name of the block is preceded by 'b”
* l'– layouts (grid)
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

CodePen [demo](http://codepen.io/bigsergey/pen/vLWxaJ).

## BEM vs Bootstrap/Foundation/Sematic-UI/etc.
The difference between BEM and Bootstrap/Foundation/Sematic-UI/etc. is that the latter are the collections of ready-made blocks. BEM, on the other hand, is a methodology that allows you to create the architecture based on independent blocks. By the way, Google’s [Material Design](http://www.getmdl.io/) Lite was built using BEM naming rules.
```html
<!-- Colored FAB button -->
<button class="mdl-button mdl-js-button mdl-button--fab mdl-button--colored">
  <i class="material-icons">add</i>
</button>
```

## BEM: The Good Parts
### How to fix .login__form__user-name__input?
That is one of the most common mistakes caused by not properly understanding BEM guidelines. You are not able to benefit from BEM’s advantages when the elements are related to each other and not to a block. Take a look at this piece of code:
```html
<div class="block">
    <div class="block__elem1">
        <div class="block__elem1__elem2"></div>
    </div>
</div>
```
It can be refactored in two ways – you may create a new block or change the block’s structure:
```html
<div class="block1">
    <div class="block1__elem1 block2">
        <div class="block2__elem1"></div>
    </div>
</div>
 
<!-- OR -->
 
<div class="block1">
    <div class="block1__elem1">
        <div class="block1__elem2"></div>
    </div>
</div>
```
In both cases, the elem1 is no longer dependent on elem2, which makes the code easier to maintain and doesn’t cause problems when you have to move elem2. The rule of thumb here is: whenever you feel like you need to create an element within another element, create a new block instead.

### Good structure, bad CSS styles

Let’s assume we have a following block:
```html
<div class="block">
    <div class="block__element">
    </div>
</div>
```
It is a perfectly fine structure according to BEM. The styles, however, look like that:
```css
.block .block__element {
  ...
}
```
The main idea behind BEM is the independence of blocks. Nested selectors increase code coupling and make it more difficult to reuse it which, of course, is not what BEM should be about. Styles should look like this:
```css
.block {
  ...
}
.block__element {
  ...
}
```

### Combined Selectors
You may wonder whether the need of preceding each modifier with a block name isn’t an overkill.
```html
<div class="block mod"></div>
<!-- instead -->
<div class="block block--mod"></div>
```
In fact, there are good reasons for sticking to the block–mod structure:
* Namespace. Blocks, elements and modifiers are unique, which helps to limit the influence of one block’s styles on another.
* Mixes. When you mix two different blocks on a single DOM node you need to know which block is a given modifier referring to.
```html
<div class="menu__item button active">Button is active or menu item?</div>
```
* Code search. When you search for a modifier called 'active' you will probably find several such instances in your code but searching for, let’s say, 'button–active' will narrow down your search significantly.

### Global modifier

Imagine you need a global 'hidden' style and you create a 'hidden' class.
```css
/* global modifier */
.hidden { display: none }
 
/* block definition */
.block { display: block }
```
At first sight, everything looks OK, so you create an html block and apply the global modifier.
```html
<div class="block hidden">
    you still see me
</div>
```
The issue is that the block selector is equally specific as the global modifer and, additionally, it appears under it in the code. As a result the block overwrites the modifier. Of course, we could use !important in the modifier’s definition, but this could be even more troublesome (more about these issues [here](http://stackoverflow.com/questions/3706819/what-are-the-implications-of-using-important-in-css)).

The next problem of global modifiers is connected to BEM-entities mixing.
```html
<div class="block mod1 mod2">
    you have no control over the block
</div>
```
In this case you lose control over the block and you may end up with unexpected behavior when you use this block in another project.

### BEM & SASS

Sass allows you to write CSS styles in different manners. The code presented below can be generated using Sass and “&”, which refers to the current parent selector.
```css
.button { display: block; }
.button__text { font-weight: bold; }
.button__text--active { color: red; }
```
SCSS code:
```scss
.button {
  display: block;
  &__text {
    font-weight: bold;
    &--active {
      color: red;
    }
  }
}
```
This kind of code takes less space and is convenient to write (no need to type names for blocks, elements or modifiers). On the other hand, however, it will be much more difficult to find a given selector in styles (button__button–active vs &–active).

Another thing is that Sass enables you to use the @extend directive. Its function is to apply one selector’s features into another (see [Sass docs](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#extend) for more information). As a result we would have:
```html
<div class="block--mod"></div>
<!-- instead -->
<div class="block block--mod"></div>
```
It seems to be just fine, there is less code for HTML, the block’s styles are applied to the modifier using @extend. This approach has flaws when it comes to CSS (the styles are oversized):
```css
/* good */
.menu,
.menu--hidden,
.menu--other-modifier {
 // base styles
}
 
/* better */
.menu {
 // base styles
}
.menu--hidden {...}
.menu--other-modifier {...}
```
Yet another issue arises when we want to apply two modifiers at the same time – the styles will apply twice as well.

### CSS property name in a modifier name – .block__element–background-color_red

When changing a component, you need to alter not only the CSS code but also the selectors’ names. For example, when the background color changes, then you have to edit the HTML code, the styles and, possibly, even JS. Once you add different features to the modifier, its name no longer makes sense.

### Don’t be afraid of long class names

From [Serge Herkül’s Twitter](https://twitter.com/_sergeh), frontend developer at Teamweek:
> Focus on self documenting class names. Don’t be afraid of long class names! His advice – “Use long, descriptive class names over short names that don’t document themselves.”

## Should you start using BEM?

Personally, I cannot recommend using BEM enough. One of the most important advantages is that you don’t have to introduce any global changes in your project before you start using BEM. All you need to do is to create a new component, following BEM rules. Trust me, BEM is very forgiving, if you can’t get it right from the get go, nothing terrible will happen. Aren’t you convinced by now?

Stay BEMed and let me know in the comments if you have any extra questions.

Link to [article](http://blog.apptension.com/2016/02/03/introduction-to-bem/) on the [Apptension blog](http://blog.apptension.com/).

Link to my [LET'S WRITE BEM CORRECTLY](http://slides.com/sergeybolshov/bem#/) presentation.

Thank you [@aniakrajenka](https://twitter.com/aniakrajenka) for help with english. 

