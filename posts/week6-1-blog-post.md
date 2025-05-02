---
title: Week 6-1 Blog
published_at: 2025-04-22
snippet: Exploring signal-based JavaScript libraries and their connection to postdigital philosophy
disable_html_sanitization: true
allow_math: true
---

# Week 6-1 Blog: Signal-Based Libraries & Postdigital Connections

## 1. JavaScript Libraries for Creative Coding

### q5.js

Q5.js is a creative coding library inspired by p5.js but focused on signal processing tools. It provides components like "Envelope", "Signal", and "Oscillator" that make it excellent for creating time-based transformations and audio-visual effects. This library particularly excels at managing smooth transitions and temporally-controlled animations.

### c2.js

C2.js specializes in mathematical expressions for creative coding. It offers powerful tools for working with geometric shapes, vector operations, and mathematical visualization. The library makes it easier to create elegant, mathematically-driven animations and visualizations based on complex formulas.

### svg.js

SVG.js is designed specifically for manipulating and animating SVG graphics on the web. It provides an intuitive interface for creating, modifying, and transforming vector graphics with smooth animations. Being DOM-based, it integrates well with other web technologies.

## 2. Comparative Analysis

| Library | Main Purpose               | Key Features                        | Ideal Use Cases                              |
| ------- | -------------------------- | ----------------------------------- | -------------------------------------------- |
| q5.js   | Signal/time-based effects  | Envelope, Signal, oscillation tools | Audio visualizations, interactive animations |
| c2.js   | Mathematical visualization | Vector/function focused             | Abstract geometry, computational aesthetics  |
| svg.js  | SVG graphic control        | DOM-based, animation capabilities   | Web UI, icons, vector animations             |

For my chaos-based ecological aesthetics project, q5.js offers the most relevant tools. Its signal processing capabilities align perfectly with creating organic, evolving visual patterns that mimic natural systems, which connects directly to Sheldrake's ideas about fungal networks.

## 3. JavaScript Module Compatibility

All three libraries can be used in JavaScript modules with different approaches:

- Q5.js and c2.js: These newer libraries support ES Modules natively
- SVG.js: Primarily designed for CommonJS but can be used with ES Modules through bundlers or CDN services

For my project, using q5.js through ES Modules will allow clean integration of signal-based animations with other components.

## 4. ESM.sh Utility

ESM.sh is particularly useful when working with libraries that don't natively support ES Modules. It converts CommonJS packages to ES Module format on-the-fly, enabling direct imports in modern JavaScript environments without complex build processes.

Example import using esm.sh:

```javascript
import * as q5 from "https://esm.sh/q5.js";
```

This approach will be valuable for my project as it allows rapid prototyping and testing of different libraries without complex local setup.

## 5. Signal-Based Animation Demo

```javascript
// Simple q5.js demo showing signal-based animation
import { createQ5 } from "https://esm.sh/q5.js";

const sketch = (q5) => {
  // Create an envelope with attack, decay, sustain, release
  const envelope = q5.createEnvelope(0.5, 1, 0.8, 2);
  let size;

  q5.setup = () => {
    q5.createCanvas(400, 400);
    q5.background(240);
    // Trigger the envelope every 3 seconds
    setInterval(() => envelope.trigger(), 3000);
  };

  q5.draw = () => {
    q5.background(240, 10);

    // Get current value from the envelope
    const value = envelope.value();

    // Map the envelope value to size and color
    size = q5.map(value, 0, 1, 20, 200);
    const hue = q5.map(value, 0, 1, 0, 360);

    q5.noStroke();
    q5.fill(hue, 80, 80);

    // Draw multiple circles with sizes based on the envelope
    for (let i = 0; i < 5; i++) {
      const angle = (i * q5.TWO_PI) / 5;
      const radius = 100 * value;
      const x = q5.width / 2 + q5.cos(angle) * radius;
      const y = q5.height / 2 + q5.sin(angle) * radius;
      q5.circle(x, y, size * (1 - i / 5));
    }
  };
};

// Initialize q5
createQ5(sketch);
```

This demo creates an organic, breathing effect using q5.js's envelope system. The circles expand and contract while changing color, mimicking organic growth patterns. This connects conceptually to my final project on ecological aesthetics, where I'm exploring similar organic, evolving visual systems.

## 6. Reading Reflections & Project Connections

### Michel Serres - Information & Thinking

Serres views information not as static data but as dynamic flows that stimulate thought. This perspective aligns with my project's use of signal-based animations, where visual information constantly evolves and invites ongoing interpretation rather than presenting fixed meanings.

### Merlin Sheldrake - What Is It Like to Be A Fungus?

Sheldrake's exploration of fungal networks as decentralized intelligence systems beautifully parallels the signal-processing approaches in q5.js. My project aims to visualize this kind of decentralized, interconnected system where small changes propagate through the entire network—much like how mycorrhizal networks function in nature.

### Laboria Cuboniks - Xenofeminism

Xenofeminism's focus on reconfiguring technology and embracing the "alien" connects to my project's aesthetic approach. By using technology to create emergent, somewhat unpredictable visual patterns, I'm exploring how digital tools can create aesthetics that feel simultaneously technological and organic—challenging the binary thinking that separates the two.

My chaos-based ecological aesthetics project draws from all three texts by embracing technology as a means to model and understand organic systems, using generative algorithms to create art that evolves in ways that mimic biological processes while remaining distinctly digital.
