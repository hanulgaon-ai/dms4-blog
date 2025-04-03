---
title: Week 3-2 Blog
published_at: 2025-03-25
snippet: Understanding programming concepts in my AT1 project
disable_html_sanitization: true
allow_math: true
---

# Week 3-2 Blog

## 1. How I'm Utilizing Programming Concepts in AT1

### Variables

My code uses variables to store and manage various data:

1. **Global Variables**:

   - `strokes` - Array storing the user's drawing strokes
   - `animals` - Array storing the generated animal objects

2. **Local Variables**:

   - Variables like `weight`, `r`, `g`, `b` in the `mouseDragged()` function for line thickness and color values
   - Variables like `avgX`, `avgY`, `variance` in the `recognizeShape()` function for shape recognition calculations

3. **Object Property Variables**:
   - Properties in the Animal class such as `this.x`, `this.y`, `this.type`, etc.

### Functions

The code is structured with functions for various purposes:

1. **p5.js Basic Functions**:

   - `setup()` - Initializes the canvas and sets the background
   - `draw()` - Updates the screen for each animation frame
   - `mousePressed()`, `mouseDragged()`, `mouseReleased()` - Handles mouse events

2. **Custom Functions**:

   - `recognizeShape()` - Analyzes user-drawn patterns and identifies them as circles or triangles

3. **Class Methods**:
   - `Animal.update()` - Updates the state of animal objects
   - `Animal.display()` - Method for drawing animals on screen

### Iteration

Loops are used to process multiple elements or generate graphics:

1. **Background Dot Generation**:

   ```javascript
   for (let i = 0; i < 5000; i++) {
     // Randomly generate small dots for the background
   }
   ```

2. **Stroke Processing**:

   ```javascript
   for (let i = 0; i < strokes.length; i++) {
     // Draw each stroke line
   }
   ```

3. **Updating and Displaying All Animals**:

   ```javascript
   for (let i = 0; i < animals.length; i++) {
     animals[i].display();
     animals[i].update();
   }
   ```

4. **Functional Iteration Over Arrays**:
   ```javascript
   strokes.forEach((s) => {
     // Process each stroke
   });
   ```

### Boolean Logic

Boolean logic is used for conditional execution and state management:

1. **Conditional Animal Creation**:

   ```javascript
   if (shape === "circle") {
     animals.push(new Animal(mouseX, mouseY, "dog"));
   } else if (shape === "triangle" || shape === "line") {
     animals.push(new Animal(mouseX, mouseY, "cat"));
   }
   ```

2. **Shape Recognition**:

   ```javascript
   if (variance < 400) {
     return "circle";
   }
   ```

3. **State Change Conditions**:

   ```javascript
   if (this.growing) {
     // Size increase logic
     if (this.animalSize > this.targetSize * 0.95) {
       this.growing = false;
     }
   }
   ```

4. **Mouse Hover Detection**:
   ```javascript
   this.hover = d < this.animalSize / 2;
   ```

### Arrays

Arrays are used to manage multiple data elements:

1. **Stroke Recording**:

   ```javascript
   strokes.push({
     x1: mouseX + xOffset,
     y1: mouseY + yOffset,
     // Other properties
   });
   ```

2. **Animal Object Management**:

   ```javascript
   animals.push(new Animal(mouseX, mouseY, "dog"));
   ```

3. **Point Collection for Shape Recognition**:

   ```javascript
   let points = [];
   // Add points
   points.push({ x: s.x1, y: s.y1 });
   ```

4. **Array Item Removal**:
   ```javascript
   animals.splice(i, 1);
   ```

### Classes

The code defines an `Animal` class for object-oriented programming:

1. **Class Definition**:

   ```javascript
   class Animal {
     constructor(x, y, type) {
       // Initialization code
     }

     update() {
       // State update method
     }

     display() {
       // Animal drawing method
     }
   }
   ```

2. **Polymorphism without Inheritance**:
   - Different animal shapes (cat or dog) are drawn based on the `type` property

This code effectively combines various programming concepts to implement an interactive graphic application, collecting user input, recognizing patterns, and processing various visual elements.

## 2. Current Updated Code

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

## 3. Discussion of Initial AT1 Version

### How well have I implemented 'cuteness' in visual, sonic, and interactive aspects?

I've implemented cuteness through round shapes, pastel color tones, smooth animations, and responsive interactions, though the current version lacks sound elements.

### What communities and learning resources did I use in the learning process?

The biggest help came from ChatGPT, which guided me step by step in implementing what I wanted for my project. It helped me with everything from creating the white canvas background to how to guide drawing and express the right feeling in each component.

### What was the most enjoyable part of this process? What was most surprising?

The character design and interaction implementation process was the most enjoyable, and I was surprised that effective shape recognition was possible with relatively simple algorithms.

### What was the most difficult part? What was most confusing?

Developing accurate shape recognition algorithms and optimizing performance was difficult, and understanding the p5.js coordinate system and event sequence was confusing. It was also challenging to refresh the code when errors occurred, and with so much code being used, conflicts seemed to happen frequently.
