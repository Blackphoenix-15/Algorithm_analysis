# A Journey in Algorithmic Efficiency: Solving the Minimum Cost Diagnostic Panel Problem

This repository documents an independent research project that began with a theoretical exploration of the Set Cover problem and culminated in a practical application: the design of cost-effective genetic diagnostic panels. This project analyzes and compares three distinct algorithmic paradigms—a greedy heuristic, an exact solver, and an LP-based approximation—to understand the fundamental trade-offs between solution optimality and computational efficiency.

## 1\. The Spark: A Deep Dive into Theory

My journey began with a foundational text on the Set Cover problem, an NP-complete challenge at the heart of theoretical computer science. The initial study, based on Tamara Stern's seminar notes from MIT's 18.434 course, provided a deep understanding of:

  * **The Formal Problem:** Defining the universe, subsets, and costs.
  * **The Greedy Algorithm:** The logic of maximizing "cost-effectiveness" at each step.
  * **The Approximation Guarantee:** The mathematical proof that the greedy algorithm is guaranteed to be within a logarithmic factor of the optimal solution.

This theoretical grounding was the essential first step before writing a single line of code.

## 2\. From Theory to Practice: Initial Implementations

With a solid theoretical understanding, the next step was to bring these concepts to life. I began by implementing the two core algorithms discussed in the initial reading:

1.  **A Greedy Algorithm:** This implementation directly follows the principle of selecting the set that provides the most newly covered elements per unit of cost.
2.  **An Exact Solver:** To have a baseline for "perfect" quality, I implemented an exact solver using a Branch & Bound technique. This algorithm is guaranteed to find the absolute minimum cost solution.

While running these on simple, arbitrary test cases was a good start, it became clear that to truly demonstrate an understanding of algorithmic efficiency, I needed to solve a meaningful, real-world problem.

## 3\. The Challenge: A Real-World Application

The abstract nature of Set Cover has powerful, tangible applications. I framed my research around a compelling challenge from bioinformatics: **designing a minimum-cost genetic diagnostic panel.**

### The Model

The problem is as follows: given thousands of hereditary diseases and thousands of available genetic marker tests, how can we select the cheapest possible set of tests to ensure we can screen for every single disease?

This maps perfectly to the Set Cover model:

  * **The Universe:** The set of all diseases to be screened.
  * **The Subsets:** The available genetic marker tests, each covering a specific set of diseases.
  * **The Costs:** The price of each individual test.

To tackle this, I developed a **synthetic data generator** that creates realistic problem instances, modeling key real-world properties like common vs. rare diseases and cheap vs. expensive tests.

## 4\. Expanding the Toolkit: LP Relaxation

The scale and complexity of the diagnostic panel problem demanded a more sophisticated tool. While the greedy algorithm was fast and the exact solver was perfect, I wanted to explore the space in between. This led me to implement a third, more powerful approximation algorithm: **Linear Programming (LP) Relaxation with Rounding**.

This method involves:

1.  Relaxing the problem's integer constraints to allow for fractional solutions.
2.  Solving this "relaxed" version efficiently using a standard LP solver (`SciPy`).
3.  Rounding the fractional results to construct a final, high-quality integer solution.

This gave me a third competitor in my analysis, creating a richer and more nuanced experiment.

## 5\. The Experiment: The Three-Way Race

I ran all three algorithms on a series of synthetically generated diagnostic panel problems of increasing size. The results below quantify the critical trade-off between cost and time.

### Plot 1: Solution Quality (Cost of the Panel)

**Analysis:** This plot shows the total cost of the diagnostic panel selected by each algorithm. The exact algorithm (blue) provides the true optimal cost. As expected, the greedy algorithm (orange) finds a low-cost panel, but the LP-based method (green) consistently gets closer to the optimal solution, often providing a **10-15% cost savings** over the simpler greedy heuristic.

### Plot 2: Computational Efficiency (Runtime)

**Analysis:** This plot, using a **logarithmic scale**, tells the other half of the story. The runtime of the exact solver explodes exponentially, becoming computationally infeasible for all but the smallest problems. In contrast, both the greedy and LP-based algorithms scale gracefully. The LP solver is slightly slower than the greedy one, but this modest increase in runtime is the price for its superior solution quality.

## 6\. Conclusion: A Story of Trade-offs

This project successfully demonstrates the practical implications of algorithmic theory. My findings show:

  * The **Exact Solver** is a theoretical benchmark, but its exponential runtime makes it impractical for real-world applications.
  * The **Greedy Algorithm** is the fastest method, providing a good, low-cost solution almost instantly. It's the ideal choice when speed is the absolute priority.
  * The **LP Relaxation Algorithm** represents a powerful middle ground. It provides a significantly more cost-effective solution than the greedy method for a modest increase in computation time, making it the superior choice for high-stakes optimization problems where solution quality is paramount.

Through this project, I have completed the full research cycle: from theoretical study and modeling to implementation, experimentation, and finally, insightful analysis.
