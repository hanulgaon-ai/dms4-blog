---
title: Week 3-1 Blog
published_at: 2025-03-23
snippet: Analyzing cuteness in Rafaël Rozendaal's work and implementing cute aesthetics
disable_html_sanitization: true
allow_math: true
---

# Week 3-1 Blog

## 1. Analyzing Rafaël Rozendaal's Cute Aesthetic

The work I've selected is "Why Was He Sad"

### Visual Elements

Light blue background with round white clouds that generate from both sides and move to the opposite side.
The clouds move at different speeds, which makes you stare at them absent-mindedly.

### Sonic Elements

Sound effects play when interacting with clouds through the mouse, and the clouds disappear.

### Interactive Elements

When the mouse touches clouds generated from both sides, they disappear with sound effects.

## 2. Implementing Cute Aesthetics in my AT1 with p5.js

```javascript
let strokes = [];
let animals = [];

function setup() {
  createCanvas(windowWidth, windowHeight);
  background(250, 240, 230);

  for (let i = 0; i < 5000; i++) {
    let x = random(width);
    let y = random(height);
    let dotSize = random(1, 3);
    noStroke();
    fill(200, 180, 150, random(20, 50));
    ellipse(x, y, dotSize, dotSize);
  }
}

function draw() {
  background(250, 240, 230);

  for (let i = 0; i < 5000; i++) {
    let x = random(width);
    let y = random(height);
    let dotSize = random(1, 3);
    noStroke();
    fill(200, 180, 150, random(20, 50));
    ellipse(x, y, dotSize, dotSize);
  }

  for (let i = 0; i < strokes.length; i++) {
    let strokeLine = strokes[i];
    strokeWeight(strokeLine.weight);
    stroke(strokeLine.color);
    line(strokeLine.x1, strokeLine.y1, strokeLine.x2, strokeLine.y2);
  }

  for (let i = 0; i < animals.length; i++) {
    animals[i].display();
    animals[i].update();
  }
}

function mouseDragged() {
  let weight = random(3, 8);
  let r = random(150, 250);
  let g = random(100, 200);
  let b = random(100, 200);

  let xOffset = random(-1, 1);
  let yOffset = random(-1, 1);

  strokes.push({
    x1: mouseX + xOffset,
    y1: mouseY + yOffset,
    x2: pmouseX + xOffset,
    y2: pmouseY + yOffset,
    weight: weight,
    color: color(r, g, b),
  });

  return false;
}

function mouseReleased() {
  if (strokes.length > 10) {
    let shape = recognizeShape(strokes);

    if (shape === "circle") {
      animals.push(new Animal(mouseX, mouseY, "dog"));
    } else if (shape === "triangle" || shape === "line") {
      animals.push(new Animal(mouseX, mouseY, "cat"));
    }

    strokes = [];
  }
}

function recognizeShape(strokes) {
  let avgX = 0,
    avgY = 0;
  let points = [];

  strokes.forEach((s) => {
    points.push({ x: s.x1, y: s.y1 });
    points.push({ x: s.x2, y: s.y2 });
    avgX += s.x1 + s.x2;
    avgY += s.y1 + s.y2;
  });

  avgX /= points.length;
  avgY /= points.length;

  let distances = [];
  points.forEach((p) => {
    distances.push(dist(avgX, avgY, p.x, p.y));
  });

  let avgDist = 0;
  distances.forEach((d) => (avgDist += d));
  avgDist /= distances.length;

  let variance = 0;
  distances.forEach((d) => {
    variance += (d - avgDist) * (d - avgDist);
  });
  variance /= distances.length;

  if (variance < 400) {
    return "circle";
  }

  return "triangle";
}

class Animal {
  constructor(x, y, type) {
    this.x = x;
    this.y = y;
    this.type = type;
    this.animalSize = 0;
    this.targetSize = random(40, 70);
    this.growing = true;
    this.hover = false;
    this.scale = 1;
    this.wiggleAmount = 0;
    this.wiggleSpeed = random(0.02, 0.05);
  }

  update() {
    if (this.growing) {
      this.animalSize += (this.targetSize - this.animalSize) * 0.1;
      if (this.animalSize > this.targetSize * 0.95) {
        this.growing = false;
      }
    }

    let d = dist(mouseX, mouseY, this.x, this.y);
    this.hover = d < this.animalSize / 2;

    if (this.hover) {
      this.scale = lerp(this.scale, 1.1, 0.1);
    } else {
      this.scale = lerp(this.scale, 1.0, 0.1);
    }

    this.wiggleAmount = sin(frameCount * this.wiggleSpeed) * 3;
  }

  display() {
    push();
    translate(this.x, this.y);
    scale(this.scale);

    if (this.type === "dog") {
      fill(255, 220, 180);
      noStroke();
      ellipse(0, 0, this.animalSize, this.animalSize);

      fill(230, 190, 150);
      ellipse(
        -this.animalSize / 3,
        -this.animalSize / 3,
        this.animalSize / 3,
        this.animalSize / 2
      );
      ellipse(
        this.animalSize / 3,
        -this.animalSize / 3,
        this.animalSize / 3,
        this.animalSize / 2
      );

      fill(60, 40, 30);
      ellipse(
        -this.animalSize / 6,
        -this.animalSize / 10,
        this.animalSize / 10,
        this.animalSize / 10
      );
      ellipse(
        this.animalSize / 6,
        -this.animalSize / 10,
        this.animalSize / 10,
        this.animalSize / 10
      );

      fill(60, 30, 30);
      ellipse(
        0,
        this.animalSize / 10,
        this.animalSize / 7,
        this.animalSize / 10
      );

      stroke(60, 30, 30);
      strokeWeight(2);
      noFill();
      arc(
        0,
        this.animalSize / 5,
        this.animalSize / 5,
        this.animalSize / 10,
        0,
        PI
      );

      if (this.hover) {
        noStroke();
        fill(255, 220, 180);
        ellipse(
          this.animalSize / 2 + this.wiggleAmount,
          0,
          this.animalSize / 4,
          this.animalSize / 6
        );
      }
    } else if (this.type === "cat") {
      fill(200, 180, 220);
      noStroke();
      ellipse(0, 0, this.animalSize, this.animalSize * 0.9);

      fill(180, 160, 200);
      triangle(
        -this.animalSize / 2,
        -this.animalSize / 2,
        -this.animalSize / 5,
        -this.animalSize * 0.7,
        -this.animalSize / 10,
        -this.animalSize / 2
      );
      triangle(
        this.animalSize / 2,
        -this.animalSize / 2,
        this.animalSize / 5,
        -this.animalSize * 0.7,
        this.animalSize / 10,
        -this.animalSize / 2
      );

      fill(60, 180, 190);
      ellipse(
        -this.animalSize / 6,
        -this.animalSize / 10,
        this.animalSize / 8,
        this.animalSize / 5
      );
      ellipse(
        this.animalSize / 6,
        -this.animalSize / 10,
        this.animalSize / 8,
        this.animalSize / 5
      );

      fill(20);
      ellipse(
        -this.animalSize / 6,
        -this.animalSize / 10,
        this.animalSize / 20,
        this.animalSize / 8
      );
      ellipse(
        this.animalSize / 6,
        -this.animalSize / 10,
        this.animalSize / 20,
        this.animalSize / 8
      );

      fill(255, 150, 180);
      triangle(
        0,
        this.animalSize / 10,
        -this.animalSize / 20,
        0,
        this.animalSize / 20,
        0
      );

      stroke(220);
      strokeWeight(1);
      line(
        -this.animalSize / 10,
        this.animalSize / 15,
        -this.animalSize / 2,
        0
      );
      line(
        -this.animalSize / 10,
        this.animalSize / 15,
        -this.animalSize / 2,
        this.animalSize / 10
      );
      line(
        -this.animalSize / 10,
        this.animalSize / 15,
        -this.animalSize / 2,
        -this.animalSize / 10
      );
      line(this.animalSize / 10, this.animalSize / 15, this.animalSize / 2, 0);
      line(
        this.animalSize / 10,
        this.animalSize / 15,
        this.animalSize / 2,
        this.animalSize / 10
      );
      line(
        this.animalSize / 10,
        this.animalSize / 15,
        this.animalSize / 2,
        -this.animalSize / 10
      );

      if (this.hover) {
        noStroke();
        fill(200, 180, 220);
        beginShape();
        vertex(this.animalSize / 2, 0);
        bezierVertex(
          this.animalSize * 0.7,
          this.animalSize / 10,
          this.animalSize * 0.8 + this.wiggleAmount,
          -this.animalSize / 5,
          this.animalSize * 0.9,
          -this.animalSize / 2
        );
        bezierVertex(
          this.animalSize * 0.8,
          -this.animalSize / 4,
          this.animalSize * 0.7 - this.wiggleAmount,
          -this.animalSize / 10,
          this.animalSize / 2,
          0
        );
        endShape();
      }
    }
    pop();
  }
}

function mousePressed() {
  for (let i = animals.length - 1; i >= 0; i--) {
    let animal = animals[i];
    let d = dist(mouseX, mouseY, animal.x, animal.y);

    if (d < animal.animalSize / 2) {
      animals.splice(i, 1);
      break;
    }
  }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
  background(250, 240, 230);
}
```

### Visual Elements

- Soft Shapes: Animal characters use round shapes and soft curves
- Bright Colors: Pastel tones create a friendly atmosphere
- Simple Animations: Animal tails appear when hovering
- Hand-drawn Feel: Crayon-like lines provide a natural drawing experience

### Sonic Elements

- Animal Sounds: Cute sound effects matching each animal's characteristics
- Feedback Sounds: Appropriate sound effects for drawing, animal creation, and disappearance
- Random Variations: Slightly different sounds each time to prevent boredom

### Interactive Elements

- Intuitive Drawing: Drawing function that naturally responds to mouse movements
- Shape Recognition: Different types of animals created based on the drawn shape
- Immediate Feedback: Visual/auditory elements that immediately respond to user actions
- Failure-free Creation: Designed so that all drawings get some form of response

## 3. Peer Feedback

### How well did I implement the cute aesthetic?

"I can't really find many aesthetically cute aspects yet. I think this part will gradually improve."

### How could I make it cuter?

"There are several ways, but one might be to create more detailed illustrations of dogs or cats. Alternatively, you could make it look cuter by inserting images."

### How could these improvements be implemented in JavaScript?

"First, it would be good to use image insertion features to display proper dog or cat shapes or images, not just the partially-formed ones that currently appear."
