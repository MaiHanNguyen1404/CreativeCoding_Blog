---
title: Assignment 1 Blog
published_at: 2024-03-30
snippet: This blog is about Assignment 1 working process.
disable_html_sanitization: true
---

# Concepts

## Research and Definition

### The Cute aesthetic
From this week's reading about Sianne Ngai’s Zany, Cute, Interesting, and some more articles, the definition of ‘cute’ aesthetic, in my opinion, is the desire to become intimate through the act of vulnerability. The cute evokes feeling through its vulnerable, diminutive form and tempting for special care. Its powerlessness can be extremely seductive (Wark 2020). The cute production could be seen as capitalism itself, an obvious example is the Kawaii culture of cuteness in Japan's post-war period through the mass production of toys, manga, and ephemera. 
<p float="center">
  <img src="/w03/kawaii1.png" width="45%" />
  <img src="/w03/kawaii2.png" width="45%%" /> 
</p>

There’s more to cuteness than tempting us for special care. The ‘cute creature can be considered our own gaze’, it’s also our own fantasy to become the ‘cute’, keeping us craving for more. It's giving us the visual language to express our desire through the act of dissolving the distinction between fantasy and reality. The artwork by Julien Ceccaldi from the Cute exhibition below conveys the idea that we are viewing the character through the door gap in the same way that they do, blurring the boundaries between the real and the imaginary. 
<p float="center">
  <img src="/w03/artwork.png" width="90%" />
</p>
*Cute (2024) Julien Ceccaldi, “Door to Cockaigne” (2022)*

Reading articles: [From emojis to coquettes and Hello Kitty, cute’s transformative potential is shaping how we see ourselves both on and off-screen](https://www.dazeddigital.com/life-culture/article/61895/1/how-cuteness-took-over-the-world-somerset-house-hello-kitty)

### Effective Complexity

The Effective Complexity in my opinion is the underlying regularity within a system. It highlights the importance of focusing on the underlying structure rather than just the total amount of data. On top of the underlying regularity, there is a slight sense of randomness in to create the ‘complexity’. However, defining what's "random" and what's a regularity can be subjective. This can lead to variations in how effective complexity is calculated depending on the observer.

In Rafael Rozendaal’s work, there’s always a repeated pattern, a ‘rule’ of how the object interacts within the screen (eg. in *falling falling*, the walls fall repeatedly after one another), however with a few unexpected elements to add in the ‘complexity’ (eg. the random color appears). 

Within the ‘cute’ aesthetic, effective complexity acts as an engagement, an element for the viewer to crave more. If the purpose of the cute is to create a fantasy or a reflection of our gaze, then the effective complexity is to ‘loop’ the fantasy while adding some unexpected elements.

## Ideation

### Rafael Rozendaal's slick quick
For this assignment, I choose to respond to the work *slick quick* of Rafael Rozendaal. 
<p float="center">
  <img src="/w03/slickquick1.png" width="45%" height="70px"/>
  <img src="/w03/slickquick2.png" width="45%" height="70px"/>
</p>

I think this work belongs to the aesthetic of 'cute' in the appearance and the movement of the object. The object appears as a small circle and moves within the screen borders, creating visually pleasing color trails, which could speak as the temptation to maintain in a frame.

For its effective complexity, *slick quick* maintains a 'rule', a regularity, which is the object bouncing across the screen, however with the random color change whenever we press the mouse. 

### My respond
In *slick quick*, I was interested in the constraintment of the circle bouncing and would like to retain that aspect. I think it speaks of a human desire to break out of the 'frame' and escape reality, which is one of the purposes of the cute aesthetic that I have mentioned above. 

However, I want to answer this *slick quick* piece with a *yes however*, yes it will be a constraint in a frame, however, there is an attempt to break free, but whether or not they successfully escape is depend on the interpretation of the viewer.

For the Cute aspect: I also want to retain the small appearance, while somewhat making it appear fragile and vulnerable. The powerlessness could shown through having an object actually constrained in a box, however, by the appearance of the trails of the box and multiplication of the objects, it will look like the object could escape.

For the Effective Complexity: 
- The underlying regularity: the objects bounce within the box and change the background whenever they touch the edges.
- Slight randomness:
    - Only when the object touches the 1 dimension of the box (not always change when touched), which could take a little time to realize
    - Objects could be multiplied and move in different directions, sometimes they will cross the same path


# Design Journey

I started looking up 3D in p5 since I wanted to have the image of a box. In addition to that, I also learned about orbit control, which allows you to drag and move around the world, along with camera settings. This control, in my opinion, creates interactivity and engagement. 
<p float="center">
  <img src="/w03/orbit_control1.png" width="45%" height="30px"/>
  <img src="/w03/orbit_control2.png" width="45%"/>
</p>

First, I created a box and a ball (sphere) in the center of the world (vector (0,0,0)) ![ams1_process](w03/create_box_sphere.png)

Then, animated the ball to bounce around the box using the same logic as the code from my first week's homework (recreating Rafael Rozendaal's work's Only Suddenly), only now I have to consider the vector of the ball in 3D. Since it used different dimensions, it took me some experiments to get the correct boundaries of the box.
<p float="center">
  <img src="/w03/ball_bounceout1.png" width="32%"/>
  <img src="/w03/ball_bounceout2.png" width="32%"/>
  <img src="/w03/ball_bounceout3.png" width="32%"/>
</p>

To tidy the code, I turned the boundaries value into a variable. 
<p float="center">
  <img src="/w03/offset.png" width="45%"/>
  <img src="/w03/ball_bounce.png" width="45%"/>
</p>

To create more balls later on, I moved the ball to a Class. I forgot to change the name of the sphere and used it to name a function, which resulted in an error. ![ams1_process](w03/naming_error.png)

After changing the name, the code worked normally.
<p float="center">
  <img src="/w03/class_inside1.png" width="45%"/>
  <img src="/w03/class_inside2.png" width="45%"/>
</p>
<p float="center">
  <img src="/w03/class_outside1.png" width="45%"/>
  <img src="/w03/class_outside2.png" width="45%"/>
</p>

To create more balls using interactivity, I researched tutorials about Array along with Push and Pop. 
<p float="center">
  <img src="/w03/array_tut.png" width="45%"/>
  <img src="/w03/push_pop.png" width="45%"/>
</p>

I followed the tutorial to use Array and Push it to create more balls when pressing the mouse. It worked in creating new balls when the mouse was pressed. ![ams1_process](w03/array_firstdraft.png)

However, the ball did not start where the mouse clicked but was in the same position as the first ball which is the vector (0,0,0). As it was a vector in the class, I couldn’t figure out how to bring it into the parameter value. I tried to put in the x and y value in the constructor parameter but the result is still the same.  
<p float="center">
  <img src="/w03/vector_prob1.png" width="32%"/>
  <img src="/w03/vector_prob2.png" width="32%"/>
  <img src="/w03/vector_prob3.png" width="32%"/>
</p>

However, when I just put the radius value in the parameter, the starting position of the new ball is different from the first one. ![ams1_process](w03/vector_value.png) 

Working next on the color of each object. As I was experimenting with different color values, I found out that removing the background from the draw function creates as trail (as it doesn’t redraw the background), which is quite interesting in 3D dimension since it could be controlled by the viewer. ![ams1_process](w03/color1.png)

Then I think of changing the color trail of the box and of course, redrawing the background after some time. So first for the color trail of the box, I used the random color inside of Stroke. ![ams1_process](w03/box_stroke.png)

Before thinking about redrawing the background, I already thought of doing something for when the ball touches the box edges for slight randomness for effective complexity elements. So then, I combined both ideas to make the background change (redraw the background) whenever the ball touched the box edges. 

I defined a background color function and then called it in the Conditional (if). The function was called only in the Condition when the ball touched the x position of the box, to not overwhelm the viewer with too much changing. ![ams1_process](w03/function_bg.png)

With the array, the ball does not appear with the box when starting the sketch, therefore, it might be confusing for the viewer and also the background doesn’t redraw which might lead to crashing later on. ![ams1_process](w03/initial_ball1.png)

So I tried to create the ball with the box first then later, more balls could be added by pressing the mouse. ![ams1_process](w03/initial_ball2.png)

Through the multiplication of the ball later on, it appears as though they could "break out" of the box, however, the initial ball was unable to do so, which indicates the desire to break free yet can not quite achieve that. 
<p float="center">
  <img src="/w03/look1.png" width="47%"/>
  <img src="/w03/look2.png" width="47%"/>
</p>
*Final visual of the sketch starting view and zooming in view* 

