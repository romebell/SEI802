# Lifting State

## ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Unidirectional Data Flow

#### Learning Objectives

_After this lesson, you will be able to:_

* Define unidirectional flow
* Diagram data in a component hierarchy

### What is Unidirectional Data Flow?

Let's start with [a video explaining this concept.](https://generalassembly.wistia.com/medias/v2uenqkgwk).

In React applications, data usually flows from the top down. Why do we care? How does this apply?

When several components in a view need to share `state`, you lift, or **hoist**, the `state` so that it's available to all the components that need it. Define the state in the highest component you can, so that you can pass it to any components which will need it. Let's look at a search filter as an example. This app will have two basic components - one that displays a list of data, and one that captures user input to filter the data.

### We do: Build a Fruit Filter 🫐

Our data will be simple - a list of fruits. The app will end up looking something like this:

![Fruit filter app](../../.gitbook/assets/filter-example%20%281%29.png)

When building a React app, it's important to take time to define the app's structure before you start writing code. We're going to define the **components** and the **state** we need before we write the code.

#### Components

This app needs two components:

* A `List` component to display the list of fruit. 
     * This component needs one piece of data: the array of fruits to display.
* An `Input` to capture the filter value from the user.
     * This component needs one piece of data: the current value of the filter.

#### State

This app needs to keep track of changes in two items:

* The filtered list of fruits 
* The value of the filter

#### Component hierarchy

We have two sibling components \(components at the same level of the tree/app\) that need to be aware of each other's data. Specifically, the `List` component needs to only show the fruits that match the filter value. So we need to get data from one sibling to another. Something like this:

![basic data flow needed](../../.gitbook/assets/fruit-filter-data.png)

How to achieve this, though? Using unidrectional data flow, of course! If we create a container component to hold both the filter value and the filtered list, we can hoist the `state` to the container so it's available to all the children. It will then be simple to display the `state` in the child components. The data will flow like this:

![unidirectional approach](../../.gitbook/assets/fruit-list-unidirectional.png)

Now that we know the components we need, the `state` we need, and where everything needs to be, we can start writing some code.

## Child Components

`List.js`
```jsx
import React from 'react';

const List = props => {

  return(
    <ul>
    {/* list will go here */}
    </ul>
  )
}

export default List;
```

`Input.js`
```jsx
import React from 'react';

const Input = props => {

  return(
    <div>
        <label htmlFor="fruit-filter">Filter these Fruits: </label>
        <input type="text" name="fruit-filter" />
    </div>
  )
}

export default Input
```

### Container Component

Our container will be a component with a few functions we'll use to initialize and update the state of the two child components. Using hooks, we'll initialize the state:

```jsx
import React, {useState} from 'react';

const FruitContainer = props => {
  const [fruitsToDisplay, setFruitsToDisplay] = useState(props.fruits);
  const [filterValue, setFilterValue] = useState('');

  return(
    //...
  )
}

export default FruitContainer;
```

We've set up state to accept a list of fruits as props from a parent component, so let's go into `App.js` and make sure everything's set up the way we need it there.

```jsx
import './App.css';
import FruitContainer from './FruitContainer'

function App() {
  const fruitArr = ['Apple', 'Banana', 'Grapes', 'Kiwi', 'Pineapple', 'Dragonfruit', 'Mango']
  return (
    <div className="App">
      <FruitContainer fruits={fruitArr} />
    </div>
  );
}

export default App;
```

We'll need a function to update the `state` when the filter value changes. This function will store the filter `state`, and filter the list of fruits to display. We'll pass this change handler to the input component to react to user behavior.

```jsx
 const handleFilterChange = e => {
    e.preventDefault();

    const newValue = e.target.value;
    setFilterValue(newValue);

    // remove fruits that don't contain the filter value
    const filteredFruitList = props.fruits.filter(fruit => {
      return fruit.toLowerCase().includes(newValue.toLowerCase());
    })
    
    setFruitsToDisplay(filteredFruitList);
  }
```

And finally, we need to render our child components.

```jsx
return (
    <div>
      <Input value={filterValue} onChange={handleFilterChange} />
      <List fruits={fruitsToDisplay} />
    </div>
  )
```

The full container component looks like this:

```jsx
import React, {useState} from 'react';
import Input from './Input';
import List from './List';

const FruitContainer = props => {
  // Initialize the fruit list to the array passed in props
  const [fruitsToDisplay, setFruitsToDisplay] = useState(props.fruits); 
  // Initialize the filter value to an empty string
  const [filterValue, setFilterValue] = useState('');

  const handleFilterChange = e => {
    e.preventDefault();

    const newValue = e.target.value;
    setFilterValue(newValue);

    // remove fruits that don't contain the filter value
    const filteredFruitList = props.fruits.filter(fruit => {
      return fruit.toLowerCase().includes(newValue.toLowerCase());
    })
    
    setFruitsToDisplay(filteredFruitList);
  }

  return (
    <div>
      <Input value={filterValue} onChange={handleFilterChange} />
      <List fruits={fruitsToDisplay} />
    </div>
  )
}

export default FruitContainer;
```

All of the data is hoisted to the top of the tree in the container, and we pass it to the child components.

Now we need to return to the children components and add the functionality to handle the data they're receiving!

## Finished Child components:

`Input.js`
```jsx
import React from 'react';

const Input = props => {

  return (
    <div>
      <label htmlFor="fruit-filter">Filter these Fruits: </label>
      <input type="text" name="fruit-filter" value={props.value} onChange={props.onChange} />
    </div>
  )
}

export default Input;
```

`List.js`
```jsx
import React from 'react';

const List = props => {
  const fruitItems = props.fruits.map((fruit, idx) => {
    return <li key={idx}>{fruit}</li>
  })

  return (
    <ul>
      {fruitItems}
    </ul>
  )
}

export default List;
```

## You do: Also display the fruits that do _not_ match the filter

* Add another child component to the

  `FruitContainer` that displays the fruits that do _not_ match the filter value

  \(this should be all the items that are not in the `fruitsToDisplay` list\).

_Hint: Will you need to have a new state?_

### Solution - Unmatching Filter

Coming Soon!

### Final Thoughts

It's important that you think through your applications before you start writing code. It's often helpful to sketch out your app, and identify:

* the **components** you will need
* the **states** you will need
* where those states need to live

Use the unidirectional data flow pattern - hoist your state toward the top of the component tree so it's available to the children that need it.
