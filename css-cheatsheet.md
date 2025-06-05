* {
  box-sizing: border-box;
}

| Box model part | Function                                                               |
| -------------- | ---------------------------------------------------------------------- |
| margin         | The outer space measured from the border to other elements on the page |
| border         | The border of the element                                              |
| padding        | The inner space between the content and the border of the element      |
| content        | The actual content box of the element                                  |

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

| Type                 | Description                                                                                                         |
| -------------------- | ------------------------------------------------------------------------------------------------------------------- |
| `position: static`   | The position of the element is determined by the document flow (default)                                            |
| `position: relative` | Position the element relative to where the element would be placed normally                                         |
| `position: absolute` | Position the element absolutely inside the **nearest non-static ancestor element**                                  |
| `position: fixed`    | Position the element on a fixed position on the screen.                                                             |
| `position: sticky`   | The element is placed normally in the document flow, but keeps an offset relative to its nearest scrolling ancestor |

## Important Flex Properties

| property                                                                            | effect                                                                                                                                       |
| ----------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| [justify-content](https://developer.mozilla.org/en-US/docs/Web/CSS/justify-content) | Defines the positioning of elements along the main axis. Useful values: `flex-start`, `flex-end`, `center` , `space-between`, `space-evenly` |
| [align-items](https://developer.mozilla.org/en-US/docs/Web/CSS/align-items)         | Defines the positioning of elements along the cross axis. Useful values: `flex-start`, `flex-end`, `center`                                  |
| [gap](https://developer.mozilla.org/en-US/docs/Web/CSS/gap)                         | Defines the minimum spacing between elements.                                                                                                |
| [flex-direction](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-direction)   | Sets the direction of the main axis. Useful values: `row`, `column`                                                                          |
| [flex-wrap](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-wrap)             | Modifies how elements can wrap into another row instead of being squashed into one row. Useful values: `wrap`, `no-wrap`                     |


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

You can target specific screen sizes with the `min-width` media features.

```css
@media (min-width: 600px) {
  /* CSS rules that are only applied when the screen is at least 600px wide */
}
```

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
### Reduced Motion

You can target users who are sensitive to animations and movement (and set up their system
accordingly) with the `prefers-reduced-motion` media feature.

```css
@media (prefers-reduced-motion: reduce) {
  /* CSS rules that are only applied when the user prefers reduced motion */
}
```

### High Contrast

You can target users who prefer a higher contrast with the `prefers-contrast` media feature.

```css
@media (prefers-contrast: more) {
  /* CSS rules that are only applied when the user prefers a higher contrast */
}
```

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
> instead.

