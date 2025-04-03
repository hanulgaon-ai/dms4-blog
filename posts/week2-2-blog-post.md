---
title: Week 2-2 Blog
published_at: 2025-03-19
snippet: Developing the concept for Assignment 1 - Kindred Spirit
disable_html_sanitization: true
allow_math: true
---

# Week 2-2 Blog

## 1. Describing the "Kindred Spirit" for AT1

### What is your relationship with it?

My relationship with it is 'fate' or 'connection'. Through my actions (mouse movements), a clear relationship with it (dog form or cat form) is formed and interacted with. Like all connections, it can suddenly appear or disappear at any moment. However, I believe that my actions and choices can form these connections, and I wanted to make this visible through this assignment.

### What is your common purpose?

Our common purpose is to interact with each other through my actions and create certain outcomes. For example, I want to express how my movements can lead to meeting new kindred spirits or causing them to disappear.

### What challenge or enemy do you face together?

The challenge we face together is how to deal with this connection. Will it eventually disappear, or will we try to preserve it?

## 2. Expanding on the Visual, Sonic, and Interactive Elements

### Visual Elements

Visually, I want to create a blank canvas (my world) where drawings (my actions through the mouse) form animals (the connections I can make).

### Sonic Elements

For sound, I want to include appropriate audio effects when animals (connections) are formed through my drawings (mouse actions). For example, when a dog is created, a "woof" sound would play, or when a cat is created, a "meow" sound would play.

### Interactive Elements

For interactive elements, I first need interaction to form animals (connections) through drawing (mouse actions). I also want to express how these connections can end through interactions like mouse clicks with the created animals.

Below is a code that attempts to create dogs or cats when I draw shapes on the canvas, and make them disappear when clicked:

```javascript
let strokes = [];
let animals = [];

function setup() {
  createCanvas(windowWidth, windowHeight);
  background(245, 230, 200);

  for (let i = 0; i < 5000; i++) {
    let x = random(width);
    let y = random(height);
    let alpha = random(50, 100);
    noStroke();
    fill(200, 180, 150, alpha);
    ellipse(x, y, 2, 2);
  }
}

function draw() {
  background(245, 230, 200);

  for (let i = strokes.length - 1; i >= 0; i--) {
    let strokeData = strokes[i];
    let age = millis() - strokeData.time;
    let alpha = map(age, 0, 3000, 255, 0);

    if (alpha <= 0) {
      strokes.splice(i, 1);
    } else {
      stroke(
        strokeData.color.levels[0],
        strokeData.color.levels[1],
        strokeData.color.levels[2],
        alpha
      );
      strokeWeight(strokeData.size);
      line(strokeData.x1, strokeData.y1, strokeData.x2, strokeData.y2);
    }
  }

  for (let i = animals.length - 1; i >= 0; i--) {
    animals[i].display();
  }
}

function mouseDragged() {
  let brushSize = random(5, 15);
  let colorVariation = random(180, 220);
  let currentTime = millis();

  for (let i = 0; i < 3; i++) {
    let xOffset = random(-2, 2);
    let yOffset = random(-2, 2);
    strokes.push({
      x1: mouseX + xOffset,
      y1: mouseY + yOffset,
      x2: pmouseX + xOffset,
      y2: pmouseY + yOffset,
      size: brushSize,
      color: color(
        colorVariation,
        colorVariation - 20,
        colorVariation - 40,
        200
      ),
      time: currentTime,
    });
  }
}

function mouseReleased() {
  let shape = recognizeShape(strokes);

  if (shape === "circle") {
    animals.push(new Animal(mouseX, mouseY, "dog"));
  } else if (shape === "triangle") {
    animals.push(new Animal(mouseX, mouseY, "cat"));
  }
}

function recognizeShape(points) {
  if (points.length < 10) return null;

  let centerX = 0,
    centerY = 0;
  points.forEach((p) => {
    centerX += (p.x1 + p.x2) / 2;
    centerY += (p.y1 + p.y2) / 2;
  });
  centerX /= points.length;
  centerY /= points.length;

  let totalDist = 0;
  points.forEach((p) => {
    totalDist += dist(centerX, centerY, (p.x1 + p.x2) / 2, (p.y1 + p.y2) / 2);
  });
  let avgDist = totalDist / points.length;

  let variance = 0;
  points.forEach((p) => {
    let d = dist(centerX, centerY, (p.x1 + p.x2) / 2, (p.y1 + p.y2) / 2);
    variance += pow(d - avgDist, 2);
  });
  variance /= points.length;

  if (variance < 100) return "circle";

  if (points.length >= 5) {
    let corners = [
      points[0],
      points[floor(points.length / 2)],
      points[points.length - 1],
    ];
    let angles = [];
    for (let i = 0; i < 3; i++) {
      let a = corners[i];
      let b = corners[(i + 1) % 3];
      let c = corners[(i + 2) % 3];
      let angle = degrees(
        atan2(c.y1 - b.y1, c.x1 - b.x1) - atan2(a.y1 - b.y1, a.x1 - b.x1)
      );
      angles.push(abs(angle));
    }

    let sumAngles = angles.reduce((sum, a) => sum + a, 0);
    if (sumAngles > 250 && sumAngles < 290) return "triangle";
  }

  return null;
}

class Animal {
  constructor(x, y, type) {
    this.x = x;
    this.y = y;
    this.type = type;
    this.size = 50;
  }

  display() {
    if (this.type === "dog") {
      fill(200, 150, 50);
      ellipse(this.x, this.y, this.size, this.size);
      ellipse(this.x - 20, this.y - 20, 20, 20);
      ellipse(this.x + 20, this.y - 20, 20, 20);
    } else if (this.type === "cat") {
      fill(150, 100, 200);
      triangle(
        this.x - 25,
        this.y + 20,
        this.x + 25,
        this.y + 20,
        this.x,
        this.y - 20
      );
      triangle(
        this.x - 15,
        this.y - 20,
        this.x - 5,
        this.y - 40,
        this.x + 5,
        this.y - 20
      );
      triangle(
        this.x + 5,
        this.y - 20,
        this.x + 15,
        this.y - 40,
        this.x + 25,
        this.y - 20
      );
    }
  }
}

function mousePressed() {
  for (let i = animals.length - 1; i >= 0; i--) {
    let a = animals[i];
    if (dist(mouseX, mouseY, a.x, a.y) < a.size / 2) {
      animals.splice(i, 1);
      return;
    }
  }
}
```

The code has several issues: the animals don't generate properly, their appearance isn't well implemented, and the sound interaction is still lacking.

## 3. Class Example Code

I couldn't solve this on my own, so I'm working to understand the code provided by the professor during class. There are still many parts I don't understand, but I'm using AI to help me comprehend it.

```javascript
// declaring a variable and assigning to it, an empty object
const faller = {};

// declaring a variable and assigning to it, an empty array
const fallers = [];

// variable to store background colour
let bg;

// defining a setup function
function setup() {
  // creating a canvas
  // make it the same size as the container window
  createCanvas(innerWidth, innerHeight);

  // no outlines
  noStroke();

  // hue / saturation / brightness colour mode
  colorMode(HSB);

  // put two random colours in an array
  // assign to .colours attributs of faller object
  faller.colours = [rand_col(), rand_col()];

  // assign to .start_points attribute of faller object
  // an array
  faller.start_points = [
    // object literal syntax
    // http://shorturl.at/Vddy0
    // each one is a starting coordinate
    { x: 0, y: height / 2 },
    { x: 0, y: 0 },
    { x: width / 4, y: 0 },
    { x: width / 2, y: 0 },
    { x: (width * 3) / 4, y: 0 },
    { x: width, y: 0 },
    { x: width, y: height / 2 },
  ];

  // assign an empty array to the .end_points attribute
  // of the faller object
  faller.end_points = [];

  // iterating through 7 coordanates
  // across the bottom of the canvas
  for (let i = 1; i < 8; i++) {
    // push the constructed object
    // into the array stored in faller.end_points
    faller.end_points.push({
      // iterate across the x-asis
      x: (i * width) / 8,

      // y-coorinate stays the same
      y: height,
    });
  }

  // construct an array with 7 random values
  // between 1 & 3
  faller.curves = new Array(7).fill().map(rand_curve);

  // assign 0 to the .phase attribute of the faller function
  faller.phase = 0;

  // push a copy of the faller object
  // into the fallers array
  fallers.push(Object.assign({}, faller));

  // assign to bg a random colour
  bg = rand_col();
}

// define a draw function
function draw() {
  // set the background colour to be whatever colour is in bg
  background(bg);

  // whonever frameCount is a multiple of 40
  if (frameCount % 40 == 0) {
    // make a copy of the faller object
    // assign it to the newly declared new faller variable
    const new_faller = Object.assign({}, faller);

    // make the first colour of the .colours array
    // the same as the background
    // set the second colour to be a random colour
    new_faller.colours = [bg, rand_col()];

    // give a different set of 7 random values
    // between 1 & 3, in an array, on the .curves attribute
    new_faller.curves = new Array(7).fill().map(rand_curve);

    // add the new_faller to the start of an array
    // fallers.reverse ()
    // fallers.push (new_faller)
    // fallers.reverse ()

    //even better
    fallers.unshift(new_faller);

    // setting the background to be a new random colour
    bg = rand_col();
  }

  // make an empty array for the redundant fallers
  const redundant = [];

  // go through each faller in the fallers array
  fallers.forEach((f, i) => {
    // change the colour mode to RGB
    colorMode(RGB);

    // change the fill colour to be somewhere between the
    // colours stored in the faller's .colours array
    fill(lerpColor(f.colours[0], f.colours[1], f.phase));

    // start beginShape
    beginShape();

    // start in the bottom left
    vertex(0, height);

    // go through the starting points
    f.start_points.forEach((s, i) => {
      // find a new point based on the starting point,
      // ending point, and phase (and curve)
      const p = find_point(s, f.end_points[i], f.phase ** f.curves[i]);

      // draw a corner here
      vertex(p.x, p.y);
    });

    // last corner in bottom right
    vertex(width, height);

    // end the shape
    endShape();

    // increment the phase
    f.phase += 0.008;

    // if the phase >1, push into the redundant array
    if (f.phase > 1) redundant.push(i);
  });

  // for each of the fallers in the redundant array
  // splice the faller out of the fallers array
  redundant.forEach((n) => fallers.splice(n, 1));
}

// lerping between coordinates
function find_point(start, end, phase) {
  const delt = {
    x: end.x - start.x,
    y: end.y - start.y,
  };
  const x = start.x + delt.x * phase;
  const y = start.y + delt.y * phase;
  return { x, y };
}

function rand_col() {
  colorMode(HSB);
  const h = floor(random() * 360);
  return color(h, 100, 100);
}

function rand_curve() {
  // return a random value between 1 and 3
  return random() * 2 + 1;
}
```

## 4. Class Implementation with Constructor

```javascript
class Faller {
  constructor(bg) {
    this.colours = [bg, rand_col()];
    faller.start_points = [
      { x: 0, y: height / 2 },
      { x: 0, y: 0 },
      { x: width / 4, y: 0 },
      { x: width / 2, y: 0 },
      { x: (width * 3) / 4, y: 0 },
      { x: width, y: 0 },
      { x: width, y: height / 2 },
    ];
    this.end_points = [];
    for (let i = 1; i < 8; i++) {
      this.end_points.push({
        x: (i * width) / 9,
        y: height,
      });
    }
    this.curves = new Array(7).fill().map(rand_curve);
    this.phase = 0;
  }
}

function rand_curve() {
  return random() * 2 + 1;
}

function rand_col() {
  colorMode(HSB);
  const h = floor(random() * 360);
  return color(h, 100, 100);
}
```
