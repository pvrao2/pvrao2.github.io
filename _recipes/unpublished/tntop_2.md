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

$$\gamma = \log \frac{D}{d_a}$$

with $$d_a$$ the quantum dimension (one for abelian anyons, greater in other cases) and $$D  = \sum_a \sqrt{d_a^2}$$ the total quantum dimension. It vanishes for noninteracting topological phases such as Chern insulators or time-reversal invariant topological insulators.  [Haldane and Li](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.101.010504) later realized that the _entanglement spectrum_ can encode properties of the edge modes the system and thereby provide more avenues for tensor network methods to be applied to diagnose and classify topological phases. Both the entanglement spectrum and TEE can be extracted from the ground state wavefunction, particularly when the ground state is approximated as an MPS and entanglement properties are readily accessible. 

### iDMRG for identifying topological phases

The applications we focus on ([here](https://arxiv.org/abs/1211.3733) and [here](https://arxiv.org/abs/1208.2623)) both focus on two dimensional systems that can be treated as quasi-1D and studied with iDMRG. For systems with topological order, we have a degenerate set of ground states on a non-trivial manifold such as a torus or cylinder, and so we focus on these geometries to exploit this property.

* topological entanglement entropy

If we apply iDMRG to our system and get back an approximate ground state wavefunction $$\ket{\Psi}$$, in the form of a MPS, we can cut our system in half and study the Schmidt decomposition of the halves of the system. Looking at the cut dependence of the Renyi entropy, we can extract the TEE.

<p align="center">
 <img src="{{site.url}}/_img/diagnose_top_phase.png" alt="singular values" width="450" height="auto"/>
</p> 

The example above shows the extraction of the TEE for the $$\nu = 2/5$$ fractional quantum Hall state, whose ground state was found using iDMRG on an infinite cylinder. Here the length dependence distinguishes the usual entropy from the TEE as $$\gamma = L \frac{\partial S}{\partial L} - S(L)$$. Here $$\gamma \rightarrow \frac{1}{2} \log 5$$, as expected for a system with five abelian anyons. 

* Cincio and Vidal paper sketch?
* Zaletel flux attachment scheme
* Application to FQHE Zaletel paper


