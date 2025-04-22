# Problem1
Step 1: Select a Regular Polygon
We'll start by selecting a regular polygon to place the point sources. For simplicity, let's consider the following polygons:

Equilateral Triangle (3 vertices)

Square (4 vertices)

Regular Pentagon (5 vertices)

We'll need to create positions for the sources corresponding to these polygons. The positions will be placed on a circle around a center point (the origin).

Step 2: Position the Sources
For a regular polygon, the vertices will be evenly spaced around a circle. The angle between adjacent vertices will be 
𝜃
=
2
𝜋
𝑛
θ= 
n
2π
​
 , where 
𝑛
n is the number of sides of the polygon.

For example, for an equilateral triangle:

The angle between any two adjacent vertices is 
𝜃
=
2
𝜋
3
θ= 
3
2π
​
 .

The vertices will be at equal distances from the origin and each other.

The position of each source can be expressed as:

Source 1: 
(
𝑟
,
0
)
(r,0) (where 
𝑟
r is the radius of the circle)

Source 2: 
(
𝑟
cos
⁡
(
2
𝜋
3
)
,
𝑟
sin
⁡
(
2
𝜋
3
)
)
(rcos( 
3
2π
​
 ),rsin( 
3
2π
​
 ))

Source 3: 
(
𝑟
cos
⁡
(
4
𝜋
3
)
,
𝑟
sin
⁡
(
4
𝜋
3
)
)
(rcos( 
3
4π
​
 ),rsin( 
3
4π
​
 ))

This approach will be generalized for any regular polygon.

Step 3: Wave Equation
The displacement 
𝜙
ϕ for a wave emitted from a point source located at 
(
𝑥
𝑠
,
𝑦
𝑠
)
(x 
s
​
 ,y 
s
​
 ) at a distance 
𝑟
r from a point 
(
𝑥
,
𝑦
)
(x,y) on the water surface can be written as:

𝜙
(
𝑥
,
𝑦
,
𝑡
)
=
𝐴
sin
⁡
(
𝑘
⋅
𝑟
−
𝜔
𝑡
+
𝜑
)
ϕ(x,y,t)=Asin(k⋅r−ωt+φ)
Where:

𝐴
A is the amplitude of the wave (same for all sources),

𝑘
=
2
𝜋
𝜆
k= 
λ
2π
​
  is the wave number,

𝜔
=
2
𝜋
𝑓
ω=2πf is the angular frequency,

𝜑
φ is the initial phase (we will assume they are all the same for simplicity),

𝑟
r is the distance from the source to the observation point.

For multiple sources, the displacement at each point is the sum of the displacements from each source. The total displacement 
Φ
(
𝑥
,
𝑦
,
𝑡
)
Φ(x,y,t) due to multiple sources is:

Φ
(
𝑥
,
𝑦
,
𝑡
)
=
∑
𝑖
=
1
𝑛
𝐴
sin
⁡
(
𝑘
⋅
𝑟
𝑖
−
𝜔
𝑡
+
𝜑
)
Φ(x,y,t)= 
i=1
∑
n
​
 Asin(k⋅r 
i
​
 −ωt+φ)
Where 
𝑟
𝑖
r 
i
​
  is the distance from the 
𝑖
i-th source to the point 
(
𝑥
,
𝑦
)
(x,y).

Step 4: Superposition of Waves
Using the principle of superposition, we will compute the total displacement at each point on the water surface due to the combination of waves from all sources. The resulting interference pattern will show areas of constructive interference (where waves reinforce each other) and destructive interference (where waves cancel each other out).

To compute the interference, we will:

Choose a grid of points on the water surface.

For each point, calculate the distance from each source.

Compute the displacement from each source at each point.

Sum the displacements to get the total wave displacement at that point.

Step 5: Visualization
Using Python's Matplotlib library, we can visualize the water surface interference pattern. We will plot the displacement 
Φ
(
𝑥
,
𝑦
,
𝑡
)
Φ(x,y,t) as a 2D heatmap or contour plot to show regions of constructive and destructive interference.

Python Code Implementation
Here’s a sample Python code to visualize interference patterns for a regular polygon with 
𝑛
n sources:


```python
import numpy as np
import matplotlib.pyplot as plt

# Parameters
A = 1  # Amplitude
lambda_ = 1  # Wavelength
f = 1  # Frequency
omega = 2 * np.pi * f  # Angular frequency
k = 2 * np.pi / lambda_  # Wave number
r = 5  # Radius of the circle for source placement
n = 4  # Number of sources (vertices of the polygon)
phi = 0  # Initial phase

# Generate source positions (vertices of the regular polygon)
angles = np.linspace(0, 2 * np.pi, n, endpoint=False)
sources = np.array([(r * np.cos(angle), r * np.sin(angle)) for angle in angles])

# Create a grid of points for visualization
x_vals = np.linspace(-8, 8, 400)
y_vals = np.linspace(-8, 8, 400)
X, Y = np.meshgrid(x_vals, y_vals)

# Function to calculate the displacement at each point (X, Y)
def displacement(x, y, sources, A, k, omega, phi):
    total_displacement = 0
    for (x_s, y_s) in sources:
        r = np.sqrt((x - x_s)**2 + (y - y_s)**2)  # Distance from source to point
        total_displacement += A * np.sin(k * r - omega * 0 + phi)
    return total_displacement

# Calculate displacement for each point on the grid
Z = np.vectorize(displacement)(X, Y, sources, A, k, omega, phi)

# Plot the interference pattern as a contour plot
plt.figure(figsize=(8, 6))
plt.contourf(X, Y, Z, levels=50, cmap='RdYlBu')
plt.colorbar(label='Displacement')
plt.title(f'Interference Pattern for {n}-sided Polygon')
plt.xlabel('x')
plt.ylabel('y')
plt.show()

Step 6: Analysis of the Interference Patterns
Constructive Interference: Occurs when the displacements from the different sources reinforce each other. In the plot, this is where the displacement is large and positive.

Destructive Interference: Occurs when the displacements cancel each other out. This will show up as regions where the displacement is near zero or negative.

Symmetry: Since the sources are placed at the vertices of a regular polygon, we expect the interference pattern to be symmetric with respect to the center of the polygon.

By varying the number of sources (vertices of the polygon), we can observe how the interference patterns change with the configuration of the point sources.



The interference patterns on the water surface are a result of wave superposition, with constructive and destructive regions. The chosen polygon affects the symmetry and nature of these patterns. The Python code provided can be easily adapted for different regular polygons and can help visualize how waves interact from multiple sources.