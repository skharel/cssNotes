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

# Collapsed margins:

When top ad/or bottom margins (note only top and bottom but not left or right) margins are adjoining, they overlap. These overlapped margins merges aka collapses to form a single margin. This is what `collapsing` margin means. When collapsing happens, if both margins had equal value, say x, then the resulting margin is equal to x. However, if the margins were x, y and y > x, the resulting margin will be equal to y (bigger margin size will be used)

If margins do not collapse as you want, you can fix using:

1. padding: if you add top and bottom padding, margins won't collpase
2. use flexboxes; margins of flexbox items won't collapse

# Spacing elements within a container

Suppose you have contaner and inside of it are 2 block items and both have class say item as:

```css
.item {
  padding: 1em;
}
```

With this you will have items nicely inside a container with little bit of space around items and the container. Now if you also want to add some space between these 2 items, you could add margin-top to this class. However, when it gets rendered you will notice that because of the padding, the top element has little extra space on top becayse the total gap is margin + padding.

Instead of adding margin to the item class, you could add margin only in the second element as:

```css
.item + .item {
  margin-top: 1em;
}
```

This will fix the problem until you have need to add 3rd element. There you can do the same trick by adding margin-top to the third element again. Everytime, you add new item to this container you will have to do this.

### Meet Lobotomized owl selector: \* + \*

"Margins are like applying glue to one side of an object before you've determined whether you actually want to stick it to something or what that something might be" - Heydon Pickering.

Lobotomized owl selector is a general solution that works no matter how your page will be strucutured. It selects all elements on the page that aren't the first child of their parent. In html body is the second child of html element, therefore you should also include body as a part of your owl selector as:

```css
body * + * {
  margin-top: 1em <== value you want;
}
```

> Note: It is good idea to add this to the top of your page but for existing project, you might have to added few fixes for this to workout

The only time this owl selector will be an issue is, if you are doing multiple column layout. In such cases for second child, you will explictly need to add margin-top: 0 to remove extra margin at top. While this seems technically like the issue we described earlier, by making use of owl selector you will write a fix like these only in very few places. However, if your website has more coulmns based layout this may not be a proper fit. Use judiciously
