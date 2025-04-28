---
title: Week 4-2 Blog
published_at: 2025-05-09
snippet: Exploring glitch aesthetics through digital self-portraiture
disable_html_sanitization: true
allow_math: true
---

# Week 4-2 Blog

## 1. Glitch Self-Portrait

I created a self-portrait using glitch and pixel sorting techniques. Here's the code with comments explaining the process:

```javascript
// Self-portrait glitch processing code
let img; // Image variable
let sortedPixels = []; // Array to store sorted pixels

function preload() {
 img = loadImage('selfportrait.jpg'); // Load self-portrait
}

function setup() {
 createCanvas(img.width, img.height);
 img.loadPixels(); // Load pixel data

 // Create a copy of the pixels
 let pixelsCopy = [...img.pixels];

 // Apply pixel sorting
 for (let y = 0; y < img.height; y++) {
   // Set a threshold for each row
   let threshold = random(100, 200);

   // Find segments to sort based on brightness
   let segments = findSegments(y, threshold);

   // Sort each segment
   for (let seg of segments) {
     sortSegment(pixelsCopy, y, seg.start, seg.end);
   }

   // Apply row offset glitch (25% chance)
   if (random() < 0.25) {
     let offset = floor(random(-30, 30));
     applyRowOffset(pixelsCopy, y, offset);
   }
 }

 // Store sorted pixel data
 sortedPixels = pixelsCopy;

 // Apply RGB channel shift
 applyRGBShift(sortedPixels, floor(random(5, 15)));

 // Add random noise
 addNoise(sortedPixels, 0.1);
}

function draw() {
 // Display the glitched image
 loadPixels();
 for (let i = 0; i < pixels.length; i++) {
   pixels[i] = sortedPixels[i];
 }
 updatePixels();
 noLoop(); // Draw only once
}

// Function to find sortable segments based on threshold
function findSegments(y, threshold) {
 // Implementation returns segments to sort
 // Based on brightness threshold
}

// Function to sort a pixel segment
function sortSegment(pixels, y, start, end) {
 // Implementation sorts pixels by brightness
}

// Function to apply row offset glitch effect
function applyRowOffset(pixels, y, offset) {
 // Implementation shifts row pixels by offset amount
}

// Function to apply RGB channel shift
function applyRGBShift(pixels, shift) {
 // Implementation moves R and B channels in opposite directions
}

// Function to add random noise
function addNoise(pixels, intensity) {
 // Implementation adds random color noise to some pixels
}

## 2. Aesthetic Analysis

Applying glitch techniques to my self-portrait transforms its aesthetic register in significant ways:
Glitch Readings Connection
Rosa Menkman's "Glitch Studies Manifesto" suggests that glitches reveal "hidden possibilities within systems" rather than just errors. My glitched portrait deliberately manipulates the fundamental structures of digital images (pixels and color channels), exposing the materiality of the medium and exploring new aesthetic possibilities.
As Menkman argues, "glitches open new possibilities of perception by destroying existing systems and expectations." The distortion and rearrangement of my digital face demonstrates both the vulnerability and fluidity of digital images, while revealing how identity can be mediated and transformed by technology.
Net Art Readings Connection
Olia Lialina's "Net Art Generations" explores the development of internet art and its aesthetic characteristics. Her description of a "new aesthetic language" focuses on acknowledging and utilizing the unique properties and limitations of digital media. My glitched portrait actively manipulates the basic elements of digital images—pixel structure and color channels—to explore this aesthetic language.
Lialina's concept of "interface aesthetics" emphasizes how technological mediation becomes part of the artwork. In my work, the code itself becomes the tool and medium of expression.
Effective Complexity Analysis
According to Murray Gell-Mann, the most interesting systems exist at a midpoint between complete randomness and complete regularity. My glitched self-portrait explores this balance:

Regularity: The pixel sorting algorithm follows a systematic structure, reorganizing pixels according to brightness values.
Randomness: Row offsets, RGB channel shifts, and random noise introduce unpredictable elements.

This combination maintains identifiable features of the original image while generating new, unexpected patterns—an example of Gell-Mann's "compressible complexity."
Ngai's Aesthetic Registers
Analyzing my glitched self-portrait through Sianne Ngai's three aesthetic registers:

Cuteness: While distant from conventional "cuteness," the portrait exhibits aspects of digital vulnerability and imperfection.
Interesting: The work primarily occupies this register. The combination of pixel sorting and glitch effects provokes intellectual curiosity about digital media's materiality and limitations.
Zany: Some extreme distortions and color shifts emphasize the instability and exaggerated nature of digital representation, connecting to the fluid and sometimes exaggerated expression of identity in contemporary digital culture.

My glitched portrait primarily occupies the "interesting" register while incorporating elements of "zany," exploring the complexities and contradictions of self-expression through digital media.

```
