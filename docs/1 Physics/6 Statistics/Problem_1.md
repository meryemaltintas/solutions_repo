# Problem 1
# 📊 Exploring the Central Limit Theorem through Simulations

---

## 🎯 Motivation

The **Central Limit Theorem (CLT)** is a cornerstone of probability and statistics.  
It states that the sampling distribution of the **sample mean** approaches a **normal distribution** as the sample size increases, regardless of the original population’s distribution.

Simulations provide an intuitive, hands-on way to observe this phenomenon in action and help understand how randomness behaves in the long run.

---

## 1️⃣ Simulating Sampling Distributions

We begin by selecting various population distributions:

- 🎲 **Uniform Distribution**
- 📈 **Exponential Distribution**
- ⚪ **Binomial Distribution**

For each distribution, we generate a large synthetic population dataset using NumPy.

---

## 2️⃣ Sampling and Visualization

We randomly sample data from the population and calculate the **sample mean** for different sample sizes:

- Sample sizes: **5, 10, 30, 50**

Each sampling process is repeated **1000 times** to construct the **sampling distribution of the sample mean**.

The results are visualized using histograms to observe how the shape of the distribution evolves with sample size.

### 🧪 Python Code

````python
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Set the style for the plots
sns.set(style="whitegrid")

# Simulation function
def simulate_clt(population_func, pop_params, sample_sizes, n_simulations=1000):
    # Generate a population (e.g., normal distribution)
    population = population_func(size=10000, **pop_params)  # Population with 10,000 elements
    
    # Create subplots for different sample sizes
    plt.figure(figsize=(16, 10))
    
    for i, sample_size in enumerate(sample_sizes, 1):  # Start subplot indexing from 1
        # Perform 1000 simulations for each sample size
        sample_means = []
        for _ in range(n_simulations):
            sample = np.random.choice(population, size=sample_size)  # Random sampling
            sample_mean = np.mean(sample)  # Calculate the sample mean
            sample_means.append(sample_mean)
        
        # Plot the histogram
        plt.subplot(2, 2, i)  # 2x2 subplot layout
        sns.histplot(sample_means, bins=30, kde=True, color="cornflowerblue")
        plt.title(f"Sample Size = {sample_size}")
        plt.xlabel("Sample Mean")
        plt.ylabel("Frequency")
    
    # Adjust layout and add a main title
    plt.tight_layout(rect=[0, 0, 1, 0.95])
    plt.suptitle("Sampling Distribution of the Mean", fontsize=16)
    plt.show()

# Define parameters and sample sizes
pop_params = {"loc": 100, "scale": 15}  # For normal distribution: mean=100, std=15
sample_sizes = [5, 10, 30, 50]  # Sample sizes to test

# Run the simulation
simulate_clt(np.random.normal, pop_params, sample_sizes, n_simulations=1000)

3️⃣ Parameter Exploration
🔍 Shape and Convergence
Distributions like the Exponential are initially skewed, but the mean's sampling distribution becomes more symmetric with larger sample sizes.

The Uniform distribution converges more quickly since it's already symmetric.

The Binomial distribution, being discrete, smooths out with increasing n.

🔍 Variance Impact
The spread (standard deviation) of the sampling distribution decreases as sample size increases.

This reflects the law of large numbers: larger samples yield more stable, accurate estimates of the population mean.

4️⃣ Practical Applications
The CLT plays a vital role in many fields:

📏 Estimating population parameters from small samples
🏭 Quality control: detecting anomalies in manufacturing processes
💹 Finance: modeling and forecasting market averages or risks

Understanding the CLT helps in making informed decisions under uncertainty, by using averages from random samples.

📦 Deliverables

✅ Python simulation scripts and/or notebooks
✅ Histograms showing the convergence to a normal distribution
✅ Explanatory discussion linking results with CLT theory

🧠 Conclusion
The Central Limit Theorem reveals that averages become normal — even when the source data is not.

"The average of the averages is almost always normal." 🌐