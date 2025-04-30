# Problem 1
Exploring the Central Limit Theorem 🎲📊

Motivation 💡

Here’s your hands-on chance to explore one of the most fundamental concepts in statistics, the Central Limit Theorem (CLT)!
🧪 We’ll visually see how data approaches a normal distribution step by step.

1. Population Distributions 🧮

Uniform Distribution 🌈

Exponential Distribution ⚡

Binomial Distribution 🎯


🔍 Large datasets generated:
# Populations

```python
import numpy as np
import matplotlib.pyplot as plt
uniform_population = np.random.uniform(0, 1, 100000)
exponential_population = np.random.exponential(1, 100000)
binomial_population = np.random.binomial(10, 0.5, 100000)

2. Sampling & Visualization 📈

Take multiple samples with different sizes (n=5, 10, 30, 50).

Calculate the mean of each sample.

Observe how the distribution of these means becomes more normal!



🎨 Sample plots:
# Sampling and plotting

```python
import numpy as np
import matplotlib.pyplot as plt
for size in [5, 10, 30, 50]:
    means = sample_means(population, size)
    plt.figure(figsize=(8, 4))
    sns.histplot(means, bins=30, kde=True)
    plt.title(f'Sampling Distribution (n={size})')
    plt.xlabel('Sample Mean')
    plt.ylabel('Frequency')
    plt.show()
3. Explore Parameters 🔍

Distribution shape and sample size influence how quickly convergence occurs.

Higher variance results in wider spread of the sampling distribution.



💡 Calculate and compare:

```python
import numpy as np
import matplotlib.pyplot as plt
pop_mean = np.mean(uniform_population)
pop_var = np.var(uniform_population)

means = sample_means(uniform_population, 30)
print(f"Mean: {np.mean(means):.4f} (Expected: {pop_mean:.4f})")
print(f"Variance: {np.var(means):.4f} (Expected: {pop_var/30:.4f})")

# 4. Practical Applications 🌍

- **Estimating population parameters** 🧾
- **Quality control in manufacturing** 🏭
- **Financial models and risk analysis** 💹

---

## Conclusion & Tips ✨

- **Larger sample sizes** produce **distributions closer to normal**!
- **Increasing variance** broadens the spread of the sampling distribution.

> 🚀 **Remember:** These simulations help you *see* the power of the CLT and understand its real-world importance!

---