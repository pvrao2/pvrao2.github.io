---

layout: blogpost
title: Tensor networks & topology (2/2)
date: August 2, 2021
description: overview of tensor networks & their application to topological matter

---

## Tensor networks & topology (2/2)

In this second part of this post, we will focus more in the connections of tensor network methods (specifically DMRG) to diagnosing and studying topological phases of matter. 

### Connection to topological matter 

The tensor network methods we have looked at so far are relevant for one and some two dimensional systems and can provide us with information about the ground state wavefunction. Several works in the mid 2000s helped lay the groundwork for a connection between topological phases and tensor network methods, showing that important details of a topological phase, such as the braiding statistics of the quasiparticle excitations, could be extracted from the ground state wavefunction of the system.  

[Levin and Wen](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.96.110405) and [Preskill and Kitaev](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.96.110404) concurrently discovered that in gapped topological phases of matter, the area law for entanglement gains an additional, _topological_ contribution:

$$S  \approx \alpha L - \gamma \;\; (1D)$$

This topological entanglement entropy (TEE) $$\gamma$$ was shown to be a partial classification of topological phases. It vanishes for noninteracting topological phases such as Chern insulators or time-reversal invariant topological insulators.  [Haldane and Li](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.101.010504) later realized that the _entanglement spectrum_ can encode properties of the edge modes the system and thereby provide more avenues for tensor network methods to be applied to diagnose and classify topological phases. 

### Application: iDMRG for diagnosing topological phases

We will briefly review the strategy behind the application of iDMRG to these toplogical systems, first on the diagnostic aspect of topological order and next 

* Cincio and Vidal paper sketch?
* Zaletel flux attachment scheme
* Application to FQHE Zaletel paper


