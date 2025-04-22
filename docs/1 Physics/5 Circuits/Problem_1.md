# Problem 1
## ⚡ Equivalent Resistance Using Graph Theory

---

### 🎯 Motivation

Calculating equivalent resistance is a fundamental task in circuit analysis. While applying series and parallel rules manually works for simple circuits, it quickly becomes impractical for **complex networks**.

**Graph theory** provides a powerful and structured approach:

- **Nodes** ⟶ Circuit junctions  
- **Edges** ⟶ Resistors (edge weights = resistance values)

This representation enables algorithmic simplification and is ideal for:
- Circuit simulation
- Optimization problems
- Automated analysis tools

Graph-based methods not only streamline calculations but also deepen our understanding of the **relationship between math and physics**.

---

## 🧠 Task Options

---

### ✅ Option 1: Simplified Task – Algorithm Description

Describe an algorithm that calculates the equivalent resistance using graph simplification:

#### 📌 Goals:
- Detect and reduce **series** and **parallel** resistor combinations.
- Continue until the graph reduces to a single edge between two terminals.


#### 💡 Nested Combination Handling

- **Series** detection uses degree-2 internal nodes.
- **Parallel** detection identifies multiple edges between the same node pair.
- Repeat until only one edge remains between terminals.

---

### 🧑‍💻 Option 2: Advanced Task – Full Implementation (Python + NetworkX)

Below is a Python implementation using NetworkX:

```python
import networkx as nx

def reduce_circuit(G, start, end):
    changed = True
    while changed:
        changed = False
        for node in list(G.nodes()):
            # Handle series
            if node != start and node != end and G.degree[node] == 2:
                neighbors = list(G.neighbors(node))
                r1 = G[node][neighbors[0]]['resistance']
                r2 = G[node][neighbors[1]]['resistance']
                R_eq = r1 + r2
                G.add_edge(neighbors[0], neighbors[1], resistance=R_eq)
                G.remove_node(node)
                changed = True
                break
        # Handle parallel
        to_merge = {}
        for u, v, data in list(G.edges(data=True)):
            key = tuple(sorted([u, v]))
            to_merge.setdefault(key, []).append(data['resistance'])
        for (u, v), resistors in to_merge.items():
            if len(resistors) > 1:
                R_eq = 1 / sum(1 / r for r in resistors)
                G.remove_edges_from([(u, v)] * len(resistors))
                G.add_edge(u, v, resistance=R_eq)
                changed = True
    return G[start][end]['resistance']
### 🧪 Example Inputs

### 🧪 Example Inputs

#### 🔹 Simple Series
Two resistors connected in series:

- \( R_1 = 5\,\Omega \)  
- \( R_2 = 10\,\Omega \)  

**Total Resistance**:  
\[
R_{\text{eq}} = R_1 + R_2 = 5 + 10 = \boxed{15\,\Omega}
\]

---

#### 🔹 Simple Parallel
Two resistors connected in parallel:

- \( R_1 = 5\,\Omega \)  
- \( R_2 = 10\,\Omega \)

**Total Resistance**:  
\[
\frac{1}{R_{\text{eq}}} = \frac{1}{R_1} + \frac{1}{R_2} = \frac{1}{5} + \frac{1}{10} = \frac{3}{10}
\]
\[
R_{\text{eq}} = \frac{10}{3} \approx \boxed{3.33\,\Omega}
\]

---

#### 🔹 Nested Configuration
A nested combination:  
5Ω in series with (10Ω parallel 20Ω)

Step 1 – Solve the parallel part:
\[
\frac{1}{R_{\text{parallel}}} = \frac{1}{10} + \frac{1}{20} = \frac{3}{20}
\quad \Rightarrow \quad R_{\text{parallel}} = \frac{20}{3} \approx 6.67\,\Omega
\]

Step 2 – Add the series resistor:
\[
R_{\text{eq}} = 5 + 6.67 = \boxed{11.67\,\Omega}
\]


