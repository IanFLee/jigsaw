# jigsaw
A library of MVC-type functions

----
# cl()

```cl();``` is ```console.log();```

```cl('hi');```

----

<h1>listen(), listenAt(), and inputC()</h1>

<h3>Similarities and Differences </h3>

The following three functions are all augmentations of addEventListener.

 - listenAt() is for DOM elements already present in the HTML, not the JS (document.getElementById(id)).
 - listenFor() is for DOM elements that have been created dynamically in the JS (document.createElement(type)).
 - inputC() is meant for adding larger amounts of event listeners. This currently only works on elements already present (getElementById).

Each is functionally equivalent but preferred based on circumstances.

# listen(el, type, fn)

usage:

```
// where el holds a DOM Element
listen(el, 'click', function() {alert('clicked')});
```

<h5>listen() is for adding individual event listeners.<br></h5>

el is the dynamically created DOM Element.<br>
type refers to a type of input event.<br>
fn is the callback function called on the input event.<br>

is equivalent to:
```
// where el holds a DOM Element
el.addEventListener(type, fn);
```


----
# listenAt(id, type, fn) 

usage:
```
<button id="btn">click me</button>
listenAt('btn', 'click', function() {alert('clicked')});
```

listenAt() is also for adding individual event listeners. This is the same as above, except that id refers to an HTML element declared inside the HTML.

is equivalent to:

```
var el = document.getElementById(id);
el.addEventListener(type, fn);
```

----

# inputC(ic)

<h5>inputC() is for adding multiple event listeners.</h5>

usage:
```
var f = function(){};
var ic = { /*input controller object*/ };
inputC(ic);
```

It takes an 'input controller' object and uses the values to attach event listeners to DOM nodes.

An input controller looks like this:

```
// functions for ic object
var turnRed = function() { /*turn red*/ };
var save = function() { /*save*/ };
var turnBorderBlue = function() { /*turn border blue*/ };
var login = function() { /*login*/ };

// ic object declaration
var ic = {
  'saveButton' : {
    click : {
      turnRed : turnRed,
      save : save
    },
    hover : {
      turnBorderBlue : turnBorderBlue
    }
  },
  'loginButton' : {
    click : {
      login : login
    }
};
```

This follow the structure:
```
var ic = {
  <id of element to which will the listener will be added> : {
    <event type> : {
      <function to run on event>
    }
  }
};
```
<h5>inputC() works well with models</h5>

```
var model = {color: 'black'};

var changeColor = function() {
 model.color = 'gold';
};

var ic = {
  'colorBox' : {
    'click' : {
     changeColor : changeColor
    }
   } 
 };
 
 inputC(ic);
```

----

# The doc object

The doc object quickens certain document processes with shorthand.

```
doc.ce(type);
document.createElement(type);
```
If doc.ce() is not given an argument, type defaults to 'div'.
Use 'btn' for 'buttton' and 'in' for 'input'.
----
```
doc.atn(element, text);
var text = document.createTextNode(text);
element.appendChild(text);
```
Create and append text node simultaneously.
----
```
doc.amc(parent, [array of children]);
for (var child of arr) {
      parent.appendChild(child);
    }
```
Append multiple children simultaneously.
----
----

# post(el)

Empties the document body. Takes a dynamically created HTMLElement and appends it to the empty document.<br>
Mainly used to publish a root HTMLElement node to the DOM.

is equivalent to:

```
document.body.innerHTML = '';
document.body.appendChild(el);
```
