#StickyState

StickyState adds state to position:sticky elements and also polyfills the missing native sticky feature.

Dependency free, pure Javascript for IE9+.

Today's browsers do not all support the position:sticky feature (which by the way is being used (polyfilled) on pretty much every site you visit) - moreover the native supported feature itself comes without a readable state. Something like `a:hover => div:sticky` to add different styles to the element in its sticky state - or to read the state if needed in JavaScript. 

Unlike almost all polyfills you can find in the wild, StickyState is highly performant. The calculations are reduced to a minimum by persisting several attributes.

In some cases you also need to know in which direction the user scrolls - for example if you want to hide a sticky header when the user scrolls up. if you set the scrollClass property of the options StickyState will add your choosen classNames to the element when it is sticky and scrolling.

As a standalone Library its 6.75kb gzipped. 

# Warning concerning Chromes implementation of native position:sticky
it looks like chromes implementaton of position:sticky is different to all other implementations out there. don't know if thats a bug - but bottom is currently not recognized by chrome. there will be a fix for this soon in sticky-state 

### Dependencies
none!

### Browser support
IE >= 9, *

<br/>

### Install
```
npm install sticky-state
```

<br/>

### Demo
#### all you can eat
https://rawgit.com/soenkekluth/sticky-state/master/examples/index.html

#### headroom style
https://rawgit.com/soenkekluth/sticky-state/master/examples/headroom.html

#### simple
https://rawgit.com/soenkekluth/sticky-state/master/examples/simple.html

<br/>

### css
Your css should contain the following lines: 
(you can specify the classNames in js)
https://github.com/soenkekluth/sticky-state/blob/master/dist/sticky-state.css
```css
.sticky {
  position: -webkit-sticky;
  position: sticky;
}

.sticky.sticky-fixed.is-sticky {
  position: fixed;
  -webkit-backface-visibility: hidden;
  -moz-backface-visibility: hidden;
  backface-visibility: hidden;
}

.sticky.sticky-fixed.is-sticky:not([style*="margin-top"]) {
  margin-top: 0 !important;
}
.sticky.sticky-fixed.is-sticky:not([style*="margin-bottom"]) {
  margin-bottom: 0 !important;
}

.sticky.sticky-fixed.is-absolute{
  position: absolute;
}

```
<br/>

### js
```javascript
var StickyState = require('sticky-state');
new StickyState(document.querySelectorAll('.sticky'));
//  all elements with class .sticky will have sticky state:
```

#### options
```javascript

var StickyState = require('sticky-state');

// the props you can set (except scrollClass this shows the default options):



var stickyOptions = {
  disabled: false, // disable or enable the sticky feature initially
  className: 'sticky', // the core class which should be equal to the css. see above.
  stateClassName: 'is-sticky',  // the state class, when the element is actually sticky
  fixedClass: 'sticky-fixed',  // the fallback class that uses position:fixed to make the element sticky 
  wrapperClass: 'sticky-wrap', // the fallback (polyfilled) version needs a placeholder that uses the space of the actual sticky element when its position:fixed
  wrapFixedSticky: true,  // by default the sticky element gets wrapped by the placeholder. if you set it to false it will be inserted right before it.
  absoluteClass: 'is-absolute',  // the polyfilled sticky element needs to be position:absolut in some cases.
  
  // scrollclass will add a class to the sticky element that is depending on the scroll direction when the element is sticky.
  // when the scrolling stops the class will be the value of "none" unless you set "persist" to true.
  
  scrollClass: {
    down: null,
    up: null,
    none: null,
    persist: false
  }
};

// instantiate with options
var stickyElements = new StickyState(document.querySelectorAll('.sticky'), stickyOptions);

```

#### api / events
```javascript
var StickyState = require('sticky-state');
new StickyState(document.querySelectorAll('.sticky'))
  .on('sticky:on', function(e){console.log('sticky:on', e.target);})
  .on('sticky:off', function(e){console.log('sticky:off' ,e.target);});

```
<br/>

### React Component
https://github.com/soenkekluth/react-sticky-state
