---
title: Week 4 Blog
published_at: 2024-04-08
snippet: This blog is about Week 4 Homework.
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

At first, I was a little infamiliar with Canvas API, so I need some time to read through the resources and watch the tutorials from Coding Train about recursion. ![W4_homework](w04/tutorial.png) 

The vector way of creating a fractal tree in the Examples was a bit confusing for me, therefore, I tried to recreate it in a simplier approach which I learnt from this tutorial. ![W4_homework](w04/tut2.png) 

First, I followed the tutorial to understand what recursion is and the approach to draw a fractal. 
<p float="center">
  <img src="/w04/one_side.png" width="45%" />
  <img src="/w04/two_side.png" width="45%" /> 
</p>

I made one side of the fractal tree first then duplicated and changed the rotation value to create the other side of the tree. In the tutorial, I learnt the *save* and *restore* function, which are similiar to the *push* and *pop* function in p5, to wrap the format only for one block. 




