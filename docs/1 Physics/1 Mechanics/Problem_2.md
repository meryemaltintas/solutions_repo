# Problem 2
## 1. Theoretical Foundation

### Differential Equation of the Forced Damped Pendulum

The motion of a forced damped pendulum is governed by the following nonlinear differential equation:

\[
\frac{d^2 \theta}{dt^2} + b \frac{d \theta}{dt} + \frac{g}{L} \sin \theta = A \cos(\omega t)
\]

Where:
- \(\theta\): Angular displacement of the pendulum (radians).
- \(\frac{d\theta}{dt}\): Angular velocity (\(\dot{\theta}\)).
- \(\frac{d^2\theta}{dt^2}\): Angular acceleration (\(\ddot{\theta}\)).
- \(b\): Damping coefficient (s\(^{-1}\)).
- \(g\): Gravitational acceleration (\(9.8 \, \text{m/s}^2\)).
- \(L\): Length of the pendulum (m).
- \(A\): Amplitude of the external driving force (rad/s\(^2\)).
- \(\omega\): Driving frequency (rad/s).
- \(t\): Time (s).

To simplify, we define:
- Natural frequency: \(\omega_0 = \sqrt{\frac{g}{L}}\),
- Damping parameter: \(\beta = b\),
- Driving amplitude: \(f = A\).

Thus, the equation can be rewritten as:

\[
\ddot{\theta} + \beta \dot{\theta} + \omega_0^2 \sin\theta = f \cos(\omega t)
\]

### Small-Angle Approximation

For small angles (\(\theta \ll 1\)), we can approximate \(\sin\theta \approx \theta\). This linearizes the equation:

\[
\ddot{\theta} + \beta \dot{\theta} + \omega_0^2 \theta = f \cos(\omega t)
\]

This is the equation of a forced damped harmonic oscillator. The homogeneous solution (without forcing) is:

\[
\theta_h(t) = e^{-\frac{\beta}{2} t} \left( A_1 \cos(\omega_d t) + A_2 \sin(\omega_d t) \right)
\]

Where \(\omega_d = \sqrt{\omega_0^2 - \left(\frac{\beta}{2}\right)^2}\) is the damped angular frequency, and \(A_1\) and \(A_2\) are constants determined by initial conditions.

The particular solution (due to the forcing term \(f \cos(\omega t)\)) can be found using the method of undetermined coefficients. Assume a solution of the form:

\[
\theta_p(t) = C \cos(\omega t) + D \sin(\omega t)
\]

Substitute into the linearized equation, solve for \(C\) and \(D\), and the steady-state solution is:

\[
\theta_p(t) = A_d \cos(\omega t - \phi)
\]

Where the amplitude \(A_d\) and phase \(\phi\) are:

\[
A_d = \frac{f}{\sqrt{(\omega_0^2 - \omega^2)^2 + (\beta \omega)^2}}, \quad \tan\phi = \frac{\beta \omega}{\omega_0^2 - \omega^2}
\]

### Resonance Conditions

Resonance occurs when the driving frequency \(\omega\) approaches the natural frequency \(\omega_0\). In the linearized case, the amplitude \(A_d\) is maximized when:

\[
\omega \approx \sqrt{\omega_0^2 - \left(\frac{\beta}{2}\right)^2}
\]

At resonance, the system absorbs energy most efficiently from the driving force, leading to large oscillations. Damping (\(\beta\)) limits the amplitude, preventing it from becoming infinite as it would in an undamped system. Resonance increases the system’s energy, which can be beneficial (e.g., in energy harvesting) or destructive (e.g., in mechanical structures like bridges).

## 2. Analysis of Dynamics

### Influence of Parameters

- **Damping Coefficient (\(\beta\))**: Higher damping reduces the amplitude of oscillations and suppresses resonance. For very large \(\beta\), the system becomes overdamped, and oscillations decay quickly.
- **Driving Amplitude (\(f\))**: Increasing \(f\) increases the amplitude of the steady-state response and can push the system into nonlinear regimes, leading to chaotic behavior.
- **Driving Frequency (\(\omega\))**: When \(\omega \approx \omega_0\), resonance occurs. For \(\omega \gg \omega_0\) or \(\omega \ll \omega_0\), the response amplitude decreases.

### Transition to Chaotic Motion

For large driving amplitudes or specific combinations of \(\beta\), \(f\), and \(\omega\), the nonlinear term \(\sin\theta\) becomes significant, and the system can exhibit chaotic behavior. This transition is characterized by:
- **Period Doubling**: The pendulum’s motion may double its period repeatedly as \(f\) increases, a hallmark of the route to chaos.
- **Sensitive Dependence on Initial Conditions**: Small changes in \(\theta(0)\) or \(\dot{\theta}(0)\) lead to drastically different trajectories.
- **Chaotic Attractors**: The system’s phase space shows a strange attractor, visible in phase portraits and Poincaré sections.

## 3. Practical Applications

The forced damped pendulum model applies to:
- **Energy Harvesting**: Piezoelectric devices can use forced oscillations to convert mechanical energy into electrical energy.
- **Suspension Bridges**: Understanding resonance helps design bridges to avoid catastrophic oscillations (e.g., Tacoma Narrows Bridge collapse).
- **Oscillating Circuits**: Driven RLC circuits behave analogously, with applications in electronics and signal processing.

## 4. Implementation

Below is a Python script to simulate the forced damped pendulum using the 4th-order Runge-Kutta method (RK4). The script visualizes the motion, phase portraits, and Poincaré sections for different parameter sets to illustrate resonance and chaotic behavior.

```python
import numpy as np
import matplotlib.pyplot as plt

# Parameters
g = 9.8  # m/s^2
L = 1.0  # m
omega_0 = np.sqrt(g / L)  # Natural frequency
beta_values = [0.1, 0.5, 1.0]  # Damping coefficients (s^-1)
f_values = [0.5, 1.2, 2.0]  # Driving amplitudes (rad/s^2)
omega = 2/3 * omega_0  # Driving frequency (rad/s)

# Time array
t_max = 100  # Total time (s)
dt = 0.01  # Time step (s)
t = np.arange(0, t_max, dt)
N = len(t)

# Initial conditions
theta0 = 0.2  # Initial angle (rad)
theta_dot0 = 0.0  # Initial angular velocity (rad/s)

# Function to compute derivatives
def pendulum_derivs(state, t, beta, f, omega, omega_0):
    theta, theta_dot = state
    dtheta_dt = theta_dot
    dtheta_dot_dt = -beta * theta_dot - omega_0**2 * np.sin(theta) + f * np.cos(omega * t)
    return [dtheta_dt, dtheta_dot_dt]

# Simulate for different parameters
for beta in beta_values:
    for f in f_values:
        # Arrays to store solution
        theta = np.zeros(N)
        theta_dot = np.zeros(N)
        theta[0] = theta0
        theta_dot[0] = theta_dot0

        # RK4 integration
        for i in range(N-1):
            state = [theta[i], theta_dot[i]]
            k1 = pendulum_derivs(state, t[i], beta, f, omega, omega_0)
            
            state_k2 = [theta[i] + 0.5 * dt * k1[0], theta_dot[i] + 0.5 * dt * k1[1]]
            k2 = pendulum_derivs(state_k2, t[i] + 0.5 * dt, beta, f, omega, omega_0)
            
            state_k3 = [theta[i] + 0.5 * dt * k2[0], theta_dot[i] + 0.5 * dt * k2[1]]
            k3 = pendulum_derivs(state_k3, t[i] + 0.5 * dt, beta, f, omega, omega_0)
            
            state_k4 = [theta[i] + dt * k3[0], theta_dot[i] + dt * k3[1]]
            k4 = pendulum_derivs(state_k4, t[i] + dt, beta, f, omega, omega_0)
            
            theta[i+1] = theta[i] + (dt/6) * (k1[0] + 2*k2[0] + 2*k3[0] + k4[0])
            theta_dot[i+1] = theta_dot[i] + (dt/6) * (k1[1] + 2*k2[1] + 2*k3[1] + k4[1])

        # Plotting
        # 1. Time series of theta
        plt.figure(figsize=(10, 4))
        plt.plot(t, theta, label=f'β={beta}, f={f}')
        plt.xlabel('Time (s)')
        plt.ylabel('Angle (rad)')
        plt.title(f'Forced Damped Pendulum: Angle vs Time (β={beta}, f={f})')
        plt.grid(True)
        plt.legend()
        plt.show()

        # 2. Phase portrait
        plt.figure(figsize=(10, 6))
        plt.plot(theta, theta_dot, label=f'β={beta}, f={f}')
        plt.xlabel('Angle (rad)')
        plt.ylabel('Angular Velocity (rad/s)')
        plt.title(f'Phase Portrait (β={beta}, f={f})')
        plt.grid(True)
        plt.legend()
        plt.show()

        # 3. Poincaré section
        poincare_theta = []
        poincare_theta_dot = []
        period = 2 * np.pi / omega  # Period of driving force
        for i in range(N):
            if abs(t[i] % period) < dt / 2:  # Sample at each driving period
                poincare_theta.append(theta[i])
                poincare_theta_dot.append(theta_dot[i])

        plt.figure(figsize=(10, 6))
        plt.scatter(poincare_theta, poincare_theta_dot, s=1, color='red', label=f'β={beta}, f={f}')
        plt.xlabel('Angle (rad)')
        plt.ylabel('Angular Velocity (rad/s)')
        plt.title(f'Poincaré Section (β={beta}, f={f})')
        plt.grid(True)
        plt.legend()
        plt.show()
5. Discussion
Limitations
The model assumes a constant driving frequency and amplitude, which may not hold in real systems with time-varying forces.
Nonlinear damping (e.g., velocity-squared damping) is not considered.
The simulation uses a fixed time step, which may introduce numerical errors for highly chaotic regimes.
Extensions
Nonlinear Damping: Introduce terms like (-\beta \dot{\theta}^2) to model air resistance more realistically.
Non-Periodic Driving: Use a stochastic or aperiodic driving force to study more complex dynamics.
Bifurcation Analysis: Vary (f) or (\omega) systematically to plot a bifurcation diagram, showing the transition to chaos.
Hints and Resources
For small angles, approximate (\sin \theta \approx \theta) to simplify the differential equation.
Employ numerical techniques (e.g., Runge-Kutta methods) for exploring the dynamics beyond the small-angle approximation.
Relate the forced damped pendulum to analogous systems in other fields, such as electrical circuits (driven RLC circuits) or biomechanics (human gait).
Utilize software tools like Python for simulations and visualizations.
This task bridges theoretical analysis with computational exploration, fostering a deeper understanding of forced and damped oscillatory phenomena and their implications in both physics and engineering.

text

Daralt

Metni gizle

Kopyala

---

### Step 4: Copy the Python Script into `forced_damped_pendulum.py`

Copy the Python code block from the Markdown document (the section between the triple backticks ```python and ```) into `forced_damped_pendulum.py`. For convenience, here it is again:

```python
import numpy as np
import matplotlib.pyplot as plt

# Parameters
g = 9.8  # m/s^2
L = 1.0  # m
omega_0 = np.sqrt(g / L)  # Natural frequency
beta_values = [0.1, 0.5, 1.0]  # Damping coefficients (s^-1)
f_values = [0.5, 1.2, 2.0]  # Driving amplitudes (rad/s^2)
omega = 2/3 * omega_0  # Driving frequency (rad/s)

# Time array
t_max = 100  # Total time (s)
dt = 0.01  # Time step (s)
t = np.arange(0, t_max, dt)
N = len(t)

# Initial conditions
theta0 = 0.2  # Initial angle (rad)
theta_dot0 = 0.0  # Initial angular velocity (rad/s)

# Function to compute derivatives
def pendulum_derivs(state, t, beta, f, omega, omega_0):
    theta, theta_dot = state
    dtheta_dt = theta_dot
    dtheta_dot_dt = -beta * theta_dot - omega_0**2 * np.sin(theta) + f * np.cos(omega * t)
    return [dtheta_dt, dtheta_dot_dt]

# Simulate for different parameters
for beta in beta_values:
    for f in f_values:
        # Arrays to store solution
        theta = np.zeros(N)
        theta_dot = np.zeros(N)
        theta[0] = theta0
        theta_dot[0] = theta_dot0

        # RK4 integration
        for i in range(N-1):
            state = [theta[i], theta_dot[i]]
            k1 = pendulum_derivs(state, t[i], beta, f, omega, omega_0)
            
            state_k2 = [theta[i] + 0.5 * dt * k1[0], theta_dot[i] + 0.5 * dt * k1[1]]
            k2 = pendulum_derivs(state_k2, t[i] + 0.5 * dt, beta, f, omega, omega_0)
            
            state_k3 = [theta[i] + 0.5 * dt * k2[0], theta_dot[i] + 0.5 * dt * k2[1]]
            k3 = pendulum_derivs(state_k3, t[i] + 0.5 * dt, beta, f, omega, omega_0)
            
            state_k4 = [theta[i] + dt * k3[0], theta_dot[i] + dt * k3[1]]
            k4 = pendulum_derivs(state_k4, t[i] + dt, beta, f, omega, omega_0)
            
            theta[i+1] = theta[i] + (dt/6) * (k1[0] + 2*k2[0] + 2*k3[0] + k4[0])
            theta_dot[i+1] = theta_dot[i] + (dt/6) * (k1[1] + 2*k2[1] + 2*k3[1] + k4[1])

        # Plotting
        # 1. Time series of theta
        plt.figure(figsize=(10, 4))
        plt.plot(t, theta, label=f'β={beta}, f={f}')
        plt.xlabel('Time (s)')
        plt.ylabel('Angle (rad)')
        plt.title(f'Forced Damped Pendulum: Angle vs Time (β={beta}, f={f})')
        plt.grid(True)
        plt.legend()
        plt.show()

        # 2. Phase portrait
        plt.figure(figsize=(10, 6))
        plt.plot(theta, theta_dot, label=f'β={beta}, f={f}')
        plt.xlabel('Angle (rad)')
        plt.ylabel('Angular Velocity (rad/s)')
        plt.title(f'Phase Portrait (β={beta}, f={f})')
        plt.grid(True)
        plt.legend()
        plt.show()

        # 3. Poincaré section
        poincare_theta = []
        poincare_theta_dot = []
        period = 2 * np.pi / omega  # Period of driving force
        for i in range(N):
            if abs(t[i] % period) < dt / 2:  # Sample at each driving period
                poincare_theta.append(theta[i])
                poincare_theta_dot.append(theta_dot[i])

        plt.figure(figsize=(10, 6))
        plt.scatter(poincare_theta, poincare_theta_dot, s=1, color='red', label=f'β={beta}, f={f}')
        plt.xlabel('Angle (rad)')
        plt.ylabel('Angular Velocity (rad/s)')
        plt.title(f'Poincaré Section (β={beta}, f={f})')
        plt.grid(True)
        plt.legend()
        plt.show()