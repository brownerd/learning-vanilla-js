# I'm trying to learn Vanilla JS
Nothing ground breaking here. I'm just trying to learn vanilla JS. This is a doc and repo of Vanilla JS code snippets to help me transition from being a shitty jQuery user to a more skilled JS dewd.

YES, these snippets are copies from elsewhere on the web. But they are in one place for me to use for references and grep until I can write this shit on my own.


## Other great  Resources
- [YOU MIGHT NOT NEED JQUERY](http://youmightnotneedjquery.com/)
- [Apollo](https://github.com/toddmotto/apollo)


## Doc ready

[jQuery $(document).ready() Equivalent in Vanilla JavaScript](http://beeker.io/jquery-document-ready-equivalent-vanilla-javascript)
```javascript

var domReady = function(callback) {
    document.readyState === "interactive" || document.readyState === "complete" ? callback() : document.addEventListener("DOMContentLoaded", callback);
};

//We can use this domReady() function just like the jQuery ready() function.

domReady(function() {
    // Your code here
});

```

## Has class

[jjmu15/has_class.js](https://gist.github.com/jjmu15/8646098)

```javascript

// hasClass, takes two params: element and classname
function hasClass(el, cls) {
  return el.className && new RegExp("(\\s|^)" + cls + "(\\s|$)").test(el.className);
}


/* use like below */
// Check if an element has class "foo"
if (hasClass(element, "foo")) {

  // Show an alert message if it does
  alert("Element has the class!");
}

```


[Creating jQuery-style functions in JavaScript, hasClass, addClass, removeClass, toggleClass](http://toddmotto.com/creating-jquery-style-functions-in-javascript-hasclass-addclass-removeclass-toggleclass/)
```javascript


function hasClass(elem, className) {
    return new RegExp(' ' + className + ' ').test(' ' + elem.className + ' ');
}
This uses a simple RegEx test, to ‘scan’ for our class name. Don’t know what RegEx is? It stands for RegularExpression, look it up – task 1!

Put into some practical use, we can then put it into practice, without duplicating the RegEx return each time:

if (hasClass(document.documentElement, 'ie6')) {
    // Do something crazy
} else {
    // Phew
}

```



## Adding a class with ‘addClass’

```javascript

function addClass(elem, className) {
    if (!hasClass(elem, className)) {
        elem.className += ' ' + className;
    }
}
//You’ll notice we use our hasClass function again! It checks to see if the element has the class, but it reverts the expression meaning it will run if the element doesn’t have a class. The ‘ ‘ is in-fact adding a space before the class so it doesn’t join another class.

//Using a bang (!) you can invert it’s meaning, so technically this means ‘if the element doesn’t have the class’. You could then use it like so on a JavaScript click handler:

document.getElementById('myButton').onclick = function() {
    addClass(document.documentElement, 'some-class');
}

```




## Removing a class with ‘removeClass’
```javascript

function removeClass(elem, className) {
    var newClass = ' ' + elem.className.replace( /[\t\r\n]/g, ' ') + ' ';
    if (hasClass(elem, className)) {
        while (newClass.indexOf(' ' + className + ' ') >= 0 ) {
            newClass = newClass.replace(' ' + className + ' ', ' ');
        }
        elem.className = newClass.replace(/^\s+|\s+$/g, '');
    }
} }
}


document.getElementById('myButton').onclick = function() {
    removeClass(document.documentElement, 'some-class');
}

```


## Adding/removing (toggling) the class with ‘toggleClass’

```javascript

function toggleClass(elem, className) {
    var newClass = ' ' + elem.className.replace( /[\t\r\n]/g, ' ' ) + ' ';
    if (hasClass(elem, className)) {
        while (newClass.indexOf(' ' + className + ' ') >= 0 ) {
            newClass = newClass.replace( ' ' + className + ' ' , ' ' );
        }
        elem.className = newClass.replace(/^\s+|\s+$/g, '');
    } else {
        elem.className += ' ' + className;
    }
}


```



## Same as above rewritten by Yannick Albert
```javascript

// Has class
Element.prototype.hasClass = function (className) {
    return new RegExp(' ' + className + ' ').test(' ' + this.className + ' ');
};

// Add class
Element.prototype.addClass = function (className) {
    if (!this.hasClass(className)) {
        this.className += ' ' + className;
    }
};


// Remove Class
Element.prototype.removeClass = function (className) {
    var newClass = ' ' + this.className.replace(/[\t\r\n]/g, ' ') + ' '
    if (this.hasClass(className)) {
        while (newClass.indexOf( ' ' + className + ' ') >= 0) {
            newClass = newClass.replace(' ' + className + ' ', ' ');
        }
        this.className = newClass.replace(/^\s+|\s+$/g, ' ');
    }
};


// Toggle Class
Element.prototype.toggleClass = function (className) {
    var newClass = ' ' + this.className.replace(/[\t\r\n]/g, " ") + ' ';
    if (this.hasClass(className)) {
        while (newClass.indexOf(" " + className + " ") >= 0) {
            newClass = newClass.replace(" " + className + " ", " ");
        }
        this.className = newClass.replace(/^\s+|\s+$/g, ' ');
    } else {
        this.className += ' ' + className;
    }
};


var elem = document.getElementById('foo');
elem.addClass('bar');
alert(elem.hasClass('bar'));
elem.removeClass('bar');
alert(elem.hasClass('bar'));
elem.toggleClass('bar');
alert(elem.hasClass('bar'));


```



[A useful function for making querySelectorAll() more like jQuery](http://codepen.io/michaelschofield/snippets/a-useful-function-for-making-queryselectorall-more-like-jquery)
```javascript

function $$(selector, context) {
    context = context || document;
    var elements = context.querySelectorAll(selector);
    return Array.prototype.slice.call(elements);
}

//The array-like NodeList is turned into a regular array with slice.call( elements ) (MDN)), which can add convenience and otherwise mitigate some of the withdrawal we in Generation jQuery feel when iterating through the DOM.

$$( '.pie' ).forEach( function( pie ) {
  pie.classList.add( 'cream' );
});

```



```javascript



```



```javascript



```




```javascript



```
