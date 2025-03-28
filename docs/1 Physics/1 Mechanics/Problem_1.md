# Problem 1
Below is a comprehensive Markdown document addressing your task on projectile motion. It includes theoretical derivations, analysis, practical applications, and a Python implementation with visualizations.

---

# Projectile Motion: Analysis and Simulation

Projectile motion is a classic problem in physics that describes the motion of an object under the influence of gravity alone, neglecting factors like air resistance in its idealized form. This document derives the governing equations, analyzes the range as a function of the angle of projection, explores practical applications, and provides a Python simulation to visualize the results.

## 1. Theoretical Foundation

### Derivation of Governing Equations

Projectile motion occurs in two dimensions: horizontal (x) and vertical (y). We assume the only force acting is gravity, with acceleration \( g \) downward, and no horizontal forces. Let’s derive the equations from Newton’s second law.

#### Horizontal Motion
No forces act in the x-direction, so acceleration \( a_x = 0 \). If the initial velocity has a horizontal component \( v_{0x} = v_0 \cos\theta \) (where \( v_0 \) is the initial speed and \( \theta \) is the projection angle), the position is:

\[
x(t) = v_{0x} t = v_0 \cos\theta \cdot t
\]

#### Vertical Motion
The vertical acceleration is \( a_y = -g \). The initial vertical velocity is \( v_{0y} = v_0 \sin\theta \). Using the kinematic equation \( y(t) = y_0 + v_{0y} t + \frac{1}{2} a_y t^2 \), with initial height \( y_0 = h \):

\[
y(t) = h + v_0 \sin\theta \cdot t - \frac{1}{2} g t^2
\]

The vertical velocity is:

\[
v_y(t) = v_{0y} + a_y t = v_0 \sin\theta - g t
\]

#### Time of Flight
The projectile hits the ground when \( y(t) = 0 \). Solving:

\[
0 = h + v_0 \sin\theta \cdot t - \frac{1}{2} g t^2
\]

Multiply through by 2 and rearrange:

\[
g t^2 - 2 v_0 \sin\theta \cdot t - 2h = 0
\]

Using the quadratic formula \( t = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a} \), where \( a = g \), \( b = -2 v_0 \sin\theta \), \( c = -2h \):

\[
t = \frac{2 v_0 \sin\theta \pm \sqrt{(2 v_0 \sin\theta)^2 + 8 g h}}{2 g}
\]

\[
t = \frac{v_0 \sin\theta \pm \sqrt{v_0^2 \sin^2\theta + 2 g h}}{g}
\]

The positive root gives the time of flight. For \( h = 0 \):

\[
t_f = \frac{2 v_0 \sin\theta}{g}
\]

#### Family of Solutions
The equations \( x(t) \) and \( y(t) \) form a parametric family of solutions depending on \( v_0 \), \( \theta \), \( g \), and \( h \). Variations in these parameters yield parabolas of different shapes, ranges, and heights, describing diverse trajectories.

## 2. Analysis of the Range

### Horizontal Range
The range \( R \) is the horizontal distance when \( y(t) = 0 \). Substitute \( t_f = \frac{2 v_0 \sin\theta}{g} \) (for \( h = 0 \)) into \( x(t) \):

\[
R = v_0 \cos\theta \cdot \frac{2 v_0 \sin\theta}{g} = \frac{2 v_0^2 \sin\theta \cos\theta}{g}
\]

Using the identity \( \sin 2\theta = 2 \sin\theta \cos\theta \):

\[
R = \frac{v_0^2 \sin 2\theta}{g}
\]

- **Dependence on \( \theta \)**: The range peaks when \( \sin 2\theta = 1 \), i.e., \( 2\theta = 90^\circ \), so \( \theta = 45^\circ \). \( R = 0 \) at \( \theta = 0^\circ \) and \( 90^\circ \).
- **Effect of \( v_0 \)**: Range scales with \( v_0^2 \), so doubling \( v_0 \) quadruples \( R \).
- **Effect of \( g \)**: Range is inversely proportional to \( g \). On the Moon (\( g \approx 1.62 \, \text{m/s}^2 \)), \( R \) is larger than on Earth (\( g \approx 9.8 \, \text{m/s}^2 \)).

For \( h \neq 0 \), the range depends on the full time-of-flight expression, complicating the relationship but still showing a maximum near \( 45^\circ \) (shifted slightly depending on \( h \)).

## 3. Practical Applications

- **Sports**: The model describes a kicked soccer ball or a thrown javelin, though air resistance modifies the trajectory in practice.
- **Engineering**: Artillery and rocket launches use adjusted versions accounting for drag and wind.
- **Astrophysics**: On other planets, varying \( g \) alters trajectories (e.g., Mars rovers’ landing systems).
- **Uneven Terrain**: If landing height differs from launch height, adjust \( y(t) = h_{\text{land}} \) and solve for \( t \).
- **Air Resistance**: Introduce a drag term (e.g., \( -k v \)) in the differential equations, requiring numerical solutions.

## 4. Implementation

Below is a Python script to simulate and visualize projectile motion.

```python
import numpy as np
import matplotlib.pyplot as plt

def projectile_range(v0, theta_deg, g=9.8, h=0):
    """Calculate range given initial velocity, angle (degrees), gravity, and height."""
    theta = np.radians(theta_deg)
    term = v0**2 * np.sin(2 * theta) / g
    if h != 0:
        t_flight = (v0 * np.sin(theta) + np.sqrt((v0 * np.sin(theta))**2 + 2 * g * h)) / g
        return v0 * np.cos(theta) * t_flight
    return term

# Parameters
v0_values = [10, 20, 30]  # Initial velocities (m/s)
g = 9.8  # Gravity (m/s^2)
h = 0  # Initial height (m)
theta_deg = np.linspace(0, 90, 91)  # Angles from 0 to 90 degrees

# Compute ranges
plt.figure(figsize=(10, 6))
for v0 in v0_values:
    ranges = [projectile_range(v0, t, g, h) for t in theta_deg]
    plt.plot(theta_deg, ranges, label=f'v0 = {v0} m/s')

# Plot settings
plt.title('Projectile Range vs. Angle of Projection')
plt.xlabel('Angle (degrees)')
plt.ylabel('Range (m)')
plt.legend()
plt.grid(True)
plt.show()

# Example trajectory
def trajectory(v0, theta_deg, g=9.8, h=0):
    theta = np.radians(theta_deg)
    t_flight = (v0 * np.sin(theta) + np.sqrt((v0 * np.sin(theta))**2 + 2 * g * h)) / g
    t = np.linspace(0, t_flight, 100)
    x = v0 * np.cos(theta) * t
    y = h + v0 * np.sin(theta) * t - 0.5 * g * t**2
    return x, y

x, y = trajectory(20, 45)
plt.figure(figsize=(10, 6))
plt.plot(x, y)
plt.title('Projectile Trajectory (v0 = 20 m/s, θ = 45°)')
plt.xlabel('Distance (m)')
plt.ylabel('Height (m)')
plt.grid(True)
plt.show()
```

### Output Description
- **Range vs. Angle**: The first plot shows \( R \) vs. \( \theta \) for different \( v_0 \). The peak at 45° is evident, with higher \( v_0 \) yielding greater ranges.
- **Trajectory**: The second plot visualizes a single trajectory, confirming the parabolic shape.

## Limitations and Extensions

- **Idealized Model**: Assumes no air resistance, constant \( g \), and flat terrain.
- **Drag**: Add \( F_d = -k v \) or \( F_d = -c v^2 \) to the equations, solved numerically (e.g., using `scipy.integrate.odeint`).
- **Wind**: Include a velocity-dependent term in the horizontal equation.
- **Terrain**: Model \( y_{\text{ground}}(x) \) and find intersection numerically.

This analysis and simulation highlight the elegance and versatility of projectile motion, bridging theory and application across physics and beyond.

--- 

This document fulfills the deliverables with derivations, analysis, visualizations, and a discussion of limitations. Let me know if you’d like further refinements!