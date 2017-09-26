# Badger Accordion
An accessible light weight, vanilla JavaScript accordion with an extensible API. Just 8.17kb Gzipped (2.49kb).

**Contents**
  - [The idea](#the-idea)
  - [Key terminologies](#key-terminologies)
  - [Basic setup](#basic-setup)
    - [How to use the plugin](#how-to-use-the-plugin)
    - [Styles](#styles)
  - [Options](#options)
  - [Methods](#methods)
  - [Roadmap](#roadmap)


## The idea
 - To make an accessible, animated, accordion with an extensible API.
 - Make it using just plain vanilla JavaScript.
 - Ensure that it has just plain simple css. Enough to get it to work. Not too much that you have to spend ages overwriting it.
 - Ensure that it is accessible as possible.


## Key terminologies
 - `panel`  - The section of the accordion than opens and closes
 - `header` - The button that opens an accordion panel


## Basic setup

Firstly create the markup for your accordion. As a bare minimum you will need to create;

 * A container with your `accordion class`. This is required and will be passed into your accordion instance.
    * Default `accordion class`: `js-badger-accordion`.
 * A button with your accordion header class.
    * Default: `js-badger-accordion-header`.
 * A panel with your accordion panel class. This panel will need to have as a bare minimum css of having `overflow: hidden` set.
    * Default: `js-badger-accordion-panel`.
 * A inner panel element.
    * Default: `js-badger-accordion-panel-inner`.

### How to use the plugin
You'll need to import the plugin and create a new instance so you can use it. There is a working example in the `example` directory (shock horror!) if you'd like something to reference.

 1. Import `badger-accordion.js`
 2. If you have not installed the plugin the NPM ensure that you have `transition-end.js` somewhere your Webpack resolver path
 3. Include the `badger-accordion.css`

I'd recommend also importing the `Array.from` pollyfill so that your accordion will work for IE9+. The (pollyfill)[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from#Polyfill] only adds `0.93kb` (`0.34kb` gzipped).
```
import pollyfill from 'array-from-pollyfill';
import BadgerAccordion from 'badger-accordion';

// Creating a new instance of the accordion
const accordion = new BadgerAccordion('.js-badger-accordion');
```

Next you'll want to create your markup. This is the minimum markup you will need for your accordion. You can use any html elements you would like but you will need to follow the nesting in the example below. I have included the selector `badger-accordion__panel` as I feel it is best to use separate selectors for targeting an element with JavaScript and CSS.
```
<dl class="js-badger-accordion">
    <dt>
        <button class="js-badger-accordion-header">
            Header Content
        </button>
    </dt>
    <dd class="badger-accordion__panel js-badger-accordion-panel">
        <div class="js-badger-accordion-panel-inner">
            Panel Content
        </div>
    </dd>
</dl>
```

#### Styles
I have created some simple CSS styles to help you with creating an accordion which are in `badger-accordion-demo.css`. There are also `scss` files with the basic css, demo & some handy mixins you could use to speed up creating a nice accordion.



## Options

The accordion has a selection of options that you can overwrite. For example if you wanted to open the first and 4th panel when the accordion is initalised;

```
new BadgerAccordion('.js-badger-accordion', {
    openHeadersOnLoad: [0, 3]    
});
```

### Options
| Option             | Type    | Default                            | Description |
| ---                | ---     | ---                                | ---   |
| headerClass        | String  | `.js-badger-accordion-header`      | Class for panel's header  |
| panelClass         | String  | `.js-badger-accordion-panel`       | Class for panel  |
| panelInnerClass    | String  | `.js-badger-accordion-panel-inner` | Class for panel inner container  |
| hidenClass         | String  | `is-hidden`                        | Class added to panels that are hidden  |
| initalisedClass    | String  | `badger-accordion--initalised`     | Class add to accordion when it has initalised   |
| headerDataAttr     | String  | `data-badger-accordion-header-id`  | Data attribute on each header   |
| openMultiplePanels | Boolean | `false`                            | Give you the ability to have mutiple panels open at one time. By default this is disabled  |
| headerOpenLabel    | String  | `Accordion open button`            | Value for header's `aria-label` when button is closed |
| headerCloseLabel   | String  | `Accordion close button`           | Value for header's `aria-label` when button is open  |


## Methods

The accordion has a series of methods allowing you to have full control over extending the plugin. For example if you wanted to close all your accordion's panels;

```
accordion.closeAll();
```


| Method          | Arguments            | Description | Example |
|---              |---                   |---          |---          |
| `getState()`    | headerId/s - `array` | Returns the state of a panel/s by passing in the _node item index/s_ as an array. |  Getting a single Id. `accordion.getState([0])`. <br> Getting multiple header's state `accordion.getState([0, 1, 2])` |
| `open()`        | headerIndex          | Opens a given panel using its `headerIndex`. Eg; ` accordion.open( 0 );` ||
| `close()`       | headerIndex          | Closes a given panel using its `headerIndex`. Eg; ` accordion.close( 0 );` ||
| `togglePanel()` | animationAction, headerIndex | Toggles panel into opening or closing. `animationAction` is either `open` or `closed`. ||
| `openAll()`     |                      | Opens all accordion panels   ||
| `closeAll()`    |                      | Closes all accordion panels  ||


### Roadmap
 - Create option for callback methods on each public method
 - Export an IE9 safe version in the repo
 - Create horizontal accordion option
