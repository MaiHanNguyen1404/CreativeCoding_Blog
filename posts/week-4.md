---
title: Week 4 Blog
published_at: 2024-04-08
snippet: Week 4 Homework - Creates fractal using recursion
disable_html_sanitization: true
---

# Homework

## Fractal

Fractal Tree link: https://week4-fractal.deno.dev/

``` javascript

document.body.style.margin   = 0
document.body.style.overflow = `hidden`

const cnv = document.getElementById (`fractal`)
cnv.width = innerWidth
cnv.height = innerHeight
document.body.appendChild (cnv)

const ctx = cnv.getContext (`2d`)

// set the fill to blue
ctx.fillStyle = `blue`
// fill the background
ctx.fillRect (0, 0, cnv.width, cnv.height)

// set the stroke color
ctx.strokeStyle = `yellow`
ctx.lineWidth = 10

// set the origin of the branch
ctx.translate (cnv.width/2, cnv.height)


function drawBranch (length) {
   // draw the base
   ctx.beginPath ()
   ctx.moveTo (0, 0) 
   ctx.lineTo (0, -length)
   ctx.stroke ()

   ctx.translate (0, -length)

   // stop the excuting the recursion if the branch length is less than 10
   if (length > 10) {
    // draw right branch
    ctx.save () 
    ctx.rotate (0.5)
    drawBranch (length * 0.75)
    ctx.restore () //return previous setting

    // draw left branch
    ctx.save ()
    ctx.rotate (-0.5)
    drawBranch (length * 0.75)
    ctx.restore () //return previous setting
   } 

}

drawBranch (200)

```

At first, I was a little unfamiliar with Canvas API, so I needed some time to read through the resources and watch the tutorials from Coding Train about recursion. ![W4_homework](w04/tutorial.png) [The coding train: Recursion](https://thecodingtrain.com/tracks/algorithmic-botany)

The vector way of creating a fractal tree in the Examples was a bit confusing for me, therefore, I tried to recreate it in a simpler approach which I learned from this tutorial. ![W4_homework](w04/tut2.png)[Franks Laboratory: Fractals](https://www.youtube.com/watch?v=dQKYao-daYw)

First, I followed the tutorial to understand what recursion is and the approach to drawing a fractal. 
<p float="center">
  <img src="/w04/one_side.png" width="45%" />
  <img src="/w04/two_side.png" width="45%" /> 
</p>

I made one side of the fractal tree first then duplicated and changed the rotation value to create the other side of the tree. In the tutorial, I learned the *save* and *restore* functions, which are similar to the *push* and *pop* functions in p5, to wrap the format only for one block. Also, I used *return* to stop executing the code if the generation is larger than the maximum number that was defined before.

Then after understanding the code better, I changed the argument inside the function to *length* (no need to define the maximum level). However, there was a problem when drawing two sides of the tree. The left and right branches of the tree all draw into one line.
<p float="center">
  <img src="/w04/onesideprob.png" width="45%" />
  <img src="/w04/onesideprob2.png" width="45%" /> 
</p>

I need to return the origin of the line to the previous place before drawing the other side of the branches. For that, I used the *save* and *restore* functions to return the previous setting.
<p float="center">
  <img src="/w04/two_side2.png" width="45%" />
  <img src="/w04/result.png" width="45%" /> 
</p>

*Can this method be used to maximize chaos?  How might you use it in your AT2?*

In my opinion, while recursion itself doesn't directly create chaos (since it creates repeated patterns), it can be a tool to explore chaotic systems with randomness. By introducing tiny variations to the initial values within the recursive calls, it could generate unpredictable patterns. For example, using random values within calculations at each level of recursion.

However, excessive randomness can quickly lead to unrecognizable patterns, which I think may disrupt the chaotic experience and effective complexity. The key is to make controlled variations that enhance the complexity of the pattern (or fractal) while maintaining its overall structure.
<p>
<br>
<p>
