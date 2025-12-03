# csci653
HPCS project for the course requirements 

## Problem description
Do Auger processes contribute significantly to the charge relaxation in perovskite quantum dots?

In quantum dots, charge carriers are strongly confined within a nanoscale volume. This confinement enhances Coulomb interactions between electrons and holes, making multi-particle scattering far more efficient than in bulk semiconductors. Under strong photoexcitation, high carrier densities generate multi-exciton states, most commonly biexcitons. In such states, one carrier can recombine non-radiatively and transfer its energy to another carrier through an Auger process. Identifying and quantifying this contribution is critical for understanding carrier lifetimes and optimizing optoelectronic applications of perovskite quantum dots.


## Methods used

Equation for the evolution of non-adiabatic dynamics:

$$
i\hbar \frac{d c_i(t)}{dt} = \sum_{j=0}^{N_b - 1} \left( E_i \delta_{ij} + d_{ij} \right) c_j(t)
$$

$$
d_{ij} \left( R  \left(t\right) \right) = -i\hbar \Big\langle \Phi_i \Big|\ \frac{\partial}{\partial t} \Big|\ \Phi_j \Big\rangle
$$

## Simulation methods and algorithms

In bulk semiconductor materials, surface hopping has been widely used to simulate charge relaxation and recombination on ultrafast timescales, where electron–phonon interactions dominate. In nanoscale materials such as quantum dots, strong Coulomb interactions coexist with electron–phonon couplings, and both must be considered.

To capture these effects, we will employ nonadiabatic molecular dynamics with surface hopping, extended to include Coulomb-mediated Auger channels. Surface hopping requires hundreds to thousands of independent trajectories to obtain converged statistics, since each trajectory stochastically samples electronic transitions. This ensemble nature makes the method highly amenable to parallelization across CPUs and GPUs. A core goal of this project is to demonstrate how scaling the number of trajectories across compute resources reduces wall-time and improves throughput.

## Expected results
By the end of the project we expect to obtain:
	•	Population decay vs. time for carriers in perovskite quantum dots, with and without Auger channels included.
	•	Scaling analysis: wall-time vs. number of CPU cores/GPUs for a fixed number of trajectories (strong scaling).
	•	Throughput analysis: trajectories completed per hour as resources increase (weak scaling).
	•	Qualitative signatures of Auger processes, such as faster non-radiative decay at high carrier density or in smaller quantum dots.