# Problem 1
Below is a comprehensive Markdown document addressing your task on projectile motion. It includes a theoretical derivation, analysis of the range, practical applications, and a Python script for simulation and visualization.

---

# Projectile Motion: Analysis and Simulation

## 1. Theoretical Foundation

Projectile motion describes the trajectory of an object launched into the air, subject only to gravity (in the idealized case). Let’s derive the governing equations from Newton’s second law.

### Derivation of Equations of Motion

Assume a projectile is launched from the origin \((x_0, y_0) = (0, 0)\) with an initial velocity \(v_0\) at an angle \(\theta\) to the horizontal. Gravity acts downward with acceleration \(-g\). We neglect air resistance for now.

- **Forces**: The only force is gravity, \(F_y = -mg\), and \(F_x = 0\).
- **Acceleration**: \(a_x = 0\), \(a_y = -g\).

Using Newton’s second law (\(F = ma\)) and integrating with respect to time:
- **X-direction** (no acceleration):
  - Velocity: \(v_x = v_0 \cos\theta\) (constant).
  - Position: \(x(t) = (v_0 \cos\theta) t\).
- **Y-direction** (constant acceleration \(-g\)):
  - Velocity: \(v_y = v_0 \sin\theta - gt\).
  - Position: \(y(t) = (v_0 \sin\theta) t - \frac{1}{2} g t^2\).

These are parametric equations describing a parabola. The initial conditions (\(v_0, \theta, g\)) define a family of solutions, as varying these parameters alters the trajectory’s shape and extent.

### Family of Solutions

- **Initial Velocity (\(v_0\))**: Higher \(v_0\) increases the parabola’s width and height.
- **Angle (\(\theta\))**: Affects the balance between horizontal and vertical components.
- **Gravity (\(g\))**: Stronger gravity compresses the trajectory vertically.

## 2. Analysis of the Range

The horizontal range \(R\) is the distance traveled when the projectile returns to \(y = 0\).

### Range Derivation

Set \(y(t) = 0\):
\[
0 = (v_0 \sin\theta) t - \frac{1}{2} g t^2
\]
Factorize:
\[
t \left( v_0 \sin\theta - \frac{1}{2} g t \right) = 0
\]
Solutions: \(t = 0\) (launch) or \(t = \frac{2 v_0 \sin\theta}{g}\) (landing). Substitute into \(x(t)\):
\[
R = x\left(\frac{2 v_0 \sin\theta}{g}\right) = (v_0 \cos\theta) \cdot \frac{2 v_0 \sin\theta}{g} = \frac{2 v_0^2 \sin\theta \cos\theta}{g}
\]
Using the identity \(2 \sin\theta \cos\theta = \sin 2\theta\):
\[
R = \frac{v_0^2 \sin 2\theta}{g}
\]

### Dependence on Angle (\(\theta\))
- \(R\) is maximized when \(\sin 2\theta = 1\), i.e., \(\theta = 45^\circ\), yielding \(R_{\text{max}} = \frac{v_0^2}{g}\).
- \(R = 0\) at \(\theta = 0^\circ\) or \(90^\circ\), as the projectile moves horizontally or vertically.
- Complementary angles (e.g., \(30^\circ\) and \(60^\circ\)) yield the same range since \(\sin 2\theta = \sin (180^\circ - 2\theta)\).

### Influence of Other Parameters
- **Initial Velocity (\(v_0\))**: \(R \propto v_0^2\), a quadratic relationship.
- **Gravity (\(g\))**: \(R \propto \frac{1}{g}\), so weaker gravity (e.g., on the Moon) increases range.

## 3. Practical Applications

This model applies to:
- **Sports**: Optimizing a basketball shot or a golf ball’s flight.
- **Engineering**: Designing artillery or water fountains.
- **Astrophysics**: Approximating satellite launches (neglecting air).

### Extensions
- **Uneven Terrain**: If launched from height \(h\), the time to ground changes, modifying \(R\).
- **Air Resistance**: Introduces a drag force proportional to velocity, requiring numerical solutions.

## 4. Implementation

Here’s a Python script to simulate and visualize projectile motion.

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
g = 9.81  # m/s^2

# Function to calculate range
def projectile_range(v0, theta_deg, g=9.81):
    theta = np.radians(theta_deg)
    return (v0**2 * np.sin(2 * theta)) / g

# Simulation parameters
v0_values = [10, 15, 20]  # Initial velocities (m/s)
theta_deg = np.arange(0, 91, 1)  # Angles from 0 to 90 degrees

# Plot range vs angle for different v0
plt.figure(figsize=(10, 6))
for v0 in v0_values:
    R = [projectile_range(v0, t) for t in theta_deg]
    plt.plot(theta_deg, R, label=f'v0 = {v0} m/s')

plt.xlabel('Angle of Projection (degrees)')
plt.ylabel('Range (m)')
plt.title('Projectile Range vs Angle of Projection')
plt.legend()
plt.grid(True)
plt.show()

# Trajectory simulation for v0 = 15 m/s, theta = 45°
v0 = 15
theta = np.radians(45)
t_flight = 2 * v0 * np.sin(theta) / g
t = np.linspace(0, t_flight, 100)
x = v0 * np.cos(theta) * t
y = v0 * np.sin(theta) * t - 0.5 * g * t**2

plt.figure(figsize=(10, 6))
plt.plot(x, y, label='Trajectory (v0 = 15 m/s, θ = 45°)')
plt.xlabel('Horizontal Distance (m)')
plt.ylabel('Height (m)')
plt.title('Projectile Trajectory')
plt.legend()
plt.grid(True)
plt.show()
```

### Outputs
1. **Range vs Angle Plot**: Shows \(R\) peaking at 45° for different \(v_0\).
2. **Trajectory Plot**: Visualizes the parabolic path for a specific case.

## Discussion

### Limitations
- **Idealization**: Assumes no air resistance, flat terrain, and constant gravity.
- **Realism**: Drag reduces range and alters the trajectory from a parabola to a skewed curve.

### Suggestions
- **Drag**: Add a term \(-k v\) to the equations and solve numerically.
- **Wind**: Introduce a horizontal force component.
- **Terrain**: Adjust \(y(t)\) for variable ground height.

This analysis and simulation highlight projectile motion’s elegance and adaptability, bridging theory and application across diverse fields.

---

This document fulfills the deliverables with derivations, analysis, visualizations, and a discussion of limitations and extensions. Let me know if you’d like further refinements!