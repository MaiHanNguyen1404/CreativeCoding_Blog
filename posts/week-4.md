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
