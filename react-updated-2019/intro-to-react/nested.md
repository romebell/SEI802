# Nested Components

### Learning Objectives

_After this lesson, you will be able to:_

* Diagram nested components
* Render components within another component
* Pass `props` to a nested component

![](https://res.cloudinary.com/briezh/image/upload/v1556226718/nested-components-we-need-to-go-deeper_pt62rf.jpg)

## `todo` We Do: Nested Components

Create a `Comment.js` file inside the `src` directory. Add the following code to it:

```jsx
import React from 'react';

function Comment(props) {
  return (
    <>
      <p>{props.body}</p>
    </>
  );
}

export default Comment;
```

Import `Comment` component into your `Dino.js` component like so:

```jsx
import React from 'react';
// import the comment component
import Comment from './Comment.js';

function Dino(props) {
  let allComments = props.comments.map((c, i)=>{
      return <Comment key={i} body={c}/>
  });

  return (
      <>
        <h1>Check out my {props.title} blog!</h1>
        <p>Written by {props.author}</p>
        <p>{props.body}</p>
        {allComments}
      </>
    );
}

export default Dino;
```

> Check it out!
