# GA-w03d01-lesson1

# HTML5 Forms and CSS Animations

| Objectives |
| :--- |
| Use query parameters |
| Create HTML Forms and Inputs |
| Explain the difference between a `method` and an `action` |
| Impliment forms with parameters |
| Implement CSS transitions and animations | 


### An Example `<form>` Element (Tag)

```html
<form method="POST" action="/page">
  <label for="name">Page Name</label>
  <input id="name" type="text" name="page_name" />
  <input type="submit" value="Create" />
</form>
```

#### Attributes

In the opening of the `<form>` tag you can see two attributes: `method` & `action`

- **method**: the HTTP verb (method) that the browser uses to submit the form.
- **action**: the path of the HTTP request page that processes the information submitted via the form.

>A `route` is simply a combination of a method & action. For example `GET '/page'` or `POST '/users'` are both valid routes.

>For now simply understand that it is convention for [GET](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html#sec9.3) to be used in a request when the client wants to receive data, and for [POST](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html#sec9.5) to be used in a request when the client wants to send data.

**Client / Server Model **

![client/server](https://mdn.mozillademos.org/files/4291/client-server.png)

### The `<label>` Element (Tag)

The `<label>` element is the formal way to define a label for an HTML form widget. 
"This is the most important element if you want to build accessible forms." *— MDN*

There are two ways to use labels correctly:

```html
<!-- Simple (nested) label example -->
<label>Click me 
  <input type="text" id="user" name="name" />
</label>

<!-- Using the "for" attribute with the input's id -->
<label for="user">Click me</label>
<input id="user" type="text" name="name" />
```

#### `<label>`'s Attributes

* The `for` in a label references an `<input>`s `id` attribute, not it's `name` attribute! Sometimes these values will be the same, but `for` always is matched with `id`.

* The `name` is the `key` of the `<input>`'s value when data is sent.

## Common Inputs

| Field Type | HTML Code | Notes |
|:-- |:-- |:-- |
| plain text | `<input type="text">` |  the type attribute can be omitted |
| password field | `<input type="password">` | echoes dots instead of characters |
| text area | `<textarea></textarea>` | a more customizable plain text area |
| checkbox | `<input type="checkbox">` |  can be toggled on or off |
| radio button | `<input type="radio">` |  can be grouped with other inputs |
| drop-down lists | `<select><option>` | [check here for more info](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select) |
| file picker | `<input type="file">` | pops up an “open file” dialog |
| hidden field | `<input type="hidden">` |  nothing there!
| submit button | `<input type="submit">` | activates the form's submission <br/>(a `POST` request or <br/>Javascript action) |

[Dive In To HTML5 — More inputs!](http://diveintohtml5.info/forms.html#type-email)

&#x1F535; **Activity**
```
* Create an HTML page with a big form on it with 5 elements of your choice from above!
* 10 minutes
```

### Important Attributes

All input types (including `<textarea>`s):

- **`type`**: the type of data that is being input (affects the "widget" that is used to display this
  element by the browser).
- **`name`**: the key used to describe this data in the HTTP request.
- **`id`**: the unique identifier that other HTML elements, JavaScript and CSS use to access this 
  element in the browser.
- **`value`**: the default data that is assigned to the element.
- **`placeholder`**: not a default value, but a useful HTML5 addition of a data "prompt" for an input.
- **`autofocus`**: defaults the cursor to a specific input when the page originally loads. You can only have one autofocus on your page.
- **`disabled`**: a Boolean attribute indicating that the "widget" is not available for interaction.

Radio buttons or checkboxes:

- **`checked`**: a Boolean that indicates whether the control is selected by default (is false unless).
- **`name`**: the group to which this element is connected. For radio buttons, only one element per 
  group (or name) can be checked.
- **`value`**: the data or value that is returned for a specific group (a multi-element control), if 
  this element is checked.
  
  &#x1F535; **Activity**
```
* Add some important attributes to your form, including:
* making a radio button checked by default, 
* adding placeholder text to a form
* add autofocus to the top input
* give one element default data
* 8 minutes

```
  
## Common Validations

Validations avoids having users submit bad data to our application. Knowing how to use them will save time and make your app a lot more usable.

Bad data could be anything from a required field being empty, an email address that was mistyped, or a password confirmation that doesn't match. Thankfully, HTML forms give us simple out-of-the-box validations for these common situations.

### Required

Try submitting the below form:

```html
<form>
  <label for="colorField">What is your favorite color?</label>
  <input id="colorField" name="favColor" required>
  <button>Submit</button>
</form>
```
Notice the `required` attribute on the input. Therefore, the form will not submit until some information is entered into the field.

### Pattern matching

```html
<form>
  <label for="kindOfBob">Do you go by bob or bobert?</label>
  <input id="kindOfBob" name="bobType" pattern="bob|bobert" required>
  <button>Submit</button>
</form>
```

The `pattern` attribute allows us to specify the values we will accept. In this case only `bob` or `bobert` are acceptable.

### Length

You may need the user to enter a specific amount of characters. Let's say you need a username to be at least 6 characters. You can use the `minlength` or `maxlength` attributes to help.

```html
<form>
  <label for="userName">What's your username?</label>
  <input id="userName" name="userName" minlength="6" required>
  <button>Submit</button>
</form>
```

  &#x1F535; **Activity**
```
* add required, pattern matching, and length validations to your form
* 10 minutes

```
# CSS Transitions and Animations

CSS supports two main kinds of animation: **transitions** and **keyframe animations**. 
They both result in styles changing over time, and both don't give you any extra styling – you can only animate using CSS properties that already exist.

**Transitions** are generally used as a reaction to a user's action - something that changes when you hover or focus or click.

**Animations** have the ability to be more complicated, can be defined more precisely, and are more flexible. They're also more code. 

## CSS Transitions

Let's start with transitions - you'll see that those are pretty simple to get started with.

Let's say, for example, when we hover over our form, it rights itself and moves a little bit:

![animated form](https://cloud.githubusercontent.com/assets/25366/9594904/8ba3527c-5016-11e5-94a5-f8affb95ffba.gif)

We can inspect our form to see how it's rotated and positioned at the beginning:

```css
form {
  /* ... */

  -ms-transform: rotate(-7deg); /* IE 9 */
  -webkit-transform: rotate(-7deg); /* Chrome, Safari, Opera */
  transform: rotate(-7deg);

  position: relative;
  left:-1rem;
  top: 0rem;
}
```

Then add a `:hover` effect that modifies those rotations and positions, something like:

```css
form:hover {
  top: -0.618rem;
  left: -0.382rem;
  -ms-transform: rotate(-2deg);
  -webkit-transform: rotate(-2deg);
  transform: rotate(-2deg);
}
```

Now the fun part:

```css
form {
  /* ... */
  transition: all 300ms ease-in-out;
}
```

The `all` means that all CSS properties will be affected by this transition. The `300ms` says the transition should last that long, in milliseconds, and the `ease-in-out` is one of a few choices that we have for _easing_. Easing makes the animation look more natural. You can list out individual properties with different transition effects like this:

```
div {
  transition: background 0.2s ease,
              padding 0.8s linear;
}
```

Note also that you can put the time in seconds.

  &#x1F535; **Activity**
```
* Add a transition on hover to your form! Be creative and make it do whatever you want
* 10 minutes

```


## CSS Animations

Now before we try it ourselves, let's see an animation. Animations are triggered, remember. By default, they are triggered when an object appears or when a class is applied to an object.

Before we can trigger a keyframe animation, we have to _define_  it with keyframes. Imagine a timeline where you're saying "At this spot, do this. At this next spot, change that. At this other spot, it should look like this."

We do that by creating a special `@keyframes` rule, and we name it whatever we like:

```css
@keyframes fadeIn {
  0% {
    opacity: 0;
  }
  80% {
    opacity: 0.5;
  }
  100% {
    opacity: 1;
  }
}
```

Of course, nearly any properties can be changed in each frame, and nearly any percentages can be included. You could have 100 keyframes if you want, or just two.

Once you have an animation defined, here's how you'd use it:

```css
ol li {
  animation-duration: 800ms;
  animation-name: fadeIn;
}
```

Just like a function, we reference the animation with the name we invented.

  &#x1F535; **Activity**
```
* add a submit button if you have not already
* Add an animation using keyframes when you hover on the submit button that changes both the opacity and color
* 10 minutes

```

## Further Reading

MDN has a number of exhaustive resources on HTML forms and inputs. It can be a lot to absorb, so look for patterns and try to grasp the big picture.

* [A downright beautiful reference for HTML5 forms](http://diveintohtml5.info/forms.html)
* [HTML Form Reference](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Forms) is a great resource and has been distilled below.
* [HTML Input Reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input)
* [Native Form Widgets](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Forms/The_native_form_widgets)
* [Form Validation](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Forms/Data_form_validation)
* [CSS Transitions](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Transitions/Using_CSS_transitions)
* [CSS Animations](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations/Using_CSS_animations)
* [Animate.css](https://daneden.github.io/animate.css/) - a Library of premade animations
