# adaptive-scss

A minimalistic scss library for working with media queries with the ability to specify custom media breakpoints.
Great for mobile-first development.
This library is just a collection of useful mixins. Assembly and processing (minimization, division into chunks, combining identical media queries) you need to configure yourself depending on the features of your project.

## Instalation

### npm

```bash
npm i adaptive-scss
```

### yarn

```bash
yarn add adaptive-scss
```

## Default breakpoints

| breakpoint name | screen width size |
| --------------- | ----------------- |
| xs              | >=0px             |
| sm              | >=576px           |
| md              | >=768px           |
| lg              | >=992px           |
| xl              | >=1200px          |
| xxl             | >=1900px          |

## Usage

### Default usage

This **scss**:

```scss
@import 'adaptive-scss';

body {
  background-color: yellowgreen;

  @include _media-up(md) {
    background-color: green;
  }

  @include _media-up(xl) {
    background-color: red;
  }
}
```

will be converted to this **css**:

```css
body {
  background-color: yellowgreen;
}

@media (min-width: 768px) {
  body {
    background-color: green;
  }
}

@media (min-width: 1200px) {
  body {
    background-color: red;
  }
}
```

### Usage with custom breakpoints list

You can set your own list of breakpoints.
The easiest way is to create a wrapper mixin.

```scss
@import 'adaptive-scss';

$list: (
  mobile: 0,
  tablet: 700px,
  desktop: 1400px,
);

@mixin media-up($name) {
  @include _media-up($name, $list) {
    @content;
  }
}

body {
  background-color: yellowgreen;

  @include media-up(tablet) {
    background-color: green;
  }

  @include media-up(desktop) {
    background-color: red;
  }
}
```

As a result, we get this:

```css
body {
  background-color: yellowgreen;
}

@media (min-width: 768px) {
  body {
    background-color: green;
  }
}

@media (min-width: 1200px) {
  body {
    background-color: red;
  }
}
```

### set size manually

You can also set size without $breakpoints-list.
In normal situations it will not to be use, but if you need this, you can do this.

```scss
.elem {
  @include _media-up(200px) {
    background-color: green;
  }
}
```

Output css:

```css
@media (min-width: 200px) {
  .elem {
    background-color: green;
  }
}
```

### mixins

---

#### **\_media-up**

_scss_

```scss
@include _media-up(sm) {
  .elem {
    color: #f00;
  }
}
```

_css_

```css
@media (max-width: 576px) {
  .elem {
    color: #f00;
  }
}
```

---

#### **\_media-down**

_scss_

```scss
@include _media-down(sm) {
  .elem {
    color: #f00;
  }
}
```

_css_

```css
@media (max-width: 576px) {
  .elem {
    color: #f00;
  }
}
```

---

#### **\_media-up-portrait**

_scss_

```scss
@include _media-up-portrait(sm) {
  .elem {
    color: #f00;
  }
}
```

_css_

```css
@media (orientation: portrait) and (min-width: 576px) {
  @content;
}
```

---

#### **\_media-up-landscape**

_scss_

```scss
@include _media-up-landscape(sm) {
  .elem {
    color: #f00;
  }
}
```

_css_

```css
@media (orientation: landscape) and (min-width: 576px) {
  @content;
}
```

---

#### **\_media-down-portrait**

_scss_

```scss
@include _media-down-portrait(sm) {
  .elem {
    color: #f00;
  }
}
```

_css_

```css
@media (orientation: portrait) and (max-width: 576px) {
  @content;
}
```

---

#### **\_media-down-landscape**

_scss_

```scss
@include _media-down-landscape(sm) {
  .elem {
    color: #f00;
  }
}
```

_css_

```css
@media (orientation: landscape) and (max-width: 576px) {
  @content;
}
```

---

#### **\_media-screen**

_scss_

```scss
@include _media-screen {
  .elem {
    color: #f00;
  }
}
```

_css_

```css
@media screen {
  .elem {
    color: #f00;
  }
}
```

---

#### **\_media-print**

_scss_

```scss
@include _media-print {
  .elem {
    color: #f00;
  }
}
```

_css_

```css
@media print {
  .elem {
    color: #f00;
  }
}
```

---

#### **\_media-portrait**

_scss_

```scss
@include _media-portrait {
  .elem {
    color: #f00;
  }
}
```

_css_

```css
@media (orientation: portrait) {
  .elem {
    color: #f00;
  }
}
```

---

#### **\_media-landscape**

_scss_

```scss
@include _media-landscape {
  .elem {
    color: #f00;
  }
}
```

_css_

```css
@media (orientation: landscape) {
  .elem {
    color: #f00;
  }
}
```

---
