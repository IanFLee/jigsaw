# jigsaw
A library of MVC-type functions

----
# cl()

```cl();``` is ```console.log();```

```cl('hi');```

----

<h1>listenAt(), listenFor(), and makeIC()</h1>

<h3>Similarities and Differences </h3>

The following three functions are all augmentations of addEventListener.

 - listenAt() is for DOM elements already present in the HTML, not the JS (document.getElementById(id)).
 - listenFor() is for DOM elements that have been created dynamically in the JS (document.createElement(type)).
 - makeIC() is meant for adding larger amounts of event listeners. This currently only works on elements already present (getElementById).

Each is functionally equivalent but preferred based on circumstances.

----
# listenAt(id, type, fn) 

usage:
```
<button id="btn">click me</button>
listenAt('btn', 'click', function() {alert('clicked')});
```

<h5>listenAt() is for adding individual event listeners.<br></h5>

id is the id of the element in the HTML.<br>
type refers to a type of input event.<br>
fn is the callback function called on the input event.<br>

is equivalent to:

```
var el = document.getElementById(id);
el.addEventListener(type, fn);
```

----
# listenFor(el, type, fn)

usage:

```
var el = document.createElement('button');
listenFor(el, 'click', function() {alert('clicked')});
```

listenFor() is also for adding individual event listeners. This is the same as above, except that el refers to a DOM node declared inside the JS.

is equivalent to:
```
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
var turnRed = function() { /*turn red*/ };
var save = function() { /*save*/ };
var turnBorderBlue = function() { /*turn border blue*/ };
var login = function() { /*login*/ };

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
----

# The doc object

The doc object quickens certain document processes with shorthand. The current list of these is:

```
doc.ce(type);
document.createElement(type);
```
----
```
doc.ctn(text);
document.createTextNode(text);
```
----
```
doc.ac(parent, type);
parent.appendChild(document.createElement(type));
```

----

# post(el)

Empties the document body. Takes a dynamically created HTMLElement and appends it to the empty document.

is equivalent to:

```
document.body.innerHTML = '';
document.body.appendChild(el);
```
