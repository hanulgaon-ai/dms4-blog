---
title: Week 5-1 Blog
published_at: 2025-04-12
snippet: Analysis of a Post-Digital artist and poetry generation using RiTa.js
disable_html_sanitization: true
allow_math: true
---

# Week 5-1 Blog: Analysis of Post-Digital Art

## 1. Selection of a Post-Digital Artist

The Post-Digital artist I've selected is **Rafael Lozano-Hemmer**. His work "Pulse Room" (2006) is an interactive installation that captures visitors' heartbeats and transforms them into light patterns in hundreds of light bulbs suspended from the ceiling. When a visitor holds the sensor, their pulse is recorded and the bulbs flash to the rhythm of their heartbeat. Each new participant's pulse pushes out the previous participant's pulse, filling the space with a collective memory of constantly changing light patterns.

## 2. Why is this Artist "Post-Digital"?

According to Florian Cramer's essay "What is Post-Digital?", post-digital refers to an approach that uses digital technology as an everyday background rather than something "new and innovative." Lozano-Hemmer's work can be considered post-digital for the following reasons:

1. **Physical-Digital Hybridization**: His work seamlessly combines analog elements (light bulbs, human bodies) with digital systems (heart rate sensors, programming). Technology is not an end in itself but a tool for mediating human experience.

2. **Backgrounding of Technology**: In "Pulse Room," digital technology recedes from being the center of attention and instead becomes a means of visualizing human biometric signals and collective presence.

3. **Return to Analog**: While using advanced sensor technology, the final output is an analog expression in the form of flickering incandescent light bulbs.

## 3. Analysis of Technology Used

"Pulse Room" utilizes the following technologies:

- **Hardware**: Pulse sensors, microcontrollers, electromagnetic relays, incandescent light bulbs, custom interface
- **Software**: Custom software for processing pulse data, algorithms for controlling light patterns
- **Network Systems**: Real-time network for transmitting data from sensors to light bulbs

## 4. If this Work Were Created in JavaScript?

If "Pulse Room" were implemented in JavaScript, the following libraries could be utilized:

1. **p5.js**: For creating visual representations of light on canvas
2. **Tone.js**: For generating sounds synchronized to heartbeats
3. **ml5.js**: For pulse detection through webcam (using rPPG technology)
4. **Socket.io**: For real-time data sharing for multi-user experiences

## 5. Poetry Generation with RiTa.js

```javascript
let ritaPoem;

function setup() {
  createCanvas(600, 400);
  textSize(16);
  textAlign(CENTER, CENTER);

  let heartWords = RiTa.markov(3);
  heartWords.addText(
    "Pulse rhythm light signal connection human technology heartbeat memory presence absence collective individual transient eternal analog digital physical virtual embodied disembodied visible invisible"
  );

  ritaPoem = heartWords.generate(7);
}

function draw() {
  background(0);
  fill(255);

  let lines = ritaPoem.split(/[,.] /);
  let y = 100;

  for (let line of lines) {
    text(line, width / 2, y);
    y += 30;
  }

  // Visual effect: light waves representing heartbeats
  let pulseSize = map(sin(frameCount * 0.05), -1, 1, 50, 100);
  noFill();
  stroke(255, 100);
  ellipse(width / 2, height / 2, pulseSize, pulseSize);
}
```

### Generated Poem: Pulse Echoes

```
Heartbeat visible in collective rhythm
Light connects physical presence
Digital signals embody human memory
Technology transforms invisible pulses
Eternal connection between analog and virtual
Transient light reveals individual presence
Pulse echoes across digital space
```

## Bonus: Enhanced Presentation

Additionally, Three.js could be used to visualize heartbeats in 3D space. Glowing spheres could change size according to heartbeats, and each line of the poem could be represented as floating text in 3D space. This would recreate the spatial qualities of Lozano-Hemmer's physical installation in a digital environment.
