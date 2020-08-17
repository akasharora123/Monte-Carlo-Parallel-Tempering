# Monte Carlo Parallel Tempering
> A simulated annealing technique to enhance Monte Carlo sampling efficiency.

## Overview
Monte Carlo methods are commonly used in chemical physics in order to compute equilibrium properties of a material at a specific temperature *T*, and comprising of volume *V*, and number of molecules *N*. Microscopically, the equilibrium state of a material is not a fixed state but comprises of several microstates/configurations, distributed according to a Boltzmann distribution,

```markdown
$p(x) = exp(-U(x)/k_BT),$
``` 
where *k_B* is the Boltzmann constant, and *U(x)* represent the energy of a microstate with molecular configuration/coordinates *x*. The equilibrium property is then computed as an average of the properties of whole ensemble of microstates. This ensemble is also referred to as Canonical ensemble or *NVT* ensemble. 

One efficient way to achieve the desired distribution is by using Metropolis Monte Carlo method (MMC). MMC is a type of Markov Chain Monte Carlo (MCMC) method which creates a Markov chain to efficiently sample the desired (apriori-defined) probability distribution. Specifically, each Monte Carlo move (going from *x to x'*) is accepted with a probability, 
```markdown
$\alpha(x\rightarrow x') = f(x)/f(x')$, 
```
where *f(x)* is the desired distribution (Boltzmann here). The efficiency of MMC simulation to achieve equilibrium ensemble strongly depends on the shape of potential energy surface, *U(x)*. For may systems, *U(x)* contains many local minima, and the simulation or Markov chain may get trapped in local minima leading to inefficient sampling (or biased representation of ensemble). Since the Boltzmann distribution is inversely proportional to temperature, the system at higher temperature easily overcomes the barrier to jump over local minima and sample the energy surface efficiently. However, the system a lower temperatures suffers from poor sampling.    

Parallel tempering is an advanced sampling method which helps systems at lower temperature to come out of local minima and sample the phase space efficiently. Specifically, in Parallel Tempering framework, several replicas of system at various temperatures are simulated and the configurations (during Markov chain) between lower and higher temperature are swapped . This allows system with lower temperature to gain energy from higher temperature systems and jumps out of local minimum. The swap between the replicas at two temperatures *T1* and *T2* is accepted using a Monte Carlo criteria, 
```markdown
$p_{swap} = \exp(U_1-U_2)/(1/T_1 - 1/T_2)$. 
```
Here we demonstrate the power of Parallel Tempering using a one-dimensional potential energy surface comprising of four local minima. 


## Prerequisites
- Python
- NumPy
- Matplotlib

## References:
- This case study is adopted from Chapter 14 of the book: Understanding Molecular Simulation: From Algorithms to Applications, Berend Smit and Daan Frenkel, Academic Press (2002). 
 
## License
[![License](http://img.shields.io/:license-mit-blue.svg?style=flat-square)](http://badges.mit-license.org)
- **[MIT license](http://opensource.org/licenses/mit-license.php)**