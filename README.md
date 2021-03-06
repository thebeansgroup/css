# Airbnb CSS / Sass Styleguide

*A mostly reasonable approach to CSS and Sass*

## Table of Contents

  1. [Terminology](#terminology)
    - [Rule Declaration](#rule-declaration)
    - [Selectors](#selectors)
    - [Properties](#properties)
  1. [CSS](#css)
    - [Formatting](#formatting)
    - [Property Separation] (#property-separation)
    - [Comments](#comments)
    - [OOCSS and BEM](#oocss-and-bem)
    - [Module Sections Separation] (#module-sections-separation)
    - [ID Selectors](#id-selectors)
    - [Modular Scale] (#modular-scale)
    - [Colour Helpers] (#colour-helpers)
    - [Z-index Layer Rules] (#z-index-layer-rules)
  1. [Sass](#sass)
    - [Syntax](#syntax)
    - [Ordering](#ordering-of-property-declarations)
    - [Mixins](#mixins)
    - [Placeholders](#placeholders)

## Terminology

### Rule declaration

A “rule declaration” is the name given to a selector (or a group of selectors) with an accompanying group of properties. Here's an example:

```css
.listing {
  font-size: 18px;
  line-height: 1.2;
}
```

### Selectors

In a rule declaration, “selectors” are the bits that determine which elements in the DOM tree will be styled by the defined properties. Selectors can match HTML elements, as well as an element's class, ID, or any of its attributes. Here are some examples of selectors:

```css
.my-element-class {
  /* ... */
}

[aria-hidden] {
  /* ... */
}
```

### Properties

Finally, properties are what give the selected elements of a rule declaration their style. Properties are key-value pairs, and a rule declaration can contain one or more property declarations. Property declarations look like this:

```css
/* some selector */ {
  background: #f1f1f1;
  color: #333;
}
```

## CSS

### Formatting

* Use soft tabs (2 spaces) for indentation
* Prefer dashes over camelCasing in class names. Underscores are OK if you're using BEM (see [OOCSS and BEM](#oocss-and-bem) below).
* Do not use ID selectors
* When using multiple selectors in a rule declaration, give each selector its own line.
* Put a space before the opening brace `{` in rule declarations
* In properties, put a space after, but not before, the `:` character.
* Put closing braces `}` of rule declarations on a new line
* Put blank lines between rule declarations

**Bad**

```css
.avatar{
    border-radius:50%;
    border:2px solid white; }
.no, .nope, .not_good {
    // ...
}
#lol-no {
  // ...
}
```

**Good**

```css
.avatar {
  border-radius: 50%;
  border: 2px solid white;
}

.one,
.selector,
.per-line {
  // ...
}
```
### Property Separation

Properties should be separated into two groups: those which affect the structure or positioning of the element and those which affect the styling of the element. Separate these properties in the class with a newline.

**Example**

```css
.example {
  display: inline-block;
  height: ms(0);
  width: ms(4);
  position: absolute;
  top: 0;
  right: 0;

  border: 1px solid blue(3);
  color: blue(3);
  font-size: ms(0);
  text-shadow: 4px 4px 2px green(1);
}
```

### Comments

* Prefer line comments (`//` in Sass-land) to block comments.
* Prefer comments on their own line. Avoid end-of-line comments.
* Write detailed comments for code that isn't self-documenting:
  - Uses of z-index
  - Compatibility or browser-specific hacks

### OOCSS and BEM

We encourage some combination of OOCSS and BEM for these reasons:

  * It helps create clear, strict relationships between CSS and HTML
  * It helps us create reusable, composable components
  * It allows for less nesting and lower specificity
  * It helps in building scalable stylesheets

**OOCSS**, or “Object Oriented CSS”, is an approach for writing CSS that encourages you to think about your stylesheets as a collection of “objects”: reusuable, repeatable snippets that can be used independently throughout a website.

  * Nicole Sullivan's [OOCSS wiki](https://github.com/stubbornella/oocss/wiki)
  * Smashing Magazine's [Introduction to OOCSS](http://www.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/)

**BEM**, or “Block-Element-Modifier”, is a _naming convention_ for classes in HTML and CSS. It was originally developed by Yandex with large codebases and scalability in mind, and can serve as a solid set of guidelines for implementing OOCSS.

  * CSS Trick's [BEM 101](https://css-tricks.com/bem-101/)
  * Harry Roberts' [introduction to BEM](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)

**Example**

```css
.person {}
.person__hand {}
.person__hand--left {}
.person--female {}
.person--female__hand {}
.person--female__hand--left {}
```

  * `.person` is the “block” and represents the higher-level component
  * `.person__hand` is an “element” and represents a descendant of `.person` that helps compose the block as a whole.
  * `.person__hand--left` is a “modifier” and represents a different state or variation on the `.person__hand` block.

### Module Sections Separation

(S)CSS modules should be broken into sections, typically by the modifications of that module. These sections should be separated using comment blocks. A module should always begin with the module name and author of the module and have a default section and then optional additional sections, depending on the module. See below for an example of the BEM example used above being separated into sections:

**Example**

```css
//
// BEM Example Module
// $author Your Name


// ==========================================================================
// Default Person
// ==========================================================================

.person {}
.person__hand {}
.person__hand--left {}


// ==========================================================================
// Female Person
// ==========================================================================

.person--female {}
.person--female__hand {}
.person--female__hand--left {}
```

### ID selectors

While it is possible to select elements by ID in CSS, it should generally be considered an anti-pattern. ID selectors introduce an unnecessarily high level of [specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) to your rule declarations, and they are not reusable.

For more on this subject, read [CSS Wizardry's article](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/) on dealing with specificity.

### Modular Scale

When defining sizes (widths, paddings, margins etc.) always use the relative `em` unit. SASS includes a modular scale mixin which provides a number of `em` unit size breakpoints. Always use this modular scale mixin for sizes if possible. See http://www.modularscale.com/?1,9.0625&em&1.5&sass&text for a visual representation of the breakpoints and see below for an example of using the modular scale mixin.

**Example**

```css
.example {
  width: ms(4);
  padding: ms(-1) * 1.5;
}
```

### Colour Helpers

When using colours, do not define your own colours. Instead use the Plinth colour helpers (defined here: https://github.com/thebeansgroup/plinth/blob/master/vendor/assets/stylesheets/_settings-colours.css.scss) to use a set of predefined colours.

**Example**

```css
.example {
  background: blue(2);
  color: blue(3);
  border: 1px solid mono(0);
}
```

### Z-index Layer Rules

To help avoid issues when using z-index, assign z-indexes according to the elements layer. The layers are are in groups of 10s as follows:

```
- UI        = 0 - 9
- Tooltips  = 10 - 19
- Takeovers = 20 - 29
- Modals    = 30 - 39
```

The 9 in each level should be reserved as an override, acting as an `!important`. This way, we can ensure an element is higher than all others in that layer and previous layers.

**Example**

```css
.takeover--example1 {
  z-index: 20;
}

.takeover--example2 {
  z-index: 21;
}

.tooltip {
  z-index: 10;
}

.tooltip--override {
  z-index: 19;
}
```

## Sass

### Syntax

* Use the `.scss` syntax, never the original `.sass` syntax
* Order your `@extend`, regular CSS and `@include` declarations logically (see below)

### Ordering of property declarations

1. `@extend` declarations

    Just as in other OOP languages, it's helpful to know right away that this “class” inherits from another.

    ```scss
    .btn-green {
      @extend %btn;
      // ...
    }
    ```

2. Property declarations

    Now list all standard property declarations, anything that isn't an `@extend`, `@include`, or a nested selector.

    ```scss
    .btn-green {
      @extend %btn;
      background: green;
      font-weight: bold;
      // ...
    }
    ```

3. `@include` declarations

    Grouping `@include`s at the end makes it easier to read the entire selector, and it also visually separates them from `@extend`s.

    ```scss
    .btn-green {
      @extend %btn;
      background: green;
      font-weight: bold;
      @include transition(background 0.5s ease);
      // ...
    }
    ```

4. Nested selectors

    Nested selectors, _if necessary_, go last, and nothing goes after them. Add whitespace between your rule declarations and nested selectors, as well as between adjacent nested selectors. Apply the same guidelines as above to your nested selectors.

    ```scss
    .btn {
      @extend %btn;
      background: green;
      font-weight: bold;
      @include transition(background 0.5s ease);

      :hover {
        background: blue(1);
      }
    }
    ```

### Mixins

Mixins, defined via `@mixin` and called with `@include`, should be used sparingly and only when function arguments are necessary. A mixin without function arguments (i.e. `@mixin hide { display: none; }`) is better accomplished using a placeholder selector (see below) in order to prevent code duplication.

### Placeholders

Placeholders in Sass, defined via `%selector` and used with `@extend`, are a way of defining rule declarations that aren't automatically output in your compiled stylesheet. Instead, other selectors “inherit” from the placeholder, and the relevant selectors are copied to the point in the stylesheet where the placeholder is defined. This is best illustrated with the example below.

Placeholders are powerful but easy to abuse, especially when combined with nested selectors. **As a rule of thumb, avoid creating placeholders with nested rule declarations, or calling `@extend` inside nested selectors.** Placeholders are great for simple inheritance, but can easily result in the accidental creation of additional selectors without paying close attention to how and where they are used.

**Sass**

```sass
// Unless we call `@extend %icon` these properties won't be compiled!
%icon {
  font-family: "Airglyphs";
}

.icon-error {
  @extend %icon;
  color: red;
}

.icon-success {
  @extend %icon;
  color: green;
}
```

**CSS**

```css
.icon-error,
.icon-success {
  font-family: "Airglyphs";
}

.icon-error {
  color: red;
}

.icon-success {
  color: green;
}
```
