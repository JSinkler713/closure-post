---
title: closure
slug: closure
author: James Sinkler
meta: 'Quick example of using closure in a function to update a score in a game'
image: ./images/cat-in-box.jpg
---

![cat in box contained](./images/cat-in-box.jpg)

# Closure

Ok so what's with the cat in the box?

Well in my mind the cat represents the variables you get access to each time you use a function that was returned by another function. In general you are grabbing the box to use as a box. <em> But </em> you get access to a cat each time as well, even though it's not really a part of the box. Hopefully by the end of this that will make sense.

We will look at how this would work in a little function to update the score in a game.

You might think, ok, I could have a global variable called score, and then inside of it just update that score each time a player gets a point.

```javascript
let score = 0;

const playerScores = ()=> {
  score++
}
```

This would work fine, and I've definitely written functions that mutate something not directly defined inside of it. <em>Functional programming</em> people would take issue with this function on the following basis.

- It accesses variables defined outside it
- It returns a different value everytime you call it
- It updates a value and mutates it to be another value


