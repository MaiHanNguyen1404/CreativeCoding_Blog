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
   // Sets the background color of the canvas to deeppink. 
   cnv.style.backgroundColor = `deeppink` 


   const ctx = cnv.getContext (`2d`)

   let img_data

    // Define a draw function with unknown image value i
    // function draw (i) {
    // ctx.drawImage (i, 0, 0, cnv.width, cnv.height)
    // }
   const draw = i => ctx.drawImage (i, 0, 0, cnv.width, cnv.height) 
   //(image, dx, dy, dWidth, dHeight)

   // Create a new image 
   const img = new Image () 

   // Run new image once the image has successfully loaded its resource
   img.onload = () => {
      // Adjusts the canvas height based on the image's aspect ratio
      cnv.height = cnv.width * (img.height / img.width) 
      // Call the draw function with the new image as the argument 
      // draw the image to the canvas
      draw (img) 
      // Set the canvas data into a image data
      img_data = cnv.toDataURL ("image/jpeg") 
      // Call the add_glitch function 
      add_glitch () 
   }
   img.src = `/240405/pfp_glasses.jpg` // The image source

   // Define a function to generate random integer within the maximum range
   const rand_int = max => Math.floor (Math.random () * max)

   // Define a glitch function 
   const glitchify = (data, chunk_max, repeats) => {
      // Picks a random chunk size (multiply by 4) within the maximum range (to glitch)
      const chunk_size = rand_int (chunk_max / 4) * 4 
      // Select a random portion of image data excluding 
      // the first 24 bytes and the glitch chunk size
      const i = rand_int (data.length - 24 - chunk_size) + 24
      // Remove the first part of the data to i
      const front = data.slice (0, i) 
      // Remove ... to the end of the data
      const back = data.slice (i + chunk_size, data.length) 
      // Combining the front and back portions of the selected data
      const result = front + back 
      // Call the function recursively
      // stops executing the function when the the repeats time reach 0
      return repeats == 0 ? result : glitchify (result, chunk_max, repeats - 1) 
   }

   // Create an empty glitch array  
   const glitch_arr = []

   // Define function to create multiple glitched versions of the image 
   // using the glitchify function
   const add_glitch = () => {
      // Create new image objects for each glitched version.
      const i = new Image () 
      // Once a glitched image has successfully loaded
      i.onload = () => { 
         // Push the glitched image object into the glitch array
         glitch_arr.push (i) 
         // Recursively call the add_glitch function 
         // if less than 12 glitched version is created
         if (glitch_arr.length < 12) add_glitch () 
         // Call the draw_frame function 
         // if the glitch array length reaches 12 or more
         else draw_frame () 
      }
      i.src = glitchify (img_data, 96, 6) //
   }

   let is_glitching = false 
   let glitch_i = 0 

   // Define a draw_frame function
   const draw_frame = () => {
      // Continue to draw the first item of the glitch array if draw_frame is false 
      // (add_glitch function still calls)
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
         glitch_i = rand_int (glitch_arr.length) 
         // Switch between displaying the glitched image and the original image
         is_glitching = !is_glitching 
      }

      requestAnimationFrame (draw_frame)
   }

</script>

```


### Pixel Sort

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

   // Create a new image 
   const img = new Image () 

   // Run new image once the image has successfully loaded 
   img.onload = () => {
      // Adjusts the canvas height based on the image's aspect ratio
      cnv.height = cnv.width * (img.height / img.width)
      // Call the draw function with the new image as the argument 
      // draw the image to the canvas
      ctx.drawImage (img, 0, 0, cnv.width, cnv.height)
      // Call the innit fuction of the sorter
      sorter.init ()
      // Call the draw_frame function
      draw_frame ()
   }

   img.src = `/240408/kornerpark.jpg` // The image source

   let frame_count = 0
   // Define a draw_frame function
   const draw_frame = () => {

      // Draw the image 
      //(image, dx, dy, dWidth, dHeight)
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

      // Call the glitch function of the sorter
      sorter.glitch (pos, dim)

      frame_count++
      requestAnimationFrame (draw_frame)
   }

</script>

```

```classjs
// pixel_sort.js

// Define a quicksort function with 'a' as the parameter
const quicksort = a => {
   // 
   if (a.length <= 1) return a

   // Take the first element of the array 'a' as the pivot
   let pivot = a[0]
   // Create an empty left array
   let left = []
   // Create an empty right array
   let right = []

   // Iterate through the remaining elements of the array (exclude the first element)
   for (let i = 1; i < a.length; i++) {
      // 
      if (a[i].br < pivot.br) left.push (a[i])
      else right.push (a[i])
   }

   const sorted = [ ...quicksort (left), pivot, ...quicksort (right) ]

   return sorted
}

export class PixelSorter {
   constructor (ctx) {
      this.ctx = ctx
   }

   init () {
      this.width = this.ctx.canvas.width
      this.height = this.ctx.canvas.height
      this.img_data = this.ctx.getImageData (0, 0, this.width, this.height).data
   }


   glitch (pos, dim) {
      const find_i = c => ((c.y * this.ctx.canvas.width) + c.x) * 4 

      for (let x_off = 0; x_off < dim.x; x_off++) {
         const positions = []

         for (let y_pos = pos.y; y_pos < pos.y + dim.y; y_pos++) {
            positions.push (find_i ({ x: pos.x + x_off, y: y_pos }))
         }

         const unsorted = []

         positions.forEach (p => {
            const r = this.img_data[p]
            const g = this.img_data[p + 1]
            const b = this.img_data[p + 2]
            const a = this.img_data[p + 3]
            const br = r * g * b
            unsorted.push ({ r, g, b, a, br })
         })

         const sorted = quicksort (unsorted).reverse ()

         let rgba = []

         sorted.forEach (e => {
            rgba.push (e.r)
            rgba.push (e.g)
            rgba.push (e.b)
            rgba.push (e.a)
         })

         rgba = new Uint8ClampedArray (rgba)

         const new_data = this.ctx.createImageData (1, dim.y)
         
         new_data.data.set (rgba)

         this.ctx.putImageData (new_data, pos.x + x_off, pos.y)
      }
   }
}

```

