---
title: Week 5 Blog
published_at: 2024-04-16
snippet: Week 5 Homework - Add explanatory comments, Creates a glitch portrait
disable_html_sanitization: true
---

# Homework

## 1. Add explanatory comments

### Glitch

<canvas id="glitch_self_portrait"></canvas>

<script type="module">

   const cnv = document.getElementById (`glitch_self_portrait`)
   cnv.width = cnv.parentNode.scrollWidth
   cnv.height = cnv.width * 9 / 16
   cnv.style.backgroundColor = `deeppink`

   const ctx = cnv.getContext (`2d`)

   let img_data

   const draw = i => ctx.drawImage (i, 0, 0, cnv.width, cnv.height)

   const img = new Image ()
   img.onload = () => {
      cnv.height = cnv.width * (img.height / img.width)
      draw (img)
      img_data = cnv.toDataURL ("image/jpeg")
      add_glitch ()
   }
   img.src = `/w05/glitch.JPG`

   const rand_int = max => Math.floor (Math.random () * max)

   const glitchify = (data, chunk_max, repeats) => {
      const chunk_size = rand_int (chunk_max / 4) * 4
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

``` html
<canvas id="glitch_self_portrait"></canvas>

<script type="module">

   // Getting canvas elements
   const cnv = document.getElementById (`glitch_self_portrait`)

   // Setting canvas size
   cnv.width = cnv.parentNode.scrollWidth
   cnv.height = cnv.width * 9 / 16 // 16:9 aspect ratio

   // Sets the background color of the canvas to deeppink. 
   cnv.style.backgroundColor = `deeppink` 

   // Getting canvas context
   const ctx = cnv.getContext (`2d`)

   // Instatiating variable for the image data
   let img_data

    // Define a function to draw an image to the canvas 
    // with unknown image value i
    // function draw (i) {
    // ctx.drawImage (i, 0, 0, cnv.width, cnv.height)
    // }
   const draw = i => ctx.drawImage (i, 0, 0, cnv.width, cnv.height) 
   //(image, dx, dy, dWidth, dHeight)

   // Create a new image element 
   const img = new Image () 

   // Define a function to run new image once the image has loaded its data
   img.onload = () => {

      // Adjusts the canvas height 
      // based on the image's aspect ratio
      cnv.height = cnv.width * (img.height / img.width) 

      // Call the draw function with the new image as the argument 
      // draw the image to the canvas
      draw (img) 

      // Set the canvas data into a image data
      // Storing image data as string in img_data
      img_data = cnv.toDataURL ("image/jpeg") 

      // Call the add_glitch function 
      add_glitch () 
   }

   // The image source 
   // Happen first then the onload block execute
   img.src = `/w05/glitch.JPG` 

   // Define a function to generate random integer 
   // within the maximum range (0 to max, excluding max)
   const rand_int = max => Math.floor (Math.random () * max)

   // Define a recursive function 
   const glitchify = (data, chunk_max, repeats) => {

      // Picks a random chunk size 
      // multiple of 4 between 0 and chunk max
      const chunk_size = rand_int (chunk_max / 4) * 4 

      // Select random position in image data 
      // between 24 and chunk size 
      // (excluding the first 24 bytes and the glitch chunk size)
      const i = rand_int (data.length - 24 - chunk_size) + 24

      // Remove the first part of the data to i
      // Grabing all the data before random position
      const front = data.slice (0, i) 

      // Leaving the gap the size of chunk size
      // Grabing the rest of the data
      const back = data.slice (i + chunk_size, data.length) 

      // Combining the front and back portions of the selected data
      // leaving out the chunk size
      const result = front + back 

      // Call the function recursively with repeats - 1
      // stops executing the function when repeats reach 0
      // ? ternary operator
      return repeats == 0 ? result : glitchify (result, chunk_max, repeats - 1) 
   }

   // Create an empty glitch array for glitched images  
   const glitch_arr = []

   // Define function to add multiple glitched image 
   // to the glitch_arr array
   const add_glitch = () => {

      // Create new image objects for each glitched version.
      const i = new Image () 

      // Define function that executes when image receives its data
      i.onload = () => { 

         // Push the glitched image object into the glitch array
         glitch_arr.push (i)

         // Recursively call the add_glitch function 
         // until there are 12 glitched images
         if (glitch_arr.length < 12) add_glitch () 

         // Stop animating once there are 12 images
         else draw_frame () 
      }

      // Give the new image some glitchtified image data
      i.src = glitchify (img_data, 96, 6)
   }

   // Instatiate variable to keep track of glitch state
   let is_glitching = false 

   // Keep track of which glitched image from the array we are using
   let glitch_i = 0 

   // Define a draw_frame function
   const draw_frame = () => {

      // Continue to draw the first item of the glitch array if draw_frame is false 
      // Check to see if we are glitching
      // if so, draw the glitched image from the array
      if (is_glitching) draw (glitch_arr[glitch_i]) 

      // Otherwise draws the original image
      else draw (img) 

      //Conditional probability: 
        //condition ? expression_if_true : expression_if_false
        // if (is_glitching) {
        //     prob = 0.05;
        // } else {
        //     prob = 0.02;
        // }
      //Probability if is_glitching is true: 5% - currently display the glitched image
      //Probability if is_glitching is false: 2% - currently display the original image
      const prob = is_glitching ? 0.05 : 0.02

      // If a random number between 0 to 1 (< 1) is less than the probability
      if (Math.random () < prob) {

         // Choose a random glitched image index
         glitch_i = rand_int (glitch_arr.length) 

         // Switch between displaying the glitched image and the original image
         is_glitching = !is_glitching 
      }

      // Call the next animation frame
      requestAnimationFrame (draw_frame)
   }

</script>

```


### Pixel Sort

<canvas id="pixel_sort"></canvas>

<script type="module">
   import { PixelSorter } from "/scripts/pixel_sort.js"

   const cnv  = document.getElementById (`pixel_sort`)
   cnv.width  = cnv.parentNode.scrollWidth
   cnv.height = cnv.width * 9 / 16   

   const ctx = cnv.getContext (`2d`)
   const sorter = new PixelSorter (ctx)

   const img = new Image ()

   img.onload = () => {
      cnv.height = cnv.width * (img.height / img.width)
      ctx.drawImage (img, 0, 0, cnv.width, cnv.height)
      sorter.init ()
      draw_frame ()
   }

   img.src = `/w05/glitch.JPG`

   let frame_count = 0
   const draw_frame = () => {

      ctx.drawImage (img, 0, 0, cnv.width, cnv.height)

      let sig = Math.cos (frame_count * 2 * Math.PI / 500)

      const mid = {
         x: cnv.width / 2,
         y: cnv.height / 2
      }

      const dim = {
         x: Math.floor ((sig + 3) * (cnv.width / 6)) + 1,
         y: Math.floor ((sig + 1) * (cnv.height / 6)) + 1
      }

      const pos = {
         x: Math.floor (mid.x - (dim.x / 2)),
         y: Math.floor (mid.y - (dim.y / 2))
      }

      sorter.glitch (pos, dim)

      frame_count++
      requestAnimationFrame (draw_frame)
   }

</script>


```javascript
<canvas id="pixel_sort"></canvas>

<script type="module">
   import { PixelSorter } from "/scripts/pixel_sort.js"

   const cnv  = document.getElementById (`pixel_sort`)
   cnv.width  = cnv.parentNode.scrollWidth
   cnv.height = cnv.width * 9 / 16 // 16:9 aspect ratio

   const ctx = cnv.getContext (`2d`)

   // Creates an instance of a PixelSorter class with context as a parameter
   const sorter = new PixelSorter (ctx) 

   // Create a new image element
   const img = new Image () 

   // Define a function to run new image once the image has loaded its data
   img.onload = () => {

      // Adjusts the canvas height 
      // based on the image's aspect ratio
      cnv.height = cnv.width * (img.height / img.width)

      // Call the draw function with the new image as the argument 
      // draw the image to the canvas
      ctx.drawImage (img, 0, 0, cnv.width, cnv.height)

      // Call the innit fuction of the sorter
      sorter.init ()

      // Call the draw_frame function
      draw_frame ()
   }

   // The image source
   img.src = `/w05/glitch.JPG` 

   let frame_count = 0

   // Define a draw_frame function
   const draw_frame = () => {

      // Draw the image 
      //(image, dx, dy, dWidth, dHeight)
      ctx.drawImage (img, 0, 0, cnv.width, cnv.height) 

      // Math.cos returns a value oscillates between -1 and 1
      // Oscillates back and forth as the frame_count increases, creating a wave-like pattern
      // Create a sig value for shimmering (wave) effect
      let sig = Math.cos (frame_count * 2 * Math.PI / 500)

      // Variable to indicate the center of the canvas
      const mid = {
         x: cnv.width / 2,
         y: cnv.height / 2
      }

      // Dimesions of the pixel sorting area
      // based on the sig value and the canvas size
      const dim = {
         x: Math.floor ((sig + 3) * (cnv.width / 6)) + 1,
         y: Math.floor ((sig + 1) * (cnv.height / 6)) + 1
      }

      // Position of the pixel sorting area
      // relative to the center of the canvas 
      const pos = {
         x: Math.floor (mid.x - (dim.x / 2)),
         y: Math.floor (mid.y - (dim.y / 2))
      }

      // Call the glitch function of the sorter
      sorter.glitch (pos, dim)

      // Increments the frame counter for animation
      frame_count++
      requestAnimationFrame (draw_frame)
   }

</script>

```

```javascript
// pixel_sort.js

// Define a quicksort function with 'a' as the parameter
const quicksort = a => {

   // If array 'a' length reaches 1, return the original array length
   if (a.length <= 1) return a

   // Take the first element of the array 'a' as the pivot element 
   let pivot = a[0]

   // Create an empty left array
   let left = []

   // Create an empty right array
   let right = []

   // Iterate through the remaining elements of the array 
   // exclude the first element
   for (let i = 1; i < a.length; i++) {

      // If the current element's brightness (a[i].br) is less than the pivot's, 
      // push the element to the left array
      if (a[i].br < pivot.br) left.push (a[i])

      // Otherwise, push the element to the right array
      else right.push (a[i])
   }

   // ()... means Spread Operators to to spread array values or iterables into an array)
   // Create a sorted array 
   // with result of recursively sorting the left array, 
   // the original pivot element (a[0]),
   // and result of recursively sorting the right array 
   const sorted = [ ...quicksort (left), pivot, ...quicksort (right) ]

   // Return the sorted array 
   // in descending order based on the brightness value
   return sorted
}

export class PixelSorter {
   // PixelSorter class with context as a parameter
   constructor (ctx) {
      this.ctx = ctx
   }

   // Define function for initialize
   init () {

      // Set the initial size
      // based on the canvas size
      this.width = this.ctx.canvas.width
      this.height = this.ctx.canvas.height

      // Method getImageData() returns an ImageData object 
      // representing the underlying pixel data for a specified portion of the canvas
      // Store the image data on the canvas in img_data
      this.img_data = this.ctx.getImageData (0, 0, this.width, this.height).data
   }

   // Define function for the glitch effect 
   // using position and dimesion as the arguments 
   // defining the area within the image to be sorted
   glitch (pos, dim) {

      // Define find_i function with c as the argument
      // to calculate the corresponding index in the image data array,
      // based on the x and y coordinates of a pixel within the canvas
      const find_i = c => ((c.y * this.ctx.canvas.width) + c.x) * 4 
      // 4 represent red, green, blue, and alpha

      // Iterate through each horizontal line (x) within the dimesion (in the argument)
      for (let x_off = 0; x_off < dim.x; x_off++) {

         // Create an empty positions array
         const positions = []

         // Iterate through each vertical line (y) within the dimesion (in the argument)
         for (let y_pos = pos.y; y_pos < pos.y + dim.y; y_pos++) {

            // Use the find_i function 
            // to calculate the index of the pixel at the current position  
            // then push to the positions array 
            positions.push (find_i ({ x: pos.x + x_off, y: y_pos }))
         }

         // Create an empty unsorted array
         const unsorted = []

         // Iterate through the positions array 
         positions.forEach (p => {

            // Red value 
            const r = this.img_data[p]

            // Green value
            const g = this.img_data[p + 1]

            // Blue value
            const b = this.img_data[p + 2]

            // Alpha value
            const a = this.img_data[p + 3]

            // Brightness value
            const br = r * g * b

            // Push RGBA and Brightness value to the unsorted array
            unsorted.push ({ r, g, b, a, br })
         })

         // Using the quicksort funtcion to sort the unsorted array
         // then reverses the order of elements
         const sorted = quicksort (unsorted).reverse ()

         // Create an empty rgba array
         let rgba = []

         // Iterate over each element (e) in the sorted array
         sorted.forEach (e => {
            // Push these extracted values (from e) 
            // in correct order red, green, blue, alpha to the rgba array
            rgba.push (e.r)
            rgba.push (e.g)
            rgba.push (e.b)
            rgba.push (e.a)
         })

         // Uint8ClampedArray: Each element in the typed array 
         // represents a single color channel value (red, green, blue, or alpha) 
         // and is clamped to a valid range (0-255
         // Convert the rgba array into a proper image data storing array
         rgba = new Uint8ClampedArray (rgba)

         // Create new image data using the canvas context
         // width = 1px, 
         // height = dim.y
         // Create a blank image buffer within the specified dimensions
         const new_data = this.ctx.createImageData (1, dim.y)
         
         // Set the data property of new_data
         // using the set method to copy the content of rgba into the new_data
         new_data.data.set (rgba)

         // Draw the new_data object
         this.ctx.putImageData (new_data, pos.x + x_off, pos.y)
      }
   }
}

```

Takes the sorted pixel information, converts it into a format suitable for image data manipulation, creates a new image buffer with the sorted data, and then draws it as a vertical strip onto the canvas at the defined position. This process is repeated for each horizontal line within the specified dimensions, creating the overall pixel sorting glitch effect.


## 2. Glitch Portrait

Glitch portrait link: https://w5-glitch-portrait.deno.dev/ 



