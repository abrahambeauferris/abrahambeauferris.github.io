---
layout: default
title: Abraham Beauferris
---

<!-- Start of inline CSS for enhancements -->
<style>
  /* Sticky navigation style */
  .sticky-nav {
    position: fixed;
    top: 0;
    width: 100%;
    background-color: #333;
    overflow: hidden;
    z-index: 1000;
  }
  .sticky-nav a {
    float: left;
    display: block;
    color: #f2f2f2;
    text-align: center;
    padding: 14px 16px;
    text-decoration: none;
  }
  .sticky-nav a:hover {
    background-color: #ddd;
    color: black;
  }
  .content {
    padding-top: 60px; /* ensure content is not hidden behind sticky nav */
  }
  /* Back-to-top button styles */
  #backToTop {
    display: none;
    position: fixed;
    bottom: 30px;
    right: 30px;
    z-index: 100;
    border: none;
    outline: none;
    background-color: #333;
    color: white;
    cursor: pointer;
    padding: 10px 15px;
    border-radius: 4px;
  }
  #backToTop:hover {
    background-color: #555;
  }
  /* Contact form styles */
  .contact-form {
    max-width: 600px;
    margin: auto;
  }
  .contact-form input, .contact-form textarea {
    width: 100%;
    padding: 12px;
    margin: 6px 0 12px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  .contact-form button {
    background-color: #333;
    color: white;
    padding: 12px 20px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  .contact-form button:hover {
    background-color: #555;
  }
</style>
<!-- End of inline CSS -->

<!-- Sticky Navigation -->
<div class="sticky-nav">
  <a href="#about">About Me</a>
  <a href="#experience">Experience</a>
  <a href="#projects">Projects</a>
  <a href="#awards">Awards & Testimonials</a>
  <a href="#multimedia">Multimedia</a>
  <a href="#contact">Contact</a>
</div>

<div class="content">

# Abraham Beauferris

Welcome to my portfolio. I am a computer graphics engineer with a deep passion for real-time photorealistic rendering, GPU optimization, and the art of visual storytelling. My journey is one of continuous learning and creative exploration—a fusion of technical innovation and artistic expression. Currently, I work at Huawei Canada’s Vancouver Research Center, where I help redefine the boundaries of cloud rendering and interactive graphics.

## About Me {#about}

I hold a First-Class Honours degree in Computer Science from the University of Calgary and have devoted my career to mastering every aspect of graphics programming. My expertise spans low-level APIs such as DirectX, OpenGL, and Vulkan, and extends to advanced techniques like ray tracing, neural rendering, and performance optimization. I believe that technology should not only solve problems but also inspire creativity and evoke emotion. My mission is to transform complex theoretical concepts into engaging, real-world visual experiences that captivate both technical and creative audiences.

## Experience {#experience}

At Huawei Canada, I joined the Cloud Rendering team during a pivotal period of innovation. In this role, I collaborated with multidisciplinary teams to integrate advanced ray tracing and AI-driven enhancements into our material creation tools and rendering pipelines. The challenging environment spurred the development of optimized solutions that achieved unprecedented levels of visual fidelity and performance, pushing the frontiers of real-time graphics.

Earlier in my career, as an Undergraduate Researcher with the Visualization and Graphics Group at the University of Calgary, I contributed to a VR surgical training system. Confronted with the challenge of balancing lifelike rendering with interactivity, I integrated advanced ambient occlusion, subsurface scattering, and dynamic resolution scaling techniques. My contributions significantly boosted both the immersive quality and educational impact of the platform.

## Projects {#projects}

### Deep Albedo: A Spatially Aware Autoencoder Approach to Interactive Human Skin Rendering  
_Technologies: C++, Python, OpenCV, UE5_

![Deep Albedo Project](assets/images/deep-albedo.png)

Deep Albedo is a groundbreaking project that bridges physics-based rendering with neural network methodologies. Confronted with the intricate challenge of realistically simulating human skin, I spearheaded the development of an autoencoder framework powered by Monte Carlo photon simulations. This system dynamically captures subtle variations in skin tone under diverse lighting conditions, enabling interactive adjustments and lifelike visual outcomes. Collaborating with experts from the University of British Columbia and Huawei Technologies Canada, our work was showcased at SIGGRAPH Asia 2023, marking a significant milestone in real-time biophysical rendering.

### Enhancing the Graphical Fidelity of the SurgiSim Platform  
_Technologies: Unreal Engine 4, C++_

![SurgiSim Project](assets/images/surgisim-platform-2.png)

In my honours research project, I set out to revolutionize the visual and interactive experience of the SurgiSim VR surgical training platform. The objective was to create an environment that was both immersive and highly responsive—capable of faithfully mimicking the intricacies of human anatomy. By integrating advanced techniques such as directional ambient occlusion and subsurface scattering, along with implementing dynamic resolution scaling, I succeeded in elevating the platform’s visual realism and performance. These enhancements not only enriched the user experience but also dramatically improved the educational impact of the system.

## Awards & Testimonials {#awards}

**Awards & Recognitions:**

- **Dean’s List:** Recognized for academic excellence in 2019 and 2020.
- **Jason Lang Scholarship:** Awarded for outstanding academic and technical achievements.
- **Alexander Rutherford Scholarship:** Honoured for exemplary performance in Computer Science.
- **SIGGRAPH Asia 2023:** Featured for innovative work on Deep Albedo.

**Testimonials:**

> "Abraham's innovative approach to graphics engineering consistently pushes the envelope of what’s possible, merging technical rigor with creative vision."  
> — Former Supervisor, Huawei Canada

> "His transformative work on the SurgiSim platform not only enhanced visual realism but redefined interactive learning in VR."  
> — Academic Advisor, University of Calgary

## Multimedia {#multimedia}

### Video Introduction

Experience a brief introduction where I discuss my professional journey and the creative process behind my work.  
<video width="640" height="360" controls poster="assets/images/video-poster.jpg">
  <source src="assets/video/introduction.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

Stay tuned for more interactive demos and animated project walkthroughs.

## Contact Me {#contact}

I welcome the opportunity to connect with fellow innovators, collaborators, and anyone passionate about the future of graphics and rendering technology. Please feel free to reach out directly using the contact details below or through the contact form provided.

**Direct Contact:**

- **Email:** [abeauferris@gmail.com](mailto:abeauferris@gmail.com)
- **Phone:** 403.874.8433  
- **LinkedIn:** [linkedin.com/in/abrahambeauferris](https://linkedin.com/in/abrahambeauferris)
- **GitHub:** [github.com/abrahambeauferris](https://github.com/abrahambeauferris)

### Contact Form

<div class="contact-form">
  <form action="https://formspree.io/f/your-form-id" method="POST">
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" placeholder="Your name" required>
    
    <label for="email">Email:</label>
    <input type="email" id="email" name="_replyto" placeholder="Your email" required>
    
    <label for="message">Message:</label>
    <textarea id="message" name="message" placeholder="Your message" rows="5" required></textarea>
    
    <button type="submit">Send Message</button>
  </form>
</div>

</div>

<!-- Back to Top Button -->
<button onclick="backToTop()" id="backToTop" title="Go to top">Top</button>

<!-- Inline JavaScript for Back to Top functionality -->
<script>
  // Show or hide the Back-to-Top button
  window.onscroll = function() {scrollFunction()};
  function scrollFunction() {
      const backToTopBtn = document.getElementById("backToTop");
      if (document.body.scrollTop > 300 || document.documentElement.scrollTop > 300) {
          backToTopBtn.style.display = "block";
      } else {
          backToTopBtn.style.display = "none";
      }
  }
  
  // Scroll to the top of the document
  function backToTop() {
      document.body.scrollTop = 0;
      document.documentElement.scrollTop = 0;
  }
</script>