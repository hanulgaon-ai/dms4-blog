---
title: Week 8-2 Blog
published_at: 2025-05-11
snippet: Live coding performance with flok.cc and exploring the live coding community
disable_html_sanitization: true
allow_math: true
---

# Week 8-2 Blog

## Live Coding Performance

We used flok.cc to create a collaborative live coding performance combining Hydra visuals with Strudel audio. The session lasted about 15 minutes.

```javascript
// Hydra visual code snippet
osc(40, 0.1, 0.8).rotate(0.1).modulate(noise(3)).blend(osc(20, 0.05)).out();
```

```javascript
// Strudel audio pattern
sound("bd hh sd hh").speed(0.8).gain(0.7).delay(0.3);
```

Working with teammates in real-time was challenging. Connection delays made synchronization difficult and some visual effects didn't render properly during the performance.

## Live Coding Community

### Interesting Content

- **Algorave performances** - Live coding electronic music events where performers show their screens
- **TOPLAP manifesto** - "Show us your screens" philosophy promotes transparency in creative process

### Community Analysis

**Domain**: Real-time audiovisual performance through code
**Repertoire**:

- Shared languages (SuperCollider, TidalCycles, Hydra)
- Live streaming platforms
- Code repositories
- Performance venues

**Values**:

- Process transparency
- Mistake acceptance
- Collaborative creation
- Technical experimentation

### Cultural Performance Impact

Live coding connects programming with performance art. Young people find it appealing because it combines technical skills with creative expression - you're coding and performing simultaneously.

This approach could change programming education by making the learning process more performative and collaborative rather than isolated.

The transparency aspect might influence public discourse - showing work processes rather than just final results.

Legislation around live coding remains unclear, especially regarding copyright when algorithms generate music in real-time.
