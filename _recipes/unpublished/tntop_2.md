---

layout: blogpost
title: Tensor networks & topology (2/2)
date: August 2, 2021
description: overview of tensor networks & their application to topological matter

---

## Tensor networks & topology (2/2)

In this second part of this post, we will focus more in the connections of tensor network methods (specifically DMRG) to diagnosing and studying topological phases of matter. 

### Connection to topological matter 

The tensor network methods we have looked at so far are relevant for one and some two dimensional systems and can provide us with information about the ground state wavefunction. Several works in the mid 2000s helped lay the groundwork for a connection between topological phases and tensor network methods, showing that important details of a topological phase, such as the braiding statistics of the quasiparticle excitations, could be extracted from the ground state wavefunction of the system.  This connection began with [Levin and Wen](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.96.110405) and [Preskill and Kitaev](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.96.110404) concurrently discovered that in gapped topological phases of matter, the area law or entanglement gains an additional, _topological_ contribution:

$$S  \approx \alpha L - \gamma$$

This topological entanglement entropy (TEE) $$\gamma$$ was shown to be a partial classification of topological phases, and is given by

$$\gamma = \log D - \log{d_a}$$

with $$d_a$$ the quantum dimension (one for abelian anyons, greater in other cases) and $$D  = \sum_a \sqrt{d_a^2}$$ the total quantum dimension. It vanishes for noninteracting topological phases such as Chern insulators or time-reversal invariant topological insulators.  [Haldane and Li](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.101.010504) later realized that the _entanglement spectrum_ can encode properties of the edge modes the system and thereby provide more avenues for tensor network methods to be applied to diagnose and classify topological phases. Both the entanglement spectrum and TEE can be extracted from the ground state wavefunction, particularly when the ground state is approximated as an MPS and entanglement properties are readily accessible. 

### iDMRG for identifying topological phases

The applications we focus on ([here](https://arxiv.org/abs/1211.3733) and [here](https://arxiv.org/abs/1208.2623)) both focus on two dimensional systems that can be treated as quasi-1D and studied with iDMRG. For systems with topological order, we have a degenerate set of ground states on a non-trivial manifold such as a torus or cylinder, and so we focus on these geometries to exploit this property.

* topological entanglement entropy

If we apply iDMRG to our system and get back an approximate ground state wavefunction $$\ket{\Psi}$$, in the form of a MPS, we can cut our system in half and study the Schmidt decomposition of the halves of the system. Looking at the cut dependence of the Renyi entropy, we can extract the TEE.

<p align="center">
 <img src="{{site.url}}/_img/diagnose_top_phase.png" alt="singular values" width="450" height="auto"/>
</p> 

The example above shows the extraction of the TEE for the $$\nu = 2/5$$ fractional quantum Hall state, whose ground state was found using iDMRG on an infinite cylinder. Here the length dependence distinguishes the usual entropy from the TEE as $$\gamma = L \frac{\partial S}{\partial L} - S(L)$$. Here $$\gamma \rightarrow \frac{1}{2} \log 5$$, as expected for a system with five abelian anyons. 

*Flux attachment and entanglement spectrum

In addition to encoding some properties of [edge modes](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.101.010504), the entanglement spectrum can also be used to about the quantized responses of a topological phase with some symmetries. To illustrate this (see [here](https://arxiv.org/abs/1405.6028) for more details), we can consider a gapped and infinite 1D chain:

<p align="center">
 <img src="{{site.url}}/_img/ringdecomposition.png" alt="singular values" width="450" height="auto"/>
</p> 

Above the top image shows the infinite chain and the finite correlation length that doesn't scale with the volume of the system (in this case the length) owing to the fact that the system is gapped. Two Schmidt decompositions of the system yields the second figure, with Schmidt values $$s_q$$ and $$s_p$$ from each SD. To view the segment $$B$$ as a ring, one can trace over the outer indices, where the ground state on the ring is viewed as

$$\ket{\psi_o^{I}} = \sum\limits_p s_p \ket{p,p}_B + \mathcal{O}(e^{-L/\xi})$$

To add flux through the ring, it is sufficient to apply a twisted boundary condition to the edges of the segment $$B$$ before gluing it together, as shown in the bottom-most figure. The resulting ground state on the ring, with flux (under a symmetry $$g$$) added, is 

$$ \ket{\psi_o^{(g)}} = \sum\limits_{p,q} s_q \ket{p,q}_B U^{(g)}_{qp} + \mathcal{O}(e^{-L/\xi})$$

We now relate this to some concrete responses to the inserted flux. As a first example, the Berry phase $$\gamma_B$$ associated with inserting a $$U(1)$$ flux $$\Phi$$ is given by

$$\gamma_B = \int_0^{2\pi} d\Phi A(\Phi) - i\log\braket{\psi_o^0}{\psi_o^{2\pi}} \rightarrow e^{i\gamma_B} = \exp{2\pi i\sum\limits_p s_p^2 Q_p}$$

We see the Berry phase is related to the entanglement spectrum (Schmidt values $$s_p$$) and charge of the Schmidt state $$Q_p$$. In 1D, this Berry phase can be interpreted as a polarization, which in this case is given by the average charge of each Schmidt state with respect to the entanglement Hamiltonian. As another example, consider a 2D system on a torus which has the following symmetry under modular transformations  

$$(x,y) \sim (x,y + L_y) \;\; \text{and} \;\;  (x+L_y,y) \sim (x,y+\tau L_y)$$

Modifying the modular parameter 𝜏 takes us to an identical torus, and we wish to calculate a Berry phase as the ground state goes from $$\tau \rightarrow \tau +1$$. This is called the modular $$T$$ matrix, and it encodes the topological spin and chiral central charge of the edge of the system ([see](https://www.worldscientific.com/doi/abs/10.1142/S0217979293003644)). If we collapse each ring on the torus at fixed x to a single site, we can view the translation $$e^{iP_y \delta y)$$ as a U(1) transformation 
 with $\Phi = 2\pi \tau$. The Schmidt states in this case have a quantized momenta $k_p$ and the Berry phase (T matrix) is
 
 $$\gamma_T = \exp(i s_p^2 k_y L_y)

In this case the Berry phase can be viewed as a momentum polarization and again it is given by the average momentum of each Schmidt state with respect to the entanglement Hamiltnonian. For fractional quantum Hall states, modular $$T$$ matrix is also related to the topological spin, chiral central charge and Hall viscosity of the system, 

$$(gamma_T)_{ab} =  \delta_{ab} \exp i(h_a - \frac{c}{24} - \frac{\eta_H}{2\pi \hbar} L_x^2)$$

By probing the entanglement spectrum one can also learn about these quantities. For example for the $$\nu = 2/5$$ fractional quantum Hall state, the chiral central charge $$c$$, topological spin $$h$$ and shift $$\mathcal{S} \sim \eta_H$$ are measured to their expected values of 2/24, 1/5, 4/16 through this method. 

<p align="center">
 <img src="{{site.url}}/_img/fqhe.png" alt="singular values" width="450" height="auto"/>
</p> 


