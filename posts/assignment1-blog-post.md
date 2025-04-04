---
title: Cute! p5.js & the Aesthetics of Inclusion - Creating Connections Through Digital Pets
published_at: 2025-04-02
snippet: An interactive canvas where drawing creates connections with animal companions
disable_html_sanitization: true
allow_math: true
---

# Cute! p5.js & the Aesthetics of Inclusion

## Assignment Overview

For this assignment, I was tasked with creating a "cute offering" for a kindred spirit using p5.js. The requirements included:

- Creating a full-screen p5.js sketch
- Writing neat, commented code
- Incorporating basic JavaScript concepts
- Achieving a cute aesthetic in visual, sonic, and interactive domains

## Concept and Inspiration

My project explores the concept of connections and fate (인연) through interactive digital art. I designed a canvas where users can draw shapes to create animal companions (dogs or cats) that respond to interaction. This represents how connections in our lives appear, grow through interaction, and sometimes fade away.

The core metaphor is:

- The canvas represents "my world"
- Drawing with the mouse represents "my actions"
- The animals that appear represent "connections" or "kindred spirits"
- Interacting with them (hovering, clicking) represents how we nurture or end relationships

By using cute animal designs, playful interactions, and a warm aesthetic, I aimed to create a reflective but joyful experience around the ephemeral nature of connections.

## Technical Implementation

The application is built using p5.js and p5.sound libraries, with a focus on creating an engaging, interactive experience. Here's a breakdown of the major components and how they fulfill the assignment requirements:

### 1. Variables

The project uses numerous variables to manage the application state:

```javascript
// Main variables for the application
let strokes = []; // Array to store brush strokes when drawing
let animals = []; // Array to store animal objects
let grassBlades = []; // Array to store grass blade objects

// Sound-related variables
let bgMusic, dogSound, catSound, clickSound, drawSound; // Sound objects
let isPlayingBgMusic = false; // Flag to track if background music is playing
let soundEnabled = true; // Flag to enable/disable all sounds
let isPlaying = false; // Flag to track if drawing sound is playing

// Loading screen variables
let loadingComplete = false;
let loadingStartTime;
```

These variables store different aspects of the application state and control various features.

### 2. Functions

The project defines multiple custom functions beyond setup/draw:

```javascript
function preload() {
  // Load sound files
}

function showLoadingScreen() {
  // Display loading progress and instructions
}

function initializeApp() {
  // Set up application after loading
}

function createGrass() {
  // Generate grass blade objects
}

function drawGrass() {
  // Render grass blades with animation
}

function toggleSound() {
  // Toggle sound on/off
}

function toggleMusic() {
  // Toggle background music
}

function recognizeShape(strokes) {
  // Analyze drawn strokes to determine shape
}
```

These functions handle different aspects of the application logic, from initialization to user interaction handling.

### 3. Iteration

Iteration is used extensively throughout the project:

```javascript
// Generate background texture
for (let i = 0; i < 5000; i++) {
  let x = random(width);
  let y = random(height);
  let dotSize = random(1, 3);
  noStroke();
  fill(200, 180, 150, random(20, 50));
  ellipse(x, y, dotSize, dotSize);
}

// Create grass blades
for (let i = 0; i < density; i++) {
  // Create grass blade object
}

// Draw all animals
for (let i = 0; i < animals.length; i++) {
  animals[i].display();
  animals[i].update();
}

// Using forEach for shape recognition
strokes.forEach((s) => {
  points.push({ x: s.x1, y: s.y1 });
  points.push({ x: s.x2, y: s.y2 });
  avgX += s.x1 + s.x2;
  avgY += s.y1 + s.y2;
});
```

These loops and iterations handle repetitive tasks efficiently, from generating visual elements to processing data.

### 4. Boolean Logic

Boolean logic controls many aspects of the application:

```javascript
// Sound toggling
if (soundEnabled) {
  // Enable sounds
} else {
  // Disable sounds
}

// Animal growth
if (this.growing) {
  this.animalSize += (this.targetSize - this.animalSize) * 0.1;
  if (this.animalSize > this.targetSize * 0.95) {
    this.growing = false;
  }
}

// Hover detection
this.hover = d < this.animalSize / 2;
if (this.hover) {
  this.scale = lerp(this.scale, 1.1, 0.1);
} else {
  this.scale = lerp(this.scale, 1.0, 0.1);
}

// Shape recognition
if (variance < 400) {
  return "circle";
} else {
  return "triangle";
}
```

These conditional statements control program flow based on different states and user interactions.

### 5. Arrays

The project uses three main arrays to organize data:

```javascript
let strokes = []; // Stores drawing strokes
let animals = []; // Stores animal objects
let grassBlades = []; // Stores grass objects
```

Operations on these arrays include:

- Adding elements: `strokes.push(...)`, `animals.push(...)`, `grassBlades.push(...)`
- Removing elements: `animals.splice(i, 1)`
- Iteration: `for` loops and `forEach` methods
- Processing: Analyzing stroke data to recognize shapes

### 6. Classes

The project defines an `Animal` class to create custom objects:

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
    // Additional properties...
  }

  update() {
    // Update animal state
  }

  display() {
    // Render animal
  }

  makeSound() {
    // Play animal sounds
  }
}
```

This class encapsulates both data (properties) and behavior (methods) for animal objects, creating a clean, modular design.

### 7. Cute Visuals

The visual design incorporates many elements of cuteness:

- **Soft, rounded shapes**: All animals use rounded forms and smooth curves
- **Pastel colors**: Warm, gentle color palette with soft pastels
- **Animated growth**: Animals start small and grow to full size
- **Expressive features**: Different breeds with unique characteristics
- **Environmental details**: Soft textured background and animated grass
- **Visual feedback**: Subtle scale changes and tail animations on hover

These elements create a visually appealing, approachable aesthetic that conveys warmth and friendliness.

### 8. Cute Sound

Sound design is an integral part of the experience:

```javascript
function preload() {
  bgMusic = loadSound("background_music.mp3"); // Gentle background music
  dogSound = loadSound("dog_bark.mp3"); // Cute dog bark sound
  catSound = loadSound("cat_meow.mp3"); // Cat meow sound
  clickSound = loadSound("pop.mp3"); // Click sound for removing animals
  drawSound = loadSound("pencil.mp3"); // Drawing sound effect
}
```

- **Background music**: Peaceful, gentle music creates a calming atmosphere
- **Animal sounds**: Cute dog barks and cat meows give personality to the animals
- **Interaction sounds**: Drawing and clicking sounds provide immediate feedback
- **Sound control**: Options to toggle all sounds or just the background music

### 9. Cute Interaction

The interaction design focuses on simple, intuitive, and delightful experiences:

- **Drawing to create**: Drawing shapes creates animals, with different shapes producing different animals
- **Hover responses**: Animals react to mouse hover with scaling and tail animations
- **Click to remove**: Clicking animals removes them, with sound feedback
- **Keyboard controls**: Simple keyboard shortcuts for sound toggling and fullscreen mode
- **Forgiving input**: Shape recognition is designed to be forgiving, not requiring precise drawing

These interactions create a sense of agency and connection, reinforcing the metaphor of relationship formation.

## Code Style and Comments

I maintained a consistent coding style with proper indentation and clear organization. Comments are provided throughout the code to explain the purpose and functionality of different sections:

```javascript
/**
 * Creates grass blades along the bottom of the screen
 */
function createGrass() {
  grassBlades = []; // Clear existing grass

  let density = 350; // Number of grass blades
  let grassHeight = 50; // Base height of grass

  // Generate each grass blade with variations
  for (let i = 0; i < density; i++) {
    // Calculate position with slight randomness
    let x = map(i, 0, density - 1, 0, width) + random(-3, 3);
    let h = random(grassHeight * 0.8, grassHeight * 1.5);

    // Create grass blade object with properties for animation and appearance
    grassBlades.push({
      x: x, // X position
      y: height, // Y position (bottom of screen)
      height: h, // Height of the blade
      width: random(4, 8), // Width of the blade
      curve: random(-8, 8), // Curvature factor
      // More properties...
    });
  }
}
```

The comments explain the purpose of functions, the meaning of variables, and the logic behind different operations, making the code accessible to readers.

## Symbolic Meaning and Design Choices

Each element of the application was carefully designed to support the central metaphor of connections:

1. **Drawing Process**: The act of drawing represents our intentional actions in forming connections.
2. **Animal Variations**: The different breeds and colors reflect the diversity of connections we form.
3. **Growth Animation**: Animals start small and grow to full size, similar to how relationships develop.
4. **Hover Interactions**: When you hover over an animal, it responds - representing how connections thrive with attention.
5. **Removal Interaction**: Clicking an animal removes it, symbolizing how connections can end.
6. **Environmental Elements**: The grass and background create a world where these connections exist.
7. **Sound Design**: The audio elements add emotional depth to the experience.

## Reflection

This project allowed me to explore how interactive digital art can express abstract concepts like connections and fate. I learned valuable lessons about:

1. **Technical Integration**: Combining visual, audio, and interactive elements into a cohesive experience
2. **Metaphorical Design**: Using code to express emotional and philosophical concepts
3. **User Experience**: Creating intuitive, forgiving interactions that feel natural
4. **Performance Optimization**: Balancing visual complexity with smooth performance

The most rewarding aspect was seeing how small details - a wiggling tail, a gentle sound, a growing animation - can create a sense of life and personality that users connect with emotionally. This project reinforces that even simple interactions can express complex human concepts when designed thoughtfully.
