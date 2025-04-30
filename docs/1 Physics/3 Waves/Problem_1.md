# Problem1
### Motivation

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Wave Interference Concepts</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <section class="interference-section">
        <h2>Wave Interference: Key Concepts</h2>
        <ul>
            <li>
                <strong>Interference Overview</strong>
                <p>Waves from different sources overlap to form new patterns.</p>
            </li>
            <li>
                <strong>Types of Interference</strong>
                <ul>
                    <li><strong>Constructive:</strong> In-phase waves, larger amplitudes.</li>
                    <li><strong>Destructive:</strong> Out-of-phase waves, reduced amplitudes.</li>
                </ul>
            </li>
            <li>
                <strong>Wave Sources</strong>
                <p>Ripples originate from distinct points (e.g., on water).</p>
                <p>Example: Two point sources interact to produce patterns.</p>
            </li>
            <li>
                <strong>Interference Patterns</strong>
                <p>Nodal lines: Areas of wave cancellation (destructive).</p>
                <p>Antinodes: Areas of wave amplification (constructive).</p>
                <p>Depend on source spacing, wavelength, and phase differences.</p>
            </li>
            <li>
                <strong>Phase Relationship</strong>
                <p>Relative wave phase dictates interference type:</p>
                <ul>
                    <li>In phase: Constructive.</li>
                    <li>Out of phase: Destructive.</li>
                </ul>
            </li>
        </ul>
    </section>
</body>
</html>

### Task

A circular wave on the water surface, emanating from a point source located at (x₀, y₀), can be described by the **Single Disturbance** equation:

$$
\text{Displacement}(r,t) = A \sin(k r - \omega t + \phi)
$$

where:

- **r** is the distance from the source to the point (x, y),
- **A** is the amplitude of the wave,
- **k** is the wave number, related to the wavelength ($\lambda$),
- **ω** is the angular frequency, related to the frequency (f),
- **t** is time,
- **φ** is the initial phase.

### Problem Statement

Your task is to analyze the interference patterns formed on the water surface due to the superposition of waves emitted from point sources placed at the vertices of a chosen regular polygon.

### Steps to Follow

1. **Select a Regular Polygon**: Choose a regular polygon (e.g., equilateral triangle, square, regular pentagon).
2. **Position the Sources**: Place point wave sources at the vertices of the selected polygon.
3. **Wave Equations**: Write the equations describing the waves emitted from each source, considering their respective positions.
4. **Superposition of Waves**: Apply the principle of superposition by summing the wave displacements at each point on the water surface:

$$
\text{Displacement}(r,t) = \sum_{i=1}^{N} A_i \sin(k r_i - \omega t + \phi_i)
$$

where **N** is the number of sources (vertices of the polygon).
5. **Analyze Interference Patterns**: Examine the resulting displacement **D(x, y, t)** as a function of position **(x, y)** and time **t**. Identify regions of constructive interference (wave amplification) and destructive interference (wave cancellation).
6. **Visualization**: Present your findings graphically, illustrating the interference patterns for the chosen regular polygon.

### Considerations

- Assume all sources emit waves with the same amplitude, wavelength, and frequency.
- The waves are coherent, maintaining a constant phase difference.
- You may use simulation and visualization tools such as Python (with libraries like Matplotlib), or other graphical software to aid in your analysis.

### Deliverables

- A Markdown document with a Python script or notebook implementing the simulations.
- A detailed explanation of the interference patterns observed for the chosen regular polygon with the goal of understanding wave superposition.
- Graphical representations of the water surface showing constructive and destructive interference regions.

```python
import numpy as np
import matplotlib.pyplot as plt
# Parameters
A = 1  # Amplitude of the wave
lambda_ = 1  # Wavelength
f = 1  # Frequency
omega = 2 * np.pi * f  # Angular frequency
k = 2 * np.pi / lambda_  # Wave number
r = 5  # Radius of the polygon (distance from center to vertices)
n = 4  # Number of sources (vertices of the polygon, e.g., square = 4)
phi = 0  # Initial phase

# Calculate positions of sources (vertices of a regular polygon)
angles = np.linspace(0, 2 * np.pi, n, endpoint=False)  # Evenly spaced angles
sources = np.array([(r * np.cos(angle), r * np.sin(angle)) for angle in angles])

# Set up the grid for visualization (water surface)
x_vals = np.linspace(-8, 8, 400)
y_vals = np.linspace(-8, 8, 400)
X, Y = np.meshgrid(x_vals, y_vals)

# Function to calculate the displacement at a given point (x, y)
def displacement(x, y, sources, A, k, omega, phi):
    total_displacement = 0
    for (x_s, y_s) in sources:
        # Calculate the distance from the source to the point (x, y)
        r_dist = np.sqrt((x - x_s)**2 + (y - y_s)**2)
        total_displacement += A * np.sin(k * r_dist - omega * 0 + phi)
    return total_displacement

# Compute the displacement at each grid point using a for loop (more efficient than np.vectorize in this case)
Z = np.zeros(X.shape)
for i in range(X.shape[0]):
    for j in range(X.shape[1]):
        Z[i, j] = displacement(X[i, j], Y[i, j], sources, A, k, omega, phi)

# Plot the interference pattern using contour plots
plt.figure(figsize=(8, 6))
plt.contourf(X, Y, Z, levels=50, cmap='RdYlBu')  # Contour plot for interference pattern
plt.colorbar(label='Displacement')  # Color bar showing displacement values
plt.title(f'Interference Pattern for {n}-sided Polygon')
plt.xlabel('x')
plt.ylabel('y')
plt.show()
```
![alt text](image-1.png)
