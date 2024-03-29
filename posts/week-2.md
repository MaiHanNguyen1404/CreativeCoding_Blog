---
title: Week 2 Blog
published_at: 2024-03-18
snippet: This blog is about Week 2 Homework.
disable_html_sanitization: true
---

# Homework

## Refactor 

For this Refactor exercise, first I watched some tutorials to understand better how Class works. I mostly watched The Coding Train tutorials and practiced alongside the video. 
<p float="center">
  <img src="/w02/tut1.png" width="45%" />
  <img src="/w02/tut2.png" width="45%%" /> 
</p>

After some practice, I tried to apply it to the given sketch. However, I was lost at first because I didn’t understand what needed to be put in the class (which properties belong to the Faller Class). ![refactor_process](w02/error_1.png)

I was struggling to refactor this given sketch and it kept showing errors. I thought the background color value also belonged to the Faller class, so when I add it to the constructor, it keeps showing that 'rand_col' is not defined (I now realize that it should be defined in the setup function). ![refactor_process](w02/color_error.png)

The next error was it could not access 'faller' before initialization. I think it's because I put the conditional If in the constructor and because I did not define a function after closing the constructor. ![refactor_process](w02/wrong_class.png)

In addition to the error, I put in the function that does not belong to the 'faller', therefore, it always shows that rand_col is not defined. ![refactor_process](w02/function_error.png)

I had many trials and failures after that, it was not until the next class session that I could finally understand what to put in the Faller class. After that, I also recreated the exercise on my own, and then added some code comments. (sketch)

## Rafael Rozendaal's not never no

In Rafael Ronzendaal's work Not never no, the circles are filled with moving gradients and the circles also slightly move their position. So firstly, I create a gradient by drawing a series of concentric circles. I used the Iteration (For loop) to create multiple smaller circles within the previous circle, then using rotation the hue value. ![notneverno_process](w02/gradient1.png) 

As I wanted to create multiple circles using the properties, I made the draw gradient a function and called that function in the draw function. However, the circle suddenly turned into a square, and when I deactivated the 'moving' code, it seemed normal again. I think the problem is with the 'moving' animation. (move_error1) (functionerror) (move)
<p float="center">
  <img src="/w02/move_error1.png" width="30%" />
  <img src="/w02/functionerror.png" width="30%%" /> 
  <img src="/w02/move.png" width="30%%" /> 
</p>

To draw many circles on the canvas, I used the Nested Loop to draw the grid first. ![notneverno_process](w02/multiple_circle.png) 

I wanted to draw the circle in random places, however, it did not turn out as expected for it not move individually but as a block. ![notneverno_process](w02/random_error.png)

Although it wasn't what I had anticipated, it was still really interesting because they moved randomly in a set rather than in the whole grid. ![notneverno_process](w02/move_error.png) 


