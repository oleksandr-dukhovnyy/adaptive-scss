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

| breakpoint name | screen width size  |
| --------------- | ------------------ |
| xs              | >=0px              |
| sm              | >=576px            |
| md              | >=768px            |
| lg              | >=992px            |
| xl              | >=1200px           |
| xxl             | >=1900px           |

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
