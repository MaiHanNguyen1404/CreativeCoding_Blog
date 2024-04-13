---
title: Week 5 Blog
published_at: 2024-04-16
snippet: This blog is about Week 5 Homework.
disable_html_sanitization: true
---

# Homework

## 1. Add explanatory comments

### Glitch

``` javascript
<canvas id="glitch_self_portrait"></canvas>

<script type="module">

   const cnv = document.getElementById (`glitch_self_portrait`)
   cnv.width = cnv.parentNode.scrollWidth
   cnv.height = cnv.width * 9 / 16 // 16:9 aspect ratio
   cnv.style.backgroundColor = `deeppink` // Sets the background color of the canvas to deeppink.


   const ctx = cnv.getContext (`2d`)

   let img_data

    // Define a draw function with unknown image value i
    // function draw (i) {
    // ctx.drawImage (i, 0, 0, cnv.width, cnv.height)
    // }
   const draw = i => ctx.drawImage (i, 0, 0, cnv.width, cnv.height) //(image, dx, dy, dWidth, dHeight)

   // Create a new image 
   const img = new Image () 

   // Define the function to run new image once the image successfully loads its resource
   img.onload = () => {
      cnv.height = cnv.width * (img.height / img.width) // Adjusts the canvas height based on the image's aspect ratio
      draw (img) // Call the draw function with the new image as the argument - draw the image to the canvas
      img_data = cnv.toDataURL ("image/jpeg") // Set the image data to jpeg
      add_glitch () // Call the add_glitch function
   }
   img.src = `/240405/pfp_glasses.jpg` // The image source

   // Define a function to generate random integer (not fractional number) within the maximum number
   const rand_int = max => Math.floor (Math.random () * max)

   // Define a glitch function 
   const glitchify = (data, chunk_max, repeats) => {
      const chunk_size = rand_int (chunk_max / 4) * 4 // 
      const i = rand_int (data.length - 24 - chunk_size) + 24
      const front = data.slice (0, i)
      const back = data.slice (i + chunk_size, data.length)
      const result = front + back
      return repeats == 0 ? result : glitchify (result, chunk_max, repeats - 1)
   }

   const glitch_arr = []

   const add_glitch = () => {
      const i = new Image ()
      i.onload = () => {
         glitch_arr.push (i)
         if (glitch_arr.length < 12) add_glitch ()
         else draw_frame ()
      }
      i.src = glitchify (img_data, 96, 6)
   }

   let is_glitching = false
   let glitch_i = 0

   const draw_frame = () => {
      if (is_glitching) draw (glitch_arr[glitch_i])
      else draw (img)

      const prob = is_glitching ? 0.05 : 0.02
      if (Math.random () < prob) {
         glitch_i = rand_int (glitch_arr.length)
         is_glitching = !is_glitching
      }

      requestAnimationFrame (draw_frame)
   }

</script>

```

