# Stratajet CSS / Sass Styleguide

  1. [Terminology](#terminology)
    - [Rule Declaration](#rule-declaration)
    - [Selectors](#selectors)
    - [Properties](#properties)
  1. [CSS](#css)
    - [Formatting](#formatting)
    - [Comments](#comments)
    - [OOCSS and BEM](#oocss-and-bem)
    - [ID Selectors](#id-selectors)
    - [JavaScript hooks](#javascript-hooks)
  1. [Sass](#sass)
    - [Syntax](#syntax)
    - [Ordering](#ordering-of-property-declarations)
    - [Mixins](#mixins)
    - [Placeholders](#placeholders)
    - [Nested selectors](#nested-selectors)

### Formatting

* Use soft tabs (2 spaces) for indentation. This is the only way to guarantee code renders the same in any person’s environment.
* Put a space before the opening brace `{` in rule declarations
* In properties, put a space after, but not before, the `:` character
* Put closing braces `}` of rule declarations on a new line
* Put blank lines between rule declarations

**Good**
```css
.c-avatar {
  border-radius: 50%;
  border: 2px solid white;
}
 
.c-one,
.c-selector,
.c-per-line {
  // ...
}
```

**Bad**
```css
.c-avatar{
    border-radius:50%;
    border:2px solid white; }
.c-one, .c-selector, .c-per-line {
    // ...
}
```

*Large blocks of single declarations can use a slightly different, single-line format. In this case, a space should be included after the opening brace and before the closing brace.

```css
.selector-1 { width: 10%; }
.selector-2 { width: 20%; }
.selector-3 { width: 30%; }
```

### Commenting

* Use single line comments (`//` in SCSS) instead of block comments
* Comments should be on their own line. Avoid end-of-line comments
* Sections should be separated with block comments in all caps, beginning with a `#`

```css
/*------------------------------------*\
    #SECTION TITLE
\*------------------------------------*/
 
.bd\(n\) {
  border: none;
  // this is what a comment should look like
}
```

## ID Selectors

*Do not use ID selectors in any case unless it is the only way to style an element from a library

### Class Names

* Prefer dashes over camelCasing in class names
* Class names must start with a prefix unless they are atomic or are generated by a JS library
* Class names can be done with BEM if necessary

**Good**

```css
.c-btn--primary {
  background-color: blue;
  padding: 1em;
  color: white;
}
```

**Bad**

```css
.cBtnPrimary {
  background-color: blue;
  padding: 1em;
  color: white;
}
```

### PX, EMS and REMS

* In theory PX should never really be used except for declaring a base font size in n a html or body selector. Although this will become 100% for future sites
* PX may also be used to specify very small sizes, but this should only be done if the alternative is beyond 3 decimal places i.e. `font-size: 0.125em`
* EMS and REMS are the recommended units for Stratajet projects
* Use REMS for units you want to be affected by the global base site
* Use EMS for units you want to be affected by the size of the container they are in

*While em is relative to the font size of its direct or nearest parent, rem is only relative to the html (root) font-size.*


### Floats or Flexbox

* Please avoid using floats at all in for any project. The presence of floats might usually be due to legacy code, or code brought in from external libraries


### Breakpoints (Media Queries)

* Media queries should be written within the selector that they affect and not in an external media queries file in order to have everything in one place. In the future we might use a PostCSS process to separate all the media queries.
* For readability and reusability all media queries must be wrapped in a breakpoint Scss mixin.

```css
@mixin breakpoint($point) {
  @if $point == lg-h {
    @media (min-height: 920px) { @content ; }
  }
}
 
.mdl-textfield__input {
  font-size: 13px;
  @include breakpoint(lg-h) {
    font-size: 16px;
  }
}
```

### Nesting
* Do not nest more than 3 levels deep. This way css doesn't become too specific making it easier to use on other parts of the site.

```css
.m-page-container {
  .o-content {
    .c-profile {
      // STOP!
    }
  }
}
```

