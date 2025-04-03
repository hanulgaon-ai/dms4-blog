---
title: Week 1-2 Blog
published_at: 2025-03-09
snippet: Exploring Rafael Rozendaal's art and creating window frames with code
disable_html_sanitization: true
allow_math: true
---

# Week 1-2 Blog

## 1. Blog Setup

With the help of a friend, I've successfully set up my blog! I'm not entirely sure if it's completely successful yet, but I've confirmed that content entered in Visual Studio Code appears on the page. I plan to ask the professor for help with additional aspects.

## 2. Rafael Rozendaal's Work Analysis

I chose Rafael Rozendaal's work "Passage" for my analysis. The reason I selected this piece is because among Rafael Rozendaal's various works, I felt that most of his pieces are geometric and use various shapes to express emotions. In particular, shapes appear to grow larger from the center point and seem to disappear outward, which gives a feeling of being continuously sucked into the center. The shapes move at a slow tempo, and the color scheme uses only black and white tones, which I think creates a more gloomy mood. I was curious about how this work was implemented through code.

### 2-1. Peer Feedback (Sumin)

Thoughts on the "Passage" work: It resembles my thinking process. When I think deeply about something, the thoughts continue endlessly, and this work seems to visualize my thoughts. It's a piece that makes me keep staring at it absent-mindedly.

What principles do you think are operating inside this work?

- It would definitely include for loops.
- It looks like four points starting from one point and moving away.

What concepts would you need to know to implement this work in p5.js?

- For loops / ???

What resources might help learn this?

- ChatGPT or YouTube or p5.js references (educator) or Thomas

No more friends...

## 3. Creating Window Frames with Code

Since my coding skills are quite limited at this point, I'll focus on creating a shape made of two connected rectangles. I determined that before using principles, I needed to create basic shapes.

```javascript
function setup() {
  createCanvas(400, 400);
  noLoop();
}

function draw() {
  background(220);

  let frameSize = 20;
  let windowSize = 300;

  let startX = (width - windowSize) / 2;
  let startY = (height - windowSize) / 2;

  let topColor = color(180);
  let bottomColor = color(100);
  let leftColor = color(150);
  let rightColor = color(80);

  noStroke();

  fill(topColor);
  rect(startX, startY, windowSize, frameSize);

  fill(bottomColor);
  rect(startX, startY + windowSize - frameSize, windowSize, frameSize);

  fill(leftColor);
  rect(startX, startY, frameSize, windowSize);

  fill(rightColor);
  rect(startX + windowSize - frameSize, startY, frameSize, windowSize);
}
```

This code was created with the help of ChatGPT to make something resembling a window frame. However, I wanted the corners to meet diagonally, so I tried a different approach.

```javascript
function setup() {
  createCanvas(400, 400);
  noLoop();
}

function draw() {
  background(220);

  let frameSize = 20;
  let windowSize = 300;

  let startX = (width - windowSize) / 2;
  let startY = (height - windowSize) / 2;

  let topColor = color(180);
  let bottomColor = color(100);
  let leftColor = color(150);
  let rightColor = color(80);

  noStroke();

  fill(topColor);
  rect(startX, startY, windowSize, frameSize);

  fill(bottomColor);
  rect(startX, startY + windowSize - frameSize, windowSize, frameSize);

  fill(leftColor);
  rect(startX, startY, frameSize, windowSize);

  fill(rightColor);
  rect(startX + windowSize - frameSize, startY, frameSize, windowSize);

  fill(220);

  triangle(
    startX,
    startY,
    startX + frameSize,
    startY,
    startX,
    startY + frameSize
  );

  triangle(
    startX + windowSize - frameSize,
    startY,
    startX + windowSize,
    startY,
    startX + windowSize,
    startY + frameSize
  );

  triangle(
    startX,
    startY + windowSize - frameSize,
    startX + frameSize,
    startY + windowSize,
    startX,
    startY + windowSize
  );

  triangle(
    startX + windowSize - frameSize,
    startY + windowSize,
    startX + windowSize,
    startY + windowSize,
    startX + windowSize,
    startY + windowSize - frameSize
  );
}
```

After several attempts, I reached this code, but it still didn't produce the shape I wanted. So, I decided to try a completely new approach.

```javascript
function setup() {
  createCanvas(400, 400);
  noLoop();
}

function draw() {
  background(220);

  let squareSize = 300;
  let startX = (width - squareSize) / 2;
  let startY = (height - squareSize) / 2;
  let maskSize = squareSize * 0.9;

  noStroke();

  fill(150);
  beginShape();
  vertex(startX, startY);
  vertex(startX + squareSize, startY);
  vertex(startX + squareSize, startY + squareSize);
  endShape(CLOSE);

  fill(80);
  beginShape();
  vertex(startX, startY);
  vertex(startX + squareSize, startY + squareSize);
  vertex(startX, startY + squareSize);
  endShape(CLOSE);

  fill(220);
  rect(startX, startY, maskSize, maskSize);

  fill(220);
  beginShape();
  vertex(startX, startY);
  vertex(startX + maskSize, startY);
  vertex(startX + maskSize, startY + maskSize);
  vertex(startX, startY + maskSize);
  endShape(CLOSE);
}
```

The code above creates a square that is diagonally half-filled with a different color, and then fills in 90% of the shape with the background color starting from the top-left corner. Using this method, I was able to create the window frame corners that I wanted.
