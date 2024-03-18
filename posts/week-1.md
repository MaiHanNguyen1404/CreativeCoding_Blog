---
title: Week 1 Blog
published_at: 2024-03-10
snippet: This is an excerpt of my first blog post.
disable_html_sanitization: true
---

# Homework

## Grid

<iframe id="homework_grid" src="https://editor.p5js.org/MaiHanNguyen1404/full/zTj7GkpDo"></iframe>

<script type="module">
  const iframe = document.getElementById (`homework_grid`)
  iframe.width  = iframe.parentNode.scrollWidth
  iframe.height = iframe.parentNode.scrollWidth + 42
</script>

First I tried to duplicate the previous code to see what would happen. The result sort of replicated a grid, however, I did not entirely understand the whole process. ![gird_process](w01s01/1.png) 

My second attempt at making a grid was trying to duplicate the line syntax. The process was easier to understand, however too long and not sufficient. Looking back at the provided code (the code during the lecture), I noticed that there were a lot of conditionals and variables being used, which made the process more efficient and ‘clean’. Therefore, I started to look up some resources to understand better the variables and conditionals syntax. ![grid_process](w01s01/2.png)

When I tried the ‘for’ condition, it kept showing an error like this. I spent quite some time here to figure out what was wrong, which turned out was because I put a colon instead of a semi-colon in the ‘for’ code. ![grid_process](w01s01/error.png)

I tried to make a row of squares first then duplicate the code for the next lines. Then combine them all into 1 condition. After that, I also tried to change the number of rows and columns in the grid. However, it was a bit ‘handy’ having to change each number, imagine working on a much bigger sketch. So I applied the nested loop to make it shorter and easier to understand.
<p float="center">
  <img src="/w01s01/duplicate.png" width="32%" />
  <img src="/w01s01/nested_loops.png" width="32%" /> 
  <img src="/w01s01/naming.png" width="32%" />
</p>

## Rafaél Rozendaal's Only Suddenly

<iframe id="homework_onlysuddenly" src="https://editor.p5js.org/MaiHanNguyen1404/full/5E5Na7L8g"></iframe>

<script type="module">
  const iframe = document.getElementById (`homework_onlysuddenly`)
  iframe.width  = iframe.parentNode.scrollWidth
  iframe.height = iframe.parentNode.scrollWidth + 42
</script>

For Rafael’s Only Suddenly piece, there was a use of both Variables and Conditionals (if). First, I searched for some tutorials about the basics of ‘bounce’ (touch the corner and return) and noticed that they are using the If condition. 
![onlysuddenly_process](w01s01/tutorial.png)

I followed the tutorial to create a basic animation of a circle moving randomly and when it hits the edge of the screen it bounces back. However, the circle only bounced back when the center of the circle touched the screen which is different from Rafael’s piece. 
![onlysuddenly_process](w01s01/bounce_canvas_half.png)

To make the circle bounce immediately when the stroke of the circle touches the edges of the canvas, I tried to add some math equations in the if condition. 
![onlysuddenly_process](w01s01/bounce_canvas_corner.png)

From the basic understanding of the circle bouncing, I then start to create a bouncing circle in a rectangle like in Only Suddenly. Some more rectangle variables were added. 
![onlysuddenly_process](w01s01/bounce_rectangle.png)

However, the difficult aspect of this piece for me was how to change the color of each object when the circle touched the edge of the rectangle. I tried to make the color change by adding the code to the if conditions, however, the color only changed when the moment the circle touched the edge. I also tried the 'else' condition but it only changed the color the moment and the circle touched the edge. 
<p float="left">
  <img src="/w01s01/change_color.png" width="45%" height=150px />
  <img src="/w01s01/opposite.png" width="45%" height=50px /> 
</p>


_underline_

**bold**



