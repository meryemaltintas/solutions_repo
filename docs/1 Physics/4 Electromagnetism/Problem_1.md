# Problem 1
# Problem 1: Simulating the Effects of the Lorentz Force

## Motivation:

The **Lorentz force** is a fundamental concept governing the motion of charged particles in electric and magnetic fields. It plays a critical role in various applications, including plasma physics, particle accelerators, and astrophysics. By simulating particle motion under the influence of these forces, we can visualize the complex paths that particles take in different field configurations.

---

## Task Overview:

### 1. Exploration of Applications:
   - Identify systems where the Lorentz force is crucial (e.g., particle accelerators, mass spectrometers, plasma confinement).
   - Discuss how **electric (\( \mathbf{E} \))** and **magnetic (\( \mathbf{B} \))** fields influence particle motion.

### 2. Simulating Particle Motion:
   - Implement a simulation to compute and visualize the trajectory of a charged particle under:
     - A uniform magnetic field.
     - Combined uniform electric and magnetic fields.
     - Crossed electric and magnetic fields.

   Simulate the particle’s circular, helical, or drift motion based on the initial conditions and field configurations.

### 3. Parameter Exploration:
   - Allow variations in:
     - Field strengths (\( B \), \( E \))
     - Initial particle velocity (\( \mathbf{v} \))
     - Charge and mass of the particle (\( q \), \( m \))

   Observe how these parameters affect the trajectory.

### 4. Visualization:
   - Highlight key physical phenomena such as the **Larmor radius** and **drift velocity**.


```python
import numpy as np
import matplotlib.pyplot as plt
# Constants
q = 1.6e-19  # Charge of the particle (Coulombs)
m = 1.67e-27  # Mass of the particle (kg), for example, a proton
B = 1.0  # Magnetic field strength (Tesla)
E = np.array([0.0, 0.0, 0.0])  # Electric field (V/m), assume zero in this example
v0 = np.array([1e5, 0, 0])  # Initial velocity (m/s)
r0 = np.array([0, 0, 0])  # Initial position (m)

# Time parameters
t_max = 1e-5  # Total simulation time (seconds)
dt = 1e-7  # Time step (seconds)
num_steps = int(t_max / dt)

# Arrays for position and velocity
r = np.zeros((num_steps, 3))
v = np.zeros((num_steps, 3))
r[0] = r0
v[0] = v0

# Euler method for numerical solution
for i in range(1, num_steps):
    # Lorentz force: F = q(E + v x B)
    cross_product = np.cross(v[i-1], [0, 0, B])  # v x B
    F = q * (E + cross_product)  # Lorentz force
    
    # Update velocity and position using Euler method
    a = F / m  # Acceleration
    v[i] = v[i-1] + a * dt  # Update velocity
    r[i] = r[i-1] + v[i] * dt  # Update position

# Larmor Radius (for visualization)
v_perp = np.linalg.norm(v0[:2])  # Perpendicular velocity component (in x-y plane)
r_L = m * v_perp / (abs(q) * B)  # Larmor radius

# 2D Plot
plt.figure(figsize=(8, 6))
plt.plot(r[:, 0], r[:, 1], label='Particle Path')
plt.title('Particle Path in a Magnetic Field', fontsize=14, color='blue')
plt.xlabel('X Position (m)', fontsize=12, color='green')
plt.ylabel('Y Position (m)', fontsize=12, color='green')
plt.grid(True)

# Highlighting Larmor Radius
circle = plt.Circle((r0[0], r0[1]), r_L, color='r', fill=False, linestyle='--', label='Larmor Radius')
plt.gca().add_artist(circle)

plt.legend()
plt.show()

# 3D Plot
fig = plt.figure(figsize=(10, 8))
ax = fig.add_subplot(111, projection='3d')
ax.plot(r[:, 0], r[:, 1], r[:, 2], label='Particle Path')
ax.set_title('3D Particle Path in a Magnetic Field', fontsize=14, color='blue')
ax.set_xlabel('X Position (m)', fontsize=12, color='green')
ax.set_ylabel('Y Position (m)', fontsize=12, color='green')
ax.set_zlabel('Z Position (m)', fontsize=12, color='green')
ax.grid(True)

plt.show()
```
![alt text](image-2.png)



## The Mathematical Model:

The **Lorentz force** is given by the equation:

$$
\mathbf{F} = q \cdot \left( \mathbf{E} + \mathbf{v} \times \mathbf{B} \right)
$$

Where:
- \( \mathbf{F} \) is the Lorentz force,
- \( q \) is the charge of the particle,
- \( \mathbf{E} \) is the electric field,
- \( \mathbf{v} \) is the velocity of the particle,
- \( \mathbf{B} \) is the magnetic field, and
- \( \times \) represents the **cross product** between velocity and magnetic field.

The motion of the particle is governed by **Newton’s second law**:

$$
m \cdot \frac{d\mathbf{v}}{dt} = \mathbf{F}
$$

Where:
- \( m \) is the mass of the particle,
- \( \frac{d\mathbf{v}}{dt} \) is the acceleration (change in velocity over time).

---

## Python Code: Simulation and Visualization

Below is the Python code used to simulate the motion of a charged particle under a magnetic field and visualize its trajectory. This code uses **Euler's method** for numerical integration:

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
q = 1.6e-19  # Charge of the particle (Coulombs)
m = 1.67e-27  # Mass of the particle (kg), e.g., proton
B = 1.0  # Magnetic field strength (Tesla)
E = np.array([0.0, 0.0, 0.0])  # Electric field (V/m), assumed to be zero for simplicity
v0 = np.array([1e5, 0, 0])  # Initial velocity (m/s)
r0 = np.array([0, 0, 0])  # Initial position (m)

# Time parameters
t_max = 1e-5  # Total simulation time (seconds)
dt = 1e-7  # Time step (seconds)
num_steps = int(t_max / dt)

# Initialize position and velocity arrays
r = np.zeros((num_steps, 3))
v = np.zeros((num_steps, 3))
r[0] = r0
v[0] = v0

# Euler method for numerical integration
for i in range(1, num_steps):
    # Compute the Lorentz force: F = q(E + v x B)
    cross_product = np.cross(v[i-1], [0, 0, B])  # v x B
    F = q * (E + cross_product)  # Lorentz force
    
    # Update velocity and position using Euler's method
    a = F / m  # Acceleration
    v[i] = v[i-1] + a * dt  # Update velocity
    r[i] = r[i-1] + v[i] * dt  # Update position

# Plot the trajectory of the particle in 2D (xy-plane)
plt.figure(figsize=(8, 6))
plt.plot(r[:, 0], r[:, 1], label='Particle Trajectory')
plt.title('Particle Trajectory in a Magnetic Field')
plt.xlabel('X Position (m)')
plt.ylabel('Y Position (m)')
plt.grid(True)
plt.legend()
plt.show()
```
![alt text](image-1.png)






