---
title: Week 5-2 Blog
published_at: 2025-04-19
snippet: Implementing Three.js examples and analyzing glitch aesthetics in digital art
disable_html_sanitization: true
allow_math: true
---

# Week 5-2 Blog: Three.js Implementation and Glitch Art Analysis

## 1. Three.js Example Implementation

For this assignment, I've selected and implemented the "Particles" example from Three.js. This example creates an immersive 3D particle system where thousands of particles move in space, creating a mesmerizing cosmic effect.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Three.js Particles</title>
    <style>
      body {
        margin: 0;
        overflow: hidden;
      }
      canvas {
        display: block;
      }
    </style>
  </head>
  <body>
    <script type="module">
      import * as THREE from "https://cdn.skypack.dev/three@0.136.0";
      import { OrbitControls } from "https://cdn.skypack.dev/three@0.136.0/examples/jsm/controls/OrbitControls.js";

      // Scene setup
      const scene = new THREE.Scene();
      scene.background = new THREE.Color(0x000000);

      // Camera setup
      const camera = new THREE.PerspectiveCamera(
        75,
        window.innerWidth / window.innerHeight,
        0.1,
        1000
      );
      camera.position.z = 50;

      // Renderer setup
      const renderer = new THREE.WebGLRenderer({ antialias: true });
      renderer.setSize(window.innerWidth, window.innerHeight);
      document.body.appendChild(renderer.domElement);

      // Controls setup
      const controls = new OrbitControls(camera, renderer.domElement);
      controls.enableDamping = true;
      controls.dampingFactor = 0.05;

      // Particles
      const particlesGeometry = new THREE.BufferGeometry();
      const particleCount = 5000;

      const positions = new Float32Array(particleCount * 3);
      const colors = new Float32Array(particleCount * 3);

      for (let i = 0; i < particleCount * 3; i += 3) {
        // Position - spread in a cube
        positions[i] = (Math.random() - 0.5) * 100;
        positions[i + 1] = (Math.random() - 0.5) * 100;
        positions[i + 2] = (Math.random() - 0.5) * 100;

        // Color - rainbow effect
        colors[i] = Math.random();
        colors[i + 1] = Math.random();
        colors[i + 2] = Math.random();
      }

      particlesGeometry.setAttribute(
        "position",
        new THREE.BufferAttribute(positions, 3)
      );
      particlesGeometry.setAttribute(
        "color",
        new THREE.BufferAttribute(colors, 3)
      );

      const particlesMaterial = new THREE.PointsMaterial({
        size: 0.5,
        vertexColors: true,
        transparent: true,
        opacity: 0.8,
      });

      const particles = new THREE.Points(particlesGeometry, particlesMaterial);
      scene.add(particles);

      // Animation
      let time = 0;
      function animate() {
        requestAnimationFrame(animate);

        time += 0.005;

        // Update particle positions for animation
        const positions = particles.geometry.attributes.position.array;

        for (let i = 0; i < positions.length; i += 3) {
          // Apply sine wave motion to create flowing effect
          positions[i + 1] += Math.sin(time + positions[i] / 10) * 0.1;
          positions[i] += Math.cos(time + positions[i + 2] / 10) * 0.1;
        }

        particles.geometry.attributes.position.needsUpdate = true;

        controls.update();
        renderer.render(scene, camera);
      }

      // Handle window resize
      window.addEventListener("resize", () => {
        camera.aspect = window.innerWidth / window.innerHeight;
        camera.updateProjectionMatrix();
        renderer.setSize(window.innerWidth, window.innerHeight);
      });

      animate();
    </script>
  </body>
</html>
```

This implementation creates a cloud of colorful particles that gently flow through space. The particles move according to sine and cosine functions, creating an organic, wave-like motion. Users can interact with the scene by rotating the view with their mouse, zooming in and out, and panning across the particle field.

## 2. Glitch Art Analysis: Sabato Visconti's flower-01C_giphy-1.gif

### Aesthetic Effects

Sabato Visconti's glitch art piece "flower-01C_giphy-1.gif" demonstrates the powerful aesthetic of digital fragmentation. The flower image appears to be "broken," revealing the underlying instability of digital media. This deliberate corruption transforms what would be a cold, perfect digital representation into something emotional and chaotic.

The core of post-digital aesthetics is embraced in this work: digital imperfection, celebrating randomness and noise instead of hiding them. By exposing the typically concealed technical underpinnings of digital media, Visconti creates a more authentic relationship with technology – acknowledging its flaws rather than pretending perfection.

### Effective Complexity

The glitch creates a fascinating balance between order and disorder. The original image (the flower) provides a structured reference point that our brains recognize, while the glitch elements introduce unpredictable chaos. This mixture of predictable and unpredictable elements creates what complexity theorists call "effective complexity" – a sweet spot that captures and holds viewer attention.

The partially corrupted image forces viewers to mentally reconstruct what's missing, creating an interactive cognitive experience that extends beyond passive viewing. The work exists in a liminal space between completely random (which would appear as pure noise) and completely ordered (which would be just a normal flower image).

### Technical Implementation

Under the hood, glitch art like Visconti's can be created through several techniques:

1. **Texture coordinate manipulation**: Distorting the UV mapping that determines how image textures are wrapped around 3D models
2. **Vertex displacement**: Randomly altering the position data of vertices in a 3D model
3. **Data manipulation**: Directly editing image data by opening image files in text editors and modifying bytes
4. **Shader implementation**: Using fragment and vertex shaders to create real-time glitch effects

In this specific piece, it appears Visconti may have used databending techniques, potentially manipulating the encoding of the GIF file and introducing controlled data corruption to create the distinct aesthetic ruptures while maintaining the recognizable elements of the original flower.

## Bonus: Applying Session 4b Glitch Concepts to Three.js

I've modified the particle system to incorporate glitch aesthetics using shader-based vertex displacement. This creates moments of unpredictable distortion in the otherwise fluid particle movement:

```javascript
// Add this shader code to the previous example
const vertexShader = `
    uniform float time;
    uniform float glitchIntensity;
    
    void main() {
        vec3 pos = position;
        
        // Normal flowing movement
        pos.y += sin(time + position.x / 10.0) * 0.1;
        pos.x += cos(time + position.z / 10.0) * 0.1;
        
        // Glitch effect - triggered occasionally with random intensity
        float glitchTrigger = step(0.97, sin(time * 0.5) * 0.5 + 0.5);
        float noise = fract(sin(dot(position.xy, vec2(12.9898, 78.233))) * 43758.5453);
        
        if (noise > 0.7 && glitchTrigger > 0.0) {
            // Apply sudden displacement to create glitch
            pos += vec3(
                sin(time * 100.0 + position.x) * glitchIntensity * 5.0,
                cos(time * 90.0 + position.y) * glitchIntensity * 5.0,
                sin(time * 80.0 + position.z) * glitchIntensity * 5.0
            );
        }
        
        gl_Position = projectionMatrix * modelViewMatrix * vec4(pos, 1.0);
        gl_PointSize = size;
    }
`;

const fragmentShader = `
    varying vec3 vColor;
    uniform float time;
    uniform float glitchIntensity;
    
    void main() {
        // Basic circle shape for particles
        if (length(gl_PointCoord - vec2(0.5)) > 0.5) discard;
        
        vec3 color = vColor;
        
        // Occasional color glitching
        float glitchTrigger = step(0.97, sin(time * 0.5) * 0.5 + 0.5);
        if (glitchTrigger > 0.0) {
            // RGB shift
            float shift = sin(time * 20.0) * glitchIntensity * 0.5;
            color.r = fract(color.r + shift);
            color.b = fract(color.b - shift);
        }
        
        gl_FragColor = vec4(color, 1.0);
    }
`;

// Update the material to use shaders
const particlesMaterial = new THREE.ShaderMaterial({
  uniforms: {
    time: { value: 0 },
    glitchIntensity: { value: 0.8 },
  },
  vertexShader: vertexShader,
  fragmentShader: fragmentShader,
  transparent: true,
});
```

This modification introduces sporadic "glitches" in the particle system. At random intervals, the particles experience sudden displacements and color shifts that break the smooth flow, creating moments of digital unpredictability similar to Visconti's aesthetic. The glitch intensity can be adjusted through the uniform parameters.

The implementation demonstrates how glitch aesthetics can transform a perfect digital simulation into something that acknowledges its digital nature through controlled failure—a core principle of post-digital art.
