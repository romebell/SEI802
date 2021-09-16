# Code-Along: Mood Points

## ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) React State: Mood Points

## Learning Objectives

_By the end of this lesson, you will be able to:_

* Define what state means in relation to React components.
* Differentiate between `state` and `props`.
* Create an initial state in a component.
* Change the state of a component.

## Let's Talk About Props!

In React, we are able to handle data in one of two ways:

* Props **represent** data that is **immutable**, or read-only. Let's see what happens when you try to directly change `props.name` in the `Hello` component.
* But, what about when we need data that is dynamic and changes? That's where React's state comes in!

## So Many Questions!

* What is state anyway?
* What's the difference between state and props?
* How do we access state?

### States

* Values stored in a component's state are **mutable**, or changeable, attributes.
* State may appear similar to props, but there are quite a few important differences.
* Like props, which we access through the `props` object, we can access state using `state`.
* As state has the ability to be changed, it is not quite as straightforward as props. However, once you get the hang of it, you'll be able to build really interactive apps!

**Talking Points:**

* Let's use `hello-world` to create a new `MoodTracker` component. Our `MoodTracker` will display a mood, and eventually a user will click a button to indicate on a scale of 1–10 how strongly they are feeling that mood.
* In order to get started with our new `MoodTracker` component, let's first create a new file called `src/MoodTracker.js`.
* Run the command `touch src/MoodTracker.js`

## MoodTracker

```jsx
// ...
import MoodTracker from './MoodTracker';

function App() {
  return (
    <div className="App">
    ...
      <MoodTracker />
    </div>
  );
}

export default App;
```

**Directions:**

* After creating the file, let's make sure to import our new component into `App.js` and put the component in our `return` statement.

## Initial State

When working with values that are dynamic and changing, it's a good idea to provide an initial value for the changing pieces of data. In some older React code, you'll see class components setting initial state by creating a `constructor`. Newer class components can set state without the constructor, which you may also see in your own research. 

We're the developers of the future, though, so we'll be taking advantage of React hooks - specifically `useState`.

```jsx
import React, {useState} from 'react';

const MoodTracker = props => {
  const [state, setState] = useState(/* define initial state here */);

  return (
    //...
  )
}

export default MoodTracker;
```

Now that we've built the skeleton for our component, let's define our state's initial value. Because we're using hooks, we can set this to whatever we want, but for now we'll create an object with a single key-value pair. The key or label in the state object will be `moodPoints`, and the initial value will be `1`.

```jsx
const [state, setState] = useState({
  moodPoints: 1
})
```


**Next Steps**:

Next, let's make sure we display that information to the user. In your `MoodTracker.js` return statement, we'll let the user know how many mood points they have by adding in the line seen here.

```markup
<p>You are this happy: {state.moodPoints}</p>
```
Like so:
```js
return (
  <div>
    <p>On a scale of 1-10</p>
    <p>You are this happy: {state.moodPoints}</p>
  </div>
)
```

Note how similar this looks to using props. All React components include both `props` and `state`, whether or not we make use of them. All together, the code inside our `MoodTracker.js` function looks like this:

```javascript
const MoodTracker = props => {
  // Define an initial state
  const [state, setState] = useState({
    moodPoints: 0
  });

  // What should the component add to the page?
  return(
    <div>
      <p>On a scale of 1-10</p>
      <p>You are this happy: {state.moodPoints}</p>
    </div>
  );
}
```

**Tips:**

* Don't spend much time on the `constructor` syntax. It may help those who are familiar with other OOP patterns, but it is not commonly used now.
* As you code along, make sure students `import` and `export` properly. Move the new component to a `components` directory if it will help with your organization.
* Now that you have a value in your `state` object, this can be a good opportunity to show how React Developer Tools can update state to help with debugging.

## Changing State

#### Events in JavaScript

* Now that we have an initial value up on the page, let's learn how to change this value and make it more dynamic.
* Step 1 in this process is to trigger an **event** — when the user interacts with the page in any way.
* Think back to using regular JavaScript or jQuery. What is the purpose of an event listener? Can you show me how to create a click event in JavaScript?

**Tips:**

* If students do not have much experience with events, make sure to talk through the `event` keyword. A good way to explore the `event` keyword is to examine the object when adding this event listener to the DOM.

```javascript
  document.body.addEventListener('keypress', (e) => console.log(e))
```

* After running that code, type a letter into the DOM and you should see the `event` object. Explore this with students so that they can see things like `e.target.value` and `e.key`.


## Events in React

**Talking Points:**

* Event listeners in React look very similar to adding events through HTML attributes. There are two main differences when working with React's synthetic events:
* React events are named using camelCase instead of lowercase:
     * `onClick` \(React\) vs. `onclick` \(HTML\)
     * `onSubmit` \(React\) vs. `onsubmit` \(HTML\)
* In JSX, you pass the actual function in as the handler, rather than a string:
     * `<button onClick={this.doSomething}>Click Me</button>` \(React\)
     * `<button onclick="doSomething()">Click Me</button>` \(HTML\)

Additionally, there are _tons_ of events available to React elements.


## Turn and Talk: Synthetic Events

Check out the [React documentation](https://reactjs.org/docs/events.html#supported-events) on supported events.

Think about the following:

1. What events could you see yourself using often?
2. What sort of events sound niche but interesting to play around with?

**Note - Make sure to highlight the following commonly used events:**

* `onClick`
* `onChange`
* `onSubmit`
* `onKeyPress`
* `onMouseOver`

## Code-Along, Continued: Setting State

We will create a button that the user can click, which will increase their mood by `1`.

### Check Your Understanding

> If we were just working with regular old JavaScript, what could we use to increase the value of a variable by `1`?
>
> How would we add or remove an item from an array?
>
> How about changing the value of a key-value pair in an object?

## Increase Mood

Unfortunately, changing the value of `state` isn't quite as straightforward as something like `state.moodPoints++`. Instead, when we want to update a value in React using hooks, we will use the `setState` function that we destructured when setting up `useState`. This function helps React update only certain parts of the DOM, resulting in a much faster website!

First, we will create a function to increase the mood. Above the `return` statement, add the method seen here.

```javascript
const increaseMood = () => {
  setState({
    moodPoints: state.moodPoints + 1
  })
}
```

> ES6 update: We are going to be using arrow functions often in React. Check out [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) for more info.
>
> Note that we call `setState` to change the state.

## Finishing Increase Mood
Now, we'll create the button to trigger calling this function. The button will be displayed to the user, so we'll add it to the `return` statement. When the user clicks it, we'll call the `increaseMood()` function.

```javascript
  // Remember: This can only return one top-level element.
return(
  <div>
    <p>On a scale of 1-10</p>
    <p>You are this happy: {state.moodPoints}</p>
    <button onClick={increaseMood}>Cheer up!</button>
  </div>
);

```

Why did we write `onClick={increaseMood}` rather than `onClick={increaseMood()}`?

> More details on [function calls versus function references](https://stackoverflow.com/questions/15886272/what-is-the-difference-between-a-function-call-and-function-reference).

## Mood Tracker

All together, your `MoodTracker.js` file now looks like this:

```javascript
// Bring in React and useState (which we'll cover in more detail soon) from React.
import React, {useState} from 'react';

// Define our MoodTracker component
const MoodTracker = props => {
  // Set initial state as an object, with an attribute setting moodPoints to 0
  const [state, setState] = useState({
    moodPoints: 0
  });

  // Increase moodPoints by 1 in the state object
  const increaseMood = () => {
    setState({
      moodPoints: state.moodPoints + 1
    })
  }

  //Return some UI to actually appear on the page
  return(
    <div>
      <p>On a scale of 1-10</p>
      <p>You are this happy: {state.moodPoints}</p>
      <button onClick={increaseMood}>Cheer up!</button>
    </div>
  );
}

export default MoodTracker;
```

> Check it out! If you browse to `http://localhost:3000`, your button now changes the state whenever it is clicked.

## Using React, **We Only Change the Parts of the DOM That Need to Be Changed**

Whenever we run `setState`, our component calculates the difference, or "diff," between the current DOM and the virtual DOM node. Then, it figures out how to update the state of the DOM in as few manipulations as possible; it only replaces the current DOM with parts that have changed.

This is super important! Using React, **we only change parts of the DOM that need to be changed**. This has implications for performance.

We do not re-render the entire application like we have been doing so far. **This is one of React's core advantages.**

## Challenge: Count to 10

After 10 clicks, the user should see the counter reset to `0`.

```javascript
const increaseMood = () => {
    let newMoodPoints;
    if (state.moodPoints >= 10) { // Check to see if current state is greater than or equal to 10
      newMoodPoints = 0; // If true, set newMoodPoints variable to 0.
    } else {
      newMoodPoints = state.moodPoints +1; // If false, set newMoodPoints to current moodPoints plus 1
    }
    setState({
      moodPoints: newMoodPoints
    })
  }
```

## Challenge: Count to 10

Or, using ternaries:

```javascript
const increaseMood = () => {
  const newMoodPoints = state.moodPoints >= 10 ? 0 : state.moodPoints + 1;
  setState({
    moodPoints: newMoodPoints
  })
};
```

## Resources

* [React State vs. Props](http://lucybain.com/blog/2016/react-state-vs-pros/)
* [Understanding State in React](https://thinkster.io/tutorials/understanding-react-state)
* [Understanding `this.setState`](https://medium.com/@baphemot/understanding-reactjs-setstate-a4640451865b)
* [Understanding `setState`](https://css-tricks.com/understanding-react-setstate/)
* [React State FAQs](https://reactjs.org/docs/faq-state.html)
