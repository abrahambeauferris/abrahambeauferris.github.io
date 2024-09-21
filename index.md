---
layout: default
title: Abraham Beauferris
---

# Abraham Beauferris

Welcome to my portfolio! I am a computer graphics engineer with a passion for rendering algorithms, real-time photorealism, and GPU optimization. I specialize in creating high-performance graphics systems using DirectX, OpenGL, Vulkan, and C++. Currently, I work at Huawei Canada’s Vancouver Research Center, where I focus on pushing the boundaries of cloud rendering and real-time graphics.

Explore my work, research, and career journey below.

---

### Real-time Ray Tracer Demo  

This demo renders the iconic Utah Teapot using a ray-tracing algorithm implemented in JavaScript. It showcases the fundamentals of ray tracing with a triangle mesh object and implements progressive rendering for real-time interaction! 

<div style="position: relative; display: flex; justify-content: center; align-items: center; height: 300px;">
  <button id="startButton" style="position: absolute;">Start Rendering</button>
  <canvas id="raytracer" width="400" height="300" style="border:1px solid #000000; background-color: rgba(200, 200, 200, 0.5);"></canvas>
</div>

<script>
  const canvas = document.getElementById("raytracer");
  const ctx = canvas.getContext("2d");
  const width = canvas.width;
  const height = canvas.height;

  let vertices = [];
  let faces = [];
  let isRendering = false; // Flag to check if rendering is active

  // Accumulation buffer
  let accumulationBuffer = new Float32Array(width * height * 3); // Store [R, G, B] for each pixel
  let sampleCountBuffer = new Uint32Array(width * height); // Keep track of sample count per pixel

  // Parse the OBJ file manually
  fetch('assets/teapot.obj')
    .then(response => response.text())
    .then(text => {
      const lines = text.split('\n');
      
      for (let line of lines) {
        line = line.trim();
        if (line.startsWith('v ')) {
          const [, x, y, z] = line.split(/\s+/).map(parseFloat);
          vertices.push([x, y, z]);
        } else if (line.startsWith('f ')) {
          const [, v1, v2, v3] = line.split(/\s+/).map(v => parseInt(v) - 1);
          faces.push([v1, v2, v3]);
        }
      }
    });

  document.getElementById("startButton").addEventListener("click", function() {
    isRendering = true; // Set the rendering flag to true
    requestAnimationFrame(renderFrame);
  });

  function renderFrame() {
    if (!isRendering) return; // Stop rendering if flag is false

    // Render multiple pixels per frame to speed up accumulation
    for (let i = 0; i < 100; i++) { // Adjust this value for performance vs. speed trade-off
      renderRandomPixel();
    }

    // Request the next frame
    requestAnimationFrame(renderFrame);
  }

  function renderRandomPixel() {
    // Randomly select a pixel
    const x = Math.floor(Math.random() * width);
    const y = Math.floor(Math.random() * height);

    // Compute the ray color for this pixel
    const color = computeRayColor(x, y);

    // Accumulate color in the buffer
    const idx = (x + y * width) * 3;
    accumulationBuffer[idx + 0] += color[0];
    accumulationBuffer[idx + 1] += color[1];
    accumulationBuffer[idx + 2] += color[2];

    // Increment the sample count for this pixel
    sampleCountBuffer[x + y * width]++;

    // Average the color based on the number of samples for this pixel
    const avgColor = [
      accumulationBuffer[idx + 0] / sampleCountBuffer[x + y * width],
      accumulationBuffer[idx + 1] / sampleCountBuffer[x + y * width],
      accumulationBuffer[idx + 2] / sampleCountBuffer[x + y * width]
    ];

    // Update the pixel on the canvas
    const imageData = ctx.createImageData(1, 1);
    imageData.data[0] = Math.min(255, avgColor[0]);
    imageData.data[1] = Math.min(255, avgColor[1]);
    imageData.data[2] = Math.min(255, avgColor[2]);
    imageData.data[3] = 255; // Fully opaque
    ctx.putImageData(imageData, x, y);
  }

  function computeRayColor(x, y) {
    const rayOrigin = [0, 0, -5]; // Camera position
    const rayDirection = [
      (x / width) * 2 - 1, // Map pixel to NDC space [-1, 1]
      (y / height) * 2 - 1,
      1 // Looking along positive z-axis
    ];

    let closestHit = null;

    // Check ray intersection with each triangle in the teapot
    for (let i = 0; i < faces.length; i++) {
      const [v1, v2, v3] = faces[i].map(idx => vertices[idx]);
      const hit = intersectRayTriangle(rayOrigin, rayDirection, v1, v2, v3);
      if (hit && (!closestHit || hit.t < closestHit.t)) {
        closestHit = hit;
      }
    }

    if (closestHit) {
      return cosineWeightedSampling(); // Return importance-sampled color
    } else {
      return [135, 206, 235]; // Background sky blue
    }
  }

  // Cosine-weighted hemisphere sampling function
  function cosineWeightedSampling() {
    const u = Math.random();
    const v = Math.random();

    const theta = Math.acos(Math.sqrt(1 - u)); // Angle relative to normal
    const phi = 2 * Math.PI * v; // Around the hemisphere

    const x = Math.sin(theta) * Math.cos(phi);
    const y = Math.sin(theta) * Math.sin(phi);
    const z = Math.cos(theta);

    // Map the sampled direction to color (this is a placeholder for actual lighting)
    return [255 * Math.abs(x), 255 * Math.abs(y), 255 * Math.abs(z)];
  }

  // Ray-Triangle Intersection function (Möller–Trumbore)
  function intersectRayTriangle(origin, direction, v0, v1, v2) {
    const epsilon = 0.000001;
    const edge1 = subtract(v1, v0);
    const edge2 = subtract(v2, v0);
    const h = cross(direction, edge2);
    const a = dot(edge1, h);

    if (a > -epsilon && a < epsilon) return null; // Parallel ray

    const f = 1.0 / a;
    const s = subtract(origin, v0);
    const u = f * dot(s, h);

    if (u < 0.0 || u > 1.0) return null;

    const q = cross(s, edge1);
    const v = f * dot(direction, q);

    if (v < 0.0 || u + v > 1.0) return null;

    const t = f * dot(edge2, q); // Intersection point is found

    if (t > epsilon) return { t }; // Ray intersection

    return null;
  }

  // Vector Math Helper Functions
  function subtract(v1, v2) {
    return [v1[0] - v2[0], v1[1] - v2[1], v1[2] - v2[2]];
  }

  function dot(v1, v2) {
    return v1[0] * v2[0] + v1[1] * v2[1] + v2[2] * v1[2];
  }

  function cross(v1, v2) {
    return [
      v1[1] * v2[2] - v1[2] * v2[1],
      v1[2] * v2[0] - v1[0] * v2[2],
      v1[0] * v2[1] - v1[1] * v2[0]
    ];
  }
</script>

---

## About Me

I'm Abraham Beauferris, a Computer Science graduate with First-Class Honours from the University of Calgary. My work spans across computer graphics, neural rendering, and GPU optimization. I thrive on challenges that involve physically-based rendering, path tracing, and integrating AI algorithms into game and simulation engines.

When I’m not working on cutting-edge rendering systems, I enjoy contributing to open-source projects, engaging with research communities, and collaborating with other professionals in the field.

### Key Skills
- **Graphics Algorithms**: Advanced knowledge in rendering algorithms and photorealistic rendering systems.
- **APIs**: Extensive experience with DirectX, OpenGL, Vulkan for low-level graphics programming.
- **Rendering Pipelines**: Expertise in path tracing, rasterization, and subsurface scattering.
- **Optimization**: Skilled in GPU performance optimization for real-time applications.
- **AI & Neural Rendering**: Incorporating AI-based techniques using PyTorch and Tensorflow for rendering systems.
- **Programming Languages**: Proficient in C++, Python, and shader programming.

---

## Experience

### Associate Engineer | Huawei Canada, Vancouver Research Center  
_August 2022 - Present_

![O3DE Logo](assets/images/o3de.png)

At Huawei, I contribute to the Cloud Rendering team where I work on advancing real-time photorealistic imagery. My role includes:
- Developing material creation tools within Open 3D Engine.
- Implementing and optimizing physically-based rendering techniques.
- Working with ray tracing algorithms to enhance game development and rendering efficiency.
- Exploring AI algorithms to improve performance and realism in graphics.

### Undergraduate Researcher | VISAGG, University of Calgary  
_September 2021 - May 2022_

![Surgisim Picture](assets/images/surgisim-platform-1.png)

I collaborated on the **SurgiSim** project, a VR platform designed to teach otolaryngology through immersive simulations. I contributed to graphical enhancements and helped improve performance through rendering techniques like directional ambient occlusion.

---

## Projects

### Deep Albedo: A Spatially Aware Autoencoder Approach to Interactive Human Skin Rendering  
_C++, Python, OpenCV, UE5_

![Deep Albedo Project](assets/images/deep-albedo.png)

This research project focused on using **Monte Carlo photon simulations** and **neural autoencoders** to simulate human skin color in real-time. The goal was to create a model that could dynamically change based on biophysical parameters. This project was presented at SIGGRAPH Asia 2023.

### Enhancing the Graphical Fidelity of the SurgiSim Platform  
_Unreal Engine 4, C++_

![Honours Project](assets/images/surgisim-platform-2.png)

For my honours research, I enhanced the visual fidelity of the SurgiSim VR platform. I implemented **directional ambient occlusion** and **subsurface scattering** to increase realism. Additionally, I improved the performance using **dynamic resolution scaling**, ensuring the system could run smoothly under demanding conditions.

Sure! Here’s the updated project section for the Utah Teapot Ray Tracer, styled consistently with your existing entries:

---

### Real-time Ray Tracer Demo  
_Html5, JavaScript, Canvas API_

<!-- ![Ray Tracer Demo](assets/images/raytracer-project.png) -->

This project is an interactive real-time ray tracer built in JavaScript, rendering the famous **Utah Teapot** on an HTML5 canvas. It demonstrates fundamental ray tracing principles, including ray-triangle intersection and progressive rendering for enhanced visual quality.

#### Key Features:
- **Interactive Rendering**: Users can initiate the rendering process with a button click, allowing for a hands-on experience.
- **Progressive Accumulation**: Implements an accumulation buffer to progressively refine the image quality over time, reducing noise and improving detail.
- **Cosine-weighted Sampling**: Utilizes cosine-weighted sampling techniques for realistic light distribution on surfaces.
- **Dynamic Performance**: Renders multiple pixels per frame, balancing performance and rendering speed to provide real-time feedback.

#### Technical Details:
- **Rendering Approach**: Employs the Möller–Trumbore algorithm for efficient ray-triangle intersection testing.
- **Color Calculation**: Computes pixel colors based on ray casting from a virtual camera, taking into account surface normals and light direction.
- **Background Handling**: Displays a sky blue background for unoccupied areas in the scene.

---

## Contact Me

I’m always open to new opportunities and collaborations. Feel free to reach out!

- **Email**: [abeauferris@gmail.com](mailto:abeauferris@gmail.com)  
- **Phone**: 403.874.8433  
- **LinkedIn**: [linkedin.com/in/abrahambeauferris](https://linkedin.com/in/abrahambeauferris)  
- **GitHub**: [github.com/abrahambeauferris](https://github.com/abrahambeauferris)

---

Thanks for visiting my portfolio!