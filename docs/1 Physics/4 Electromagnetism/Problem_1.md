# Problem 1
# ⚡ Simulating the Effects of the Lorentz Force

## 🎯 Motivation

The **Lorentz force** governs the motion of charged particles under the influence of electric and magnetic fields. It plays a foundational role in fields such as plasma physics, particle accelerators, electromagnetic traps, and space physics. The force is defined by the equation:

\[
\vec{F} = q(\vec{E} + \vec{v} \times \vec{B})
\]

Where:
- \( \vec{F} \) is the total force on the particle,
- \( q \) is the electric charge,
- \( \vec{E} \) is the electric field,
- \( \vec{B} \) is the magnetic field,
- \( \vec{v} \) is the velocity of the particle.

By simulating this force, we gain intuition into how particles behave in controlled environments like cyclotrons or natural ones like the Earth’s magnetosphere.

---

## 🧠 Real-World Applications

The Lorentz force is pivotal in many systems, including:

- **Cyclotrons**: Charged particles undergo circular motion due to magnetic fields, gaining energy from oscillating electric fields.
- **Mass Spectrometers**: Ions are deflected by magnetic fields depending on their mass-to-charge ratio.
- **Tokamaks and Magnetic Confinement**: Plasma particles follow helical paths confined by toroidal magnetic fields.
- **Hall Effect Sensors**: Electrons pushed sideways by the Lorentz force create a measurable voltage.
- **Auroras**: Solar wind particles spiral along Earth's magnetic field lines, interacting with the atmosphere.

---

## ⚙️ Simulation Methodology

We simulate a charged particle’s motion under different configurations of electric and magnetic fields using the **Euler method**, solving Newton’s second law:

\[
\frac{d\vec{v}}{dt} = \frac{q}{m} (\vec{E} + \vec{v} \times \vec{B})
\]

We examine three primary scenarios:
1. **Uniform magnetic field only**
2. **Uniform electric and magnetic fields (parallel)**
3. **Crossed electric and magnetic fields (perpendicular)**

---

## 🧪 Python Code

```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

# Constants
q = 1.6e-19  # Charge (C)
m = 9.11e-31  # Mass (kg)
B = np.array([0, 0, 1])  # Magnetic field (T)
E = np.array([0, 0, 0])  # Electric field default (V/m)
v0 = np.array([1e5, 0, 0])  # Initial velocity (m/s)
r0 = np.array([0, 0, 0])  # Initial position
dt = 1e-11  # Time step (s)
steps = 5000  # Number of steps

def simulate_motion(E_field, B_field, v0, r0):
    r = np.zeros((steps, 3))
    v = np.zeros((steps, 3))
    r[0] = r0
    v[0] = v0
    for i in range(steps - 1):
        F = q * (E_field + np.cross(v[i], B_field))
        a = F / m
        v[i + 1] = v[i] + a * dt
        r[i + 1] = r[i] + v[i + 1] * dt
    return r

trajectory_B = simulate_motion(np.array([0, 0, 0]), B, v0, r0)
trajectory_EB = simulate_motion(np.array([0, 0, 1e3]), B, v0, r0)
trajectory_cross = simulate_motion(np.array([1e3, 0, 0]), B, v0, r0)

def plot_trajectory(r, title):
    fig = plt.figure(figsize=(10, 6))
    ax = fig.add_subplot(111, projection='3d')
    ax.plot(r[:, 0], r[:, 1], r[:, 2])
    ax.set_title(title)
    ax.set_xlabel('x (m)')
    ax.set_ylabel('y (m)')
    ax.set_zlabel('z (m)')
    plt.show()

plot_trajectory(trajectory_B, "Trajectory in Magnetic Field Only")
plot_trajectory(trajectory_EB, "Trajectory in Parallel E and B Fields")
plot_trajectory(trajectory_cross, "Trajectory in Crossed E and B Fields")

```
![alt text](image-4.png)
![alt text](image-5.png)
📈 Simulation Results and Interpretation
We visualize the results from each field configuration:

🔁 Case 1: Uniform Magnetic Field Only
The particle follows a circular path due to the influence of a magnetic field. This motion is described by the Larmor radius:
$$
r_L = \frac{m v_\perp}{q B}
$$
Where:

- \( r_L \): Larmor radius (radius of circular motion),
- \( m \): particle mass,
- \( v_\perp \): component of velocity perpendicular to the magnetic field \( \vec{B} \),
- \( q \): electric charge,
- \( B \): magnetic field strength.

This scenario produces **uniform circular motion** in the plane perpendicular to \( \vec{B} \).
🌀 **Case 2:**  
\( \vec{E} \parallel \vec{B} \) — Parallel Electric and Magnetic Fields

When the electric field \( \vec{E} \) is parallel to the magnetic field \( \vec{B} \), the particle undergoes **helical motion**. It spirals along the direction of the magnetic field while simultaneously being accelerated by the electric field:
$$
\vec{v}(t) = v_\perp \hat{\theta}(t) + v_{\parallel}(t) \hat{z}
$$
The circular motion remains in the plane perpendicular to \( \vec{B} \).

The particle gains speed along the field direction \( \hat{z} \), forming a helix.

➡️ **Case 3:**  
\( \vec{E} \perp \vec{B} \) — Crossed Electric and Magnetic Fields

In this configuration, the particle undergoes **spiral motion** while also drifting in the direction perpendicular to both \( \vec{E} \) and \( \vec{B} \). This drift is described by the \( \vec{E} \times \vec{B} \) drift velocity:
$$
\vec{v}_d = \frac{\vec{E} \times \vec{B}}{B^2}
$$
The motion still includes circular components due to \( \vec{B} \).

The particle drifts in a straight line at constant speed \( \vec{v}_d \).
🧮 Parameter Effects
Increasing Magnetic Field: Decreases the Larmor radius, tightens the spiral.

Stronger Electric Field: Increases the drift speed in crossed fields.

Heavier Particles: Larger mass means a larger radius and slower acceleration.

Charge Sign: Positive/negative particles spiral in opposite directions.

#📊 HTML Comparison Table
<table border="1">
  <tr>
    <th>Case</th>
    <th>Fields</th>
    <th>Motion Type</th>
    <th>Observation</th>
  </tr>
  <tr>
    <td>1</td>
    <td>B ≠ 0, E = 0</td>
    <td>Circular</td>
    <td>Larmor radius motion</td>
  </tr>
  <tr>
    <td>2</td>
    <td>E ∥ B</td>
    <td>Helical</td>
    <td>Acceleration along B</td>
  </tr>
  <tr>
    <td>3</td>
    <td>E ⊥ B</td>
    <td>Drift + Spiral</td>
    <td>Classic E × B drift</td>
  </tr>
</table>







