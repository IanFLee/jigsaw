# jigsaw
A library of client-side MVC-type functions
<ul>
 <li><a href="#listen-listenat-and-inputc">listener functions make adding event listeners quicker and easier</a></li>
 <li><a href="#the-doc-object">the doc object is shorthand for document functions</a></li>
 <li><a href="#the-mdl-object">the mdl object is shorthand for dynamically creating Material Design Lite class elements</a></li>
</ul>

----
# cl()


```function cl(x) { console.log(x); }```

----

<h3>Abstractions of addEventListener.</h3>

 - listenAt() is for DOM elements already present in the HTML
 - listen() is for DOM elements that have been created dynamically in the JS
 - inputCAt() is meant for adding larger amounts of event listeners by the element's id
 - inputC() is meant for adding larger amounts of event listeners by references to dynamically created elements

Each is functionally equivalent but preferred based on circumstances.

# listen(el, type, fn)

usage:

```
var el = document.createElement('button');
listen(el, 'click', function() {alert('clicked')});
```
----
# listenAt(id, type, fn) 

usage:
```
<button id="btn">click me</button>
listenAt('btn', 'click', function() {alert('clicked')});
```
----

# inputC(ic) or inputCAt(ic)

<h5>inputC() is for adding multiple event listeners.</h5>

usage:
```
var f = function(){};
var ic = { /*input controller object*/ };
inputC(ic);
```

It takes an 'input controller' object and uses the values to attach event listeners.

An input controller looks like this:

```
// functions for ic object
var turnRed = function() { /*turn red*/ };
var save = function() { /*save*/ };
var turnBorderBlue = function() { /*turn border blue*/ };
var login = function() { /*login*/ };

// ic object declaration for inputCAt()
var ic = {
  'saveButton' : {
    click : [turnRed, save],
    hover : [turnBorderBlue]
  },
  'loginButton' : {
    click : [login]
};

// ic object declaration for inputC()
var ic = {
  saveButton : {
    el : saveButton,
    click : [turnRed, save],
    hover : [turnBorderBlue],
  },
  loginButton : {
    el : loginButton,
    click : [login]
  }
};

```

This follow the structure:
```
var ic = {
  <id of element to which will the listener will be added> : {
    <event type> : [<array of functions to run on event>]
  }
};
inputCAt(ic)

or

var ic = {
  <semantic name of element> : {
    el : <reference to HTMLObject element>,
    <event type> : [<array of functions to run on event]
  }
};
inputC(ic);
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

is

document.createElement(type);
```
If doc.ce() is not given an argument, type defaults to 'div'.
Use 'btn' for 'buttton' and 'in' for 'input'.
----
Create and append text node simultaneously.
```
doc.atn(element, text);

is

var text = document.createTextNode(text);
element.appendChild(text);
```
----
Append multiple children simultaneously.
```
doc.amc(parent, [array of children]);
```
----

# The mdl object

This object provides shorthand for creating certain Material Design Lite class elements.

```
var parentGrid = mdl.parentGrid('1000px');
```
Returns an mdl grid, setting the max-width;

----
```
var childGrid = mdl.childGrid();
```

----
```
var cell = mdl.col(12, 6, 3);
```
Takes column sizes for desktop, tablet and phone and returns an mdl cell.

----
```
var textfield = mdl.input('passwordInput', 'What is the super secret password?');
```
Takes an element id and label text and returns an mdl textfield component such as:
```
<div class='mdl-textfield mdl-js-textfield mdl-cell--12-col'>
  <input class='mdl-textfield__input' type='text' id='passwordInput'>
  <label class='mdl-textfield__label'>What is the super secret password?</label>
</div>
```

----
```
var multiLineTextfield = mdl.multiInput('novelInput', 'Tell us your life story', 20);
```
Is the same as above, but returns a multi-line textfield. The third argument sets the number of rows.

----
# post(el)

Empties the document body and appends a dynamically created HTMLElement to the empty document.<br>
Mainly used to publish a root HTMLElement node to the DOM.

----
# style(el, obj)

Adds styling to an element

```
style(btn1, {
  border: 'solid',
  width: '50vw',
  height: '50vh'
});
