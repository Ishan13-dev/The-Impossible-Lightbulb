# 💡 The Impossible Lightbulb

An interactive animated lightbulb experiment built with **HTML, CSS, SVG, and JavaScript**, powered by **GSAP**.

The concept is simple: **turn on the light by pulling the cord**.

The problem?

**The lightbulb doesn't exactly want to cooperate.** 🐻

Try pulling the cord. Pull it farther. Pull it repeatedly. The experience reacts with animated SVG elements, a moving door, and an increasingly angry bear.

### 🔗 Live Demo

**[The Impossible Lightbulb](https://ishan13-dev.github.io/The-Impossible-Lightbulb/)**

---

## ✨ Features

* 💡 Interactive SVG lightbulb
* 🪢 Drag-and-pull light cord
* 🐻 Animated bear that reacts to repeated attempts
* 🚪 3D-style animated door
* 🎨 Dynamic light/dark environment
* ⚡ GSAP-powered animations
* 🧬 SVG path morphing with MorphSVGPlugin
* 🖱️ Draggable interaction using GSAP Draggable
* 🔊 Interactive sound effects
* 📱 Responsive design using viewport-based CSS sizing
* 🎭 Dynamic bear anger system
* 🌈 CSS custom properties used for dynamic lighting and colors
* 🧩 Pure frontend implementation with no framework

---

## 🎮 How It Works

The main interaction is the hanging cord.

Users can **click/touch and drag the cord**. JavaScript calculates how far the cord was pulled.

If the user pulls far enough, the animation sequence begins.

### Interaction Flow

```text
User grabs cord
       ↓
Cord follows pointer
       ↓
Release cord
       ↓
Calculate pulling distance
       ↓
     ┌───────────────┐
     │ Distance > 50 │
     └───────┬───────┘
             │
          Yes│
             ↓
      Trigger animation
             ↓
      Door opens
             ↓
       Bear appears
             ↓
      Bear reacts
             ↓
       Door closes
             ↓
     Cord resets
```

Repeated unsuccessful interactions increase the bear's **anger state**, eventually causing its eyebrows to appear.

Because apparently even a fictional bear has a lower tolerance for user error than most software engineers.

---

## 🛠️ Technologies Used

### HTML5

The structure of the project is created using semantic HTML elements and inline SVG graphics.

The SVG scene contains:

* Lightbulb
* Pull cord
* Bear arms and paws
* Bear
* Door
* Door handle
* Interactive hit area

The project also uses external GSAP libraries through CDN scripts.

### CSS3

CSS handles:

* Layout
* Responsive sizing
* Dynamic colors
* Lighting effects
* Door styling
* 3D transformations
* SVG styling
* CSS custom properties

A major part of the visual system is controlled through CSS variables such as:

```css
--on
--depth
--size
--bg
--cord
--stroke
--shine
--cap
--filament
```

The `--on` variable controls the visual state of the environment.

---

## ⚡ JavaScript & GSAP

The interaction and animation system is built with **GSAP**.

The project uses:

* GSAP Timeline
* GSAP `set()`
* GSAP `to()`
* GSAP `Draggable`
* GSAP `MorphSVGPlugin`
* GSAP utility functions

External dependencies are loaded directly in `index.html`:

```html
<script src="https://unpkg.co/gsap@3/dist/gsap.min.js"></script>
<script src="https://assets.codepen.io/16327/MorphSVGPlugin3.min.js"></script>
<script src="https://unpkg.com/gsap@3/dist/Draggable.min.js"></script>
```

---

## 🧬 SVG Morphing

The pull cord is not just a static line.

Multiple SVG cord paths are defined and GSAP's **MorphSVGPlugin** is used to transition between them.

This creates the visual effect of the cord bending and moving during interaction.

Conceptually:

```text
Straight Cord
     ↓
Curved Cord
     ↓
Different Cord Shape
     ↓
Cord Returns
     ↓
Reset
```

This makes the interaction feel much more physical than simply moving an HTML element.

---

## 🪢 Drag Interaction

GSAP's `Draggable` API is used to control the invisible proxy element associated with the cord.

When the user presses the cord:

```javascript
onPress
```

the starting coordinates are recorded.

While dragging:

```javascript
onDrag
```

the SVG cord endpoint follows the pointer.

When released:

```javascript
onRelease
```

the total travel distance is calculated.

The project uses the Euclidean distance formula:

```text
distance = √(Δx² + Δy²)
```

If the travelled distance exceeds `50px`, the main interaction animation is triggered.

---

## 🐻 Bear Reaction System

The bear has an internal anger state:

```javascript
const STATE = {
  ON: false,
  ANGER: 0
};
```

Each successful interaction can increase:

```javascript
STATE.ANGER
```

The bear's animation behavior changes based on this value.

For example, higher anger can result in:

* Faster arm movement
* Faster animations
* Different movement timing
* Visible eyebrows

The eyebrow threshold is controlled through:

```javascript
BROWS: 4
```

So after enough interactions, the bear starts looking considerably less interested in helping you.

---

## 🚪 Animated Door

The door uses CSS 3D transformations combined with GSAP.

Opening:

```javascript
rotateY: 25
```

Closing:

```javascript
rotateY: 0
```

The door also changes visually according to the light state through CSS variables.

This creates the illusion that the environment itself is reacting to the lightbulb.

---

## 💡 Dynamic Lighting

The project uses CSS custom properties to dynamically change the environment.

For example:

```css
--bg: hsl(
  calc(200 - (var(--on) * 160)),
  calc((20 + (var(--on) * 50)) * 1%),
  calc((20 + (var(--on) * 60)) * 1%)
);
```

When the light state changes, the background, bulb, filament, cord, and door can visually transition between states.

This avoids manually changing multiple CSS properties with JavaScript.

Instead:

```text
JavaScript
    ↓
--on changes
    ↓
CSS recalculates colors
    ↓
Entire scene changes
```

---

## 🔊 Audio

The project also defines audio effects for different interactions:

* Bear sounds
* Door opening
* Door closing
* Click sound

Example:

```javascript
const AUDIO = {
  BEAR_LONG: new Audio('...'),
  BEAR_SHORT: new Audio('...'),
  DOOR_OPEN: new Audio('...'),
  DOOR_CLOSE: new Audio('...'),
  CLICK: new Audio('...')
};
```

Some bear audio behavior is currently commented out in the JavaScript, so the audio system exists but can be expanded further.

---

## 📁 Project Structure

A simple version of the project can be organized as:

```text
The-Impossible-Lightbulb/
│
├── index.html
├── style.css
├── script.js
└── README.md
```

### `index.html`

Contains:

* Page structure
* SVG artwork
* Lightbulb
* Cord
* Bear
* Door
* External library imports

### `style.css`

Contains:

* Layout
* Colors
* Responsive sizing
* SVG styling
* Door styling
* 3D effects
* Animation-related styles

### `script.js`

Contains:

* GSAP animation logic
* Drag interaction
* Cord morphing
* Bear behavior
* Door animation
* Light state
* Audio
* Interaction calculations

---

## 🚀 Running Locally

Clone the repository:

```bash
git clone https://github.com/ishan13-dev/The-Impossible-Lightbulb.git
```

Move into the project:

```bash
cd The-Impossible-Lightbulb
```

Then open:

```text
index.html
```

in a browser.

Because the project uses CDN-hosted libraries, an internet connection may be required for all external dependencies and audio assets to load correctly.

---

## 🌐 Deployment

The project is deployed using **GitHub Pages**.

### Live Website

**https://ishan13-dev.github.io/The-Impossible-Lightbulb/**

The site is completely client-side, so no backend or server is required.

---

## 🧠 What I Learned

This project explores several useful frontend concepts:

* Working with inline SVG
* Manipulating SVG elements with JavaScript
* GSAP animation timelines
* GSAP Draggable
* SVG path morphing
* CSS custom properties
* CSS 3D transformations
* Pointer-based interactions
* Event-driven animation
* State management in JavaScript
* Calculating interaction distance
* Coordinating multiple animations
* Building interactive UI without a frontend framework

---

## 🔮 Possible Improvements

Some ideas for future versions:

* [ ] Add better mobile/touch optimization
* [ ] Add a proper sound on/off control
* [ ] Enable the full bear sound system
* [ ] Add more bear reactions
* [ ] Add different difficulty levels
* [ ] Add a visible interaction counter
* [ ] Add particle effects when the bulb turns on
* [ ] Add more environmental animations
* [ ] Add keyboard accessibility
* [ ] Improve accessibility for screen readers
* [ ] Add reduced-motion support
* [ ] Store interaction state using `localStorage`
* [ ] Add a reset button
* [ ] Add additional interactive characters
* [ ] Add a loading state for external assets

---

## 📜 Credits & Dependencies

This project uses:

* **GSAP** for animation
* **GSAP MorphSVGPlugin** for SVG path morphing
* **GSAP Draggable** for drag interaction
* SVG for the visual scene
* CodePen-hosted assets for some external resources

The implementation is primarily built with vanilla:

```text
HTML + CSS + JavaScript + SVG
```

No React.

No Vue.

No massive dependency jungle.

Just frontend code doing frontend things.

---

## 👨‍💻 Author

**Ishan Verma**

GitHub:
https://github.com/ishan13-dev

Project:
https://github.com/ishan13-dev/The-Impossible-Lightbulb

Live Demo:
https://ishan13-dev.github.io/The-Impossible-Lightbulb/

---

## ⭐ Support

If you found the project interesting, consider giving the repository a ⭐ on GitHub.

Every star is a tiny indication that humans occasionally appreciate unnecessarily complicated animated light switches.
