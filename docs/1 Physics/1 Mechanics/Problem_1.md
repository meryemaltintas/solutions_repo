# Problem 1

# Projectile Motion: Analysis and Simulation

#Motivation

Projectile motion, while seemingly simple, offers a rich playground for exploring fundamental principles of physics. The problem is straightforward: analyze how the range of a projectile depends on its angle of projection. Yet, beneath this simplicity lies a complex and versatile framework. The equations governing projectile motion involve both linear and quadratic relationships, making them accessible yet deeply insightful.

What makes this topic particularly compelling is the number of free parameters involved in these equations, such as initial velocity, gravitational acceleration, and launch height. These parameters give rise to a diverse set of solutions that can describe a wide array of real-world phenomena, from the arc of a soccer ball to the trajectory of a rocket.

## 1. Theoretical Foundation

Projectile motion describes the trajectory of an object launched into the air, subject only to gravity in the idealized case. We start with Newton’s second law to derive the governing equations, assuming no air resistance.

### Derivation of Equations of Motion

We consider a projectile launched with an initial velocity \(v_0\) at an angle \(\theta\) from the horizontal, with gravity acting downward (\(a_y = -g\)).

#### Coordinate System and Initial Conditions
- **X-axis**: Horizontal direction (positive rightward).
- **Y-axis**: Vertical direction (positive upward).
- Initial velocity components:
  - \(v_x(0) = v_0 \cos\theta\)
  - \(v_y(0) = v_0 \sin\theta\)
- Initial position: \((x_0, y_0) = (0, 0)\).

#### Equations of Motion
The only force is gravity, acting along the y-axis (\(a_y = -g\)), with \(a_x = 0\).

- **Horizontal Motion** (constant velocity):

  $$
  \frac{d^2 x(t)}{dt^2} = 0 \quad \text{(no acceleration in x-direction)}
  \frac{dx(t)}{dt} = v_0 \cos\theta
  $$

  Integrating:
  \[
  x(t) = v_0 \cos\theta \cdot t
  \]

- **Vertical Motion** (constant acceleration):

  $$
  \frac{d^2 y(t)}{dt^2} = -g
  \frac{dy(t)}{dt} = v_0 \sin\theta - g t
  $$

  Integrating again:
  
  $$
  y(t) = v_0 \sin\theta \cdot t - \frac{1}{2} g t^2
  $$

These are the parametric equations of motion, forming a parabolic trajectory.

### Family of Solutions
The parameters (\(v_0, \theta, g\)) define a family of solutions:
- **Initial Velocity (\(v_0\))**: Higher \(v_0\) increases the parabola’s width and height.
- **Angle (\(\theta\))**: Affects the balance between horizontal and vertical components.
- **Gravity (\(g\))**: Stronger gravity compresses the trajectory vertically.

## 2. Analysis of the Range

The horizontal range \(R\) is the distance traveled when the projectile returns to \(y = 0\).

### Range Derivation
Set \(y(t) = 0\):
$$
0 = (v_0 \sin\theta) t - \frac{1}{2} g t^2
$$
$$
t \left( v_0 \sin\theta - \frac{1}{2} g t \right) = 0
$$
Solutions: \(t = 0\) (launch) or \(t = \frac{2 v_0 \sin\theta}{g}\) (landing). Substitute into \(x(t)\):

$$
R = x\left(\frac{2 v_0 \sin\theta}{g}\right) = (v_0 \cos\theta) \cdot \frac{2 v_0 \sin\theta}{g} = \frac{2 v_0^2 \sin\theta \cos\theta}{g}
$$

Using \(2 \sin\theta \cos\theta = \sin 2\theta\):
$$
R = \frac{v_0^2 \sin 2\theta}{g}
$$

### Dependence on Angle (\(\theta\))
- Maximum range at \(\theta = 45^\circ\) (\(\sin 2\theta = 1\)): \(R_{\text{max}} = \frac{v_0^2}{g}\).
- \(R = 0\) at \(\theta = 0^\circ\) or \(90^\circ\).
- Complementary angles (e.g., \(30^\circ\) and \(60^\circ\)) yield the same range.

### Influence of Other Parameters
- **Initial Velocity (\(v_0\))**: \(R \propto v_0^2\).
- **Gravity (\(g\))**: \(R \propto \frac{1}{g}\).

## 3. Practical Applications
- **Sports**: Optimizing a basketball shot or golf ball flight.
- **Engineering**: Designing artillery or water fountains.
- **Astrophysics**: Approximating low-altitude satellite trajectories.

### Extensions
- **Uneven Terrain**: Adjust landing condition for height \(h\).
- **Air Resistance**: Add drag force, solve numerically.

## 4. Implementation

Below is a Python script to simulate and visualize projectile motion, including range vs. angle and trajectory plots.

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
1. **Range vs Angle Plot**: Shows how range varies with angle for different initial velocities, peaking at 45°.
2. **Trajectory Plot**: Displays the parabolic path for \(v_0 = 15 \, \text{m/s}, \theta = 45^\circ\).

## 5. Discussion

### Limitations
- Assumes no air resistance, flat terrain, and constant gravity.
- Real-world trajectories deviate due to drag and wind.

### Suggestions
- **Drag**: Add a \(-k v\) term and solve numerically.
- **Wind**: Include a horizontal force.
- **Terrain**: Adjust \(y(t)\) for variable ground height.

This analysis and simulation highlight projectile motion’s elegance and adaptability, bridging theory and application across diverse fields.

---

### Explanation of Changes
- **Theoretical Foundation**: The derivation now exactly matches your friend's screenshot, including the use of `\frac` for fractions in the equations (e.g., \(\frac{d^2 x(t)}{dt^2}\), \(\frac{1}{2} g t^2\)).
- **Consistency**: Ensured that the notation and structure align with the screenshot while maintaining clarity in English.
- **Simulation Code**: Kept the corrected Python script from the previous response, ensuring it runs without errors.
- **Outputs**: Described the graphical outputs as required.
- **Discussion**: Included limitations and suggestions for extensions, addressing real-world factors like drag and wind.


![alt text](image-2.png)
