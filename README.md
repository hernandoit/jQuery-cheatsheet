# jQuery cheat sheet

Table of Contents

find
hide
show
html
text
val
append
prepend 
css
attr
data
on
off
each

## `.find`

> is a method that searches through the descendants(child) in the DOM tree and gets all child elements. Will move through multiple levels of children.

### `.find( selector )`

> Check elements inside & use a selector expression to filter descendents.

Selector expression example:
`'body'`, `'#my-id'`, `'.my-class'`

### `.find( element )`

HTML:

```html
<button><p></p></button>
```

jQuery:

```js
// Selector example
$('button').find('p')
// Element/jQuery object example
const $pTags = $('p')
const $allThePTagsInTheButton = $('button').find($pTags)
```

## `.hide`

> Hides an HTML element

### `.hide( [duration] [, complete] )`

```html
<p id="my-paragraph"></p>
```

```js
// Ends up setting css `display` to `none`
// replace with example without callback function
$('#my-paragraph').hide()

// replace with example with callback function
$('#my-paragraph').hide(1000, function () { console.log('goodbye') })
```

## `.show`

> Shows an HTML element

### `.show()`

### `.show( [duration] [, complete] )`

```html
<p id="my-paragraph"></p>
```

```js
// Sets css `display` to `block` or back to what it was before it was hidden
// replace with example without callback function
$('#my-paragraph').show()

// replace with example with callback function
$('#my-paragraph').show(1000, function () { console.log('hello') })
```

## `.html`

> Get the HTML contents of the first element selected OR set the HTML contents of every element selected

### `.html()` - Getter

> Finding the first selected element & return the HTML contents of that element as a string

```html
<body>
  <p>Words</p>
</body>
```

```js
// replace with GETTER example
const myBodyHtml = $('body').html()
console.log(myBodyHtml) // '<p>Words</p>'
```

### `.html( function )` or `.html( htmlString )` - Setter

> Sets the child elements of the selected element

```html
<body>
</body>
```

```js
// replace with SETTER example
$('body').html('<p>Here's a paragraph</p>')

// Function example:
$('body').html(function(index, oldHtml) {
  return '<p>New paragraph</p>'
})
```

## `.text`

> Gets or sets the text inside matched elements

### `.text( text )` - Setter

### `.text()` - Getter

```html
<p>Some text</p>
```

```js
// replace with GETTER example
$('p').text() // return 'Some text'

// replace with SETTER example
$('p').text('New text') // sets the paragraph text to 'New text'
```

## `.val`

> Get the current value of the first element in the set of matched elements or set the value of every matched element.

### `.val( value )` - Setter

> A string of text, a number, or an array of strings corresponding to the value of each matched element to set as selected/checked.

### `.val()` - Getter

> .val() method is primarily used to get the values of form elements such as input, select and textarea. When called on an empty collection, it returns undefined.

```html
<!-- Inputs have values instead of text -->
<input id="name" type="text" value="Starting value" placeholder="Starter content">
```

```js
// getter example
$('input:text').val()

// replace with SETTER example
$('input:text').val('name')
```

## `.append`
> adds content to the end of the selected DOM element, so this will end up being the `last child` element

### `.append( content [, content ] )`
We can send just one item to be appended or multiple (the optional `content` param).

```html
<p id="prefilled">Text</p>
<p id="empty"></p>
```

```js
// Use .append to add the string of " add to end" to the end of the p element with an id of "prefilled"
$('#prefilled').append(' add to end')
// Use .append to add some text to the empty p element with the id of "empty"
$('#empty').append('some text')
```

Output HTML:

```html
<p id="prefilled">Text add to end</p>
<p id="empty">some text</p>
```

## `.prepend`

> same as append, but it does it to the beginning od the selected DOM element rather than the end.

### `.prepend( content [, content ] )`
We can send just one item to be prepended or multiple (the optional `content` param).

```html
<p id="prefilled">Some text</p>
<p id="empty"></p>
```

```js
// Use .prepend to add some text to the beginning of the p element with an id of "prefilled"
$('#prefilled').prepend('add to beginning')
// Use .prepend to add some text to the empty p element with an id "empty"
$('#empty').prepend('some text')
```

Output HTML:

```html
<p id="prefilled">add to beginningSome text</p>
<p id="empty">some text</p>
```

## `.css`

> Gets the CSS properties for the first selected element, or sets the CSS properties for all selected elements.

### `.css( propertyName )` - Getter!

```css
p {
  color: green;
}
```

```html
<p></p>
```

```js
$('p').css('color') // returns 'green'
```

### `.css( propertyName, value )` - Setter!

```html
<p style="color: green"></p>
```

```js
$('p').css('color', 'yellow') // sets p tag color to yellow
```

## `.attr`

> Get the value of an attribute for the first element in the set of matched elements or set one or more attributes for every matched element.

### `.attr( attributeName )` - Getter

> Get the value of an attribute for the first element in the set of matched elements

### `.attr( attributeName, value )` - Setter

> set one or more attributes for every matched element.

```html
<p id="paragraph"></p>
```

```js
// replace with GETTER example for getting the attribute of "test"
$('p').attr( 'id' )
// replace with SETTER example for setter a new id attribute of "a-new-value"
$('p').attr( 'class', 'newClass' )
// $('a').attr('href', 'www.google.com')
// $('img').attr('alt', 'src')
// $('link').attr('src')
// $('button').attr('type')
```

## `.data`

> Store arbitrary data associated with the matched elements or return the value at the named data store for the first element in the set of matched elements.

### `.data( key, value )` - Setter!

### `.data( key )` - Getter!

```html
<p data-thing="some stuff"></p>
```

```js
// replace with GETTER example for getting the data attribute of "thing"
$('p').data('thing')
// replace with SETTER example for setting the value of the data attribute "thing" to a new value
$( 'p' ).data( 'thing', 'ourData' )
// New data:
$('p').data('someNewKey', 'some new data')
```

## `.on` - Event Listener!!!

> Attach a function to the page that will be run on a certain event. The `.on` is the "listener" that will run our "handler" (callback function) when the event occurs.

Good practice: Only set up event listeners when the page first loads. Otherwise, we risk adding multiple event listeners to single elements.

### `.on( events [, selector ] [, data ], handler )`

`events` - Name of event(s) to listen for.
`[, selector]` - Targeted element inside the selected element.
`[, data]` - Optional data to be passed to handler.
`handler` - A function to execute when the event is triggered. ALWAYS GETS EVENT OBJECT AS PARAM!!!

```html
<p id="clickable"></p>
<!-- Pretend element that doesn't exist when the page loads -->
<p id="shows-up-later"></p>
```

```js
// replace with example for an event listener .on that will 'listen' for a click on the p element with an
// id of 'clickable' and console.log the string of 'we clicked the p tag!'
$('#clickable').on('click', function (event) {
  // This function will automagically (via jQuery) get
  // an argument passed to it which is an object
  // representing the event that occurred
  console.log('We clicked it!')
  // event.target will be the element the event ocurred on
  // Best practice: use `event.target` instead of `this` to be more accurate
  $(event.target).text('Clicked')
  // vs not as good:
  // $(this).text('clicked')
})

$('body').on('click', '#shows-up-later', function (event) {
  // This function will only run if an element in the body
  // with an ID of `shows-up-later` is clicked on
  // This supports this element not being on the page
  // when this listener (`.on`) runs.
  console.log('We clicked it!')
})
```

## `.off`

> Opposite of `.on` - removes event handlers

### `.off( events [, selector ] [, handler ] )`

```html
<p id="clickable"></p>
```

```js
// replace with example for an event listener .off that will 'listen' for a click on the p element with an
// id of 'clickable' and console.log the string of 'we STOPPED the click on the p tag!'
const myEventHandler = function () { console.log('Clicked') }
$('#clickable').on('click', myEventHandler)
// $('#clickable').off()
// $('#clickable').off('click')
// If you're using `.off` make sure to reference the EXACT SAME handler function
// NOT a new anonymous function
$('#clickable').off('click', myEventHandler)
```

**NOTE:** For `.on` if you use an anonymous function for the handler, `.off` will not know what to turn off!
Instead, use named functions :)

## `.each`

> each goes through a jquery object and applies a function to each element

### `.each( function )`

```html
<div>foo</div>
<div>bar</div>
<div>baz</div>
```

```js
// changes the color of each div to `'blue'`
$('div').each( function ( index, element ) {
  // vanilla js:
  // this.style.color = 'blue'
  // jQuery:
  // $(this).css('color', 'blue')
  $(element).css('color', 'blue')
})
```