# FD Dev living style-guide

> Rules are the children of principles.

## CSS Preprocessor: SASS

Keypoint: very strict syntax that help standardization

### Variables

- name in `camelCase`

## Naming convention for classes: [BEM](https://en.bem.info/)!

### Block

- the Block is the top level wrapper
- name in `PascalCase`
- one single file for each Block
- font size in `rem`

```
.SearchBox
    padding: 20px
    font-size: 2rem
    ...
```

### Element

- an Element is a single part of a Block
- name in `camelCase`
- prefixed by double underscores `__`
- font-size in `em` so the Block can scale easily and consistently

```
.SearchBox__inputField
    ...

.SearchBox__mainButton
    font-size: 2em
    ...
```

### Modifier

- a variation of the block or of the element
- name in `camelCase`
- prefixed by double dash `--`
- font-size in `em`

```
/* Block modifier */
.SearchBox--compact
    padding: 0

/* Element modifier */
.SearchBox__mainButton--small
    font-size: 1.4em
```

### State classes

- a class that can change during the life of the application
- name in `camelCase`
- prefixed by `is-`
- **MUST** always been combined to a Block or to an Element
- font-size in `em`

```
.SearchBox__mainButton.is-focused
    transform: scale(1.2)
```

### Utility classes

- a class to provide common functionalities
- prefixed by a `u-`
- name in `camelCase`
- can use `!important` [Use only proactively, not reactively!]

```
.u-alignRight
    text-align: right !important

.u-hidden
    display: none !important
```

### JS hooks

Never use styling classes for js functionalities, use ad-hoc classes prefixed by `js-`

## Semantic Class Names

Using a class name to describe content is redundant because content describes itself.
We need a class name that describes the style that we want to apply to that element with a good abstraction


```
/* Runs the risk of becoming out of date; not very maintainable. */
.blue {
    color: blue;
}

/* Too specific; limits our ability to reuse. */
.header-color {
    color: blue;
}

/* Nicely abstracted, very portable, doesn’t risk becoming out of date. */
.highlight-color {
    color: blue;
}
```

## Code Style

### General Rules [from CSS Guidelines](http://cssguidelin.es/)

* **Select what you want explicitly**, rather than relying on circumstance or coincidence. Good Selector Intent will rein in the reach and leak of your styles.
* **Write selectors for reusability**, so that you can work more efficiently and reduce waste and repetition.
* **Do not nest selectors unnecessarily**, because this will increase specificity and affect where else you can use your styles. *[if a selector will work without it being nested then do not nest it]*
* **Do not qualify selectors unnecessarily**, as this will impact the number of different elements you can apply styles to. *[Use IDs only to explicit the uniqueness of an element in a page]*
* **Keep selectors as short as possible**, in order to keep specificity down and performance up.

### Editor rules

- 2 spaces for indentation
- max 80 column *[always remember the first quote of the document]*

#### [.editorconfig](http://editorconfig.org)

Use the .editorconfig file that you can find in the repo

### General styles

- 1 empty line before each selector
- every selector on his own line
- a space after our property–value delimiting colon ` : `

#### For plain CSS or SCSS

- a space before our opening brace ` { `
- properties and values on the same line
- each declaration on its own new line
- the opening brace ` { ` on the same line as our last selector;
- our first declaration on a new line after our opening brace ` { `
- our closing brace ` } ` on its own new line at the same level of the selector
- a trailing semi-colon ` ; ` on our last declaration

### Comments

Use comments to explain what the css can not say, like hacks (why there's an `overflow: hidden` here? for clearfix, to hide contents? or whatelse?) or the instruction to use an element.

In BEM developing can be useful to have a table of content for each block to describe all the elements, the html structure expected and everything to help others to use our own wonderful code and don't waste time reading all the code.

Using preprocessors we need to explicit all the dependencies (mixins, variables) of our code.

## File structure

- {cssroot}/
    - style.preprocessor [^1]
    - helpers/ [^2]
        - _helperName.preprocessor
    - blocks/ [^3]
        - _BlockName.preprocessor

[^1]: a single file that includes all the dependencies
[^2]: variables, function, generators, and all stuffs that doesn't compile any code
[^3]: one file for each block

## Examples

### SASS

Indentation not for nesting selectors but to concatenate names

```
.SearchBox
    padding: 20px
    font-size: 2rem
    ...

    &--compact
        padding: 0

    &__inputField
        ...

    &__mainButton
        font-size: 2em
        ...

        &--small
            font-size: 1.4em

        &.is-focused
            transform: scale(1.2)

```

### Jade

```
.SearchBox
    input.SearchBox__inputField
    button.SearchBox__mainButton
```
```
.SearchBox.SearchBox--compact
    input.SearchBox__inputField
    a.SearchBox__mainButton.SearchBox__mainButton--small
```

### CSS Comments

```
/*------------------------------------------------------*\

    BLOCK DESCRIPTION

    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Debitis et, quo
    voluptate unde soluta quod ipsum explicabo sunt expedita? Quod.


    TABLE OF CONTENT

    .SearchBox
    .SearchBox--blockModifier

    .SearchBox__inputField

    .SearchBox__mainButton
    .SearchBox__mainButton--small


    EXAMPLE OF USE

    .SearchBox
        input.SearchBox__inputField
        button.SearchBox__mainButton


    DEPENDENCIES

    Variables:
    - $colorPrimary
    - $colorSecondary

    Mixins:
    - clearfix()

\*------------------------------------------------------*/
```
