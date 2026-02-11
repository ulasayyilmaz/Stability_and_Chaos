# Project: Stability and Chaos in Networks of Spiking Neurons
Master Program Computational Neuroscience,
Winter 2025/26 


## Introduction
In the theory of dynamical systems a central question is whether small
perturbations to a system’s trajectory diminish, i.e. the perturbed trajectory evolves as unperturbed, or whether initially small perturbations grow. The former expresses stability to perturbations. On the other side, if perturbations grow exponentially fast, irrespective of the initial condition, the system is chaotic. Both, stability and chaos, can be desirable for neural networks; stability is useful for memory and reliability, chaos is useful for distinction and classification.

Networks of spiking neurons can display a combination of stability and chaos: Monteforte and Wolf (2012) study an Erdös-Rényi network of inhibitory LIF neurons with constant excitation. After a small perturbation to the membrane voltages, the network state evolves almost like unperturbed. However, for perturbations above a critical magnitude, the network will take an entirely different path. Thus, to every possible trajectory of the network there corresponds a ”flux tube” of states. Inside each flux tube, perturbations decay. Leaving the flux tube puts the network into a different flux tube, which deviates infinitely fast from the original one.

The goal of this project is to determine the critical magnitude from simulations, and to understand and illustrate the intricate structure of the phase space.



## Steps
1. Using Brian (www.briansimulator.org), implement a network of leaky integrate-and-fire neurons as detailed in Monteforte and Wolf (2012), specifically in the caption of their Fig. 1. Plot the spikes of 30 randomly chosen neurons, the voltage dynamics and spikes of one neuron, and the inter-spike interval distribution. Compare to Figure 1.
(Hint: You may use smaller values of N and K, but expect deviations!)

2. Implement a function that transforms voltages to phases $\Phi(\mathbf{V})$ element-wise according to Monteforte and Wolf (2012), first equation on page 3. Further implement the inverse function $\mathbf{V}(\Phi)$.

3. Implement the following procedure: (i) Integrate the network for a time $T$ as in the first task and store the final voltages, lets call them $\mathbf{V}_0 = \mathbf{V}_{init}(T)$. (ii) For the same connectivity, integrate the dynamics starting from $\mathbf{V}_0$ and store the resulting voltages $\mathbf{V}(t)$. (iii) For the same connectivity, integrate the dynamics starting from a perturbed initial point $\mathbf{V}(\Phi_0 + ε\mathbf{r})$, where $\Phi_0 = \Phi(\mathbf{V}_0)$ and $\mathbf{r}$ is a normalized random vector. The random vector can be generated e.g. using `r = np.random.normal(0, 1, N)` and `r /= np.linalg.norm(r)`. Store the resulting voltages $\mathbf{V}_ε(t)$. (iv) Compute the time dependent difference of (ii) and (iii) in terms of their phases $D_\Phi(t) = \|\Phi(\mathbf{V}(t)) − \Phi(\mathbf{V}_ε(t)\|$.

4. Find two values of $ε$ such that (i) $D_\Phi(t)$ diminishes over time and (ii) $D_\Phi(t)$ grows over time, cf. Figure 5a left and right of Monteforte and Wolf (2012). Reproduce both cases for at least 3 realizations. How would you call the two cases?

5. Repeat the preceding experiment for several values of $ε$ and multiple realizations, to assess for each $ε$ the number of realizations where $D_\Phi(t)$ does not go towards zero, i.e. $D_\Phi(t)$ jumps. For example, one could test, if the final value of $D_\Phi(t)$ is larger than the initial value $D_\Phi(0)$. Divide the number of jumps per $ε$ by the number of realizations per $ε$ to estimate the probability of increased perturbation. Compare your results to Figure 5b.

6. (Extra) Sample two normalized random vectors $\mathbf{p}$ and $\mathbf{q}$. For a relatively small network $N = 200$, simulate the network from (at least) $20 \times 20$ initial conditions $\mathbf{V}_{ij} = \mathbf{V} [(−0.1 + i * 0.01)\mathbf{p} + (−0.1 + j * 0.01)\mathbf{q}]$, using the inverse function implemented above, where $i$ and $j$ range from 0 to 20. Compare the difference $D_\Phi(t)$ between each pair of simulations and check, which pairs converge and which pairs diverge. Identify groups of initial conditions that converge to the same trajectory. In the plane of initial conditions, colorcode every such group, reproducing Figure 7a, left.



## References
M. Monteforte and F. Wolf. **Dynamic flux tubes form reservoirs of stability in neuronal circuits.** *Physical Review X*, 2(4):041007, 2012.