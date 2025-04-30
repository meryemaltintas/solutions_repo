# Problem 1
Exploring the Central Limit Theorem through Simulations

📌 Motivation
The Central Limit Theorem (CLT) asserts that the distribution of the sample mean of a sufficiently large number of independent samples from any population will approximate a normal distribution, regardless of the population's original shape.

This notebook explores the CLT by simulating sampling distributions from various types of population distributions and examining how sample size influences the convergence to normality.
1️⃣ Population Distributions
We will simulate three different population distributions:

Uniform Distribution

Exponential Distribution

Binomial Distribution

```python
import numpy as np
import matplotlib.pyplot as plt

# Set consistent style
sns.set(style="whitegrid")

# Population size
pop_size = 100000

# Generate populations
pop_uniform = np.random.uniform(0, 1, pop_size)
pop_exponential = np.random.exponential(scale=1.0, size=pop_size)
pop_binomial = np.random.binomial(n=10, p=0.5, size=pop_size)


2️⃣ Sampling and Visualization
For each population, we'll:

Take samples of sizes 5, 10, 30, and 50.

Compute the mean of each sample.

Repeat the process 1,000 times to form a sampling distribution of the mean.

Plot the resulting histograms.

Function for Sampling and Plotting
def simulate_sampling(population, sample_sizes, n_samples=1000, title_prefix=""):
    fig, axs = plt.subplots(1, len(sample_sizes), figsize=(18, 4))
    
    for i, size in enumerate(sample_sizes):
        means = [np.mean(np.random.choice(population, size=size, replace=False))
                 for _ in range(n_samples)]
        
        sns.histplot(means, bins=30, kde=True, ax=axs[i], color='skyblue')
        axs[i].set_title(f"{title_prefix} Sample Size = {size}")
        axs[i].set_xlabel("Sample Mean")
        axs[i].set_ylabel("Frequency")
    
    plt.tight_layout()
    plt.show()
 Uniform Distribution
    simulate_sampling(pop_uniform, [5, 10, 30, 50], title_prefix="Uniform")
Exponential Distribution
simulate_sampling(pop_exponential, [5, 10, 30, 50], title_prefix="Exponential")
Binomial Distribution
simulate_sampling(pop_binomial, [5, 10, 30, 50], title_prefix="Binomial")
3️⃣ Parameter Exploration
Observe how sample size affects convergence to normality.

Note: The Exponential Distribution, being highly skewed, requires a larger sample size to approximate normality.

The variance of the population directly influences the spread of the sampling distribution (i.e., standard error).

import pandas as pd

def summary_statistics(population):
    return {
        "Mean": np.mean(population),
        "Variance": np.var(population),
        "Standard Deviation": np.std(population)
    }

summary_df = pd.DataFrame({
    "Uniform": summary_statistics(pop_uniform),
    "Exponential": summary_statistics(pop_exponential),
    "Binomial": summary_statistics(pop_binomial)
})
summary_df
4️⃣ Practical Applications of CLT
The Central Limit Theorem underpins many statistical methods and real-world applications:

✅ Estimating Population Parameters: Sample means provide unbiased estimates of population means.

🏭 Quality Control: In manufacturing, averages of product measurements are monitored using control charts.

💸 Finance & Risk Management: Assumes normally distributed returns for modeling and predictions.

📈 Summary & Reflection
Through these simulations, we observe:

Regardless of the original distribution, the sampling distribution of the mean becomes increasingly normal with larger sample sizes.

Populations with higher variance lead to wider sampling distributions.

Skewed distributions (like exponential) need larger samples to achieve approximate normality.



