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

   // Run new image once the image has successfully loaded its resource
   img.onload = () => {
      cnv.height = cnv.width * (img.height / img.width) // Adjusts the canvas height based on the image's aspect ratio
      draw (img) // Call the draw function with the new image as the argument - draw the image to the canvas
      img_data = cnv.toDataURL ("image/jpeg") // Set the canvas data into a image data 
      add_glitch () // Call the add_glitch function
   }
   img.src = `/240405/pfp_glasses.jpg` // The image source

   // Define a function to generate random integer (not fractional number) within the maximum range
   const rand_int = max => Math.floor (Math.random () * max)

   // Define a glitch function 
   const glitchify = (data, chunk_max, repeats) => {
      const chunk_size = rand_int (chunk_max / 4) * 4 // Picks a random chunk size (multiply by 4) within the maximum range (to glitch)
      const i = rand_int (data.length - 24 - chunk_size) + 24 // Select a random portion of image data excluding the first 24 bytes and the glitch chunk size
      const front = data.slice (0, i) // Remove the first part of the data to i
      const back = data.slice (i + chunk_size, data.length) // Remove ... to the end of the data
      const result = front + back // Combining the front and back portions of the selected data.
      return repeats == 0 ? result : glitchify (result, chunk_max, repeats - 1) // Call the function recursively, stops executing the function when the the repeats time reach 0
   }

   // Create an empty glitch array  
   const glitch_arr = []

   // Define a add_glitch function to create multiple glitched versions of the image using the glitchify function.
   const add_glitch = () => {
      const i = new Image () // Create new image objects for each glitched version.
      // Once a glitched image has successfully loaded
      i.onload = () => { 
         glitch_arr.push (i) // Push the glitched image object into the glitch array
         if (glitch_arr.length < 12) add_glitch () // Recursively call the add_glitch function if the glitch array length is less than 12 (12 glitched version is created)
         else draw_frame () // Call the draw_frame function if the glitch array length reaches 12 or more
      }
      i.src = glitchify (img_data, 96, 6) //
   }

   let is_glitching = false 
   let glitch_i = 0 

   const draw_frame = () => {
      if (is_glitching) draw (glitch_arr[glitch_i]) // Continue to draw the first item of the glitch array if draw_frame is false (add_glitch function still calls)
      else draw (img) // Otherwise draws the original image

      //Conditional probability: 
        //condition ? expression_if_true : expression_if_false
        // if (is_glitching) {
        //     prob = 0.05;
        // } else {
        //     prob = 0.02;
        // }
      // Probability if is_glitching is true: 0.05 (5%) - currently display the glitched image, Probability if is_glitching is false: 0.02 (2%) - currently display the original image
      const prob = is_glitching ? 0.05 : 0.02
      // If a random number between 0 to 1 (< 1) is less than the probability
      if (Math.random () < prob) {
         glitch_i = rand_int (glitch_arr.length) //
         is_glitching = !is_glitching //Switch between displaying the glitched image and the original image
      }

      requestAnimationFrame (draw_frame)
   }

</script>

```

