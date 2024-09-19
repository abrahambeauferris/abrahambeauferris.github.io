---
layout: default
title: Abraham Beauferris
---

# Abraham Beauferris

Welcome to my portfolio! I am a computer graphics engineer with a passion for rendering algorithms, real-time photorealism, and GPU optimization. I specialize in creating high-performance graphics systems using DirectX, OpenGL, Vulkan, and C++. Currently, I work at Huawei Canada’s Vancouver Research Center, where I focus on pushing the boundaries of cloud rendering and real-time graphics.

Explore my work, research, and career journey below.

---

## Fun Interactive Demo - Simple Ray Tracer

This is an example of a ray tracer implemented in JavaScript, rendering directly onto an HTML canvas. The current version displays a ray-traced sphere. Soon, I'll be adding a model of my own face for a unique self-portrait!

<div>
  <canvas id="raytracer" width="400" height="300" style="border:1px solid #000000;"></canvas>
</div>

<script>
  const canvas = document.getElementById("raytracer");
  const ctx = canvas.getContext("2d");
  const width = canvas.width;
  const height = canvas.height;

  function rayTrace() {
    const imageData = ctx.createImageData(width, height);
    const data = imageData.data;

    for (let y = 0; y < height; y++) {
      for (let x = 0; x < width; x++) {
        const color = computeRayColor(x, y);
        const index = (x + y * width) * 4;
        data[index + 0] = color[0]; // R
        data[index + 1] = color[1]; // G
        data[index + 2] = color[2]; // B
        data[index + 3] = 255;      // A
      }
    }
    ctx.putImageData(imageData, 0, 0);
  }

  function computeRayColor(x, y) {
    const sphere = {
      center: [200, 150, 50],
      radius: 50,
    };
    const rayOrigin = [x, y, 0];
    const rayDirection = [0, 0, 1];

    const t = intersectRaySphere(rayOrigin, rayDirection, sphere);
    if (t > 0.0) {
      return [255, 0, 0]; // Sphere hit, return red
    } else {
      return [135, 206, 235]; // Sky blue background
    }
  }

  function subtract(v1, v2) {
    return [v1[0] - v2[0], v1[1] - v2[1], v1[2] - v2[2]];
  }

  function dot(v1, v2) {
    return v1[0] * v2[0] + v1[1] * v2[1] + v1[2] * v2[2];
  }

  function intersectRaySphere(origin, direction, sphere) {
    const oc = subtract(origin, sphere.center);
    const a = dot(direction, direction);
    const b = 2.0 * dot(oc, direction);
    const c = dot(oc, oc) - sphere.radius * sphere.radius;
    const discriminant = b * b - 4 * a * c;
    if (discriminant < 0) {
      return -1.0; // No hit
    } else {
      return (-b - Math.sqrt(discriminant)) / (2.0 * a); // Closest hit
    }
  }

  rayTrace();
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

### Real-time Ray Tracer Demo  
_Html5, JavaScript, Canvas API_

![Ray Tracer Demo](assets/images/raytracer-project.png)

This project is a simple real-time ray tracer built in JavaScript and rendered onto an HTML5 canvas. It demonstrates fundamental ray tracing principles, including ray-sphere intersection. The current scene consists of a ray-traced red sphere on a sky blue background. I plan to expand this demo with more complex objects, lighting, and a fun self-portrait model.

[Try the interactive demo above](#fun-interactive-demo-simple-ray-tracer).

Key Features:
- Ray-sphere intersection
- Basic color rendering
- Expandable to include more features such as lighting, shadows, and multiple objects

---

## Contact Me

I’m always open to new opportunities and collaborations. Feel free to reach out!

- **Email**: [abeauferris@gmail.com](mailto:abeauferris@gmail.com)  
- **Phone**: 403.874.8433  
- **LinkedIn**: [linkedin.com/in/abrahambeauferris](https://linkedin.com/in/abrahambeauferris)  
- **GitHub**: [github.com/abrahambeauferris](https://github.com/abrahambeauferris)

---

Thanks for visiting my portfolio!