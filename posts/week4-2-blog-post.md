---
title: Week 4-2 Blog
published_at: 2025-04-05
snippet: Exploring glitch aesthetics and pixel sorting techniques applied to self-portraiture
disable_html_sanitization: true
allow_math: true
---

# Week 4-2 Blog

## 1. Applying Glitch/Pixel Sorting Techniques to Self-Portrait

Below is my implementation of a real-time glitch effect applied to webcam capture. The technique creates a self-portrait through random pixel sampling and variable-sized squares, resulting in a fragmented, pixelated aesthetic that evolves over time:

```javascript
// image from:
// https://medium.com/processing-foundation/a-p5-js-web-editor-for-all-64aaa3f9d767
let capture;

function setup() {
  createCanvas(600, 400);
  rectMode(CENTER);
  noStroke();
  capture = createCapture(VIDEO);
  capture.hide();
}

function draw() {
  let max = sin(frameCount / 40); // [-1, 1]
  max += max + 1; // [0, 2]
  max *= 20; // [0, 40]
  max += 5; // [5, 45]

  for (let i = 0; i < 4; i++) {
    const pos = rand_pos();
    const col = capture.get(pos.x, pos.y);
    fill(col);
    square(pos.x, pos.y, 20);
    square(pos.x, pos.y, random(1, max));
  }
}

function rand_pos() {
  const x = random(width);
  const y = random(height);
  return createVector(x, y);
}
```

### Live Interactive Example:

<iframe src="https://editor.p5js.org/hanulgaon-ai/full/O1FNU-auH"></iframe>

<script type="module">
    const iframe = document.querySelector('iframe')
    iframe.width = iframe.parentNode.scrollWidth
    iframe.height = iframe.width * 9 / 16 + 42
</script>

The implementation creates a dynamic self-portrait that balances order and chaos through:

1. **Random sampling** - Pixels are sampled from random locations in the webcam feed
2. **Variable sizing** - Square sizes oscillate based on a sine wave, creating a breathing effect
3. **Layering** - Each frame adds just a few squares (4 per frame), allowing the portrait to build up over time
4. **Color preservation** - Colors are preserved from the original image, maintaining recognizability despite distortion

## 2. Aesthetic Analysis

Glitch aesthetics create visual ruptures by deviating from expected digital logic. The pixel sorting technique I applied is, technically, a simple manipulation of image data, but it results in a visual experience of digital instability. This connects to Rosa Menkman's assertion that glitches are not merely errors but rather "intentional aesthetic strategies."

The glitch effect reveals "chaos within order." The original image represented a kind of _structure_, and the pixel sorting simultaneously deconstructs this order while creating new visual patterns. This generates "effective complexity" that differs from pure randomness. In other words, it creates "patterns that appear random but are actually manipulated," producing complex visual interest.

Of Sianne Ngai's aesthetic registers, both **"zany"** and **"interesting"** connect well with this glitched image. The glitched self-portrait is not simply beautiful or sublime, but rather possesses peculiar and experimental (zany) characteristics distorted by technical manipulation. Simultaneously, viewers engage with the image in an "interesting" manner as they attempt to deduce why and how it was created.

## 3. Bonus: Creating an Algorithm for Maximum-Diversity Group Assignment

```javascript
function makeGroups(students, groupSize) {
  // students: [{name, major, skill, ...}]
  // groupSize: number of students per group
  let groups = [];
  let shuffled = shuffle(students);
  while (shuffled.length) {
    let group = [];
    while (group.length < groupSize && shuffled.length > 0) {
      // Choose students with the most different characteristics (e.g., major, skill combination)
      let candidate = shuffled.pop();
      group.push(candidate);
    }
    groups.push(group);
  }
  return groups;
}

// Random shuffle function
function shuffle(array) {
  let a = [...array];
  for (let i = a.length - 1; i > 0; i--) {
    let j = Math.floor(Math.random() * (i + 1));
    [a[i], a[j]] = [a[j], a[i]];
  }
  return a;
}
```

📌 Explanation:
This code randomly shuffles the array of all students and divides them into groups of the given size. While the base implementation uses randomization, it can be extended to ensure that students with different characteristics (major, skill, interests) are grouped together. For example, a diversity score calculation could be added to find optimal group combinations based on maximizing differences in predetermined attributes across group members.
