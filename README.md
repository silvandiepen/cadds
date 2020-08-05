# CaDDS

CaDDS or Config and Data Driven Styling is a styling methodology based on styling a complete project from one single config file. It might sound odd, but it's possible without making it too complicated.


### Why?
The idea is to create a config file which holds all the styling for a project. By including this file into another with some different defaults, you can completely alter the outcome and create themes.


## How?

To use the CADDS styling you need to make sure your project has a few things in stock; Knowledge of the CSS cascade, BEM and install CaDDS and Sass in your project.

```npm install cadds sass```


### Basic example

A very simpole cadds styling file;

**main.scss**
```scss
$color-primary: red !default;
$color-secondary: blue !default;
$base-space: 1em !default;

$cadds: (
  'header__border': 1px solid $color-primary,
  'header__background: $color-secondary,
  'header__padding': $base-space,
  'main__padding': $base-space,
  'main__background': white,
  'footer__background': black,
  'footer__color': white,
  'footer__padding': $base-space
);
```

will output;
**style.css**
```css
.header{
  border: var(--header__border,1px solid var(--color-primary,red));
  background: var(--header__background,var(--color-secondary,blue));
}
.main{
  padding:var(--main__color,1em);
  background: var(--footer__background,white);
}
footer{
  padding: var(--footer__padding,1em);
  background: var(--footer__background,black;
  color: var(--footer__color,white);
}
```

But if you want to make an alternative theme file with the same css but different values;
```scss
$color-primary: brown;
$color-secondary: green;
@import 'main.scss';
```

will output;
```css
.header{
  border: var(--header__border,1px solid var(--color-primary,brown));
  background: var(--header__background,var(--color-secondary,green));
}
.main{
  padding:var(--main__color,1em);
  background: var(--footer__background,white);
}
footer{
  padding: var(--footer__padding,1em);
  background: var(--footer__background,black;
  color: var(--footer__color,white);
}
```

As you can see, all output automatically have defined custom properties, which makes every theme easy to adjust even without editting the css. The last file could also be written as;

```css
:root{
  --color-primary: brown;
  --color-secondary: green;
}
@import 'style.css';
```

