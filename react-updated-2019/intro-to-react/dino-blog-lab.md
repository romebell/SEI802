# Dino Blog Activity

## ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Lab: Dino Blog

### Part 1 
Let's have some practice creating a React component from scratch. How about a blog post?

1. Change directories to `labs` where you're going to create the next project
2. Create a repo called `dino-blog` ( make it public ). Add a `README.md`.
3. Clone down your `dino-blog` repo. 
4. `cd` into `dino-blog` and add react

```zsh
$ npx create-react-app .
```

If you need to refresh your memory, refer below or view the official [`create-react-app` Github repository](https://github.com/facebookincubator/create-react-app).
<p align='center'>
<img src='https://cdn.jsdelivr.net/gh/facebook/create-react-app@27b42ac7efa018f2541153ab30d63180f5fa39e0/screencast.svg' width='600' alt='npm start'>
</p>

   > Note: If you are running something else on port 3000 - like a Node app or another React app, you may get prompted to use 3001 or specify a new port. You can do this or you can kill the process that's already running.

### Part 2 
3. Create a `dino` object in `src/App.js` that has the following properties:
   * `title`  \(example value: `"Dinosaurs are awesome"`\)
   * `author` \(example value: `"Stealthy Stegosaurus"`\)
   * `body` \(example value: `"Check out this body property!"`\)
   * `comments` \(example value: `["First!", "Great post", "Hire this author now!"]`\)
4. Create a `Dino` component inside `src/Dino.js`
5. Render your `App` component with the information from your `Dino` component and pass in the `dino` object as props values to the `Dino` component. For now, only display one of the comments, `comments[0]`. You decide how you want to display the `title`, `author`, `body`, and `comment`, or 
Take a screenshot and post in `Slack`.
The `Solution` section below as inspiration.
6. Optional: adjust the CSS of your index file body to align your text to the center of the document.

## Solution

Here's what the solution might look like:

![Solution for Project](https://res.cloudinary.com/briezh/image/upload/v1556226300/props_solution_wawthy.png)

## Going forward

Hang onto this code - we'll make some improvements to it so we can see all of the comments!
