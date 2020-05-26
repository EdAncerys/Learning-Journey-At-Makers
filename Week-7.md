# Week 7 Goals

#### By the end of the week all developers can:

- Build a front-end app in Javascript
- Work competently in Javascript
- Reason about asynchronous behaviour in Javascript

This week is analogous to week 2 in that developers will be wrestling with some underlying language concepts that are not well understood (by Makers).

Most of the work and interventions we have run historically are meant to 'de-magic' Javascript and force developers to confront the pieces they are glossing over in an attempt to get work done.

## Daily Goals
### Tuesday 26 of May 2020

## Morning Goals

- Code Review for the weekend **Bowling** challenge.
- Attend week 7 *kick off*.
- Set a working plan for the new week

##### Plan:

- Review weekend challenge in pair. Will be reviewing Jo's code.
- Set goals for the new week

### Weekly Morning Goals

- Events and event handlers.
- Manipulating the Document Object Model (DOM).
- Ajax.
- Frontend templating.
- Frontend routing.

#### Explain events and event handlers.

**Plan:**

- Perform research online individually.  
- Describe what **events and event handlers are** and it's usages.
- Summarize and give some practical example.

**Process:**

#### Events

In programming, an event is an action that occurs as a result of the user or another source, such as a mouse click. An event handler is a routine that deals with the event, allowing a programmer to write code that will be executed when the event occurs.

#### Registering onevent handlers

The onevent handlers are properties on certain DOM elements to manage how that element reacts to events. Elements can be interactive (links, buttons, images, forms, and so forth) or non-interactive (such as the base <body> element). HTML Events are actions like:

- Web page has finished loading
- An input field was changed
- Being clicked
- Detecting pressed keys
- Getting focus

The on-event handler is usually named with the event it reacts to, like onclick, onkeypress, onfocus, etc.

#### Events on the Web

Another example of an event is a user clicking on a button within a web page. This action creates what is known as a "click" event. JavaScript could then be used to program a reaction to the event, for instance, you could use the onclick event handler shown in the following box:
```
<form action="#" method="post">
<input type="button" value="Click for a Message" onclick="window.alert('Hello!');">
</form>
```
Or by setting the corresponding property from JavaScript:
```
document.querySelector("button").onclick = function(event) { … }.
```

**What I've Learned:**

> The Web platform provides several ways to be notified of DOM events. Two common approaches are addEventListener() and the specific onevent handlers.  
> HTML events are "things" that happen to HTML elements.  
> When JavaScript is used in HTML pages, JavaScript can "react" on these events.
