# Getting Started

- Clone this repository
- In terminal, run: `python -m SimpleHTTPServer`
- Navigate to `http://localhost:8000/index.html`

# Lesson

## Angular's Built-In Directives

### Working with the DOM can be tedious

Angular's built-in directives are a way of simplifying the way we interact with and control the DOM. Imagine trying to make a list of items in HTML based on an array, call the array `things`.  What are some of the ways we have been doing that so far?

#### Vanilla JavaScript
With vanilla JavaScript it could look something like this:

*index.html*
```HTML
<ul><ul>
```

*app.js*
```javascript
var element = document.querySelector('ul');

for (var i = 0; i < things.length; i++) {
  var li = document.createElement('li')
  var thing = document.createTextNode(things[i])
  li.appendChild(thing)
  element.appendChild(li)
}

```

The code to modify the view (html) is in a separate file (app.js), and we have to first use JavaScript to find the element we want to append list items to.

#### EJS

Using EJS, it's a little bit cleaner since we can keep view logic in the view:

*index.ejs*
```javascript
<% for(var i = 0; i < things.length; i ++;) %>
    <li><%= things[i] %></li>
<% end %>
```

There's still lots of syntax going on here.  First we have to create special tags to indicate that what we're typing is EJS. We're then using raw JavaScript to render HTML elements.  There's EJS is embedded in the HTML, and HTML embedded in the EJS, it is messy.

#### Angular

Here's how you can add list items using Angular's built-in directives:

```HTML
<li ng-repeat='thing in things'>{{thing}}</li>
```

### Built-in Directives

Directives are Angular's way of extending HTML. Angular uses directives to add functionality to HTML elements and attributes.  

#### ng-hide, ng-show

Two of the simplest Angular directives are ng-hide and ng-show. Both are used to conditionally hide or show certain elements in the DOM. Here are some examples of how they work:

```
<div ng-show="3 + 4 == 5">
  3 + 4 isn't 5, don't show
</div>

<div ng-show="3 + 4 == 7">
  3 + 4 is 7, do show
</div>

<div ng-hide="3 + 4 == 5">
    3 + 4 isn't 5, don't hide
</div>

<div ng-hide="3 + 4 == 7">
  3 + 4 is 7, do hide
</div>
```

 - How does Angular make the DOM elements show/hide?  

#### ng-if

```
<div ng-if="3 + 4 == 7">
  3 + 4 is 7, do show
</div>
```

 - How does ng-if work?  
 - What could the consequences be of using ng-if instead of ng-show/ng-hide?

#### ng-class

What if we want to conditionally _style_ elements on the page, rather than conditionally hiding or showing them? For this, we can use the `ng-class` directive. There are a few different ways to use `ng-class`, but one of the most common is to pass in an object of key-value pairs:

`<div ng-class="{class1: boolean-expression1, class2: boolean-expression2, ... }">`

In this case, the div will have a class of `class` if `conditional-expression1` evaluates to true, and similarly for `class2`.

Here's a more concrete example. What will each of the following divs look like?

```
<div ng-class="{redbg: 1 + 1 === 2, 'text-lg': 0 !== 1 }">Here's some large text on a red background.</div>
<div ng-class="{redbg: [1,2].length > 2, 'text-lg': true }">Here's some large text on a white background.</div>
<div ng-class="{redbg: 5 % 3 === 2, 'text-lg': true && false }">Here's some normal-sized text on a red background.</div>
<div ng-class="{redbg: 'hi'.indexOf('e') > -1, 'text-lg': 'bye'[3] }">Here's some normal-sized text on a white background.</div>
```

#### ng-model, ng-init

One of the most important directives you'll see is the `ng-model` directive. This directive binds data inside inputs, checkboxes, etc. to properties on our model. (We'll see more about how that's done when we talk about controllers). To see an example of this, work through the [introductory example](https://github.com/gSchool/angular-curriculum/blob/master/Unit-1/01-intro-and-setup.md) in the Angular curriculum. Then, try to solve the first three exercises in [Unit 1, section 4](https://github.com/gSchool/angular-curriculum/blob/master/Unit-1/04-expressions-and-filters.md) of the curriculum.

Cool, right? What do you think `ng-init` does? To check, compare the following two examples in a simple angular app:

Example 1:

```
<input type="text" placeholder="What's your favorite color?" ng-model="favColor">
<p>My favorite color is {{ favColor }}</p>
```

Example 2:

```
<input type="text" placeholder="What's your favorite color?" ng-model="favColor" ng-init="favColor='blue'">
<p>My favorite color is {{ favColor }}</p>
```
