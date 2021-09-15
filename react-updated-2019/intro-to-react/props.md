# Props

### Learning Objectives

_After this lesson, you will be able to:_

* Describe props
* Create a component that renders props

## Component Data with Props

The React framework was built to handle data that changes over time.

So far, we have defined a `Hello` component inside `App.js`. The component's returns a `div` with a `<h1>` heading, written in JSX.

In `index.js`, we are importing the `App`component and all of the `contents` inside ( i.e. `<Hello />`). We are appending the `App` component to the virtual DOM, and rendering that in the `root` node. Cool!

This is great, but it doesn't involve any data yet, let alone data that changes over time! Let's make it more interesting.

Rather than simply display "Hello world", let's display a `greeting` to the user. We'll make the `greeting` change dynamically based on the user's name.

The question is, how do we add a name to our `Hello` component without hardcoding it into the component's `return` statement?

Find out! Try it yourself alongside [this video](https://generalassembly.wistia.com/medias/gchiu63slo) in [this codepen](https://codepen.io/susir/pen/vxWypq) _\(note: right click both for new tab!\)_

### `todo` You Do `hello-world` Exercise

#### Code along: Adding props to our component

Let's use **`props`** to make our "Hello World" app more flexible.

**First, a single `PROP`**

We want to make a `greeting` that's reusable for many different users, so we'll have a `name` prop for the name of the user.

In your `src/App.js`, we'll change the line that renders the `Hello` component to include this `name` prop. The new line will be:

`<Hello name={"Jay"} />`

> We pass in data wherever we are rendering our component. In rendering the `Hello` component above, we pass in a prop called "name" with a value of "Jay".

Your `App.js` should now look like this:

```javascript
import React from 'react';
import Hello from './Hello.js';

function App() {
  return (
    <div >
      <Hello name={"Jay"} />
    </div>
  );
}

export default App;
```

Now, every time we render our component, we will pass in data.

* When the `Hello` component renders, we pass the `Hello` component a `prop` called `name` with a value of `Jay`.

If you check your application now, look at the `React Developer Tools` nothing has changed. We're passing the `name` prop into the component, but the component isn't _using_ it yet.

In our `Hello` component definition, we will add `props` as a argument to our `Hello function (props){}`. Next, change the `<h1>Hello World!</h1>` to `<h1>Hello {props.name}!</h1>`. The portion `{props.name}` deserves a closer look:

* `props` is an `OBJECT` that will collect all the props that were passed down to it from the parent component `App`
* `props.name` pulls out the name property from `props` and returns value `Jay`.

> The `{}` syntax in JSX renders the result of any expression inside it. It works even without props. If you wrote `{2+2}` in your JSX, `4` would be rendered.

In `App.js`, your `Hello` class should now look like this:

```jsx
function Hello(props) {
  return (
    <div>
        <h1>Hello {props.name}!</h1>
        <h3>It is time for tea.</h3>
    </div>
  );
}
```

In the above example, we replaced "world" with `{props.name}` = `Jay`.

> Check it out! You should be able to browse to [http://localhost:3000](http://localhost:3000) to view this change!

## What about... multiple props?

Of course, we often want components to display more complex information. To do so, we can pass multiple properties to our component! We'll use the same two steps we took to add the first prop.

First, add another prop to the component call: `<Hello name={"Jay"} />,` changes to `<Hello name={"Jay"} age={24} />`.

Update your `App.js` file to reflect this:

```javascript
import React from 'react';
import Hello from './Hello.js';

function App() {
  return (
    <div >
      <Hello name={"Jay"} age={24} />
    </div>
  );
}

export default App;
```

Now, in our component definition we have access to both values. The second step is to change the `Hello` component class in `App.js` to use the age information!

```javascript
function Hello(props) {
  return (
    <div>
        <h1>Hello {props.name}!</h1>
        <p>You are {props.age} years old.</p>
        <h3>It is time for tea.</h3>
    </div>
  );
}
```

> Check it out! You should be able to browse to [http://localhost:3000](http://localhost:3000) to view this change!

## What about... multiple props passed from an object?

If we have many props, it might get difficult to keep track when we're passing everything. A better practice is to organize values in some kind of `object` and then pass `props` to the component from that object. Let's see this strategy.

Currently, in `App.js`, we put Jay's `name` and `age` directly into the `Hello` component. Instead, we'll create an object that holds Jay's `name` and `age`, making it clearer for other developers and easier to change in the future. In your `App.js file`, below the `import` statements, add this object definition:

```javascript
let person = {
  name: "Jay",
  age: 24
}
```

Next, we'll update what's passed into the `Hello` component:

```javascript
function App() {
  let person = {
    name: "Jay",
    age: 24
  }

  return (
    <div >
      <Hello name={person.name} age={person.age} 
      />
    </div>
  );
}

export default App;
```

We don't have to change anything in `Hello.js`, because it's still receiving exactly the same values for exactly the same two props - `name` and `age`. We're just sending it those values in a slightly different way.

> Check it out! If you browse to [http://localhost:3000](http://localhost:3000) nothing should have changed.
>
> Try changing the values inside the `person` object. See how the page updates.

#### Multiple props from a more complex object

Since we're just pulling props out of an object, we can use any object we want. For example, we can nest an array inside it.

Let's say our user has some favorite animals. Update your object to include an array:

```javascript
let person = {
  name: "Jay",
  age: 24,
  favorites: ["Dogs", "Tigers", "Lions"]
}
```

Now we can use this new information as a prop, just like normal. You could choose to pass a single element \(`favorites[0]`\) or the entire array. We'll use the entire array so that the component can display _all_ a person's favorite animals. First, update your `ReactDOM.render()` call in `index.js`:

```javascript
function App() {
  let person = {
    name: "Jay",
    age: 24,
    favorites: ["Dogs", "Tigers", "Lions"]
  }
  
  return (
    <div >
      <Hello
        name={person.personName}
        age={person.personAge}
        animals={person.favorites}
      />
    </div>
  );
}

```

If you check your application now, nothing has changed. Remember, a component class will just ignore any props it receives that it doesn't use. But, we want to use the `favorites`! Therfore, next, update your `Hello` component `return` statement

```jsx
<div>
  <h1>Hello {this.props.name}!</h1>
  <p>You are {this.props.age} years old.</p>
  <p>You love: {this.props.animals}</p>
</div>
```

If you check the page now, you'll see React prints the entire array, as that's what was passed in. If we wanted to include all the animals clearly, we could fix the spacing. Instead, to review some syntax, let's just modify the code to render the last animal.

```jsx
<div>
  <h1>Hello {this.props.name}!</h1>
  <p>You are {this.props.age} years old.</p>
  <p>You love: {this.props.animals[2]}</p>
</div>
```

If you want to learn more.

[_Read more about using props in JSX, if you'd like!_](https://facebook.github.io/react/docs/jsx-in-depth.html) _This link is also in the Further Reading page at the end of the React module, under the Facebook documentation._

