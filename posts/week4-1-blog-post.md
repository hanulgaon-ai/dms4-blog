````
---
title: Week 4-1 Blog
published_at: 2025-03-29
snippet: Exploring complexity and compression through generative patterns
disable_html_sanitization: true
allow_math: true
---

# Week 4-1 Blog

## 1. Three Example Compositions

### 1) High Compressibility

Regular grid patterns can be expressed with simple repetitive rules (two for loops), making them highly compressible.

```javascript
// This function runs once at the start
function setup() {
  // Create a canvas that is 400x400 pixels in size
  createCanvas(400, 400);
  // Don't run the draw function continuously, just once
  noLoop();
}

// This function contains all the drawing code
function draw() {
  // Set the background color to light gray (240)
  background(240);

  // Set up the styling for our grid lines
  strokeWeight(1); // Make lines 1 pixel thick
  stroke(0); // Set line color to black

  // Define how far apart the grid lines should be (20 pixels)
  let spacing = 20;

  // Draw all vertical lines
  // Start at x=0, continue until the width of the canvas, increment by spacing amount
  for (let x = 0; x <= width; x += spacing) {
    // Draw a line from (x,0) at the top to (x,height) at the bottom
    line(x, 0, x, height);
  }

  // Draw all horizontal lines
  // Start at y=0, continue until the height of the canvas, increment by spacing amount
  for (let y = 0; y <= height; y += spacing) {
    // Draw a line from (0,y) at the left to (width,y) at the right
    line(0, y, width, y);
  }
}
```

### 2) Low Compressibility

Completely random pixel patterns require separate information for each pixel, making them almost impossible to compress.

```javascript
// This function runs once at the start
function setup() {
  // Create a canvas that is 400x400 pixels in size
  createCanvas(400, 400);
  // Don't run the draw function continuously, just once
  noLoop();
}

// This function contains all the drawing code
function draw() {
  // Set the background color to light gray (240)
  background(240);

  // Generate completely random pixels
  // This loads the pixel data from the canvas into the pixels[] array
  loadPixels();
  // Loop through every row of pixels
  for (let y = 0; y < height; y++) {
    // Loop through every column of pixels
    for (let x = 0; x < width; x++) {
      // Calculate the index position in the pixels array
      // Each pixel takes up 4 values in the array (R,G,B,A)
      // So we multiply by 4 to get the starting index for this pixel
      let index = (x + y * width) * 4;

      // Set each RGB value randomly for each pixel
      pixels[index] = random(255); // R (red value between 0-255)
      pixels[index + 1] = random(255); // G (green value between 0-255)
      pixels[index + 2] = random(255); // B (blue value between 0-255)
      pixels[index + 3] = 255; // Alpha (opacity - fully opaque)
    }
  }
  // Update the canvas with our new pixel data
  updatePixels();
}
```

### 3) High Effective Complexity

Tree generation using L-systems combines simple rules with a touch of randomness to create natural and complex results.

```javascript
// L-system tree generation code
let axiom = "F"; // Starting character (axiom)
let sentence = axiom; // Current state of the L-system
let rules = {
  F: "FF+[+F-F-F]-[-F+F+F]", // Replacement rule: F becomes a complex branch structure
};
let len = 100; // Initial length of segments
let angle; // Angle for rotations

function setup() {
  createCanvas(600, 600); // Create a 600x600 pixel canvas
  angle = radians(25); // Convert 25 degrees to radians for rotation
  stroke(70, 40, 20); // Set stroke color to brown (tree color)
  background(220); // Set background to light gray

  // Apply L-system rules 4 times to create complex branching
  for (let i = 0; i < 4; i++) {
    generate();
  }

  // Start drawing from the bottom center of the canvas
  translate(width / 2, height);
  // Reduce length for more natural appearance
  len = len * 0.5;
  // Draw the L-system
  turtle();
}

function generate() {
  // Function to apply the replacement rules to the current sentence
  let nextSentence = "";
  for (let i = 0; i < sentence.length; i++) {
    let current = sentence.charAt(i);
    // If the character has a rule, replace it
    if (current in rules) {
      nextSentence += rules[current];
    } else {
      // Otherwise keep the character as is
      nextSentence += current;
    }
  }
  sentence = nextSentence; // Update the sentence with new generation
  len *= 0.5; // Reduce length for each generation (branches get smaller)
}

function turtle() {
  // Function to interpret the L-system string and draw the tree
  for (let i = 0; i < sentence.length; i++) {
    let current = sentence.charAt(i);

    // Draw a line segment for 'F'
    if (current == "F") {
      // Add slight randomness to length for natural look
      let actualLen = len * (0.9 + random(0.2));
      strokeWeight(len / 10); // Make stroke width proportional to segment length
      line(0, 0, 0, -actualLen); // Draw a vertical line upward
      translate(0, -actualLen); // Move to the end of the line
    }
    // Rotate right
    else if (current == "+") {
      // Add slight randomness to angle for natural look
      rotate(angle * (0.9 + random(0.2)));
    }
    // Rotate left
    else if (current == "-") {
      rotate(-angle * (0.9 + random(0.2)));
    }
    // Save current position and angle (start a branch)
    else if (current == "[") {
      push();
    }
    // Return to saved position and angle (end a branch)
    else if (current == "]") {
      pop();
    }
  }
}

function draw() {
  // This function remains empty because we're creating a static image,
  // not an animation. All drawing happens in setup().
}
```

## 2. Brief Explanation of Philip Galanter's Argument

The concept Galanter mentions that "structure depends on the subjective perspective of the viewer" is useful in generative art because:

1. Diversity of Interpretation - Different audiences can discover different structures and meanings in the same work, adding depth to the piece.
2. Encouraging Participation - The first example (grid) is simple, and the second example (random pixels) is complex, but the third example (L-system tree) sits somewhere in between, actively encouraging viewers to find patterns and interpret them.

Key elements creating the structure in the third example:

- L-systems - Simple rules that evolve into complex forms
- Controlled Randomness - Maintaining the basic pattern while adding slight variations in length and angle
- Balance - The combination of deterministic structure and random elements creates natural complexity

## 3. Structure and Randomness in an Artist's Work

Effective complexity in Manfred Mohr's work consists of:

1. Mathematical Foundation - Using clear mathematical structures such as hypercubes
2. Calculated Variations - Applying limited randomness within structural rules to create diversity
3. Balance - Forming unpredictable yet comprehensible patterns at the midpoint between strict order and randomness

Mohr's work follows clear geometric rules while leaving room for viewers to form their own interpretations through variations. This demonstrates how the subjectivity of structure adds value to generative art.

## Interactive Examples

<iframe id="grid_example" src="https://editor.p5js.org/capogreco/full/Fkg05m7aA"></iframe>

<script type="module">
    const iframe = document.getElementById(`grid_example`)
    iframe.width = iframe.parentNode.scrollWidth
    iframe.height = iframe.width * 9 / 16 + 42
</script>

```

```
````
