---
title: Week 2-1 Blog
published_at: 2025-03-16
snippet: Exploring concepts of cuteness through interactive visuals
disable_html_sanitization: true
allow_math: true
---

# Week 2-1 Blog

## Exploring Cuteness

While I don't have a clear, well-defined concept of cuteness yet, there are several elements I can consider. First, visually, pastel tones and round shapes seem to convey cuteness. Second, sound-wise, I think bouncy "pop" sounds rather than harsh, solid sounds would feel cute. Finally, regarding interactive elements, I need to think more about this, but for now, having elements follow the mouse seems fun. Below is a code example using ChatGPT to create something as cute as possible within my abilities.

```javascript
let faceColor;
let faceSize = 100;
let eyeSize = 25;

function setup() {
  createCanvas(400, 400);
  faceColor = color(255, 200, 200); // Initial face color: soft pink
}

function draw() {
  background(240);

  // Draw the face (circle)
  fill(faceColor);
  noStroke();
  ellipse(mouseX, mouseY, faceSize, faceSize); // Face follows mouse position

  // Draw the eyes
  fill(255); // White of the eyes
  ellipse(mouseX - 20, mouseY - 20, eyeSize, eyeSize); // Left eye
  ellipse(mouseX + 20, mouseY - 20, eyeSize, eyeSize); // Right eye

  // Draw the pupils (small black circles)
  fill(0); // Black pupils
  ellipse(mouseX - 20, mouseY - 20, eyeSize / 2, eyeSize / 2); // Left pupil
  ellipse(mouseX + 20, mouseY - 20, eyeSize / 2, eyeSize / 2); // Right pupil
}

function mousePressed() {
  // Change the face color to a pastel tone on click
  faceColor = pastelColor(); // Call the pastel color function
}

// Function to generate a random pastel color
function pastelColor() {
  let r = random(180, 255); // Light red tone (pastel)
  let g = random(180, 255); // Light green tone (pastel)
  let b = random(180, 255); // Light blue tone (pastel)
  return color(r, g, b); // Return the random pastel color
}
```

I created a pastel-colored circle with eyes that follows the mouse cursor, and the color changes when clicked. For sound, I would need to add sound files directly, but I'll leave that for later and proceed with what I have so far.

## Colorful Rectangles

```javascript
function setup() {
  createCanvas(400, 400);
  background(0);
}

function draw() {
  rectMode(CORNERS);
  fill(random(0, 255), random(0, 255), random(0, 255), 40);
  rect(
    random(0, width),
    random(0, height),
    random(0, width),
    random(0, height)
  );
}
```

This time, I created an animation where various colored rectangles continuously appear. Using CORNERS mode, rectangles generate from each corner of the canvas. The diverse colors and shapes of rectangles rapidly appearing and overlapping remind me of a child's imagination, which I find quite cute.

## Assignment 1 Ideation

For Assignment 1, I quickly thought of a few examples during class. The first is a companion that has a cat's appearance but could be called a dog. This friend has both cat and dog behaviors and makes people think the opposite of what they normally assume. The simplest approach I can think of is to have a shape that changes from a cat to a dog through mouse interaction.

```javascript
let isCat = true;

function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);

  if (isCat) {
    drawCat();
  } else {
    drawDog();
  }
}

function drawCat() {
  fill(255, 200, 0);
  stroke(0);

  ellipse(200, 200, 120, 120);

  triangle(160, 150, 180, 90, 200, 150);
  triangle(240, 150, 220, 90, 200, 150);

  fill(0);
  ellipse(180, 190, 15, 15);
  ellipse(220, 190, 15, 15);

  fill(255, 0, 0);
  triangle(195, 210, 205, 210, 200, 220);

  noFill();
  arc(190, 230, 20, 10, 0, PI);
  arc(210, 230, 20, 10, 0, PI);
}

function drawDog() {
  fill(150, 100, 50);
  stroke(0);

  ellipse(200, 200, 130, 120);

  ellipse(150, 180, 30, 50);
  ellipse(250, 180, 30, 50);

  fill(0);
  ellipse(180, 190, 15, 15);
  ellipse(220, 190, 15, 15);

  fill(0);
  ellipse(200, 220, 15, 10);

  line(195, 230, 205, 230);
}

function mousePressed() {
  isCat = !isCat;
}
```

The code above, created using ChatGPT, represents an interaction where a cat changes to a dog when clicked.
