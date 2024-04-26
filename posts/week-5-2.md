---
title: Week 5.2 Blog
published_at: 2024-04-16
snippet: Week 5 Homework - 2. Creates a glitch portrait, 3. Discussion
disable_html_sanitization: true
---

## 2. Glitch Portrait

[Glitch portrait (using Net Art template)](https://w5-glitch-portrait.deno.dev/) 

```html
// index.html 
<!doctype html>
<head>
    <title> Glitch Portrait (W5) </title>
</head>
<body>
<div>
    <canvas id="glitch_portrait"></canvas>
    <script src="glitch.js" type="module"></script> 

    <canvas id="pixelsort_portrait2"></canvas>
    <script src="pixel_sort2.js" type="module"></script>
</div>
</body>
```

The pixel sort javascript file did not show up previously. After the lecture in class in Week 6, I then realized that I had to add the type="module" into the script tag. 

```javascript

// glitch.js 
document.body.style.margin   = 0
document.body.style.overflow = `hidden`

const cnv = document.getElementById (`glitch_portrait`)

// Setting canvas size
cnv.width = innerWidth/2
cnv.height = innerHeight

// Set canvas background to dark blue
cnv.style.backgroundColor = `dark blue`

// Getting canvas context
const ctx = cnv.getContext (`2d`)

// Instatiating variable for the image data
let img_data

// Define a function to draw an image to the canvas 
const draw = i => ctx.drawImage (i, 0, 0, cnv.width, cnv.height) 
//(image, dx, dy, dWidth, dHeight)

// Create a new image element 
const img = new Image () 

// Define a function to run new image once the image has loaded its data
img.onload = () => {

  // Adjusts the canvas height 
  // based on the image's aspect ratio
  cnv.height = cnv.width * (img.height / img.width) 

  // Draw the image to the canvas
  draw (img) 

  // Set the canvas data into a image data
  // Storing image data as string in img_data
  img_data = cnv.toDataURL ("image/jpeg") 

  // Call the add_glitch function 
  add_glitch () 
}

// The image source 
img.src = `/glitch.JPG` 

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
   i.src = glitchify (img_data, 100, 7)
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
```

The code was heavily inspired by the Glitch blog in the module, I have changed some values within the code to see the differences between the results.  

```javascript
// pixel_sort2.js
document.body.style.margin   = 0
document.body.style.overflow = `hidden`

import { PixelSorter } from "/pixel_sort_class.js"

const cnv  = document.getElementById (`pixelsort_portrait2`)
cnv.width  = innerWidth/-3
cnv.height = innerHeight

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
    ctx.drawImage (img, 0, cnv.height/-2, cnv.width * 2, cnv.height * 2)

    // Call the innit fuction of the sorter
    sorter.init ()

    // Call the draw_frame function
    draw_frame ()
}

// The image source
img.src = `glitch_hw.jpg` 

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
        x: cnv.width / 3,
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
```

```javascript
//pixel_sort_class
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

The code was heavily inspired by the Pixel Sort blog in the module, I have changed some values within the code to see the differences between the results. However, I had a problem with adjusting the size of the canvas. I think to make both images in the same frame, I have to create a div to contain both the canvas (as shown in the index.html file). They both display in the same frame, however, the Pixel sort image is smaller than the Glitch image.

## 3. Discussion

*Which of Ngai's aesthetic categories does your self-portrait (and glitch more generally) belong to, and why?* 

In my opion, the images above and Glitch generally belong to both Ngai's Zany and Interesting aesthetics.

The Zany aesthetic involves excessive and sharp implements, an unpredictable imitation. While Glitch aesthetic disrupts the intended presentation of an image or video, introducing visual noise, fragmentation, and distortions. In *Glitch is Skin* by Russell, ‘the presence of a glitch makes the “digital skin” visible, reminding us of the fallibility of the machine and the presence of its hardware, revealing its edges and seams’. The instability and 'edges revelation' nature of Glitch effectively represents the Chaotic aesthetic. 

The repetitive nature of Glitch and its alternatively flips between the orginal and the alter version correlate with the Interesting aesthetic's repetitive flick between the familiar and unfamiliar, continuity and break. 

*Does glitch increase or decrease effective complexity, and why?*

I think overall, glitch tends to decrease effective complexity since they bring in instability and unpredictability. However, with controlled amount of glitches could introduce a slight randomness that enhances the complexity of the whole system. Also, their repetitive nature could create a pattern to which the viewer could predict the upcoming elements yet anticipate the tiny variations, an unpredictable imitation nature of the Chaotic (Zany) aesthetic.
<p>
<br>
<p>








