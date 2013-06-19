#Bootstrap Tipover

**Provided by [Clay Street Online](http://www.claystreet.com) under an MIT License**

Visit the [live demo site](http://www.claystreet.com/sites/claystreet/dev/bootstrap/tipover/demo.html) for an interactive demo.

### Purpose

Facilitates adding custom CSS styling to Bootstrap Tooltips and Popovers.

### The Problem

The HTML source for Bootstrap Tooltips and Popovers is embedded in the JavaScript code which dynamically inserts
and removes it from the DOM.  Thus, by default, Bootstrap does not allow the flexibility for multiple tooltip or popover
styles on a page.

### The Fix

Bootstrap actually provides the hook for the fix by supporting a "template" option when initializing tooltips and popovers.
The code associated with this "tipover" solution takes advantage of this "template" option to allow a custom class
to be inserted into the tooltip and popover markup.  CSS can then be generated to provide unique styling using this
custom class.

### How does it work?

There are 3 key files provided with this "tipover" solution:

1. tipover.js
2. tooltip-custom.less
3. popover-custom.less

*tipover.js* - contains two simple functions intended to be invoked when initializing tooltips and popovers in JavaScript.
These functions return an "option" object that includes a template with the specified custom className included.
Other tooltip and popover options can be passed as the second parameter.

* ttOptions('className', additionalOptions) - returns tooltip options with a template containing 'tooltip.className'
* poOptions('className', additionalOptions) - returns popover options with a template containing 'tooltip.className'

The following Javascript initializes two custom tooltip styles:
```javascript
$(document).ready(function() {
    // initialize all elements with the 'grayTip' class to use the 'tooltip.gray' style
    $('.grayTip').tooltip(ttOptions('gray')); 
    
    // initialize all elements with the 'whiteBlueTip' class to use the 'tooltip.whiteBlue' style
    // ...additionally, specify the 'placement' option to provide a right-side tooltip
    $('.whiteBlueTip').tooltip(ttOptions('whiteBlue', {'placement': 'right'})); 
});
```

*tooltip-custom.less* - contains less mixins to allow custom tooltip styles to be easily generated.
For example, the 'gray' and 'whiteBlue' styles for the JavaScript above could be generated as follows:

```css
.tooltip.gray {
  .tooltip-custom-opacity(#fff; #555; 90); // background-color, text-color, opacity
}

.tooltip.whiteBlue {
  .tooltip-custom-opacity(#08c; #fff; #08c; 90);  // background-color, text-color, border-color, opacity
}

```

*popover-custom.less* - contains less mixins to allow custom popover styles to be easily generated.

Javascript to initialize custom styled Bootstrap popovers:
```javascript
$(document).ready(function() {

    // initialize '.blackPop' elements to use the 'popover.black' style
    $('.blackPop').popover(poOptions('black', {
        'placement': 'right',
        'html': true,
        'title': 'Custom Black Popover',
        'content': ' This is my custom popover<br>It is a simple black popover'
    }));
    
    // initialize '.blueWhitePop' elements to use the 'popover.blueWhite' style
    $('.blueWhitePop').popover(poOptions('blueWhite', {
        'placement': 'right',
        'html': true,
        'title': 'Custom White-Blue Popover',
        'content': ' This is another popover<br>It is Blue &amp; White'
    }));

});
```

The associated less file would include the following:
```css
.popover.black {
  .popover-custom-dark(#000); // #000 = content background-color, other colors auto-generated from that
}

.popover.blueWhite {
  .popover-custom(#333, #fff, #fff, #08c, #06a); // full color specification
}
```

Please look at less/demo.less and demo.html if you need more details.
I hope you find this useful!
The [live demo site](http://www.claystreet.com/sites/claystreet/dev/bootstrap/tipover/demo.html)
