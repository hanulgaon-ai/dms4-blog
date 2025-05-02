---
title: Week 7-2 Blog
published_at: 2025-05-03
snippet: Exploring zaniness and fungal network visualization project analysis
disable_html_sanitization: true
allow_math: true
---

# Week 7-2 Blog: Zaniness and AT2 Project

## 1. Reflections on Zaniness

### The meaning of "the zany works against its constraints"

Zaniness actively twists and violates rules rather than following them. While the interesting operates within existing order, the zany strives to push beyond boundaries.

### Comparing chaos and zaniness

**Similarities**: Both exhibit disorder and unpredictability.  
**Differences**: Chaos is neutral, while zaniness contains intentionality and human energy.

### Zany aspects of my AT2

- How particles excessively react to mouse movements
- Unpredictable branching patterns
- Unstable transitions between order and disorder

### Making it more zany

- Adding exaggerated responses to user input
- Giving particles "personalities"
- Incorporating intentional glitch elements

## 2. AT2 Code Analysis

### Key code elements

**Variables**: `particles`, `hue`, `mouseX`, `mouseY`, `isPressed`, etc. track system state

**Iteration**: For loops used for particle creation and updates

```javascript
for (let i = 0; i < particles.length; i++) {
  particles[i].update();
  particles[i].draw();
}
```

**Functions**:

```javascript
function dist(x1, y1, x2, y2) {
  return Math.sqrt((x2 - x1) * (x2 - x1) + (y2 - y1) * (y2 - y1));
}
```

**Boolean logic**:

```javascript
if (isPressed) {
  drawBranch(mouseX, mouseY, -Math.PI / 2, 20, 3);
}
```

**Arrays**: `particles` array manages all fungal particles

**Classes**: `Particle` class defines properties and behaviors of each fungal cell

**Recursion**:

```javascript
function drawBranch(x, y, angle, len, depth) {
  // Draw base branch
  drawBranch(endX, endY, angle + 0.5, len * 0.7, depth - 1);
  drawBranch(endX, endY, angle - 0.5, len * 0.7, depth - 1);
}
```

### Response to Sheldrake's text

1. Distributed network structure representing fungi's decentralized nature
2. Particles responding to environmental stimuli (mouse)
3. Lines visualizing interconnectedness of fungal networks

### Post-digital characteristics

1. Using digital tools to represent biological systems
2. Embracing noise and imperfection as aesthetic elements
3. Emphasizing interaction between audience and system
