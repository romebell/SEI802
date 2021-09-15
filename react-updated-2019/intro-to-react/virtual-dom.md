# Virtual DOM

## Learning Objectives

_After this lesson, you will be able to:_

* Describe the Virtual DOM versus the standard DOM
* Understand how components are called

## Review `src/index.js`

> Keeping components separate and organized is a best practice, so we created the Hello component in its own file.

To show up on the page, though, that component still needs to actually be called from somewhere. The main "HUB" 🛖 of our React app is `src/index.js`. We'll investigate how `src/index.js` is currently loading and rendering the `App` component. Look at your `src/index.js` file, and contrast it with the code below.

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App.js';

ReactDOM.render(
  <App />,
  document.getElementById('root')
)
```


> The `App` component is being imported in from `src/App.js` Remember, the `default` part of `export default App` in `src/App.js` means that importing other names - like `App` - actually _already_ brings in the `App` component! As a best practice, though, we're going to leave this file alone. We will import `Hello` inside of the `App` along with other components, such as `Dog` and `Human`. Pretty cool!!

The last difference is that `ReactDOM.render( <App />,`.

> This changes the `ReactDOM.render()` call to explicitly say "Render whatever the component `App` returns."

## Let's Hack away!

### Code along: Calling our `Hello` component explicitly

Update your `index.js` file to have the three changes listed above:

* Delete the CSS import.
* Change the `App` component name that's imported to be your `Hello` component.
* Change the component name that's used inside `ReactDOM.render` to be your `Hello` component.

> Check it out! You should be able to browse to [http://localhost:3000](http://localhost:3000) and see that nothing has changed.

## Virtual DOM Intro

You should be familiar with the DOM. You may have noticed that our `src/index.js` code mentions `ReactDOM`. `ReactDOM` doesn't refer to the same DOM we know. Instead, it refers to a **Virtual DOM**. The Virtual DOM is a key piece of how React works.

So, how is different? Watch [this video](https://generalassembly.wistia.com/medias/v5qyqsir0s) to find out. _\(note: right click for new tab!\)_

In React, the virtual DOM is a staging area for changes that will eventually be implemented.

![Virtual DOM Diagram](https://docs.google.com/drawings/d/11ugBTwDkqn6p2n5Fkps1p3Elp8ZToIRzXzvM4LJMYaU/pub?w=543&h=229)

You know every component has, at a minimum, a `return` statement. The `return` generates a `Virtual DOM` `node` to be added to the actual DOM.

The contents of this `node` are what we define in the `return` statement, using JSX.

The `ReactDOM.render()` function takes two arguments:

```javascript
ReactDOM.render(
  <Hello />,
  document.getElementById('root')
)
```

* `<Hello />` uses **the name of the component to render**. In our `Hello.js` file, the `Hello` component returns the content to render:  a `div` with "Hello World!" and heading tags \(written in JSX\). As a reminder, this is the `Hello` component:

```javascript
import React from 'react';
import Hello from './Hello';

function App() {
  return (
    <div>
        <Hello />
    </div>
  );
}

export default Hello;
```

* The second argument of the `ReactDOM.render()` function is `document.getElementById('root')`; this finds **the DOM `element` to append that content to**. This argument can be any element on the page. Here, we're simply appending it to an element with the id `root`.  \(Look through the `index.html` file if you're curious about the HTML structure from `create-react-app`.\)

When our `index.js` is processed, React compares the `Virtual DOM` to the regular DOM and only updates the `root` element on the page. Dope!

> Side note: What is `<Hello />` written in? JSX! Whenever you use a self-closing tag in JSX, you **MUST** end it with a `/`, like `<Hello />` in the above example. If you don't use a self-closing tag, JSX will look for a closing tag and never find it!

* Let's switch it back to `<App />`!

> If you're you have 35 mins of nothing to do on the weekend, check out this video with history on the Virtual to learn more, [check this video out](https://www.youtube.com/watch?v=-DX3vJiqxm4). _\(note: right click for new tab!\)_