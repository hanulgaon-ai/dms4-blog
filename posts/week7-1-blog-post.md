---
title: Week 7-1 Blog
published_at: 2025-04-29
snippet: Sound design for fungal network visualization
disable_html_sanitization: true
allow_math: true
---

# Week 7-1 Blog: Chaotic Sound Design

## 1. Sound Design Plan for AT2 Project

I've planned a chaotic sound design to complement my fungal network visualization:

### In terms of effective complexity:

- **Structure**: Combining basic patterns with randomness to represent both regularity and variation in mycelial growth
- **Noise vs. Sound**: Finding balance between complete noise and musical structure to express how fungi respond to environmental stimuli
- **Voice-like elements**: Implementing resonance and modulation to create sound patterns that suggest fungal "communication"

### Role of de-familiarization:

Subtly transforming natural sounds to guide listeners toward experiencing sound in new ways

### Inspiring sound references:

1. MyNoise Forest generator - For representing microscopic sounds of natural environments
2. Pink Trombone - For organic sound generation methods
3. Thunder generator - For expressing signal transmission across fungal networks

## 2. Sound Design Experiment

```javascript
// Core audio elements
let synths = []; // Representing mycelial strands
let noiseGen = []; // Representing environmental elements
let chaosLevel = 0; // Degree of chaos

// Using sinusoid for 24-second cycle of chaos
function updateChaos(time) {
  chaosLevel = (1 + Math.sin((time * Math.PI) / 12)) / 2;
}

// Generating sound through user interaction
function createSound(x, y) {
  // Converting x position to pitch, y position to sound duration
  const note = getNoteFromPosition(x);
  const duration = getDurationFromPosition(y);

  // Modifying sound characteristics based on chaos level
  playSoundWithChaos(note, duration, chaosLevel);
}
```

This experiment uses Tone.js to create a sonic representation of fungal networks:

1. Multiple sound layers representing mycelium and environment
2. A 24-second cycle that shifts from order to chaos and back
3. Mouse/touch interaction for user engagement

### Evaluation

This sound design achieves effective complexity by balancing structure and disorder. In future iterations, I plan to develop more sophisticated sound patterns using actual fungal growth data.
