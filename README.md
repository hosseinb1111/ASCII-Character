# ASCII Character

An interactive 3D character rendered entirely as ASCII art in the browser.

Move your mouse around the character, change its emotion, switch between visual scenes, adjust ASCII density, and interact with the character to trigger reactions. The underlying scene is built with **Three.js**, while `AsciiEffect` converts the rendered 3D model into an ASCII representation.

> A small experiment combining 3D graphics, procedural animation, interaction design, and ASCII rendering.

---

## ✦ Features

### Character interaction

* Mouse and touch tracking
* Character looks toward the pointer
* Idle look-around behavior
* Automatic blinking
* Eye saccades
* Breathing animation
* Antenna movement
* Click-based reactions
* Animated waving reaction
* Spring-based facial animation

### Expressions

The character currently supports:

* Neutral
* Happy
* Sad
* Angry
* Surprised
* Sleepy
* Love
* Wink
* Confused
* Smug
* Thinking
* Giggle

Expressions can be selected from the interface or through keyboard shortcuts where supported.

### ASCII rendering

The 3D scene is converted into ASCII using:

* Three.js
* `AsciiEffect`
* Multiple ASCII character ramps
* Adjustable rendering density
* Optional color rendering

Three detail levels are available:

```text
COARSE
NORMAL
FINE
```

---

## 🎨 Visual Scenes

The interface includes multiple visual themes:

```text
paper
aurora
starfield
nebula
vaporwave
cyberpunk
matrix
sunset
midnight
frost
```

Each theme controls the ASCII character ramp, foreground color, rendering behavior, and vignette intensity.

---

## 🕹 Controls

### Mouse / Touch

Move around the page to influence the character's gaze.

Click the character to trigger a reaction.

### Keyboard

| Key     | Action                       |
| ------- | ---------------------------- |
| `1`–`9` | Select an emotion            |
| `0`     | Select an additional emotion |
| `T`     | Cycle visual theme           |
| `D`     | Cycle ASCII density          |
| `R`     | Shuffle theme + emotion      |
| `Space` | Trigger a blink              |

The on-screen controls can also be used without a keyboard.

---

## ⚙️ Technical Architecture

The project uses a relatively small client-side architecture:

```text
Browser
   │
   ├── Three.js Scene
   │      ├── Camera
   │      ├── Lights
   │      └── 3D Character
   │
   ├── Character Animation
   │      ├── Expressions
   │      ├── Blinking
   │      ├── Saccades
   │      ├── Idle Look
   │      └── Interaction Reactions
   │
   └── AsciiEffect
          │
          ▼
      ASCII Output
```

The character itself is constructed from Three.js meshes rather than an imported model.

---

## 🧩 Character Construction

The character is assembled procedurally from basic Three.js geometry.

Examples include:

```text
SphereGeometry
CylinderGeometry
CapsuleGeometry
BoxGeometry
TorusGeometry
ConeGeometry
```

The model is organized into reusable groups such as:

```text
bodyGroup
└── headGroup
    ├── head
    ├── eyes
    ├── pupils
    ├── brows
    ├── nose
    ├── mouth
    ├── ears
    └── antenna
```

This makes individual facial elements independently controllable during animation.

---

## 🧠 Expression System

Expressions are represented as target values rather than completely separate character models.

For example, an emotion can define:

```javascript
{
    browL_y,
    browL_rot,
    browR_y,
    browR_rot,
    mouth_rot,
    mouth_sx,
    mouth_sy,
    mouth_y,
    head_tilt_y,
    head_tilt_x,
    head_bias_x,
    antenna_speed,
    eye_open,
    eyeL,
    eyeR
}
```

The current state is then animated toward those targets using a simple spring-damper system.

This produces smoother transitions than instantly changing facial geometry.

---

## ✨ Animation System

Several animation systems work together:

### Spring animation

Facial parameters smoothly interpolate toward expression targets using spring physics.

### Blinking

The eyes periodically close automatically with randomized timing.

### Saccades

Small randomized pupil movements make the character feel less static.

### Idle behavior

When the pointer has been inactive for a while, the character occasionally looks in a different direction.

### Interaction reactions

Clicking the character can trigger temporary expressions such as:

```text
giggle
happy
surprised
```

A short wave animation is also triggered.

---

## 💾 Persistence

The selected configuration can persist between visits using `localStorage`.

Saved values include:

```text
emotion
theme
density
```

The project also supports configuration through URL parameters:

```text
?emotion=happy
?theme=matrix
?density=fine
```

These can be combined, for example:

```text
?emotion=thinking&theme=cyberpunk&density=fine
```

---

## 📱 Responsive Design

The control interface adapts to smaller screens.

On mobile:

* Controls wrap naturally
* Secondary keyboard instructions are hidden
* Touch movement can control the character
* Buttons remain accessible
* The WebGL/ASCII presentation continues to fill the viewport

The experience is designed around the visual interaction rather than a traditional content-heavy layout.

---

## ♿ Accessibility & Reduced Motion

The project respects the user's system preference:

```css
@media (prefers-reduced-motion: reduce)
```

When reduced motion is enabled, several continuous animations are reduced or disabled.

The interface also uses semantic buttons and visible interaction states for the controls.

---

## 🚀 Running Locally

No build system is required.

The page can be opened as a normal HTML document, although serving it through a local development server is recommended for a more consistent browser environment.

For example:

```bash
git clone https://github.com/hosseinb1111/ASCII-Character.git
cd REPO-NAME
```

Then serve the directory with any static HTTP server.

The project currently loads Three.js from a CDN through an import map:

```text
https://unpkg.com/three@0.169.0/
```

---

## 📦 Dependencies

The project intentionally keeps dependencies minimal.

### Three.js

Used for:

* 3D rendering
* geometry
* lighting
* camera
* animation scene

### AsciiEffect

Used to transform the rendered 3D scene into ASCII output.

Both are loaded from the browser through the existing import map.

---

## 🔬 Why ASCII?

The project is intentionally not another conventional Three.js character demo.

ASCII rendering creates a different visual layer between the underlying 3D scene and the visitor.

Instead of seeing the geometry directly:

```text
3D Scene
   ↓
Lighting
   ↓
Rasterized Render
   ↓
ASCII Conversion
   ↓
Character made from text
```

The result combines a traditional 3D animation pipeline with a much more constrained visual representation.

---

## 🛠️ Customization

The main systems are intentionally exposed in the source.

You can customize:

```javascript
EMOTIONS
THEMES
DENSITIES
```

You can also modify:

* character geometry
* lighting
* camera position
* ASCII ramps
* animation constants
* reaction behavior
* colors
* UI controls

The project is therefore useful as a starting point for experimenting with ASCII-rendered 3D scenes.

---

## 📁 Project Structure

The current implementation is intentionally compact:

```text
.
└── index.html
```

The HTML file contains:

```text
HTML
CSS
Three.js scene
Character construction
Expression system
Animation system
Theme system
ASCII renderer
Interaction handling
Persistence
Keyboard controls
```

This keeps the experiment easy to inspect and modify.

---

## 💡 What This Experiment Explores

This project is primarily an exploration of:

* browser-based 3D graphics
* ASCII rendering
* procedural character construction
* interactive animation
* state-driven expressions
* spring-based motion
* pointer interaction
* visual experimentation
* lightweight creative frontend development

It is intentionally experimental rather than a production application.

---

## 🔗 Project

**Repository**

https://github.com/hosseinb1111/ASCII-Character

---

## 👤 Author

**Hossein Seyed Bagheri**

Computer Engineering student and developer interested in web development, AI applications, interactive software, Cloudflare systems, realtime applications, and technical experiments.

---

## 📄 License

This project is under MIT Licence
