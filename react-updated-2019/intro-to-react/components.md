# Components and JSX

## ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Components and JSX

### Learning Objectives

_After this lesson, you will be able to:_

* Identify and define React components
* Describe why we use components in React
* Build a React component
* Describe JSX

## Components

The basic unit you'll be working with in ReactJS is a **component**. Components are pieces of our application that we can define once and reuse all over the place.

For an intro to components, watch [this video](https://generalassembly.wistia.com/medias/h64z7lp1ir) \(note: right click to open in a new tab!\).

If you're used to writing out all of a page's view in a single HTML file, using components is a very different way of approaching web development.

With components, there is more integration and less separation of HTML, CSS, and JavaScript.

* Instead of creating a few large files, you will organize your web app into small, reusable components that encompass their own content, presentation, and behavior.

When using React, building components will be your main front-end task.

* Because they're so encapsulated, components make it easy to reuse your code, test, and separate concerns.

### Identifying Components

Take a look at [Tesla.com](https://www.tesla.com/home) \(note: right click to open in a new tab!\). We want to browse the page. Guess what, Tesla built their website using `React`. Let me prove it to you. Open a new tab. We are going to download the `React Developer Tools` from Google Extensions. Let's do that now. [Click here](chrome://extensions/). 
* Type in React Developer Tools in the search bar. 
* Install the extension ( may need to restart Google Chrome )
* Go back to [Tesla.com](https://www.tesla.com/home) and inspect the page
* Look for a tab inside of the Chrome Dev Tools called `Components`

You should be able to see a `component` and it's `properties`

Let us look at one more, [CraigsList](https://losangeles.craigslist.org/d/apartments-housing-for-rent/search/apa) \(note: right click to open in a new tab!\).

![Components](https://res.cloudinary.com/briezh/image/upload/v1556229627/craigslist_example_ruvqji.png)

ach listing is a component. How can you identify this?

* Listings look identical in structure, but have different information populating them
* Listings are dynamically generated based on the user's search

Now take a look at the listing page. Scrolling down it, identify the visual "components" the website is comprised of. We suggest drawing this out on paper! So something like this...

![Component diagram](https://res.cloudinary.com/briezh/image/upload/v1556229627/wireframe_deconstructed_fwf6dn.png)

As you're drawing this out, think about the following questions...

* Where do you see "nested components;" that is, where are there components inside another component? Where do you see just one "layer" instead?
* Are there any components that share the same structure?
* For components that share the same structure, what is different about them?

### So -

What does a simple component look like? Let's start with a simple "Hello World" example...

#### Code along: A Very Basic Component

In this section, we'll walk through:

* Removing the pre-filled contents of your `hello-world` app.
  * `create-react-app` filled your app with sample content - let's make room for your app!
* Adding your own component definition.
  * You want the app to display the words "Hello World!"
* Going through what we've done in detail!

To start, remove the contents inside of the `App` component located in `src/App.js` file.

Next, let's create a file called `src/Hello.js` 

Write the code below inside of `Hello.js`

```javascript
// import React
import React from 'react';

function Hello() {
  return <h1>Hello World!</h1>
}

export default Hello;
```

Let's break down the things we see here...

**`import React from 'react'`**

We first start off by import `React`

**`function Hello() {}`**

This is the component we're creating. In this example, we are creating a `functional` component and calling it "Hello."


**`return()`**

Every component has, at minimum, returns some `JSX` ( HTML "like" syntax). The `returns` is what renders the `component` to the screen, so it controls what is displayed for this component. From this function, we return what we want to display.

* In our case, we are rendering a "Hello World!" heading: `<h1>Hello World!</h1>`.

> Note! That heading tag above looks like it's straight out of HTML, but it's actually a special language called JSX, which you'll see on the next page. For now, know that JSX will act like HTML when it's rendered to the screen.

**`export default Hello`**

**This exposes the `Hello` class to other files**. This means that other files can `import` from the `Hello.js` file in order to use the `Hello` component. In our case, we'll be importing it into `App.js` by calling an `import` to `Hello.js`.

When we try to import something from `Hello.js`, JavaScript will attempt to match a named export.

* Our only named export in `Hello.js` is `Hello`.

The `default` keyword means that if we try to import anything from this file that the app can't find, JavaScript will automatically revert to importing `Hello` instead.

* Only one default export is allowed per file.

### Check it out!

Start your server ( `npm start` ). Now switch to your browser and navigate to [http://localhost:3000](http://localhost:3000), you can see your "Hello World!" heading. This app dynamically reloads each time you save, so you can check your changes at any point.

### Wait - What's that HTML doing in my Javascript?

This is currently the contents of our `src/App.js` file:

```javascript
// import React, Hello component
import React from 'react';
import Hello from './Hello';

// define our Hello component

function App() {
  // what should the component render?
  // Whatever is returning from the Hello component.
  return (
      // make sure to return some UI
    <div>
        <Hello />
    </div>
  );
}

export default Hello;
```

Let's add a little styling inside `index.css`

```css
html, body
  height: 100%;
  
body
  background: #333;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: Helvetica Neue;
  
h1
  font-size: 2em;
  color: #eee;
  display: inline-block;

a
  color: white;
p
  margin-top: 1em;
  text-align: center;
  color: #eee;
```

Let's talk about the value that the render method returns. It looks an awful lot like an HTML heading, but it's not. We often write out React components in **JSX**.

So, JSX allows us to write code that strongly resembles HTML. It is eventually compiled to lightweight JavaScript objects.

Your `Hello` component returns:

* Currently returns JSX, not HTML.
* The JSX creates a heading with `'Hello World!'`.
* Your component reads this and renders a "Hello World!" heading.

React can be written without `JSX`. We won't be doing this. 👎🏽
```js
import React from 'react';
import ReactDOM from 'react-dom';

var ui =
      React.createElement('div', {}, 
        React.createElement('h1', {}, "Hello World!")
      )

ReactDOM.render(ui, document.getElementById('root'))
```

Another example using React written without JSX.
```js
var ui =
      React.createElement('div', {}, 
        React.createElement('h1', {}, "Contacts"),
        React.createElement('ul', {},
          React.createElement('li', {},
            React.createElement('h2', {}, "James Nelson"),
            React.createElement('a', {href: 'mailto:james@jamesknelson.com'}, 'james@jamesknelson.com')
          ),
          React.createElement('li', {},
            React.createElement('h2', {}, "Joe Citizen"),
            React.createElement('a', {href: 'mailto:joe@example.com'}, 'joe@example.com')
          )
        )
      )

    ReactDOM.render(ui, document.getElementById('react-app'))
```

### Challenge: Greet the day!

* Change your `App` component to display the `Hello` component multiple lines.
* Add a line inside of your `App.js` below the last "Hello World!" heading that will display `"It is time for tea."` in an `h3`.

> IMPORTANT: Remember, you can only return one DOM element. You can, however, place multiple elements within a parent `div` element. or a single fragment `<>`\*

## `todo` We Do: Create a `Dog` component

## `todo` You Do: Create a `Human` component

## `todo` You Do: Add some styling to the `Dog` component ( create `Dog.css` )