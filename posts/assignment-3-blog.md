---
title: Assignment 3 Blog 
published_at: 2024-06-15
snippet: This blog is about Assignment 3 working process.
disable_html_sanitization: true
---

# Concept

## The Interesting aesthetic

Through the reading about *Sianne Ngai’s Zany, Cute, Interesting* by Wark and *Our aesthetic categories* by Sianne Ngai, the Interesting aesthetic, in my opinion, is the combination of interest and boredom. It involves using boredom to exhibit moments of slowness, and stillness to open up a time for the audience to think and feel while anticipating the slight interesting elements.  

The Interesting aesthetic is also about the circulation of information, a serial, recursive aesthetic of informational relays and communicative exchange. It is *the low affect that accompanies the perception of minor differences against a backdrop of the generic, in the case of the interesting* (Ngai 2012). 

I think, to achieve the Interesting aesthetic, is to exhibit boredom through the circulation of information while also introducing a slight bit of interesting elements to both create a moment of slowness and anticipation.

## Ideation

My 6-year-old cousin, who is the core group I focus on as the domain for the Community of Practice, primarily learn about music through passive methods like Youtube songs and shows. While this offers some good content, it lacks interaction for kids and therefore, reduces engagement and their learning efficiency. 

As discussed in the video, my project aims to address this by creating an interactive website. This website will teach musical notes in an engaging way through activities that incorporate body movement.

### Inspirations 

Before starting to work on the project, I did some research on some ways for kids to learn about musical notes through Youtube shows. In these shows (the links below), they often use vibrant colors and interesting graphics (cartoon, animation) to illustrate the notes.

<p float="center">
  <img src="/w12/ref.png" width="45%" height="70px"/>
  <img src="/w12/ref1.png" width="45%" height="70px"/>
</p>

[Musical Notation - Music for kids](https://www.youtube.com/watch?v=JryT5ywzrsk&t=84s) and
[Learn Music w/ Mr. Rob](https://www.youtube.com/watch?v=qb1n7BDsNo4&t=506s)

I was particularly interested in these contents (Sound of Music and Sweet Beet Pilot). Instead of just reciting the notes, they assign a word to each note to create a memory aid. With that inspiration, I also include the emoji of animals that correspond to the start of each note, for example, Do for Dolphin, etc.

<p float="center">
  <img src="/w12/soundofmusic.png" width="45%" height="70px"/>
  <img src="/w12/beet.png" width="45%" height="70px"/>
</p>

["Do-Re-Mi" - THE SOUND OF MUSIC (1965)](https://www.youtube.com/watch?v=drnBMAEA3AM) and 
[Sweet Beets Pilot | Music Lessons For Kids](https://www.youtube.com/watch?v=VTmk_ADNOgg&t=56s)

## Project Description

*Note Drops*

The website is a game to make the note drop down to the bottom of the screen using interaction with the webcam, to hear the corresponding musical notes. The reflection of the player (my cousins) on the screen will be black and white and the player will try to make white space for the note to drop. 

The screen will act as an invisible virtual piano where the player can also press down their cursor to hear the corresponding note along with its name displayed.

# Design Journey

I was inspired by *[this Text Rain (Drawing w Webcam) sketch](https://www.youtube.com/watch?v=1GfKfjgf4cQ&t=460s)* from Patt Vira to understand the way how I should start my work. 
<p float="center">
  <img src="/w12/camera_tut.png" width="90%" height="70px"/>
</p> 

With that tutorial, I started with setting up the camera and using the threshold value to calculate the position of the notes on the screen (white space means move down, black space means re-calculate and move up to the highest threhold value).
<p float="center">
  <img src="/w12/cam1.png" width="30%" height="70px"/>
  <img src="/w12/cam2.png" width="30%" height="70px"/>
  <img src="/w12/threshold.png" width="30%" height="70px"/>
</p> 

At first, I created random shapes in p5 as the falling down elements, however, I figured that it was not straightforward enough for kids to imagine it as a virtual piano. Therefore, I made the notes graphic first in Illustrator then exported it as png, and used the preloads function to display the notes in p5. 
<p float="center">
  <img src="/w12/preload.png" width="45%" height="70px"/>
  <img src="/w12/notedesign.png" width="45%" height="70px"/>
</p> 

Then I create a Note class to display 8 notes with the same properties. However, to display different note images, I have to specify the note in the array, and for me, the most effective way is to create a function to choose the note based on the choice parameter. 
<p float="center">
  <img src="/w12/class1.png" width="45%" height="70px"/>
  <img src="/w12/class2.png" width="45%" height="70px"/>
</p>
<p float="center">
  <img src="/w12/randomnote1.png" width="45%" height="70px"/>
  <img src="/w12/randomnote2.png" width="45%" height="70px"/>
</p> 

To create the sound of the notes, I started to look for references on how to use the oscillator and sound library in p5. 
<p float="center">
  <img src="/w12/soundtut1.png" width="45%" height="70px"/>
  <img src="/w12/soundtut2.png" width="45%" height="70px"/>
</p> 

[The Coding Train Sound in p5](https://www.youtube.com/watch?v=Pn1g1wjxl_0&t=4s) and
[Piano in p5](https://www.youtube.com/watch?v=ShCNc8t9kYs&t=538s)

From these tutorials, I used the oscillator and sound library in p5 to create a function to execute the MIDI notes, then called that in 'touch' function to play the sound when the notes fall down and also when the mouse is pressed. I also mapped the sound based on the note's position in the order of piano keys.
<p float="center">
  <img src="/w12/playnotefunction.png" width="45%" height="70px"/>
  <img src="/w12/touchfunction.png" width="45%" height="70px"/>
</p> 

A problem with sound that I encountered when running the code in full screen was that the audio was not allowed to play because there wasn't a control to initiate or pause the sound. From [this tutorial of The Coding Train](https://www.youtube.com/watch?v=YcezEwOXun4&t=228s), I added a play and pause button at the bottom of the canvas.
<p float="center">
  <img src="/w12/buttontut.png" width="30%" height="70px"/>
  <img src="/w12/button1.png" width="30%" height="70px"/>
  <img src="/w12/button2.png" width="30%" height="70px"/>
</p> 

There are also texts that appear when the note is played. The corresponding name of each note based on its position is displayed when the mouse is pressed. Also, as I have mentioned in the Inspirations above, the emoji of an animal that corresponds to the start of each note, for example, Do for Dolphin, is displayed when the note touches the bottom of the screen.
<p float="center">
  <img src="/w12/notename1.png" width="45%" height="70px"/>
  <img src="/w12/notename2.png" width="45%" height="70px"/>
</p> 

However, the mouse pressed function did not work on touchscreen devices. It was quite a shame because my cousins are more familiar with the Ipad than the computer browser. 
<p float="center">
  <img src="/w12/touchprob.png" width="90%" height="70px"/>
</p> 

*Final visual of the website when the notes drop and when the mouse is pressed*
<p float="center">
  <img src="/w12/look1.png" width="45%" height="70px"/>
  <img src="/w12/look2.png" width="45%" height="70px"/>
</p> 

[Notes Drop Website](https://editor.p5js.org/MaiHanNguyen1404/full/vGpnVPKAu)

<p>
<br>
<p>











