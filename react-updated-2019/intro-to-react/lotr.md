# Lab: Lord of the Rings

Let's build something small to reinforce what you've learned so far. We're going to practice creating components and passing information into them.

We'll build a simple website that shows title and runtime information about the original `Lord of the Rings Trilogy`.

![lotr image](https://image.cnbcfm.com/api/v1/image/106832365-1611930800281lord-of-the-rings-Cropped-jpg?v=1611930819&w=1600&h=900)

Specifically, at the end of this lesson, your solution will look like this: ![Lord of the Rings movie info](./lotr.png)

### Setup

Fork and clone this repo. 


```bash
$ cd lord-of-the-rings
$ npx create-react-app .
$ npm start
```

### Create A Simple Movie Component

Open up your `./src` directory in your favorite text editor.

Inside of `./src` folder, create a new React Component file called `Movie.js`.

**src/Movie.js**

or, we could write it as a functional component, like so:

```javascript
import React from 'react';

function Movie() {
   return (
     // code goes here!
   );
}

export default Movie;
```

Let's add some JSX to this component will be visible in our application. Let's keep the JSX simple for now, and we'll make it more complex once we're sure it works.

Remember, our goal is to display the movie title and runtime information.

Let's add one `<h1>` for the movie title, and a `<p>` for the runtime. Remember, the JSX of each component in React ultimately must descend from just one parent element. Wrap the `<h1>` and `<p>` in a `<div>`.

The JSX will look like this:

```jsx
<div>
  <h1>The Lord of the Rings: A Trilogy</h1>
  <p>4h 37min</p>
</div>
```

Add this JSX to the component so that it's returned.

**src/Movie.js**

```javascript
import React from 'react';

function Movie(props) {
   return (
      <div>
        <h1>The Lord of the Rings: A Trilogy</h1>
        <p>4h 37min</p>
      </div>
   );
}

export default Movie;
```

### Viewing the Component

Let's make this component appear on the page. One great thing about using `create-react-app` is it tells us exactly what we need to do to start editing our application. The homepage says, "To get started, edit `src/App.js` and save to reload." Let's do that!

Open `src/App.js`.

Add our `<Movie />` component inside of the `App` component. Go back to `Chrome browser` and see if it appears.

### Common Error

Uh oh. There's an error.

```zsh
Failed to compile
./src/App.js
  Line 15:  'Movie' is not defined  react/jsx-no-undef
```

`'Movie'` is not defined? Ah.

One does not simply refer to components in React. In our `src/App.js`, we're saying "Display what's returned from the `Movie` component." However - we haven't told `src/Apps.js` where to find the `Movie` component! We must import a component before using it.

Add this import statement with the other imports at the top of the `src/App.js` file.

```js
import Movie from './Movie';
```

Now you should see the page without the error message, and it should have the JSX from the Movie component.

The entire `App.js` should look like this:

**src/App.js**

```javascript
import React from 'react';
import './App.css';
import Movie from './Movie';

function App() {
  return (
    <div>
      <Movie />
    </div>
  );
}

export default App;
```

### Passing Information via Properties

We need to make our Movie component accept information so we can use it to display different titles and runtimes. In the `src/App.js` file, add `title`, `hours`, and `minutes` props to the `<Movie />` tag. We'll be able to read the value of these props from inside the component. You can name props pretty much anything you want - but it's good practice to be descriptive!

```javascript
<Movie 
  title="The Fellowship of the Ring" 
  hours="2" 
  minutes="58" 
/>
```

We'll be able to read the value of these `props` from inside the component. You can name props pretty much anything you want - but it's good practice to be descriptive!

React gathers all of the props we added to the call to `<Movie />` and makes them each available through the `props` object. This means that inside the `Movie` component, we can now access the values of props through `props.title`, `this.props.hours` and `props.minutes`. Remember, we use curly braces `{ }` to display the value of something.

In `src/Movie.js`, change the `<h1>` to display the value of the `title` prop by writing `{props.title}`.

There was also the `hours` and `minutes` props. Update the JSX to access and display the value of each prop we created.

The `render()` function ends up looking like this:

**src/Movie.js**

```javascript
import React from 'react';

function Movie(props) {
  return (
    <div>
      <h1>The Lord of the Rings: {props.title}</h1>
      <p>{rops.hours}h {props.minutes}mins</p>
    </div>
  );
}

export default Movie;
```

Refresh the page and make sure everything works correctly.

### Reusing the Component

Once you've got props working for one component, then write two more!

In `src/App.js`, call the `<Movie />` component again with different values for the `title`, `hours` and `minutes` properties. Display information for the complete trilogy! \(If you don't know everything about Lord of the Rings off the top of your head, here it is\).

```js
<Movie 
  title="The Fellowship of the Ring" 
  hours="2" 
  minutes="58"
/>

<Movie 
  title="The Two Towers" 
  hours="2" 
  minutes="59" 
/>
<Movie 
  title="The Return of the King" 
  hours="3" 
  minutes="21" 
/>
```

## Solution

When you're finished, review the reflections below.

### Reflecting on Reusability

Components are great because they allow us to compartmentalize code and easily reuse parts we create. We simply set the value of `props` and the component defines how everything should be displayed.

In this instance, we factored out some redundancy of the movie titles.

* All these movies start with `"Lord of the Rings:"`, so only the unique part is the prop.
* Similarly, we don't have to rewrite the format of the runtime information.

Building and reusing components becomes especially powerful the more complex components become.

* Imagine building a component for video search results inside YouTube.
  * The `props` object is huge:
    * ton of links
    * time information
    * preview images
    * options to add the result to a playlist
    * and all sorts of other things.

Building one component to rule all them all would save you a lot of time and headaches!

### Bonus: Check out these sites below and add a few more `props`.

In case you want to nerd out, here are handy links to the IMDB page for each movie:

* [Lord of the Rings: The Fellowship of the Ring](http://www.imdb.com/title/tt0120737/)
* [Lord of the Rings: The Two Towers](http://www.imdb.com/title/tt0167261/)
* [Lord of the Rings: The Return of the King](http://www.imdb.com/title/tt0167260/)

### Make an `array` of `objects` with all of `LOTR` movies and properties.

### Post `screenshot` in Slack

### Push to `Github`
