---
title: Assignment 1 - Idea 1
published_at: 2025-04-2
snippet: An interactive canvas where drawing creates connections with animal companions
disable_html_sanitization: true
allow_math: true
---

# Assignment 1: Kindred Spirits - Initial Concept

## Concept and Inspiration

For my Assignment 1, I wanted to explore the concept of "connections" or "fate" (인연) through interactive digital art. The idea is to create a world (canvas) where my actions (mouse drawings) can create new connections (dogs or cats) that interact with me and eventually fade away through interaction (clicks). This represents how connections in life can suddenly appear, develop through interaction, and sometimes disappear.

By expressing these connections through cute animals and soft, pastel colors, I aimed to create a warm, inviting experience that reflects on the ephemeral nature of relationships while maintaining a playful aesthetic.

## Visual Design Elements

The visual design includes several key elements:

1. **Textured Background**: A soft, warm canvas with subtle texture that represents "my world"
2. **Drawing Interface**: Crayon-like strokes that follow the mouse movement
3. **Animal Characters**: Cute, simplified cats and dogs with breed variations
4. **Grass Elements**: Swaying grass along the bottom edge to create a grounded environment
5. **Interactive Animations**: Animals that respond to hover with tail movements

The color palette consists primarily of soft pastels for the background, vibrant but gentle colors for the drawings, and carefully selected color variations for each animal breed to enhance the cute aesthetic.

## Technical Implementation

The code is structured into several major components:

### 1. Canvas Setup and Background Creation

```javascript
function setup() {
  createCanvas(windowWidth, windowHeight);
  background(250, 240, 230);

  // Generate grass blades along the bottom edge only
  createGrass();

  // Create background texture
  for (let i = 0; i < 5000; i++) {
    let x = random(width);
    let y = random(height);
    let dotSize = random(1, 3);
    noStroke();
    fill(200, 180, 150, random(20, 50));
    ellipse(x, y, dotSize, dotSize);
  }
}
```

The setup function initializes the canvas to fill the window and creates a textured background with thousands of tiny dots. This gives the canvas a warm, papery feel, enhancing the drawing experience. It also calls the `createGrass()` function to generate grass along the bottom edge.

### 2. Grass Generation System

```javascript
function createGrass() {
  // Clear existing grass
  grassBlades = [];

  // Number of grass blades along the bottom edge
  let density = 350; // Higher density
  let grassHeight = 50; // Longer grass

  // Create grass along bottom edge only
  for (let i = 0; i < density; i++) {
    let x = map(i, 0, density - 1, 0, width) + random(-3, 3);
    let h = random(grassHeight * 0.8, grassHeight * 1.5);
    // Thicker grass
    grassBlades.push({
      x: x,
      y: height,
      height: h,
      width: random(4, 8),
      curve: random(-8, 8),
      color: color(random(60, 120), random(160, 210), random(60, 100)),
      swaySpeed: random(0.01, 0.03),
      swayAmount: random(2, 4),
    });
  }
}

function drawGrass() {
  for (let blade of grassBlades) {
    push();
    noStroke();
    fill(blade.color);

    // Bottom edge grass
    let sway = sin(frameCount * blade.swaySpeed) * blade.swayAmount;

    beginShape();
    vertex(blade.x, height);
    bezierVertex(
      blade.x - blade.width / 2 + sway / 2,
      height - blade.height / 3,
      blade.x - blade.width / 2 + blade.curve + sway,
      height - (blade.height * 2) / 3,
      blade.x + sway,
      height - blade.height
    );
    bezierVertex(
      blade.x + blade.width / 2 + blade.curve - sway,
      height - (blade.height * 2) / 3,
      blade.x + blade.width / 2 - sway / 2,
      height - blade.height / 3,
      blade.x,
      height
    );
    endShape(CLOSE);
    pop();
  }
}
```

The grass system creates a natural environment at the bottom of the canvas. Each blade of grass has its own properties including position, height, width, curve, color, and sway animation parameters. The `drawGrass()` function renders each blade with a gentle swaying motion using sine waves, creating a peaceful, living environment where the animals exist.

### 3. Drawing System

```javascript
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
```

The drawing system tracks mouse movements and creates stroke objects that store the line's start and end points, thickness, and color. The slight randomness in position, weight, and color gives the drawing a natural, crayon-like quality. These strokes represent the active creation of connections through the user's actions.

### 4. Shape Recognition System

```javascript
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

  // Collect all points and calculate center
  strokes.forEach((s) => {
    points.push({ x: s.x1, y: s.y1 });
    points.push({ x: s.x2, y: s.y2 });
    avgX += s.x1 + s.x2;
    avgY += s.y1 + s.y2;
  });

  avgX /= points.length;
  avgY /= points.length;

  // Calculate distances from center
  let distances = [];
  points.forEach((p) => {
    distances.push(dist(avgX, avgY, p.x, p.y));
  });

  // Calculate average distance
  let avgDist = 0;
  distances.forEach((d) => (avgDist += d));
  avgDist /= distances.length;

  // Calculate variance of distances
  let variance = 0;
  distances.forEach((d) => {
    variance += (d - avgDist) * (d - avgDist);
  });
  variance /= distances.length;

  // Determine shape based on variance
  if (variance < 400) {
    return "circle";
  }

  return "triangle";
}
```

The shape recognition system analyzes the drawn strokes to determine what kind of animal to create. It works by calculating the variance in distance from the center point of all the strokes - a low variance suggests a circular shape (creating a dog), while a higher variance creates a cat. This system allows for intuitive creation without requiring perfect drawings, making the interaction accessible and forgiving.

### 5. Animal Class

```javascript
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

    // Generate random colors
    if (this.type === "dog") {
      // Dog breed (random integer between 0-3)
      this.breed = floor(random(4));

      // Dog colors (body, ears, eyes, nose/mouth)
      this.bodyColor = color(
        random(200, 255),
        random(180, 240),
        random(120, 200)
      );

      this.earColor = color(
        red(this.bodyColor) * random(0.7, 0.9),
        green(this.bodyColor) * random(0.7, 0.9),
        blue(this.bodyColor) * random(0.7, 0.9)
      );

      // Additional color properties...
    } else if (this.type === "cat") {
      // Similar color generation for cats...
    }
  }

  update() {
    // Growing animation
    if (this.growing) {
      this.animalSize += (this.targetSize - this.animalSize) * 0.1;
      if (this.animalSize > this.targetSize * 0.95) {
        this.growing = false;
      }
    }

    // Hover detection
    let d = dist(mouseX, mouseY, this.x, this.y);
    this.hover = d < this.animalSize / 2;

    // Scaling animation on hover
    if (this.hover) {
      this.scale = lerp(this.scale, 1.1, 0.1);
    } else {
      this.scale = lerp(this.scale, 1.0, 0.1);
    }

    // Tail wiggle animation
    this.wiggleAmount = sin(frameCount * this.wiggleSpeed) * 3;
  }

  display() {
    // Complex drawing code for different animal types and breeds...
  }
}
```

The Animal class is the most complex part of the code, handling the creation, appearance, and behavior of each animal. Key features include:

- **Growth Animation**: Animals start small and grow to their target size
- **Random Breed Selection**: Four different breeds for both cats and dogs
- **Color Variations**: Each animal has unique, harmonious color combinations
- **Hover Interactions**: Animals respond when the mouse hovers over them
- **Tail Animation**: Tails wiggle with unique speeds and amplitudes

The display method contains detailed drawing instructions for each breed of dog and cat, creating unique characters with distinct visual traits.

### 6. Interaction System

```javascript
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
```

The interaction system allows users to remove animals by clicking on them, representing how connections can end. The code checks if the mouse is over any animal during a click and removes it from the array if so.

## Current State and Future Improvements

This version represents my initial implementation of the concept. While the visual and interactive elements are working well, there are several planned improvements:

1. **Sound Elements**: Adding appropriate sounds for drawing, animal creation, and interactions
2. **Improved Shape Recognition**: Enhancing the algorithm to better distinguish different shapes
3. **Animation Refinements**: Adding more life-like behaviors and movements
4. **Background Elements**: More dynamic environmental elements
5. **Performance Optimization**: Reducing the computational load for smoother experience

## Reflection

Creating this project helped me explore how interactive digital art can express abstract concepts like connections and fate. The challenge of balancing technical implementation with aesthetic goals pushed me to develop both my coding and design skills.

The most rewarding aspect was seeing the animals come to life through small animations and interactions, creating a sense of personality and connection. The project reinforces how even simple interactions can create meaningful experiences when they're designed to express human concepts.
