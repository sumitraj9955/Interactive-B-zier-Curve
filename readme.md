# Interactive Physics Bézier Curve

A visual simulation of a "rope-like" curve that reacts naturally to mouse movements. This project implements a **Cubic Bézier Curve** from scratch, using a custom physics engine to animate the control points.

## How to Run
1. Download or clone this repository.
2. Open `index.html` in any modern web browser (Chrome, Firefox, Edge).
3. Move your mouse to interact with the curve!

---

## The Math (Bézier Logic)
Instead of using built-in drawing tools, I calculated the curve manually using the **Cubic Bézier Formula**.

The curve is defined by **4 points**:
1. **P0 & P3 (Anchors):** Fixed points on the left and right edges.
2. **P1 & P2 (Controls):** Invisible points that pull the curve to give it shape.

### The Formula
To draw the smooth line, the code calculates hundreds of tiny dots along the path ($t$ going from 0 to 1) using this equation:

```math
B(t) = (1-t)³P₀ + 3(1-t)²tP₁ + 3(1-t)t²P₂ + t³P₃
```

### Tangents (Direction Lines)
To visualize the direction of the curve (the blue lines), I calculated the **Derivative** of the curve. This tells us the exact slope at any given point.

---

## The Physics Model
The curve doesn't just snap to the mouse instantly. To make it feel like a heavy rope, the control points ($P_1, P_2$) follow a **Spring-Damper System**.

### How it works:
1. **Target:** The mouse position acts as a "magnet."
2. **Spring Force:** The further the points are from the mouse, the harder they are pulled.
3. **Damping (Friction):** As the points move, "air resistance" slows them down so they don't bounce forever.

**Physics Logic:**
```js
Acceleration = (Target - Position) * Stiffness
Velocity = (Velocity + Acceleration) * Damping
Position = Position + Velocity
```

*   **Stiffness:** 0.08 (How snappy the rope is)
*   **Damping:** 0.85 (How fast it settles down)

---

##  Design Choices

1.  **From Scratch:** No external libraries (like Matter.js or D3.js) were used. All vector math and physics logic are written in pure JavaScript.
2.  **Visual Debugging:**
    *   **⚪ White Line:** The actual curve.
    *   **🔴 Red Dots:** The physics control points (usually invisible in drawing apps, but shown here to understand the movement).
    *   **🔵 Blue Lines:** Tangent vectors showing the curve's flow.
3.  **Modular Code:** The code is split into clear classes (`Vector2`, `SpringPoint`, `BezierCurve`) to keep the math separate from the drawing logic.

---

