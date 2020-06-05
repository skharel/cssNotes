## Hard problem in CSS 2 equal height columns layout and vertical centering

# Document flow note:

https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Normal_Flow

# Box Model:

![box model](./assets/Boxmodel.png)

- Box model goes as: Margin, Border, padding [MBP] and then content

- **Default** When you specify width or height, you are specifying width or height of the content. Any margin, border or padding are then added to it. This is almost not what you want (almost always)
- **you want** your width to include the value of border and padding too (css limitation and can't support margin)
- `box-sizing` property controls the behaviour you want. Default value for this property is `content-box` and you want to set to `border-box` (CB to BB)
- do universal border fix in your code as:

```css
:root {
  box-sizing: border-box;
}

*,
::before,
::after {
  box-sizing: inherit;
}
```

- this can screw up for third party css you bring in who are using it w/o thinking about this fix. Fix third party css by targeting their top-level container as:

```css
.thirdPartyContainer {
  box-sizing: content-box;
}
```

# Overflow behavior

- setting height of an element instead of letting it organically be determined based on content causes the risk of overflow
- document flow doesn't account for overflow and any content below the container will render over the top of the overflowing container
- use css property `overflow` to control the behavior in case of overflow
- 4 possible values: visible (default), hidden, scroll, auto
- auto is what you want most of the time

# Equal height columns

- no more floats with new css support (not 2000's anymore)
- use `display: table` or flexible boxes `display: flex`

### css based table layout;

- set container to `display: table`, `width: 100%` and `border-spacing: x y` to add gutter
- for each column in the container set `display: table-cell`
- you will notice margin in the column will not work and might have to pull in negative margin hack

### Flexbox (more later in other section)

- use flexbox (and if you need to support IE9, find new job)
- set container to `display: flex`
- child containers, aka columns, will have same height
- do not explictly set height of an element

# min-height

- min-height ensures the content will be at least of specified height
- browser will allow the element to grow naturally to prevent overflow

# max-height

- allows element to grow up to certain height and no more
- after the max-height is reached overflow will happen

## min-width and max-width

> same as min/max-height
