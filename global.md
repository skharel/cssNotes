# Things that you should "almost always" have in your CSS no matter what library you use

```css
:root {
  font-size: calc(0.5em + 1vw);  <== dynamic font-size wrt screen size
  box-sizing: border-box; <== can screw up 3rd party css
}

*,
::before,
::after {
  box-sizing: inherit;
}

/* conditionally needed */
.thirdPartyContainerFix {  <== fix 3rd party code related to box-sizing
  box-sizing: content-box;
}

/* lobotomized owl selector; might cause issue if your website is primarily doing multi column layout. See notes in 3-boxmodel*/
body * + * {
  margin-top: 1.5em; <== value might be different from 1.5
}

```
