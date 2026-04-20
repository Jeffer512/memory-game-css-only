# Pure CSS Logic Engine: Memory Game

This repository contains a technical implementation of a memory matching game built entirely with **HTML5 and CSS3**. The project serves as a demonstration of using the DOM as a state-driven database without the use of JavaScript.

**Deployment:** https://jeffer512.github.io/memory-game-css-only/

## Project Origin
This project was originally developed as a group assignment during a web development bootcamp. The original codebase was audited to remove redundant CSS selectors. Specifically, invalid general sibling combinators (~) attempting to target elements preceding the trigger in the DOM.

## Technical Architecture

### 1. Declarative State Management (The Checkbox Hack)
The "memory" of the game is stored in the state of hidden `<input type="checkbox">` elements. 
*   **Input State:** Each card is associated with a specific ID.
*   **Trigger:** `<label>` elements are used as the UI interface to toggle these inputs via the `for` attribute.
*   **Logic Gates:** The **General Sibling Combinator (`~`)** is used to evaluate the state of the inputs and apply styles to the "boxes" container based on which IDs are currently `:checked`.

### 2. 3D Transform & Rendering
The card-flipping mechanism utilizes the CSS 3D rendering context:
*   **`transform-style: preserve-3d`**: Ensures that the front and back faces of the cards maintain their coordinates in 3D space during rotation.
*   **`backface-visibility: hidden`**: Prevents the "mirror image" of the faces from rendering when turned away from the user, ensuring a clean transition.
*   **`rotateY(180deg)`**: Used to pre-orient the back face and to flip the parent container when the state changes.

### 3. Simulated Randomization
Since CSS cannot generate random values, a **High-Speed Grid Shuffle** was implemented:
*   **Grid Areas:** Each card is assigned a unique `grid-area`.
*   **Layout Animation:** A high-frequency `@keyframes` animation redefines the `grid-template-areas` map every few milliseconds.
*   **State Locking:** When the "Start" checkbox is toggled, the `animation-play-state` is set to `paused`, effectively "freezing" the cards in a pseudo-random configuration.
