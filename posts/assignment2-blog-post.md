---
title: Chaos! Ecological Aesthetics in the Postdigital
published_at: 2025-04-29
snippet: Digital visualization of mycelial networks inspired by fungal ecology
disable_html_sanitization: true
allow_math: true
---

# DMS4 Assignment 2: Mycelial Dreams - Digital Visualization of Mycelial Networks

## Project Overview

This project is an interactive digital art piece inspired by Merlin Sheldrake's essay "What Is It Like to Be A Fungus?" It expresses the growth and interactions of mycelial networks through interactive digital visualization.

## Development Process and Evolution

### Initial Concept

Initially, I aimed to represent the networked characteristics of fungi purely visually. I started with basic canvas setup and a particle system, attempting to express the network structure of mycelium through connections between particles.

### Adding Interactive Elements

Next, I added mouse interaction. To mimic how fungi respond to their environment, I implemented particles that move according to mouse position, and a feature that generates new mycelium when clicked.

### Implementation of Fractals and Recursion

A significant advancement was implementing fractal patterns through recursive functions. I developed the `drawFractal()` function to express the branching growth patterns of fungi, creating organic and natural growth patterns.

### Integration of Sonic Elements

I felt that visual elements alone couldn't fully express the multidimensional existence of fungi. Using the Web Audio API, I added a sound system that responds to particle interactions and fractal growth, providing an auditory representation of the invisible communication in fungal networks. The continuous and unexpected sounds that occur during growth emphasize complexity and indeterminacy, creating an effect different from what might be conventionally expected.

### Enhancement of Post-Digital Aesthetics

I added moiré patterns and glitch effects to strengthen the post-digital aesthetic. Specifically, the `drawMoirePattern()` and `applyGlitchEffect()` functions express the complexity and indeterminacy of fungal ecosystems.

### 3D Effects and Ecological Simulation

Finally, I implemented 3D depth by adding z-axis information to particles and created a simulation of "nutrient" exchange between particles to more vividly express the ecological characteristics of fungi.

## Technical Implementation

### Use of JavaScript Core Concepts

- **Variables and Constants**: Variables controlling particle characteristics, color ranges, noise scales, etc.
- **Loops**: Repetitive structures used for particle creation, updates, and connection exploration
- **Functions**: Modularized features (drawFractal, playTone, simulateMyceliumBehavior, etc.)
- **Boolean Logic**: Conditional interactions and event handling
- **Arrays**: Managing particle collections and storing color schemes
- **Classes**: Object-oriented design through the Particle class
- **Recursion**: Natural branching structures created through recursive calls to the drawFractal function

### Visual, Auditory, and Interactive Elements

- **Visual Chaos**: Noise-based movement, fractal patterns, moiré effects, glitches
- **Auditory Chaos**: Sound patterns that change according to distance, depth, and interaction
- **Interactive Chaos**: Organic system responding to mouse movements and clicks, color change functionality

## Philosophical Meaning

This work explores philosophical concepts through the mode of existence of fungi:

- **Distributed Intelligence**: The distributed intelligence structure of fungi, processing information through networks without a central brain
- **Interconnectedness**: The interdependent nature of ecosystems where all elements influence each other
- **Blurred Boundaries**: Like the relationship between individual particles and the entire network, fungi blur the boundaries between individual and collective
- **Non-linear Growth**: Like fractal patterns, fungi grow in unpredictable yet patterned ways

## Learning Reflection

Through this project, I was able to apply various JavaScript concepts including recursion, object-oriented programming, and audio APIs. In particular, I learned how to create organic patterns through noise functions and fractal generation algorithms.

The most challenging aspect was meaningfully integrating visual and auditory elements. I strived to build a sound system that conceptually connects to fungal ecology, rather than simply adding sound.

This experience taught me that code can have meaning beyond simple functional implementation. The process of exploring biological concepts and philosophical questions through code has shown new possibilities for connections between technology, art, and nature.

## Conclusion

"Mycelial Dreams" is an attempt to explore the worldview of fungi through code. It encourages viewing the world from the perspective of other life forms beyond human-centered thinking, and presents a new perspective on how we view life and intelligence through concepts such as network thinking, interconnectedness, and distributed intelligence.
