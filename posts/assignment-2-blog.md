---
title: Assignment 2 Blog 
published_at: 2024-05-05
snippet: This blog is about Assignment 2 working process.
disable_html_sanitization: true
---

# Concepts

## The Chaotic aesthetic

Through the reading about Sianne Ngai’s Zany, Cute, Interesting by Wark, the Chaotic aestheitc in my opinion, is a performative aesthetic that is anxious and excessive. It involves excessive and sharp implements, an unpredictable imitation - a repetitive flick between the familiar and unfamiliar, continuity and break, *as if trying to copy what someone else does but doing it clumsily* (Wark 2020). 

There's is a sense of instability and unpredictability inside of Chaotic. It works against constraints, trying to break out of their given form. It is a feeling of *flailing helplessness* and frenzy. If the Cute is intimate, domestic, the Chaotic is to be held at a distance. 

I think overall, the Chaotic brings in the randomness (unpredictability), which could enhances the non-redundancy aspect of effective complexity. However, too much chaos tends to disrupt the experience. The key things for Chaotic to increase effective complexity is using their repetitive nature to create a pattern to which the viewer could predict the upcoming elements yet adding a controlled amount of variations for anticipation.

## Inspiration

### Desmond Paul Henry 

For this project, I choose to respond to the works of Desmond Paul Henry.
<p float="center">
  <img src="/w08/desmond1.png" width="45%" height="70px"/>
  <img src="/w08/desmond2.png" width="45%" height="70px"/>
</p>

*[Desmond Paul Henry 1962 (4th set)](https://desmondhenry.com/gallery/)*

I was inpsired by the trails of lines and shapes movements in these works. It was not neccessary too excessive or involves sharps elements, however, in my opinion, these works also belong to the Chaotic aesthetic for the unpredictability of movements. They works through the constraintment of shapes, yet maintaining a pattern (with colors, strokes, etc.) which speaks as an effective complexity.

### Internet pop-up ad

For the visual of this project, I took inspiration from these kind of pop-up art from the 'old' internet.
<p float="center">
  <img src="/w08/ad1.png" width="45%" height="70px"/>
  <img src="/w08/ad2.png" width="45%" height="70px"/>
</p>

These kind of pop-up ad continously appears whenever we mistakenly click on strange website tends to be very frustrating trying to turn them off, however couldn't in a short period of time. I think this coud be use a sharp element for the Chaotic experience. Also, the use of vibrant mixture of colours in these ads could contribute to the Chaotic aesthetic. 

In both the works of Desmond Paul Henry and these ads, there is a similarity with the trails of objects, which I found very interested visually and conceptually (in terms of the Chaotic aesthetic). With Desmond's works, the trails is visually pleasing while the ads is quite upsetting because of their overwhelming presence. Therefore, I want to apply these kind of trails into my work, with the movements of the trails visually pleasing while overwhelm the viewer with their repetitiveness.

## Ideation

*For the Chaotic aesthetic:*

The idea of bombard the viewer with overload of information could be a sharp element for the Chaotic aesthetic and experience. Therefore with this, my concept for the Chaotic aesthetic is using the repetitive overload of demanding, aggressive word 'click' to overwhelm the viewer, while the 'click' action (mouse click) acts as a way to clear the screen.

The appearance of the word trails 'cilck' could be sharp with vibrant colours, while the word appear when click on the canvas could be softer with a neutral colours and a soft tune (audio) accompany. I think this creates a tension between these two elements, which correlate to the working against contraints aspect of the Chaotic experience that I have mentioned above. 

*For the Effective Complexity:*

- Non-redundancy: 
    - The random colours and letters appear in the word trails 
    - The random period of time between each music notes, which later on interact with the second letter traisl (when mouse click)

- Non-randomness: The underlying regurlarity of the same letters within the canvas and same music notes. Also, the colours change in each letter of a trail overall, create a pattern.

# Design Journey

I was inspired by this Floating Typography sketch from Patt Vira to understand the way how I should start my work. ![ams2_process](w08/Typtut.png) 
*[Interactive Floating Typography by Patt Vira](https://www.youtube.com/watch?v=-6v_AYyn49k&t=7s)*

First, I create a class to draw a letter trail root that grows at random speed and direction. At first I put the class in seperate file, however, I think as I was using a lot of 'ctx' variable, the class in seperate file could not get the canvas context. I tried to change the order of the code and adding 'import' and 'export', it still didn't work. 
<p float="center">
  <img src="/w08/class_prob1.png" width="30%"/>
  <img src="/w08/class_prob2.png" width="30%"/>
  <img src="/w08/class_prob4.png" width="30%"/>
</p>

As I put the class back in the original file, it did work well. 
<p float="center">
  <img src="/w08/class_sol1.png" width="45%"/>
  <img src="/w08/class_sol2.png" width="45%"/>
</p>

Then to draw the growing animation from the root of the trail, I created some variables to move their positions based on their size (bigger as they move) until they reach a certain maximum size. At first it did not create a smooth trail as I thought, because the code only executed once. So to draw the segment continously until it reach the maximum size, I added the requestAnimationFrame.
<p float="center">
  <img src="/w08/without_request.png" width="30%"/>
  <img src="/w08/with_request1.png" width="30%"/>
  <img src="/w08/with_request2.png" width="30%"/>
</p>

At first, I tested to see if the trail work by using simple square trail, then I changed it with the letter trails. I researched for some tutorial on adding typography to web API on [Tutorials Point website](https://www.tutorialspoint.com/How-to-set-the-font-family-for-text-with-JavaScript) and [MDN web docs](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/font).
<p float="center">
  <img src="/w08/typotut_1.png" width="45%"/>
  <img src="/w08/typotut_2.png" width="45%"/>
</p>

I also asked Gemini (Google AI) for some suggestion of some typography properties in Javascript. I gave me some more idea about displaying random letter from an array.
<p float="center">
  <img src="/w08/typo_sol1.png" width="45%"/>
  <img src="/w08/typo_sol2.png" width="45%"/>
</p>
<p float="center">
  <img src="/w08/typo_sol3.png" width="45%"/>
  <img src="/w08/typo_sol4.png" width="45%"/>
</p>

The interaction of viewer to the website was added using the 'mouse' function of Javascript. I found out more about this function and how it works through [MDN Web Doc](https://developer.mozilla.org/en-US/docs/Web/API/Element/mousemove_event). I used the 'mousemove' function for the first letter trails, which contains the word 'click'. The 'mouseup' and 'mousedown' function was used for the second trails and the music note since the audio context need a pause elements. 
<p float="center">
  <img src="/w08/mouse_tut.png" width="45%"/>
  <img src="/w08/mouse_function.png" width="45%"/>
</p>

After creating the first growing animation for the letter trails, I decided to test out different values (like shadow, color choice, blend mode, etc.) to the sketch.

*The sketch without the angle variations:*
<p float="center">
  <img src="/w08/withoutangle_1.png" width="45%"/>
  <img src="/w08/withoutangle_2.png" width="45%"/>
</p>

*With angle variations within the trails:*
<p float="center">
  <img src="/w08/withangle_1.png" width="45%"/>
  <img src="/w08/withangle_2.png" width="45%"/>
</p>

*Different colors, shadow and blend mode (globalCompositeOperation) values:*
<p float="center">
  <img src="/w08/var1.png" width="45%"/>
  <img src="/w08/var2.png" width="45%"/>
</p>
<p float="center">
  <img src="/w08/var3.png" width="45%"/>
  <img src="/w08/var4.png" width="45%"/>
</p>
<p float="center">
  <img src="/w08/var5.png" width="90%"/>
</p>

For the second letter trails animation (sprout animation), after some test, I decided to try using a recursion function. First it turn out to be static and quite predictable, which is a round curve. 
<p float="center">
  <img src="/w08/recursive1.png" width="45%"/>
  <img src="/w08/recursive2.png" width="45%"/>
</p>

I was inspried by [this Transient Synths code in the lecture blog](https://blog.science.family/240320_web_audio_api_synths), which I think also fit with my 'trails' concept. I thought of how to incorporate sound and create the interaction between sound and visual, so I decided to add the Transient Synths to my sketch while changing some value to match the visual.

Before incorporate the audio synthesis into the sketch, first I put the code in separate file to see if it works on a whole canvas inner width and height, which came a promblem that all the notes came in together with first click. However, after adding the mouse up and down events, and put the 'running' state to the right events, the code works normally. ![ams2_process](w08/audiotrial.png)

I combined the code to my sketch. In the audio code, when the cursor move on canvas there is different period of time between each note, therefore, I thought of making the second letter trails appear base on the period value. For that to work, I put the  period value in the argument of the sprout function, then using the recursive function to call itself again according to period of times between each note. 

*The sprout function call itself again after a period of time between each note using the setTimeOut function:* 
<p float="center">
  <img src="/w08/recursive3.png" width="45%"/>
  <img src="/w08/recursive4.png" width="45%"/>
</p>

The color of the shadow is the same with the background to giving the illusion of ‘erasing’ the screen with the white words. 
<p float="center">
  <img src="/w08/shadow.png" width="90%"/>
</p>

*Final visual of the sketch when move the cursor over the canvas and after click on the canvas*
<p float="center">
  <img src="/w08/move.png" width="45%"/>
  <img src="/w08/click.png" width="45%"/>
</p>

['Click' Final Sketch](https://chaotic-project.deno.dev/)

<p>
<br>
<p>





















