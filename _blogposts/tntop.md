---

layout: blogpost
title: tensor networks & topology
date: August 2, 2021
description: overview of tensor networks & their application to topological matter

---

## tensor networks & topology

In this post, we will summarize some of the basic ideas behind tensor network methods for simulating quantum matter and touch on some of the connections between these methods and topological


* image compression and SVD
* Schmidt decomposition
* Tensor formalism
* MPS and relation to SVD
* DMRG and iDMRG
* Topology

### Connection to topological matter

The tensor network methods we have looked at so far are relevant for one and some two dimensional systems and can provide us with information about the ground state wavefunction. Several works in the mid 2000s helped lay the groundwork for a connection between topological phases and tensor network methods, showing that important details of a topological phase, such as the braiding statistics of the quasiparticle excitations, could be extracted from the ground state wavefunction of the system.  

[Levin and Wen]() and [Preskill and Kitaev]() concurrently discovered that in gapped topological phases of matter, the area law for entanglement gains an additional, _topological_ contribution. This topological entanglement entropy (TEE) was eventually shown to be a partial classification of topological phases, as it vanishes for noninteracting topological phases such as Chern insulators or time-reversal invariant topological insulators. However, [Haldane and Li]() later realized that the _entanglement spectrum_ can encode properties of the edge modes the system and thereby provide more avenues for tensor network methods to be applied to diagnose and classify topological phases. 