# Positioning

- `position: static | fixed | relative | absolute`
- eg usage: to build dropdown menus, modal dialogs, sidebar etc.

## Positioned or not?

- `inital value` of position property is `static`
- If you change value of the position property to anything, the element is said to be positioned; thus an element with static positioning is called `not positioned`

## What does positioning do?

Layout such as flexbox or grid, manipulates the document flow behvaior; In contrast, positioning removes an element from the document flow entierly thus allowing you to place it somewhere else in the screen. A classic usage of this is modal where you would use fixed positioning to show it in the screen and cover certain area. (With stacking context, you will ensure it will always be at the top and therefore use can see it)

## Fixed postion: position: fixed

- allows you to position element arbitrarily `relative to the viewport`. Viewport is the containinig block for the fixed elements
- `4 companion` properties `top, right, bottom and left` which implicitly define the width and height
- eg 1: `top: 3em` on fixed element means its top edge will be 3 em from the top of viewport
- width eg: `left: 2em` and `right: 2em` means left and right edge will both be 2 em from respective edges. This leads to the element width being explictly defined which will be 4 em less then total viewport width.
- height eg: make use of top and bottom property!
- use all 4 and now you have defined the width and height!
- By using fixed position, this element is removed from document flow. Other elements in the page will follow the normal document flow as if this fixed element doesn't exist. More often, these other elements will flow behind the fixed element and will be hiddent from view. This is the kind of behavior ideal for modal but if you are building components such as sidebar, make use of left or right margin to prevent other contents from hiding.

## Absolute position

- Absolute position is positioned relative to the closest positioned ancestor element.
