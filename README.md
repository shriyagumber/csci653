# csci653
HPCS project for the course requirements 

## Problem description
Do Auger processes contribute significantly to the charge relaxation in perovskite quantum dots?

In quantum dots, charge carriers are strongly confined within a nanoscale volume. This confinement enhances Coulomb interactions between electrons and holes, making multi-particle scattering far more efficient than in bulk semiconductors. Under strong photoexcitation, high carrier densities generate multi-exciton states, most commonly biexcitons. In such states, one carrier can recombine non-radiatively and transfer its energy to another carrier through an Auger process. Identifying and quantifying this contribution is critical for understanding carrier lifetimes and optimizing optoelectronic applications of perovskite quantum dots.


## Methods used

\begin{equation}
\Phi_i(1, 2, \ldots, N) = \hat{A}[{\phi}_{i_1}(1){\phi}_{i_2}(2) \ldots {\phi}_{i_N}(N)]
\end{equation}

\begin{equation}
d_{ij}(R(t)) = - i\hbar \langle \Phi_i \left| \frac{\partial}{\partial t} \right| \Phi_j \rangle
\end{equation}

For instance, for the given two SDs: \(\Phi_i = \hat{A}[{\phi}_{1} \ldots {\phi}_{m} \ldots {\phi}_{n} \ldots {\phi}_{N}] \) and \(\Phi_j = \hat{A}[{\phi}_{1} \ldots {\phi}_{p} \ldots {\phi}_{q} \ldots {\phi}_{N}] \), the charge-charge interaction is given by: 

\begin{equation}
V_{ij} = \langle \Phi_i | \hat{V} | \Phi_j \rangle = \langle mn|pq \rangle - \langle mn|pq \rangle
\end{equation}
where \(\langle mn|pq \rangle\) is the coulomb integral. Coulombic tetradic tensor is evaluated within the Projector augmented wave (PAW) methodology, as proposed by Kresse and co-workers.\cite{10.1063/1.5065504, 10.1063/1.1926272} It can be written as:

\begin{equation}
\langle mn|pq \rangle = \frac{e^2}{2} \int dr_1 dr_2 \phi_m^*(r_1) \phi_n^*(r_2) r_{12}^{-1} \phi_p(r_1) \phi_q(r_2)
\end{equation}
After addition of the coulomb matrix elements, Hamiltonian can be rewritten as:
\begin{equation}
H = E_i \delta_{ij} + d_{ij} + V_{ij}
\end{equation}


## Simulation methods and algorithms

In bulk semiconductor materials, surface hopping has been widely used to simulate charge relaxation and recombination on ultrafast timescales, where electron–phonon interactions dominate. In nanoscale materials such as quantum dots, strong Coulomb interactions coexist with electron–phonon couplings, and both must be considered.

To capture these effects, we will employ nonadiabatic molecular dynamics with surface hopping, extended to include Coulomb-mediated Auger channels. Surface hopping requires hundreds to thousands of independent trajectories to obtain converged statistics, since each trajectory stochastically samples electronic transitions. This ensemble nature makes the method highly amenable to parallelization across CPUs and GPUs. A core goal of this project is to demonstrate how scaling the number of trajectories across compute resources reduces wall-time and improves throughput.

## Expected results
By the end of the project we expect to obtain:
	•	Population decay vs. time for carriers in perovskite quantum dots, with and without Auger channels included.
	•	Scaling analysis: wall-time vs. number of CPU cores/GPUs for a fixed number of trajectories (strong scaling).
	•	Throughput analysis: trajectories completed per hour as resources increase (weak scaling).
	•	Qualitative signatures of Auger processes, such as faster non-radiative decay at high carrier density or in smaller quantum dots.