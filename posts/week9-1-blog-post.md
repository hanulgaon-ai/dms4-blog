---
title: "Week 9-1 Blog"
published_at: 2025-05-18
snippet: "Local LLM brainstorming for AT3 and Processing GIF creation"
disable_html_sanitization: true
allow_math: true
---

# Week 9-1 Blog

## Local LLM Brainstorming for AT3

I downloaded three different LLMs using Ollama: Llama 3.1, Mistral, and Qwen2. Here's how each helped brainstorm my CheckMate roommate app idea.

### Llama 3.1 Discussion

**Community Analysis:**

- Domain: Shared living space management
- Repertoire: Task tracking, fair cost splitting, conflict resolution
- Values: Transparency, fairness, accountability

**Code Ideas:**

- Real-time dashboard showing task completion
- Gamification with points and achievements
- Integration with calendar apps for scheduling

**Feasibility:** Suggested React Native for mobile, Node.js backend, SQLite for local storage.

### Mistral Discussion

**Community Focus:**

- Emphasized social dynamics over technical features
- Suggested incorporating behavioral psychology
- Recommended gradual feature rollout

**Code Ideas:**

- Social pressure mechanics through visibility
- Anonymous feedback system
- Habit tracking integration

**Feasibility:** Recommended starting with web app, then mobile. Suggested Firebase for quick deployment.

### Qwen2 Discussion

**Practical Approach:**

- Focused on MVP features first
- Discussed data privacy concerns
- Suggested offline-first architecture

**Code Ideas:**

- Simple check-in system with photo verification
- Automated expense calculation
- Export functionality for settlements

**Feasibility:** Recommended Progressive Web App, local storage first, cloud sync optional.

### LLM Comparison

Llama 3.1 was most technical and comprehensive. Mistral focused on social aspects and user psychology. Qwen2 was practical and privacy-focused. All three provided useful but different perspectives.

## Processing GIF Creation

Following the bleuje tutorial on morphing shapes, I created a GIF showing geometric patterns transforming through time.

```processing
// Core animation loop
void draw() {
  background(20);
  translate(width/2, height/2);

  for(int i = 0; i < 8; i++) {
    pushMatrix();
    rotate(TWO_PI * i / 8);

    // Morphing between circle and square
    float t = (frameCount * 0.02) % 1.0;
    float morph = sin(t * PI);

    drawMorphShape(morph, 100);
    popMatrix();
  }

  saveFrame("frames/frame####.png");
}

void drawMorphShape(float morph, float size) {
  beginShape();
  for(int i = 0; i < 100; i++) {
    float angle = map(i, 0, 100, 0, TWO_PI);

    // Interpolate between circle and square
    float circleX = cos(angle) * size;
    float circleY = sin(angle) * size;

    float squareX = size * (cos(angle) > 0 ? 1 : -1);
    float squareY = size * (sin(angle) > 0 ? 1 : -1);

    float x = lerp(circleX, squareX, morph);
    float y = lerp(circleY, squareY, morph);

    vertex(x, y);
  }
  endShape(CLOSE);
}
```

The tutorial's morphing concept worked well but I added rotational symmetry and color transitions. Converting frames to GIF using ImageMagick was straightforward.

The process helped me understand how mathematical interpolation creates smooth animations. Could be useful for the CheckMate app's progress visualizations.
