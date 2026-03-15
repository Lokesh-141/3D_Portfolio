# React + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react) uses [Babel](https://babeljs.io/) (or [oxc](https://oxc.rs) when used in [rolldown-vite](https://vite.dev/guide/rolldown)) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh

### 🏗️ Project Architecture Map

```
📁 3D_Portfolio
├── 📁 public               # static assets (GLTF models, textures, images)
├── 📁 src
│   ├── 📁 components       # Reusable React & 3D sub-components
│   ├── 📁 sections         # Main page sections (Hero, Showcase, Contact)
│   ├── 📁 constants        # Configuration and data files
│   ├── 📁 assets           # Stylesheets and global assets
│   ├── 📄 App.jsx          # Main entry and layout orchestrator
│   └── 📄 main.jsx         # React mounting point
├── 📄 index.html           # HTML template
├── 📄 vite.config.js       # Build & Dev performance config
└── 📄 README.md            # Advanced documentation
```

---

## 🎨 3D Scene Hierarchy (Hero Section)

This diagram visualizes how the **React-Three-Fiber** scene is structured for spatial rendering.

```mermaid
graph TD
    Canvas[R3F Canvas] --> Camera[Perspective Camera: 45 FOV]
    Canvas --> Orbit[OrbitControls: Zoom/Rotate]
    Canvas --> Lights[HeroLights: Ambient/Spot]
    Canvas --> Scene[Three.js Scene]
    
    subgraph "Spatial Environment"
        Scene --> Group1[group: Mobile/Tablet Scaling]
        Group1 --> Model[Room.jsx: GLTF Model]
        Scene --> Particles[Particles.jsx: 100 Floating Points]
    end
```

---

## 🎬 Interaction & Animation Workflow

The sequence of events from page load to cinematic interactive state:

```mermaid
sequenceDiagram
    actor User
    participant Browser
    participant React as React (App.jsx)
    participant R3F as React-Three-Fiber
    participant GSAP as GSAP Engine

    User->>Browser: Load Portfolio URL
    Browser->>React: Mount Core Components
    React->>R3F: Initialize 3D Canvas
    R3F->>Browser: Request GPU Context (WebGL)
    
    activate R3F
    R3F->>R3F: Load GLTF Models & Textures
    R3F-->>React: Scene Ready
    deactivate R3F
    
    React->>GSAP: Trigger Entrance Timeline (useGSAP)
    GSAP->>React: Fade in Navbar & Counter
    GSAP->>R3F: Animate Camera Sweep & Room Scale
    
    User->>Browser: Mouse Drag / Touch
    Browser->>R3F: OrbitControls Interaction
    R3F->>R3F: Update Camera Matrix in Real-time
```

---

## ✨ Features

## React Compiler

The React Compiler is not enabled on this template because of its impact on dev & build performances. To add it, see [this documentation](https://react.dev/learn/react-compiler/installation).

## Expanding the ESLint configuration

If you are developing a production application, we recommend using TypeScript with type-aware lint rules enabled. Check out the [TS template](https://github.com/vitejs/vite/tree/main/packages/create-vite/template-react-ts) for information on how to integrate TypeScript and [`typescript-eslint`](https://typescript-eslint.io) in your project.
