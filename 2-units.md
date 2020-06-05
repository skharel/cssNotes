**pixel**: pixel is misleading name not same as monitors pixel

## em & rem:

**em**:

- most common relative unit
- 1 font size of current element
- value declared using relative units are evaluated by browser to an absolute value called computed value
- em is convinent to use for margin, padding, height, width or border radius
- if font-size has em, then inheritance comes into play to figure out which font-size to use

**rem**:

- root em aka relative to root element (as opposed to being relative to current element like em)
- eg below shows how to use root selector to set a default font size for your page (you could set it in pixel too but I have used 1em to select browser's default, 16px). Later in your page you could increase (or decrease) font-size at particular places relative to the root using rem.

```css
:root {
  font-size: 1em; <=== means what user agent default font is;
}

.myClass {
    font-size: 1.5rem;  <==== means 1.5 * root selector
    padding: .8em; <=== scale it relative to current font size
}

```

## Viewport relative units:

> viewport: framed area in browser window where the webpage is visible

**vh**:

- 1/100th of viewport height (think as x percentage of visible height)
- eg: 20vh means 20% of visible height

**vw**:

- 1/100th of viewport width

**vmin**:

- 1/100th of smaller dimension of visible height or width
  > https://caniuse.com/#search=vmin

**vmax**:

- 1/100th of larger dimension of visible height or width
  > https://caniuse.com/#search=vmax

## calc function:

> Syntax: `calc(a operator b operator c <and so on>)`

- supports addition, subtraction, multiplication and division
- **MUST** use space around the operator (just do it!)
- best part is that the units can be different for each variable
- can be used to dyanmically compute font size based on screen size w/o using media queries that impacts your entire site
- eg below will use 0.5 of user agent default (16px); the 1vw components will scale the fontsize based on screen height resulting in larger screen having bigger font and smaller one with slightly smaller font

```css
:root {
  font-size: calc(0.5em + 1vw);
}
```

## css variables:

> Syntax:

- Declaration: `--varName: value`
- Usage:

  ```css
  <selector > {
    css-props: var(--varName, fallback);
  }
  ```

- inheritance comes into play for variable scopes
