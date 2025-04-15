# Problem 1
Kepler's Third Law: Orbital Period and Radius Relationship

1. Derivation of Kepler's Third Law for Circular Orbits

Kepler's Third Law states that the square of the orbital period ( T ) of a body in circular orbit is proportional to the cube of its orbital radius ( r ). Mathematically, for a planet or satellite orbiting a central body:

[ T^2 \propto r^3 ]

To derive this, consider a satellite of mass ( m ) in a circular orbit around a central body of mass ( M ) (where ( M \gg m )) with radius ( r ). The gravitational force provides the centripetal force required for circular motion.

Gravitational Force:

The gravitational force between the satellite and the central body is:

[ F_g = \frac{G M m}{r^2} ]

where ( G ) is the gravitational constant (( G = 6.67430 \times 10^{-11} , \text{m}^3 \text{kg}^{-1} \text{s}^{-2} )).

Centripetal Force:

For circular motion, the centripetal force is:

[ F_c = \frac{m v^2}{r} ]

where ( v ) is the orbital velocity.

Equating the two forces:

[ \frac{G M m}{r^2} = \frac{m v^2}{r} ]

Simplify by canceling ( m ) (since ( m \neq 0 )) and multiplying through by ( r ):

[ \frac{G M}{r} = v^2 ]

Orbital Velocity:

The orbital period ( T ) is the time taken for one complete orbit. The circumference of the circular orbit is ( 2 \pi r ), so the orbital velocity is:

[ v = \frac{2 \pi r}{T} ]

Square the velocity:

[ v^2 = \frac{4 \pi^2 r^2}{T^2} ]

Substitute ( v^2 ) into the force balance equation:

[ \frac{G M}{r} = \frac{4 \pi^2 r^2}{T^2} ]

Multiply both sides by ( T^2 ):

[ \frac{G M T^2}{r} = 4 \pi^2 r^2 ]

Rearrange:

[ G M T^2 = 4 \pi^2 r^3 ]

[ T^2 = \frac{4 \pi^2}{G M} r^3 ]

This is Kepler's Third Law for circular orbits, where ( T^2 \propto r^3 ), and the constant of proportionality is ( \frac{4 \pi^2}{G M} ), which depends on the mass of the central body.

2. Implications for Astronomy

Kepler's Third Law is a powerful tool in astronomy with several applications:





Determining Planetary Masses: By observing the orbital period and radius of a moon or satellite orbiting a planet, we can calculate the mass of the central body. For example, the Moon's orbit around Earth allows us to estimate Earth's mass:

[ M = \frac{4 \pi^2 r^3}{G T^2} ]





Measuring Orbital Distances: If the mass of the central body is known (e.g., the Sun), the law can be used to determine the orbital radius of a planet or asteroid given its orbital period.



Exoplanet Studies: For exoplanets, Kepler's Third Law helps estimate the mass of the host star or the semi-major axis of the planet's orbit based on transit or radial velocity data.



Satellite Orbits: The law is used to design orbits for artificial satellites, ensuring they maintain stable periods for communication or observation.

3. Real-World Examples

Moon's Orbit Around Earth





Orbital Radius: ( r \approx 384,400 , \text{km} = 3.844 \times 10^8 , \text{m} )



Orbital Period: ( T \approx 27.32 , \text{days} = 27.32 \times 86400 \approx 2.360 \times 10^6 , \text{s} )



Earth's Mass: Using Kepler's Third Law:

[ M = \frac{4 \pi^2 r^3}{G T^2} ]

[ r^3 = (3.844 \times 10^8)^3 \approx 5.678 \times 10^{25} , \text{m}^3 ]

[ T^2 = (2.360 \times 10^6)^2 \approx 5.570 \times 10^{12} , \text{s}^2 ]

[ M = \frac{4 \pi^2 (5.678 \times 10^{25})}{(6.67430 \times 10^{-11}) (5.570 \times 10^{12})} \approx 5.972 \times 10^{24} , \text{kg} ]

This matches Earth's known mass, confirming the law's accuracy.

Planets in the Solar System

For planets orbiting the Sun, the constant ( \frac{4 \pi^2}{G M} ) is the same (where ( M ) is the Sun's mass). The law can be expressed in astronomical units (AU) and years for simplicity:

[ T^2 = r^3 ]





Earth: ( r = 1 , \text{AU} ), ( T = 1 , \text{year} ). Thus, ( 1^2 = 1^3 ).



Mars: ( r \approx 1.524 , \text{AU} ), ( T \approx 1.881 , \text{years} ). Check: ( 1.881^2 \approx 3.538 ), and ( 1.524^3 \approx 3.539 ), which are nearly equal.

4. Computational Model

Below is a Python script that simulates circular orbits and verifies Kepler's Third Law by plotting ( T^2 ) versus ( r^3 ) for various orbital radii. The script uses Matplotlib to generate graphical representations.

import numpy as np import matplotlib.pyplot as plt
# Kepler's Third Law: Orbital Period and Radius Relationship
pip install numpy matplotlib
import numpy as np
import matplotlib.pyplot as plt

# Constants
GRAVITATIONAL_CONSTANT = 6.67430e-11  # gravitational constant (m^3 kg^-1 s^-2)
MASS_SUN = 1.989e30  # mass of the Sun (kg)
MASS_EARTH = 5.972e24  # mass of Earth (kg)

# Function to calculate orbital period
def calculate_orbital_period(radius, central_mass):
    """
    Calculates the orbital period: T = sqrt((4 * pi^2 * r^3) / (G * M))
    Parameters:
        radius: orbital radius (meters)
        central_mass: mass of the central body (kg)
    Returns: period (seconds)
    """
    return np.sqrt((4 * np.pi**2 * radius**3) / (GRAVITATIONAL_CONSTANT * central_mass))

# Function to calculate central mass (e.g., Earth's mass from Moon's orbit)
def calculate_central_mass(radius, period):
    """
    Calculates the central body's mass: M = (4 * pi^2 * r^3) / (G * T^2)
    Parameters:
        radius: orbital radius (meters)
        period: orbital period (seconds)
    Returns: mass (kg)
    """
    return (4 * np.pi**2 * radius**3) / (GRAVITATIONAL_CONSTANT * period**2)

# 1. Simulation: Orbits around the Sun
orbital_radii = np.linspace(0.5e11, 5e11, 100)  # radii from 0.5 to 5 AU (meters)
orbital_periods_sun = calculate_orbital_period(orbital_radii, MASS_SUN) / (365.25 * 86400)  # periods in years

# 2. Moon's orbit around Earth
moon_radius = 3.844e8  # Moon's orbital radius (meters)
moon_period = 27.32 * 86400  # Moon's orbital period (seconds)
moon_period_calculated = calculate_orbital_period(moon_radius, MASS_EARTH) / 86400  # calculated period (days)

# 3. Calculate Earth's mass from Moon's orbit
earth_mass_calculated = calculate_central_mass(moon_radius, moon_period)

# 4. Plot 1: T^2 vs r^3 (Verification of Kepler's Third Law)
radii_cubed = orbital_radii**3  # cube of orbital radius
periods_squared = (orbital_periods_sun * 365.25 * 86400)**2  # square of period (seconds^2)
plt.figure(figsize=(8, 6))
plt.scatter(radii_cubed, periods_squared, label='Simulated Orbits (Sun)', color='blue')
plt.plot(radii_cubed, periods_squared, 'b-', alpha=0.5)
plt.xlabel('Orbital Radius Cubed (m³)')
plt.ylabel('Orbital Period Squared (s²)')
plt.title('Kepler\'s Third Law: T² vs r³')
plt.grid(True)
plt.legend()
plt.savefig('kepler_third_law.png')
plt.close()

# 5. Plot 2: Visualization of Moon's circular orbit
theta = np.linspace(0, 2 * np.pi, 100)
x_coords = moon_radius * np.cos(theta) / 1e6  # x coordinates (km)
y_coords = moon_radius * np.sin(theta) / 1e6  # y coordinates (km)
plt.figure(figsize=(6, 6))
plt.plot(x_coords, y_coords, 'b-', label='Moon\'s Orbit')
plt.scatter(0, 0, c='green', s=200, label='Earth')
plt.xlabel('X (km)')
plt.ylabel('Y (km)')
plt.title('Circular Orbit of the Moon')
plt.grid(True)
plt.legend()
plt.axis('equal')
plt.savefig('circular_orbit.png')
plt.close()

# 6. Print results
print("=== Kepler's Third Law Simulation Results ===")
print(f"Moon's orbital radius: {moon_radius/1e3:.2f} km")
print(f"Calculated Moon orbital period: {moon_period_calculated:.2f} days")
print(f"Expected Moon orbital period: 27.32 days")
print(f"Calculated Earth mass: {earth_mass_calculated:.2e} kg")
print(f"Expected Earth mass: {MASS_EARTH:.2e} kg")

# 7. Additional verification for Jupiter
jupiter_radius = 5.204 * 1.496e11  # Jupiter's orbital radius (meters)
jupiter_period = calculate_orbital_period(jupiter_radius, MASS_SUN) / (365.25 * 86400)  # Jupiter's period (years)
print(f"\nJupiter verification:")
print(f"Jupiter's orbital radius: {jupiter_radius/1.496e11:.3f} AU")
print(f"Calculated Jupiter orbital period: {jupiter_period:.3f} years")
print(f"Expected Jupiter orbital period: 11.862 years")
print(f"Kepler's Third Law check: T² = {jupiter_period**2:.3f}, r³ = {(jupiter_radius/1.496e11)**3:.3f}")

Constants

G = 6.67430e-11 # gravitational constant (m^3 kg^-1 s^-2) M_sun = 1.989e30 # mass of the Sun (kg) M_earth = 5.972e24 # mass of Earth (kg)

Function to calculate orbital period given radius and central mass

def orbital_period(r, M): return np.sqrt((4 * np.pi2 * r3) / (G * M))

Simulate orbits for different radii (around the Sun)

r_values = np.linspace(0.5e11, 5e11, 100) # radii from 0.5 to 5 AU in meters T_values_sun = orbital_period(r_values, M_sun) / (365.25 * 86400) # convert to years

Simulate Moon-like orbit around Earth

r_moon = 3.844e8 # Moon's orbital radius (m) T_moon = orbital_period(r_moon, M_earth) / 86400 # convert to days

Plot 1: T^2 vs r^3

r_cubed = r_values**3 T_squared = (T_values_sun * 365.25 * 86400)**2 # convert back to seconds for consistency plt.figure(figsize=(8, 6)) plt.scatter(r_cubed, T_squared, label='Simulated Orbits (Sun)', color='b') plt.plot(r_cubed, T_squared, 'b-', alpha=0.5) plt.xlabel('Orbital Radius Cubed (m³)') plt.ylabel('Orbital Period Squared (s²)') plt.title('Kepler's Third Law: T² vs r³') plt.grid(True) plt.legend() plt.savefig('kepler_third_law.png') plt.close()

Plot 2: Circular Orbit Visualization

theta = np.linspace(0, 2 * np.pi, 100) x = r_moon * np.cos(theta) / 1e6 # convert to km for plotting y = r_moon * np.sin(theta) / 1e6 plt.figure(figsize=(6, 6)) plt.plot(x, y, 'b-', label='Moon's Orbit') plt.scatter(0, 0, c='green', s=200, label='Earth') plt.xlabel('X (km)') plt.ylabel('Y (km)') plt.title('Circular Orbit of the Moon') plt.grid(True) plt.legend() plt.axis('equal') plt.savefig('circular_orbit.png') plt.close()

Print verification for Moon

print(f"Moon's orbital radius: {r_moon/1e3:.2f} km") print(f"Calculated orbital period: {T_moon:.2f} days") print(f"Expected period: 27.32 days")