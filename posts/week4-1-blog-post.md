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
  img = loadImage("selfportrait.jpg"); // Load self-portrait
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
  let segments = [];
  let inSegment = false;
  let segStart = 0;

  // Check each pixel in the row
  for (let x = 0; x < img.width; x++) {
    let idx = (y * img.width + x) * 4;
    let r = img.pixels[idx];
    let g = img.pixels[idx + 1];
    let b = img.pixels[idx + 2];
    let brightness = (r + g + b) / 3;

    if (brightness > threshold && !inSegment) {
      // Start segment
      inSegment = true;
      segStart = x;
    } else if (brightness <= threshold && inSegment) {
      // End segment
      inSegment = false;
      segments.push({ start: segStart, end: x - 1 });
    }
  }

  // Close any open segment at the end of row
  if (inSegment) {
    segments.push({ start: segStart, end: img.width - 1 });
  }

  return segments;
}

// Function to sort a pixel segment
function sortSegment(pixels, y, start, end) {
  let segment = [];

  // Extract segment pixels
  for (let x = start; x <= end; x++) {
    let idx = (y * img.width + x) * 4;
    segment.push({
      r: pixels[idx],
      g: pixels[idx + 1],
      b: pixels[idx + 2],
      a: pixels[idx + 3],
    });
  }

  // Sort pixels by brightness
  segment.sort((a, b) => {
    let brightnessA = (a.r + a.g + a.b) / 3;
    let brightnessB = (b.r + b.g + b.b) / 3;
    return brightnessA - brightnessB;
  });

  // Put sorted pixels back into array
  for (let i = 0; i < segment.length; i++) {
    let idx = (y * img.width + (start + i)) * 4;
    pixels[idx] = segment[i].r;
    pixels[idx + 1] = segment[i].g;
    pixels[idx + 2] = segment[i].b;
    pixels[idx + 3] = segment[i].a;
  }
}

// Function to apply row offset glitch effect
function applyRowOffset(pixels, y, offset) {
  let rowPixels = [];

  // Store row pixels
  for (let x = 0; x < img.width; x++) {
    let idx = (y * img.width + x) * 4;
    rowPixels.push({
      r: pixels[idx],
      g: pixels[idx + 1],
      b: pixels[idx + 2],
      a: pixels[idx + 3],
    });
  }

  // Apply offset and reposition pixels
  for (let x = 0; x < img.width; x++) {
    let newX = (x + offset + img.width) % img.width;
    let idx = (y * img.width + newX) * 4;
    pixels[idx] = rowPixels[x].r;
    pixels[idx + 1] = rowPixels[x].g;
    pixels[idx + 2] = rowPixels[x].b;
    pixels[idx + 3] = rowPixels[x].a;
  }
}

// Function to apply RGB channel shift
function applyRGBShift(pixels, shift) {
  let pixelsCopy = [...pixels];

  for (let i = 0; i < pixels.length; i += 4) {
    // Shift red channel forward
    if (i + shift * 4 < pixels.length) {
      pixels[i] = pixelsCopy[i + shift * 4];
    }

    // Shift blue channel backward
    if (i - shift * 4 >= 0) {
      pixels[i + 2] = pixelsCopy[i - shift * 4 + 2];
    }
  }
}

// Function to add random noise
function addNoise(pixels, intensity) {
  for (let i = 0; i < pixels.length; i += 4) {
    if (random() < intensity) {
      pixels[i] = random(255); // R
      pixels[i + 1] = random(255); // G
      pixels[i + 2] = random(255); // B
    }
  }
}
```
