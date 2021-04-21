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
  return score
}
```

This would work fine, and I've definitely written functions that mutate something not directly defined inside of it. <em>Functional programming</em> people would take issue with this function on the following basis.

- It returns a different value everytime you call it
- It accesses variables defined outside it
- It updates a value and mutates it to be another value

![injected apple](./images/mutated-apple.jpg)

Coming from a math background, I can get behind the idea that a function, given an argument should always return the same result.
This function is literally always going to return a different result, so it's not very dependable. But with closures we are still going to end up being able to update it, it's a crafty way to have a functional function that returns different results.

Ok. Back to the cat in the box. <em>`score`</em> is the cat in this case. We want to make it a part of the function.

```javascript

const playerScores = ()=> {
  let score = 0;
  score++
  return score
}
```

How about this? Problem solved right?
- we call playerScores()
- score is initialized at 0
- score is updated by 1
- score returns 1
(The issue of course is when we call it again the same thing happens and it always returns 1)

I'm imagining maybe I have multiple levels to this game, and when we get to a new level, the score goes back to 0. So there is some value in that `let score = 0` declaration. But at the same time, it won't be a fun game if we can only get to score 1.

Enter the closure. If we go ahead and declare score like we did, but then <em>return</em> a new function that updates score we get access to it. Huh?

```javascript

const playerScores = ()=> {
  let score = 0;
  return updateScore() {
    score++
    return score
  }
}
```

Now when we call `playerScores()` we don't update the score, we get the inner function returned, but it has access to that `score` initialized in the parent. <em>It get's access to the cat in the box</em>.

```javascript
// save the reeturned function to a variable
const roundOnePlayerScores = playerScores()

// call that returned function
roundOnePlayerScores()

// call it again
roundOnePlayerScores()

// call it three times
let thirdReturn = roundOnePlayerScores()
console.log(thirdReturn) // what's the score?
```

It was the same cat in the box each time you called it. It was the same score that was originally initialized when we created `roundOnePlayerScores`. Our returned function had it in it's <em>closure</em>. It looks back at the function that defined it, and when it is asked to update score, `score++`, it says hmm there's no score defined in myself, was there one back in that box? Yes! So it goes ahead and updates the one defined above it in the parent scope.

What I find nice about this, is now if we want our player to go to level2 and restart the score, I can just call a new instance of playerScores.

```javacript
const roundTwoPlayerScores = playerScores()

roundTwoPlayerScores() // this will only update the new score that was just initialized

// so score = 1 in round two now,
// while score = 3 in round one still,
```

So when you call that parent function again for a new instance of the returned function. You get a new `score` initialized. It's like getting a whole new box, with a different kitten inside.

Hope you found that enjoyable, maybe you will find a usecase for this somewhere soon.
Happy Coding,

James

