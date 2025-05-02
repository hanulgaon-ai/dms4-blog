---
title: Week 6-2 Blog
published_at: 2025-04-26
snippet: Exploring shaders and developing an interactive mycelial network visualization as a response to Merlin Sheldrake's essay
disable_html_sanitization: true
allow_math: true
---

# Week 6-2 Blog: Mycelial Network Visualization

## 1. Shader Implementation

For this week's assignment, I've implemented a simple fragment shader using Three.js that creates a flowing, organic effect. This shader will be incorporated into my final project to enhance the visual representation of mycelial networks.

```javascript
// Fragment shader implementation using Three.js
const fragmentShader = `
  uniform float time;
  uniform vec2 resolution;
  
  void main() {
    vec2 uv = gl_FragCoord.xy / resolution.xy;
    
    // Create organic flowing pattern
    float noise1 = sin(uv.x * 10.0 + time) * 0.5 + 0.5;
    float noise2 = cos(uv.y * 8.0 + time * 0.7) * 0.5 + 0.5;
    float combinedNoise = noise1 * noise2;
    
    // Color palette inspired by fungi
    vec3 color1 = vec3(0.2, 0.4, 0.5); // Dark blue-green
    vec3 color2 = vec3(0.8, 0.7, 0.3); // Mushroom yellow
    
    vec3 finalColor = mix(color1, color2, combinedNoise);
    
    gl_FragColor = vec4(finalColor, 1.0);
  }
`;

// This shader would be used with a Three.js setup
// to create flowing, fungal-inspired background effects
```

## 2. Selected Text for AT2

For my AT2 project, I've chosen to respond to **Merlin Sheldrake's "What Is It Like to Be A Fungus?"**. This text explores the decentralized intelligence of fungal networks and challenges our anthropocentric understanding of consciousness and connection.

## 3. Impactful Sentences from Sheldrake's Text

Three sentences that particularly inspired my approach:

1. "Fungal networks have no central command center and yet can coordinate their behavior across their entire body."
2. "The mycelial network is a living, constantly changing map of the fungus's recent history."
3. "Fungi form networks that link the roots of different plants, allowing them to exchange nutrients and information."

These concepts directly influenced my prototype's design, emphasizing decentralized networks, constant change, and interconnectedness.

## 4. Technical Approaches

My prototype combines two techniques from our coursework:

- **Recursion**: Implemented through the `drawBranch()` function that creates fractal-like mycelial structures
- **Glitch aesthetics**: The particles occasionally exhibit unpredictable behavior, representing the "noise" and unexpected connections in fungal networks

## 5. AT2 Prototype Draft

My prototype visualizes a mycelial network as an interactive particle system with branching structures. Here's a breakdown of the code:

```javascript
// Core functionality explained
class Particle {
  // Particles represent individual fungal cells
  // They move semi-randomly but respond to both
  // neighboring particles and user interaction

  update() {
    // Random movement with slight unpredictability
    // Plus response to mouse position (environmental stimulus)
  }

  draw() {
    // Visualization of the particle
  }
}

function drawBranch(x, y, angle, len, depth) {
  // Recursive function creating mycelial branches
  // This represents how fungi grow through branching patterns
  // The recursion depth controls the complexity
}

// The connection lines between particles represent
// the communication pathways in the mycelial network
```

The key conceptual connections to Sheldrake's text:

1. **Decentralized Intelligence**: The system has no central control point. Each particle follows simple rules, yet complex collective behavior emerges—just like fungal networks.

2. **Environmental Response**: Particles react to mouse position (representing environmental stimuli) similar to how fungi sense and respond to their environment.

3. **Network Formation**: Particles connect when close to each other, creating a dynamic network topology that constantly shifts and adapts.

4. **Recursive Growth**: The branching pattern created when clicking mimics how fungi extend mycelial threads through their environment in fractal-like patterns.

When you interact with the canvas:

- Mouse movement causes particles to move away (like fungi responding to environmental changes)
- Clicking creates branching structures (representing mycelial growth)
- Spacebar changes the color (representing different chemical signals or nutrients)

## 6. Peer Feedback

I wasn't able to gather feedback from three peers for this prototype due to scheduling constraints.

## 7. Next Development Steps

Based on my own critical evaluation, here are the key improvements planned for my AT2 project:

1. **Enhanced Biological Accuracy**: Refine particle behavior to more accurately reflect how fungal networks actually grow and respond to stimuli

2. **Incorporate Shader Effects**: Integrate the fragment shader to create a more immersive visual environment that better represents the organic nature of mycelial networks

3. **Data Visualization Component**: Add visualization of nutrient flows through the network, showing how resources move through mycelial connections

4. **Sound Design**: Add audio elements that respond to network activity, creating an auditory representation of fungal communication

5. **Narrative Elements**: Incorporate text elements from Sheldrake's essay that appear based on certain interaction patterns, helping viewers make connections between the visual experience and the concepts

These enhancements will help create a more complete and conceptually rich response to Sheldrake's exploration of fungal consciousness and interconnectedness.
