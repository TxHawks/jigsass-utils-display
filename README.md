# JigSass Utils Display
[![NPM version][npm-image]][npm-url]  [![Dependency Status][daviddm-image]][daviddm-url]   

A collection of dynamically generated css `display` utility classes.

Class names follow the [Emmet](http://docs.emmet.io/cheat-sheet/) abbreviation
syntax, with colons (':') replaced by two dashes (`--`) to follow BEM naming
conventions (It modifiies the user agent's default display).
E.g., the `display: none` utility class name is `.u-d--n`.

## Available classes

  - `.u-d--b` (display: block)
  - `.u-d--f` (display: flex)
  - `.u-d--if` (display: inline-flex)
  - `.u-d--i` (display: inline)
  - `.u-d--ib` (display: inline-block)
  - `.u-d--inher` (display: inherit)
  - `.u-d--init` (display: initial)
  - `.u-d--li` (display: list-item)
  - `.u-d--n` (display: none)
  - `.u-d--tb` (display: table)
  - `.u-d--iteb` (display: inline-table)
  - `.u-d--tbcp` (display: table-caption)
  - `.u-d--tbcl` (display: table-column)
  - `.u-d--tbclg` (display: table-column-group)
  - `.u-d--tbhg` (display: table-header-group)
  - `.u-d--tbfg` (display: table-footer-group)
  - `.u-d--tbr` (display: table-row)
  - `.u-d--tbrg` (display: table-row-group)
  - `.u-d--tbc` (display: table-cell)
  - `.u-d--rb` (display: ruby)
  - `.u-d--rbb` (display: ruby-base)
  - `.u-d--rbbg` (display: ruby-base-group)
  - `.u-d--rbt` (display: ruby-text)
  - `.u-d--rbtg` (display: ruby-text-group)


## Installation

Using npm:

```sh
npm i -S jigsass-utils-display
```


## Usage
Import JigSass Utils Display into your main scss file near its very end, together with all
other utilities (utilities should always be the last to be imported).

```scss
@import 'path/to/jigsass-utils-display/scss/index';
```

Like all other JigSass Utils, JigSass Display does not automatically generate any CSS
when imported. You would need to explicitly indicate that each individual display
class should actually be generated in each component or object it is used in
(clarification: This will include style declarations inside `.foo` and .`bar`):

```scss
// _c.foo.scss
.foo {
  @include jigsass-util(u-d, $modifier: b); // <-- display: block

  ...
}
```

```scss
// _c.bar.scss
.bar {
  @include jigsass-util(u-d, $modifier: ib);  // <-- display: inline-block
  @include jigsass-util(
    u-d,
    $modifier: f,
    $from: large
  ); // <-- display: flex from large bp an on.

  ...
}
```

Doing so helps us a great deal with portability, as no matter where we import component or object
partials, the correct utility classes will be generated. Think of it as a poor man's dependency
management.

Developer communication is also assisted by including "dependencies" wherever they are required,
as anyone going through a partial, can easily understand how it should be marked up with just a
glance.

As far as bloat goes, just don't worry about it - the actual styles will only be generated once,
at the location in the cascade where the Jigsass Clearfix partial was imported into the main file.


JigSass Display classes are responsive-enabled, using [JigSass MQ](https://txhawks.github.io/jigsass-tools-mq/)
and the breakpoints defined in the [$jigsass-breakpoints](https://txhawks.github.io/jigsass-tools-mq/#variable-jigsass-breakpoints) variable.

Based on the breakpoint arguments passed to `jigsass-util` when including a display class, responsive
modifiers are generated according to the following logic:

```scss
.u-d--<modifier>[-[-from-<breakpoint-name>][-until-<breakpoint-name>][-misc-<breakpoint-name>]]
```

So, assuming the `medium`, `large` and `landscape` breakpoints are defined in `$jigsass-breakpoints`
as `600px`, `1024px` and `(orientation: landscape)` respectively,

```scss
@include jigsass-util(u-d, $modifier: f);
```
will generate the `.u-d--f` class, which is not limited to any media-query.

```scss
@include jigsass-util(u-d, $modifier: f, $until: medium);
```

will generate the `.u-d--f--until-medium` class, which will be in effect at
`(max-width: 37.49em)` and will override styles in the default class until that point.

```scss
@include jigsass-util(u-d, $modifier: f, $from: large, $misc: landscape);
```

will generate the `.u-d--f--from-large-when-landscape` class, which will go into
effect at `(min-width: 64em) and (orientation: landscape)` and will override styles in the default
class under these  conditions.

## Documentation

The full documentation was generated using mdcss, and is available at 
[https://txhawks.github.io/jigsass-utils-display/](https://txhawks.github.io/jigsass-utils-display/)

## Contributing

It is a best practice for JigSass modules to *not* automatically generate css on `@import`, but 
rather have the user explicitly enable the generation of specific styles from the module.

Contributions in the form of pull-requests, issues, bug reports, etc. are welcome.
Please feel free to fork, hack or modify JigSass Display in any way you see fit.

#### Writing documentation

Good documentation is crucial for usability, scalability and maintainability. When 
contributing, please do make sure that both its Sass functionality (functions, mixins, 
variables and placeholder selectors), as well as the CSS it generates (selectors, 
concepts, usage exmples, etc.) are well documented.

Jigsass Display uses Jonathan Neal's [mdcss](//github.com/jonathantneal/mdcss).

When styles and documentation comments are not automatically generated by your module on `@import`,
please use the `sgSrc/sg.scss` file to enable their generation.

In addition, any file in `sgSrc/assets` will be available for use in the style guide.



## File structure
```bash
┬ ./
│
├─┬ scss/ 
│ └─ index.scss # The module's importable file.
│
├─┬ sgSrc/      # Style guide sources
│ │
│ ├── sg.scc    # It is a best practice for JigSass 
│ │             # modules to not automatically generate 
│ │             # css and documentation on `@import.` 
│ │             # Please use this file to enable css
│ │             # and documentation comments) generation.
│ │
│ └── assets/   # Files in `sgSrc/assets` will be 
│               # available for use in the style guide
│
└─┬ docs/      # Documention
  │
  └── styleguide/ # Generated documentation 
                  # of the module's CSS
```


**License:** MIT



[npm-image]: https://badge.fury.io/js/jigsass-utils-display.svg
[npm-url]: https://npmjs.org/package/jigsass-utils-display

[daviddm-image]: https://david-dm.org/TxHawks/jigsass-utils-display.svg?theme=shields.io
[daviddm-url]: https://david-dm.org/TxHawks/jigsass-utils-display
