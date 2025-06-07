---
title: "Week 10-2 Blog"
published_at: 2025-06-02
snippet: "Learning Manim for mathematical animation and creative coding"
disable_html_sanitization: true
allow_math: true
---

# Week 10-2 Blog

## Manim Exploration

I chose Manim (Mathematical Animation Engine) because it combines programming with visual storytelling, which could be useful for explaining CheckMate's algorithm concepts.

### Why Manim?

Manim appeals to me because it can create clean, educational animations programmatically. For my AT3 project, I could use it to create explainer videos showing how fair cost distribution works or visualize roommate interaction patterns.

### Learning Process

I followed the official Manim tutorial and created a basic animation showing geometric transformations:

```python
from manim import *

class TaskVisualization(Scene):
    def construct(self):
        # Create task completion circles
        circle1 = Circle(radius=1, color=BLUE).shift(LEFT*2)
        circle2 = Circle(radius=1, color=RED).shift(RIGHT*2)

        # Add labels
        label1 = Text("Changjo", font_size=24).next_to(circle1, DOWN)
        label2 = Text("Sejun", font_size=24).next_to(circle2, DOWN)

        # Animate circle growth based on task completion
        self.play(Create(circle1), Create(circle2))
        self.play(Write(label1), Write(label2))

        # Show task completion over time
        for i in range(3):
            self.play(
                circle1.animate.scale(1.2),
                circle2.animate.scale(1.1)
            )
            self.wait(0.5)

        # Final transformation showing fair payment
        payment_text = Text("Fair payment calculated!", font_size=36)
        self.play(Transform(VGroup(circle1, circle2), payment_text))
        self.wait(2)
```

The script creates animated circles representing roommate task completion, growing over time to show accumulated contributions.

### Creative Practice Applications

For CheckMate, Manim could create:

- Animated explanations of the scoring algorithm
- Visual progress reports showing monthly patterns
- Educational content for onboarding new users
- Data visualizations for settlement discussions

The programmatic approach means I could generate personalized animations based on actual user data.

### Scripting Language Comparison

**Manim Strengths:**

- Excellent for mathematical/educational content
- High-quality vector graphics output
- Good documentation and community
- Integrates well with Python ecosystem

**Manim Weaknesses:**

- Limited to animation/visualization
- Steep learning curve for complex scenes
- Render times can be slow
- Not suitable for interactive applications

**Scripting vs Compiled Languages**

Scripting languages like Python excel at rapid prototyping and automation. For creative coding, the immediate feedback loop helps iterate quickly on visual ideas.

Compiled languages offer better performance but slower development cycles. For animation tools like Manim, the scripting approach makes sense because render time matters more than real-time performance.

Manim specifically bridges the gap between programmatic control and visual output quality, making it powerful for educational content creation even if it's not suitable for interactive applications.
