# jigsaw
A library of MVC-type functions

----
# cl()

cl(); is console.log();
----

<h3>listenAt(), listenFor(), and makeIC()</h3>

# Similarities and Differences

The following three functions are all condensations of addEventListener.
listenAt() is for DOM elements already present in the HTML, not the JS (document.getElementById(id)).
listenFor() is for DOM elements that have been created dynamically in the JS (document.createElement(type)).
makeIC() is meant for adding larger amounts of event listeners. This currently only works on elements already present (getElementById).

Each is functionally equivalent but preferred based on circumstances.

----
# listenAt(id, type, fn) 

<button id="btn">click me</button>
listenAt('btn', 'click', function() {alert('clicked')});

listenAt() is for adding individual event listeners.
id is the id of the element in the HTML.
type refers to a type of input event.
fn is the callback function called on the input event.

var el = document.getElementById(id);
el.addEventListener(type, fn);
----
# listenFor(el, type, fn)

var el = document.createElement('button');
listenFor(el, 'click', function() {alert('clicked')});

listenFor() is also for adding individual event listeners. This is the same as above, except that el refers to a DOM node declared inside the JS.

el.addEventListener(type, fn);
----
# makeIC(ic)

makeIC() is for adding multiple event listeners.

It takes an input controller object and uses the values to attach event listeners to DOM nodes.

An input controller looks like this:

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

This follow the structure:

var ic = {
  <id of element to which will the listener will be added> : {
    <event type> : {
      <function to run on event>
    }
  }
};

----

# The doc object

The doc object quickens certain document processes with shorthand. The current list of these is:

doc.ce(type); --- is the same as --- document.createElement(type);
doc.ctn(text); --- is the same as --- document.createTextNode(text);
doc.ac(parent, type); --- is the same as --- parent.appendChild(document.createElement(type));

----

# post(el)

Empties the document body. Takes a dynamically created HTMLElement and appends it to the empty document.

document.body.innerHTML = '';
document.body.appendChild(el);
