# CSS Basics

## Learning Objectives

- [ ] having a general understanding of the purpose of CSS
- [ ] knowing what Cascading Style Sheets means
- [ ] understanding the fundamentals of CSS: CSS syntax, selectors, box model,
      inline & block elements
- [ ] linking stylesheets to the HTML document

## What is CSS?

With CSS (_Cascading Stylesheets_) you can add styling to your HTML elements.

![Comparison of HTML, CSS and JavaScript](assets/animated-gif-for-comparison.gif)

The term _cascading_ in CSS refers to an algorithm that resolves conflicts when multiple styles are defined for a particular element. When deciding which style to apply, CSS takes into account three key factors: specificity, source order, and inheritance.

- Specificity refers to how precisely a selector targets an element. Styles with higher specificity take precedence over those with lower specificity.

- The source order of styles also plays a role in determining which style should be applied. When multiple styles with the same specificity are defined, the style that appears last in the stylesheet will override any previous styles for that element.

- Additionally, CSS allows styles to be inherited from parent elements to their child elements. This means that certain styles can be passed down through the document tree, affecting multiple elements simultaneously.

The term _stylesheet_ refers to a collection of rulesets declared using CSS, usally within a `.css` file.

## Linking Stylesheets

To separate your HTML and CSS code, you can create a new file, like `css/styles.css` and link it to
your HTML file by placing a `<link>` tag in the `<head>` of your HTML document.

```html
<head>
  …
  <link rel="stylesheet" href="css/styles.css" />
</head>
```

## CSS syntax

Any stylesheet consists of a collection of **ruleset**s. A ruleset consists of four parts:

![CSS syntax](assets/css-syntax.png)

|                | Description                                                                                                              |
| -------------- | ------------------------------------------------------------------------------------------------------------------------ |
| Selector       | Selects to which elements the style declarations are applied, followed by curly braces (`{}`) enclosing the declarations |
| Declaration    | A combination of a property and a property value, separated by a colon (`:`) and ending with a semicolon (`;`)           |
| Property       | The property you want to style, e.g. `color`, `font-size`, `text-align`                                                  |
| Property Value | The value assigned to the property, e.g `blue` for the `color` property, `3rem` for the `font-size` property             |

A ruleset can have multiple declarations:

```css
h1 {
  color: blue;
  font-size: 3rem;
  text-align: center;
}
```

## Selectors

There are different CSS selectors you can use to select elements to which you want to apply styles.

### Type selector

The type selector selects all elements of a specific element type.

**Syntax**: `article`, `h1`, `p`, `div`, `a`, `input`, `button`, …

**Example**:

Select all `article` elements.

```css
article {
  color: red;
}
```

```html
<article>…</article>
```

### Class selector

The class selector selects all elements that have the specified class.

**Syntax**: `.superpink` (the user defined class name from the HTML but starting with a dot `.`)

**Example**:

Select all elements with the class `superpink`.

```css
.superpink {
  color: hotpink;
}
```

```html
<aside class="superpink">…</aside>
```

HTML elements can have multiple classes separated by a space. The selector `.superpink` would
also select the following element:

```html
<aside class="broccoli superpink some-other-class">…</aside>
```

The order of the classes in the HTML attribute doesn't matter.

### Pseudo-classes

The pseudo-class selector selects all elements that are in a specific state. It is used in combination with other selectors.

**Syntax**: `:hover`, `:focus`, … (the pseudo-class name starting with a colon `:`)

#### `:hover`

Selects an element when you hover over it with the mouse.

**Example**:

Select all hovered links.

```css
a:hover {
  color: hotpink;
}
```

```html
<a href="https://www.neuefische.de">neuefische</a>
```

#### `:focus`

Selects an element when it is focused. This is usually the case when you click into an input field or select an element with the tab key.

**Example**:

Select all focused input fields.

```css
input:focus {
  border: 1px solid hotpink;
}
```

```html
<input type="text" />
```

#### Other pseudo-classes

There are many more pseudo-classes like `:active`, `:first-child`, `:last-child`, `:first-of-type`, `:last-of-type`, `:nth-child()`, `:nth-of-type()`, `:not()`, …

> 📙 You can find a list of all [**Pseudo-classes** on mdn](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes).

### Attribute selectors

The attribute selector selects all elements based on the presence or value of a given attribute.

#### Basic attribute selector

Selects all elements with the specified attribute.

**Syntax**: `[attribute]` (attribute name in square brakets `[]`)

**Example**:

Select all elements that have a `type` attribute.

```css
[type] {
  border: 1px solid hotpink;
}
```

```html
<input type="text" />
```

#### Attribute value selector

Selects all elements with the specified attribute and value.

**Syntax**: `[attribute="value"]` (attribute name followed by `=` and the attribute value in quotation marks `""` — all in square brakets `[]`)

**Example**:

Select all elements that have a `type` attribute with the value `text`.

```css
[type="text"] {
  border: 1px solid hotpink;
}
```

```html
<input type="text" />
```

#### Advanced attribute selectors

With advanced attribute selectors you can also select elements that have an attribute with a
specific value at the beginning, end or in the middle of the value.

> 📙 You can find more information about [**Attribute selectors** on the mdn](https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors).

### Universal selector

The universal selector `*` selects all elements in the document.

**Syntax**: `*`

**Example**:

Select all elements.

```css
* {
  border: 1px solid hotpink;
}
```

> ❗️ The universal selector is rarely used for anything but resets. Do not use it unless you know what you are doing.

## Combining Selectors

Combinators are used to combine multiple selectors to create a new selector.

### Combine multiple selectors with a comma

You can combine multiple selectors with a comma to create a new selector that selects all elements that are selected by **any one** of the selectors.

**Syntax**: `selector1, selector2, …`

**Example**:

Select all `h1`, `h2` and `h3` elements.

```css
h1,
h2,
h3 {
  color: hotpink;
}
```

### Descendant combinator

The descendant combinator ` ` (space) selects all elements that are descendants (children) of another selector.

**Syntax**: `selector1 selector2 …`

**Example**:

Select all `.superpink` elements that are descendants of an `article` element.

```css
article .superpink {
  color: hotpink;
}
```

```html
<article>
  <p class="superpink">I am pink</p>
  <p>I am not pink</p>
  <footer>
    <p class="superpink">
      I am pink, even though I am not a direct descendant of the article
    </p>
  </footer>
</article>
<p class="superpink">
  I am not pink because I am not a descendant of an article
</p>
```

### Other combinators

There are many more combinators like the direct descendant combinator `>`, the adjacent sibling combinator `+` and the general sibling combinator `~`. A good general rule is to use combinators (except the comma to combine selectors) very sparingly and only when necessary.

> 📙 You can find more information about [**Combinators** on the mdn](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors#combinators).

## CSS Properties

There are a lot of CSS properties and you will discover new ones every day. Therefore the following list shows only a few examples:

| Property           | Effect                                         |
| ------------------ | ---------------------------------------------- |
| `color`            | Color of an elements text                      |
| `font-size`        | Defines the size of a font                     |
| `text-align`       | Defines the alignment of text                  |
| `background-color` | Background color of an element                 |
| `border`           | Defines the border of an element.              |
| `padding`          | Defines the padding of an element.             |
| `margin`           | Defines the margin of an element.              |
| `width`            | This property defines the width of an element. |

> 📙 You can find more properties in the [alphabetic list of **Properties** on CSS-Tricks](https://css-tricks.com/almanac/properties/)
> or in the [**Index** of properties, pseudo-classes, pseudo-elements, data types, functional notations and at-rules on the mdn](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference#index).

## Inheritance

Some CSS properties are inherited from the parent element to the child element. This means that the child element inherits the value of the property from the parent element if it is not set explicitly.

**Example**:

```css
body {
  color: hotpink;
}

p {
  /* The color of the paragraph is hotpink because it is inherited from the body */
}
```

```html
<body>
  <p>I am hotpink</p>
</body>
```

This is very useful for properties like `color` or `font-family` because you can set them on any element and all child elements will inherit the value.

> 📙 You can find more information about [**Inheritance** on the mdn](https://developer.mozilla.org/en-US/docs/Web/CSS/inheritance).

## Box Model

All elements of a website are rectangular boxes described by the **box model**. Each of those boxes has four areas: content, padding, border and margin.

| Box model part | Function                                                               |
| -------------- | ---------------------------------------------------------------------- |
| margin         | The outer space measured from the border to other elements on the page |
| border         | The border of the element                                              |
| padding        | The inner space between the content and the border of the element      |
| content        | The actual content box of the element                                  |

<img src="./assets/box-model.excalidraw.png" width="500" alt="A chart describing the different boxes making up the box model">

The browser knows two ways to calculate the size (`width` and `height`) of an element in this model: `content-box` (the default, old) and `border-box` (the modern variant).

In `content-box` mode, `width` and `height` only describe the size of the content box: The padding and border are added to the size of the element. This can be confusing and lead to unexpected results.

We can set the `box-sizing` property to `border-box` for all elements (using the universal selector) to make the `width` and `height` of an element include the padding and border box.

```css
* {
  box-sizing: border-box;
}
```

Now, the `width` property defines the size of the border box, padding and border width are
subtracted to calculate the available space for the content. This code will be in all used in all future projects to set a sensible default.

<img src="./assets/box-model-border-box-vs-content-box.excalidraw.png" width="768" alt="A chart describing the different boxes making up the box model">

> 💡 The CSS Working Group (which produces the specification for CSS) keeps an [**Incomplete List of Mistakes in the Design of CSS**](https://wiki.csswg.org/ideas/mistakes), saying that `box-sizing: border-box` should have been the default from the start.
>
> It is not possible to change the default behavior of `box-sizing` in the specification and in browsers (or fix any of the other "mistakes"), because it would break many websites that rely on the current behavior.

## Inline and block elements

There are basically two types of elements: inline-level and block-level elements.

### Inline elements

Inline elements **are as wide as their maximum content width** and **flow with the text lines**. They start and end within a line of text. Their box can be cut into multiple parts by line breaks.

Common inline elements include:

- `a`
- `span`
- `strong`
- `em`
- `img`
- `input`
- `button`
- …

### Block elements

Block elements **take up the full width of their parent element** and **always start on a new line**.

Common block elements are:

- `p`
- `h1` - `h6`
- `div`
- `section`
- `article`
- `header`
- `footer`
- `nav`
- …

### Example

In the following example, the `h2` and `p` elements are block-level elements. The `a` element is an inline-level element.

```html
<h2>Coding Bootcamp</h2>
<p>
  If you want to participate in a bootcamp, visit
  <a href="https://www.neuefische.de">neuefische.de</a>
</p>
```

### Display property

You can change the default behavior by using the CSS `display` property.

```css
h2 {
  display: inline;
}
```

This will make all `h2` elements behave like an inline elements. The same works the other way around:

```css
a {
  display: block;
}
```

This will make all `a` elements behave like a block elements.

## Resources

- [CSS on the mdn](https://developer.mozilla.org/en-US/docs/Web/CSS)
- [CSS first steps on the mdn](https://developer.mozilla.org/en-US/docs/Learn/CSS/First_steps)
- [Combinators on the mdn](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors#combinators)
- [Alphabetic List of Properties on CSS-Tricks](https://css-tricks.com/almanac/properties/)
- [Index of properties, pseudo-classes, pseudo-elements, data types, functional notations and at-rules on the mdn](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference#index)
- [Inheritance on the mdn](https://developer.mozilla.org/en-US/docs/Web/CSS/inheritance)
- [CSS styling text on the mdn](https://developer.mozilla.org/en-US/docs/Learn/CSS/Styling_text)
- [box-sizing on the mdn](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing?retiredLocale=de)
- [Incomplete List of Mistakes in the Design of CSS on the CSS Working Group Wiki](https://wiki.csswg.org/ideas/mistakes)

  Handout:
  https://github.com/neuefische/allspice-cgn-fssd-25/blob/main/sessions/css-basics/css-basics.md?plain=1

  ----------------------------------------------------------------------------------------------------------------------------------------------
# CSS Positioning

## Learning Objectives

- using the different types of positioning
- knowing the CSS properties to define a position
- understanding the basics of z-index

---

## Positioning

The position property comes in handy if you want to place an HTML element manually. There are 5
different values to define the position:

| Type                 | Description                                                                                                         |
| -------------------- | ------------------------------------------------------------------------------------------------------------------- |
| `position: static`   | The position of the element is determined by the document flow (default)                                            |
| `position: relative` | Position the element relative to where the element would be placed normally                                         |
| `position: absolute` | Position the element absolutely inside the **nearest non-static ancestor element**                                  |
| `position: fixed`    | Position the element on a fixed position on the screen.                                                             |
| `position: sticky`   | The element is placed normally in the document flow, but keeps an offset relative to its nearest scrolling ancestor |

The position is then specified by the four position properties `top`, `bottom`, `right`, `left`.
These work differently depending on the positioning method.

---

## `position: static`

Elements are positioned according to the normal document flow. The properties `top`, `bottom`,
`right`, `left` have no effect. This is the default value.

---

## `position: relative`

Elements are positioned according to the normal document flow and then displaced by the `top`,
`bottom`, `right`, `left` properties. This method is also used to set the reference frame for an
absolutely positioned child element. By doing so, the child element will be placed absolutely inside
this element.

![example for position relative](assets/position-relative.png)

## `position: absolute`

Elements are removed from the normal document flow and no space is created for them - so they leave
no gap in the page. With position absolute you place an element (with the `top`, `bottom`, `right`,
`left` properties) relative to a reference frame. The reference frame is the view-box of the closest
ancestor element that does not have `position: static` (default).

In the picture below you can see two examples.

In the first, no non-static ancestor element exists, therefore the reference frame falls back to the
page.

In the second example, the element is inside another element with `position: relative`. Therefore,
the element is placed absolutely towards this element and not the entire page.

![example for position absolute](assets/position-absolute.png)

---

## `position: fixed`

Elements are removed from the normal document flow and no space is created for them - so they leave
no gap in the page. An element with position fixed is not influenced by scrolling and therefore
stays at the specified position. This is often used for navigation bars or "back to top" buttons.

![example for position absolute](assets/position-fixed.png)

---

## `position: sticky`

This is an unusual but very nifty positioning method. The element is not affected by the positioning
until it comes near the border of its scrolling container (normally the page itself). When the user
continues scrolling, a specified offset is enforced. The element sticks to this offset and appears
like a fixed element.

![example for position absolute](assets/position-sticky.png)

---

## `z-index`

The z-index defines the stacking order of html elements. Elements with a higher stacking order
appear on top if they overlap with other elements. The z-index can be an integer number (negative
numbers are possible) or it can have the default value `auto` which sets the stack order equal to
its parents. The z-index only effects positioned elements - that is elements with a non-static
position value.

---

## Resources

- [MDN web docs: position](https://developer.mozilla.org/en-US/docs/Web/CSS/position)
- [MDN web docs: Using positioning](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Positioning)
- [MDN web docs: z-index](https://developer.mozilla.org/en-US/docs/Web/CSS/z-index)
- [MDN web docs: Using z-index](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/Adding_z-index)
- [MDN web docs: Stacking context](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context)
- [`z-index` and stacking context by Josh W. Comeau](https://www.joshwcomeau.com/css/stacking-contexts/)

  handout:
  https://github.com/neuefische/allspice-cgn-fssd-25/blob/main/sessions/css-positioning/css-positioning.md?plain=1
  ----------------------------------------------------------------------------------------------------------------------------------------------
# CSS Flexbox

## Learning Objectives

- understanding the purpose of flexbox:
  - letting items fill out the possible space in their container
  - distributing elements for different screen sizes
  - making the website more responsive with flexbox
- understanding the most important flexbox properties
- knowing the difference between **main-axis** and **cross-axis**

---

## Flexbox

Flexbox is a powerful CSS tool to layout your HTML elements, especially when you want to align
elements horizontally. It is defined on a container element, containing multiple elements whose
position will be determined by the flexbox rules. You define it as follows:

```css
.container-element {
  display: flex;
}
```

Flexbox does the following:

- All child elements will be displayed next to each other along the main axis, the horizontal axis
  by default. The perpendicular axis is called cross axis.
- If the width of all child elements exceeds the container's width, the child elements will be
  shrunk such that they all fit into the available space.

This behavior can be modified to achieve some very useful layouts. The most important flex
properties are listed in the following table.

---

## Important Flex Properties

| property                                                                            | effect                                                                                                                                       |
| ----------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| [justify-content](https://developer.mozilla.org/en-US/docs/Web/CSS/justify-content) | Defines the positioning of elements along the main axis. Useful values: `flex-start`, `flex-end`, `center` , `space-between`, `space-evenly` |
| [align-items](https://developer.mozilla.org/en-US/docs/Web/CSS/align-items)         | Defines the positioning of elements along the cross axis. Useful values: `flex-start`, `flex-end`, `center`                                  |
| [gap](https://developer.mozilla.org/en-US/docs/Web/CSS/gap)                         | Defines the minimum spacing between elements.                                                                                                |
| [flex-direction](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-direction)   | Sets the direction of the main axis. Useful values: `row`, `column`                                                                          |
| [flex-wrap](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-wrap)             | Modifies how elements can wrap into another row instead of being squashed into one row. Useful values: `wrap`, `no-wrap`                     |

> 💡 [This very detailed cheatsheet](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
> includes everything you will ever need when working with flexbox.

---

## Flex-direction

This very fundamental property lets you define which axis should act as main axis. In this picture
you can see its effect.

![flex-direction](assets/flex-direction.png)

As you can see it changes the layout completely. Also notice, that the property `align-items`, which
defines the positioning on the cross axis, also changes with the definition of the flex-direction.

---

## Flex-wrap

This property is very useful for creating responsive layouts. With the property set to
`flex-wrap: wrap` the elements flow into the next row when they wouldn't fit into the current row.
Depending on the screen width, the content can align itself, as shown in the following example.

![flex-wrap](assets/flex-wrap.png)

---

### CSS Grid Layout

CSS Grid is another powerful tool to layout your HTML elements. While flexbox excels at laying out
elements in one dimension (if you ignore wrapped items), CSS Grid is used to layout elements in two dimensions.

> 📑 Learn more about [**CSS Grid Layout** in the document we prepared](./assets/css-grid.md).

---

## Resources

- [Flexbox Cheat Sheet](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- [An Interactive Guide to Flexbox by Josh W. Comeau](https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/)
- [MDN web docs: Flexbox](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox)
- [CSS Battle](https://cssbattle.dev/)
- [📑 CSS Grid Layout document](./assets/css-grid.md)
- [Flexbox playground](https://the-echoplex.net/flexyboxes/)

Handout:
https://github.com/neuefische/allspice-cgn-fssd-25/blob/main/sessions/css-flexbox/css-flexbox.md?plain=1

  ----------------------------------------------------------------------------------------------------------------------------------------------
Good Link: https://css-tricks.com/snippets/css/a-guide-to-flexbox/
  ----------------------------------------------------------------------------------------------------------------------------------------------
# CSS Structure

## Learning Objectives

- Understanding how the browser decides which CSS property to use when there are conflicting rules,
  regarding CSS cascade and CSS specificity
- Structuring CSS to improve maintainability and readability
- Organizing and naming CSS classes with BEM method
- Creating and reusing Custom CSS properties, also called CSS variables

---

## CSS Cascade

The cascade is the algorithm that defines which CSS rules are being applied when there are
conflicting rules.

When styling an element the browser:

1. Searches for all rules with matching selectors
2. Sorts the rules by their importance taking into account:
   - Whether the declaration is followed by **!important**
   - The rule's origin (Browser stylesheet, User stylesheet, Author stylesheet)
3. Sorts rules by their [specificity](#specificity), if there are multiple rules with the same
   importance according to no. 2.
4. Chooses the last declaration over previous ones, if there are multiple rules with the same
   importance and the same specificity.

You can read about the details in the
[CSS Cascade mdn docs](https://developer.mozilla.org/en-US/docs/Web/CSS/Cascade).

> ❗️ We recommend never using !important unless you absolutely have to. It is almost impossible to
> overwrite a CSS rule with !important.

---

## Specificity

The specificity of a CSS selector tells the browser which rule is most relevant for an element. The
more specific rules win over less specific ones.

You can find a list of the specificity of different selectors on
[specifishity.com](https://specifishity.com/).

The **universal selector** is the lease specific one. It is overwritten by any other CSS rule with
any other matching CSS selector.

**type selectors** like `div` have a low specificity and can easily be overwritten.

**class selectors** like `.bright` and **attribute selectors** like `[type=checkbox]` have a higher
specificity.

---

## CSS Structure best practices

- keep your CSS consistent throughout a project. In collaborative projects, there are often coding
  style guidelines.
- separate global and local styles into different files (or sections of files)
- create multiple stylesheets for different parts of your application
  - structure your code by thinking in reusable **components**. You can write your CSS for every
    component in its own CSS file.

### How to import one stylesheet or multiple stylesheets into another stylesheet

You can import one stylesheet into another stylesheet using **@import**:

```css
@import "customer-card.css";
```

---

## CSS practical strategies

There is no single strategy to approach HTML and CSS cooperation, since it mostly depends on the website / application size and target.

Here we present some concrete scenarios.

### Highlight a product in offer

```html
<article class="product">
  <h2>Amazing Article</h2>
  <span>Price: 66</span>
</article>
<article class="product product-in-offer">
  <h2>Intrepid Item</h2>
  <span>Price: 99</span>
</article>
<article class="product">
  <h2>Pretty Product</h2>
  <span>Price: 54</span>
</article>
```

```css
.product {
  background-color: yellow;
  padding: 1rem;
  border-radius: 0.5rem;
}

.product-in-offer {
  background-color: orange;
}
```

### Preventing unwanted cascading

Let's say we have an homepage with multiple `.homepage-section`, one of them looking like this:

```js
<section class="homepage-section">
  <h2>About us<h2>
  <p>We offer the following services:</p>
  <ul>
    <li>Service one</li>
    <li>Service two</li>
    <li>Service three</li>
  </ul>
  <div class="cards">
    <article>
      <h3>Why you should choose us</h3>
      <ul>
        <li>Reason one</li>
        <li>Reason two</li>
        <li>Reason three</li>
      </ul>
    </article>
    <article>...</article>
    <article>...</article>
  <div>
</section>
```

The section has some cards at the bottom, yielding the following output:

![Example 01](./assets/example_01.png)

Now both the section itself and the first article have a `<ul>`, and styling them in an incautious way would propagate the definitions to the article, see:

```css
.homepage-section ul {
  padding: 0 1rem;
  margin-bottom: 2rem;
}

.homepage-section .cards article ul {
  margin: 0;
  padding: 0;
  list-style: none;
}
```

Even to the padding is overridden by the second definition, the margin from the first one would still applied.

Possible solution? Use the `>` selector:

```css
.homepage-section > ul {
  padding: 0 1rem;
  margin-bottom: 2rem;
}
```

Now the definition applies just to the `<ul>`s that are **direct descendants** of the section.

[You can see a working example here][CSS Structure Example #1].

### BEM

Among the various naming conventions, a popular one is [BEM][Introduction to BEM]. It suggests the concept of blocks, elements and modifiers like:

```html
<article class="product">
  <h2 class="product__title">Amazing Article</h2>
  <span class="product__price">Price: 66</span>
</article>
<article class="product product--in-offer">
  <h2 class="product__title">Intrepid Item</h2>
  <span class="product__price">Price: 99</span>
</article>
<article class="product">
  <h2 class="product__title">Pretty Product</h2>
  <span class="product__price">Price: 54</span>
</article>
```

- the `<article>` is a **block**;
- the `<h2>` and `<span>` are **elements** contained in the block, and are named like `{block}__{elementName}`;
- the second `<article>` is displayed in a different way thanks to the `product--in-offer` modifier class, that is named like `{block}--{modifierName}`.

You are not required to use BEM, but you may encounter it in some challenges or examples.

### Kebab Case naming convention

The kebab case naming convention defines to use hyphens to separate words in variables. Many
developers use the kebab case convention to write css classes. In BEM we also use kebab case, for
example:

```css
.customer-card {
  ...;
}

.customer-card__button {
  ...;
}

.customer-card--disabled {
  ...;
}
```

---

## Custom properties (CSS variables)

You can store values in custom properties, so you can use them again multiple times without having
to write the value.

A common practice is to define variables in the `:root` pseudo class selector as follows:

```css
:root {
  --primary-color: #ff00ff;
  --secondary-color: #f00f0f;
}
```

> ❗️ Custom properties have to be prefixed with `--`

You can use the custom properties as follows:

```css
.customer-card {
  color: var(--primary-color);
  background-color: var(--secondary-color);
}
```

---

## Resources

- [MDN docs: CSS Cascade](https://developer.mozilla.org/en-US/docs/Web/CSS/Cascade)
- [specifishity.com](https://specifishity.com/)

[Introduction to BEM]: http://getbem.com/introduction/

Handout:
https://github.com/neuefische/allspice-cgn-fssd-25/blob/main/sessions/css-structure/css-structure.md?plain=1
  ----------------------------------------------------------------------------------------------------------------------------------------------

# CSS Grid Layout

## Learning Objectives

- using CSS Grid to layout Webpages
- positioning elements in Grid cells
- aligning cells in a Grid

---

## CSS Grid Layout

With [CSS Grid Layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout), you can
position HTML elements in a grid structure, reposition individual elements, stretch items across
multiple cells and much more. It's a very powerful layout tool.

Working with CSS Grid Layout contains two major parts:

1. Defining the layout on a container element
1. Positioning the children on the grid cells

## Grid container

Just like CSS flexbox, the display mode is defined on a container element that contains all the
elements to be positioned as direct children in the grid.

```css
.container {
  display: grid;
}
```

The grid is defined by the number and size of it's rows and columns. By default, the grid consists
of one column. The properties for defining the columns and rows are
[grid-template-columns](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-template-columns) and
[grid-template-rows](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-template-rows). With the
[gap](https://developer.mozilla.org/en-US/docs/Web/CSS/gap) property you can define a space between
the grid cells.

### `fr` Unit

The grid layout has the fraction unit `fr` as a special sizing unit (next to `px`, `rem` or `%`)

1. It splits the remaining space in a grid into equally sized fractions. The number of these parts
   is determined by the total amount of fraction units distributed in the row/column template.
2. The individual rows / columns take up the assigned number of fractions.

In the following picture, the last two columns are sized with fraction units. The first of them has
twice the width of the second one.

![grid-template](assets/grid-layout.png)

## Element Positioning

After the grid is set up on the container element, its children are placed inside the grid cells
from left to right, top to bottom. By default, the elements are stretched such that they take up all
the available cell space.

![grid-template](assets/element-positioning-1.png)

You can change an element's positioning by using the the CSS properties
[grid-column](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-column),
[grid-rows](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-row) or
[grid-area](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-area), which combines the former
into a single CSS shorthand property. Elements can also be stretched over multiple cells.

Each element can be positioned on the columns and rows by using these values:

1. **Column / row index** (see picture above).
2. Negative **index**. Indexing the lines from the other side.
3. The **`span`** value. Defines how many cells the item should stretch across.

Here is an example:

![grid-positioning](assets/element-positioning-2.png)

> ❗️ Positioning properties are set on the child elements, not on the container!

## `grid-template-areas`

A completely different approach to position elements inside a grid is to use `grid-template-areas`.

- First the template cells are grouped into named areas. Every created cell is assigned an **area
  name**. Cells with the same name are grouped together to one area. This is done on the container
  element:
  ```css
  grid-template-areas:
    "a a b c"
    "d d d c"
    "e e e e";
  ```
- Then the grid elements are assigned to one of these areas with the `grid-area` property:
  ```css
  .element-a {
  	grid-area: a;
  }
  .element-b {
  	grid-area: b;
  }
  ...
  ```

This will result in the same layout as shown above.

> ❗️ Make sure that the named areas are geometrically possible in the defined grid, otherwise your
> grid won't work.

## Column and Row Alignment

The combined size of the grid columns/rows you defined might be less than a given height/width of
the grid container. In this case you can distribute the columns or rows inside the grid container.

| Property                                                                            | Effect                                          |
| ----------------------------------------------------------------------------------- | ----------------------------------------------- |
| [justify-content](https://developer.mozilla.org/en-US/docs/Web/CSS/justify-content) | Sets the alignment of the `columns`.            |
| [align-content](https://developer.mozilla.org/en-US/docs/Web/CSS/align-content)     | Sets the alignment of the `rows`.               |
| [place-content](https://developer.mozilla.org/en-US/docs/Web/CSS/place-content)     | Sets the alignment of the `rows` and `columns`. |

## Cell Alignment

The position of the elements _inside_ their cells can be specified on the grid container.

| Property                                                                        | Effect                                          |
| ------------------------------------------------------------------------------- | ----------------------------------------------- |
| [justify-items](https://developer.mozilla.org/en-US/docs/Web/CSS/justify-items) | Sets the `horizontal` alignment.                |
| [align-items](https://developer.mozilla.org/en-US/docs/Web/CSS/align-items)     | Sets the `vertical` alignment.                  |
| [place-items](https://developer.mozilla.org/en-US/docs/Web/CSS/place-items)     | Sets the `vertical` and `horizontal` alignment. |

---

## Resources

- [Complete Guide to CSS Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)

  Handout:
  https://github.com/neuefische/allspice-cgn-fssd-25/blob/main/sessions/css-grid/css-grid.md?plain=1
  
  ----------------------------------------------------------------------------------------------------------------------------------------------
# CSS Responsive

## Learning Objectives

- [ ] Understanding the concept of responsive design
- [ ] Understanding why we work mobile first (in design and CSS)
- [ ] Understanding responsive units
- [ ] Understanding media queries

---

## Mobile First Design

When authoring CSS, it's a very helpful convention to first define all your mobile styles, and then
add media queries to adjust the styles for larger screens. It's easier to reason about, and it
results in a simpler CSS structure. Your code will be more similar to the way other people write
CSS.

When designing, it makes sense to begin designing mobile first, because most users are on mobile
devices. This also helps you to focus on the most important information (you have less space), and
to structure it in a way that makes sense for mobile users.

---

## Responsive Units

Responsive units are units that are relative to the size of the viewport, the current font size, or
the size of their parent element.

- `vh` (viewport height): 1vh is 1% of the viewport height
- `vw` (viewport width): 1vw is 1% of the viewport width
- `em`: 1em is the font size of the current element
- `rem`: 1rem is the font size of the root element
- `%`: is relative to the related property of the parent or current element - every property has
  it's own rules what it is relative to:
  - `width: 1%` is set relative to the parents element width
  - `padding-top: 10%` means 10% of the parents height
  - `font-size: 50%` means half as big as the parent font-size
  - `transform: translateX(50%)` means translate on the x axis by 50% of the current elements width
- `calc()`: allows you to combine multiple units and do math
  - e.g. `calc(100vh - 100px)`
  - or `calc(50% - 10rem)`

---

## Media Queries

Media queries allow you to write CSS for specific media types, screen sizes, orientations and more.

They follow the following syntax:

```css
@media (media feature) {
  /* CSS rules */
}
```

### Media Types

You can target a specific media type with the `screen` and `print` media types.

```css
@media screen {
  /* CSS rules that are only applied on screens */
}

@media print {
  /* CSS rules that are only applied when printing */
}
```

### Screen Size

You can target specific screen sizes with the `min-width` and `max-width` media features.

```css
@media (min-width: 600px) {
  /* CSS rules that are only applied when the screen is at least 600px wide */
}

@media (max-width: 600px) {
  /* CSS rules that are only applied when the screen is at most 600px wide */
}
```

> 💡 Avoid `max-width` media queries, because they are harder to reason about. It's easier to think
> about the smallest screen size first, and then add media queries for larger screens.

### Orientation

You can target specific orientations with the `orientation` media feature.

```css
@media (orientation: portrait) {
  /* CSS rules that are only applied when the screen is in portrait orientation */
}

@media (orientation: landscape) {
  /* CSS rules that are only applied when the screen is in landscape orientation */
}
```

> 💡 You can also target a specific aspect ratio with the
> [`aspect-ratio` media feature](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/aspect-ratio).

### Pointer

You can target specific pointer types with the `any-pointer` media feature.

```css
@media (any-pointer: none) {
  /*
		CSS rules that are only applied when the device has no pointer
		(neither touch nor cursor)
	*/
}

@media (any-pointer: coarse) {
  /*
		CSS rules that are only applied when the device has a coarse pointer
		(mostly touch)
	*/
}

@media (any-pointer: fine) {
  /*
		CSS rules that are only applied when the device has a fine pointer
		(cursor)
	*/
}
```

### Device Pixel Ratio (Pixel Density)

You can target specific device pixel ratios with the `device-pixel-ratio` media feature.

```css
@media (device-pixel-ratio: 1) {
  /*
		CSS rules that are only applied when the device has a pixel ratio of 1
		(mostly older screens)
	*/
}

@media (device-pixel-ratio: 2) {
  /*
		CSS rules that are only applied when the device has a pixel ratio of 2
		(newer screens like the retina screen on your MacBook)
	*/
}

@media (device-pixel-ratio: 3) {
  /*
		CSS rules that are only applied when the device has a pixel ratio of 3
		(some high resolution tablets and phones)
	*/
}
```

### Color Scheme

You can target specific color schemes with the `prefers-color-scheme` media feature.

```css
@media (prefers-color-scheme: dark) {
  /* CSS rules that are only applied when the user prefers a dark color scheme */
}

@media (prefers-color-scheme: light) {
  /* CSS rules that are only applied when the user prefers a light color scheme */
}
```

> 💡 You can change your preferred color scheme in your operating system settings. On macOS, you can
> do this in System Preferences > General > Appearance.

### Reduced Motion

You can target users who are sensitive to animations and movement (and set up their system
accordingly) with the `prefers-reduced-motion` media feature.

```css
@media (prefers-reduced-motion: reduce) {
  /* CSS rules that are only applied when the user prefers reduced motion */
}
```

> 💡 You can change your preferred reduced motion setting in your operating system settings. On
> macOS, you can do this in System Preferences > Accessibility > Display > Reduce motion.

### High Contrast

You can target users who prefer a higher contrast with the `prefers-contrast` media feature.

```css
@media (prefers-contrast: more) {
  /* CSS rules that are only applied when the user prefers a higher contrast */
}
```

> 💡 You can change your preferred contrast setting in your operating system settings. On macOS, you
> can do this in System Preferences > Accessibility > Display > Increase contrast.

### Other Media Features

There are also media features for other (accessibility) features, like
[`inverted-colors`](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/inverted-colors). The
list of all media features is always growing. Check out
[the full list](https://developer.mozilla.org/en-US/docs/Web/CSS/@media#media_features) on mdn.

### Combining Media Features

You can combine multiple media features with `and`.

```css
@media (min-width: 600px) and (orientation: landscape) {
  /* CSS rules that are only applied when the screen is at least 600px wide and in landscape orientation */
}
```

### Testing for multiple Media Features

You can use a comma-separated list to apply styles when the user's device matches any one of various
media types using `,`

```css
@media (min-width: 600px), (orientation: portrait) {
  /* CSS rules that are only applied when the screen is either at least 680px high or in portrait orientation */
}
```

### Simulating Media Features

You can simulate media features in the browser devtools. For example, you can change your screen
size in the devtools by clicking the device icon in the top left corner of the devtools.

### Common Breakpoints

When using `min-width` media queries it can be helpful to use common breakpoints.

- no media query (default): extra-small, xs, mobile
- `(min-width: 600px)`: small, sm, large mobile
- `(min-width: 900px)`: medium, md, tablet
- `(min-width: 1200px)`: large, lg, desktop
- `(min-width: 1536px)`: extra-large, xl, large desktop

> 💡 These breakpoints are based on the
> [MUI breakpoints](https://mui.com/material-ui/customization/breakpoints/). Other frameworks and
> projects might define a completely different set of breakpoints. Mostly they are defined to be
> between the most common screen sizes. Another example for common breakpoints are
> [the ones from Tailwind CSS](https://tailwindcss.com/docs/breakpoints).

🪄 **Pro Tip**: You can use media queries to redefine the values of CSS custom properties. This way
you can use the property as a value that dynamically changes based on the media query.

```css
:root {
  --font-size: 12px;
}

@media (min-width: 600px) {
  :root {
    --font-size: 16px;
  }
}

@media (min-width: 1200px) {
  :root {
    --font-size: 20px;
  }
}

body {
  font-size: var(--font-size);
}
```

---

## Showing different images based on media queries

You can use media queries to show different images based on the screen size.

The html `picture` element allows you to define multiple `source` elements for an image. The browser
will choose the _first_ source that matches the given media query. If no `source` element matches,
the browser will use the `img` element as a fallback.

The `img` element is required, so that there is always a fallback.

```html
<picture>
  <source
    media="(min-width: 1200px)"
    srcset="https://source.unsplash.com/random/1400x1050"
  />
  <source
    media="(min-width: 900px)"
    srcset="https://source.unsplash.com/random/800x600"
  />
  <img src="https://source.unsplash.com/random/400x300" alt="" />
</picture>
```

> 💡 Note that the `source` element doesn't have a `src` attribute but uses the `srcset` attribute
> instead. This can be used to help with performance but is not relevant for this session.

---

## Resources

- [Using Media Queries](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries)
- [Responsive Design on mdn](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Responsive_Design)
- [Responsive Web Design Basics on web.dev](https://web.dev/responsive-web-design-basics/)
- [Values and Units on mdn](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Values_and_units)
- [Beginner's Guide to Media Queries on mdn](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Media_queries)
- [@media on mdn](https://developer.mozilla.org/en-US/docs/Web/CSS/@media)
- [The Picture element on mdn](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/picture)
- [Is your web page mobile-friendly? on Google](https://search.google.com/test/mobile-friendly)

- Handout:
  https://github.com/neuefische/allspice-cgn-fssd-25/blob/main/sessions/css-responsive/css-responsive.md?plain=1
  
  ----------------------------------------------------------------------------------------------------------------------------------------------
