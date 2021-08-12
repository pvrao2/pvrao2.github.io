---

layout: blogpost
title: Tensor networks & topology
date: August 2, 2021
description: overview of tensor networks & their application to topological matter

---

## Tensor networks & topology 

In this post, we will summarize some of the basic ideas behind tensor network methods for simulating quantum matter and touch on some of the applications of these methods to diagnosing and studying topological phases of matter. 

### Image compression and SVD

We’ll begin by discussing the seemingly unrelated topic of image compression. It turns out that both compressing classical images and quantum states of gapped hamiltonians relies on a key principle - the singular value decomposition (SVD).

SVD factorizes a $$m \times n$$ matrix $$M$$ into a product of two unitary matrices and a diagonal matrix:
 
 $$M = U \Sigma V^\dagger$$

Here $$U$$ and $$V^\dagger$$ are both semi-unitary matrices, which are $$n \times k$$ and $$k \times m$$ respectively, and the matrix of singular values $$\Sigma$$ is diagonal and has rank $$k$$, which is also the rank of the matrix $$M$$.  

To compress an image, represented by a matrix $$I$$, we simply take the SVD of $$I$$ and decide how many singular values we’d like to keep around to represent the image. If we keep one singular value, for example let’s call it $$\sigma$$, then our compressed image

$$ compressed image $$


### Schmidt decomposition 

There will turn out to be a useful parallel between the compression of images and the compression of _quantum states_ that relies on the singular value decomposition, and more deeply, on entanglement. We first need to introduce a concept called the Schmidt decomposition of a quantum state. 

We start by considering an arbitrary quantum state $$\psi$$ which we represent generically as

$$ \ket{\psi} = \sum\limits_{j_1, … , j_N} \psi_{j_1, … , j_N}  \ket{j_1, … , j_N}$$

Now let’s decompose our system into two parts, represented visually in the figure below.

<figure>
  <img src=“{{site.url}}/_img/schmidt_pic.png” style=“display: block; margin: auto;” width=75%; height=auto; />  <figcaption>This is my caption text.</figcaption>
</figure>
 

* Schmidt decomposition
* Tensor formalism
* MPS and relation to SVD
* DMRG and iDMRG

### Connection to topological matter

The tensor network methods we have looked at so far are relevant for one and some two dimensional systems and can provide us with information about the ground state wavefunction. Several works in the mid 2000s helped lay the groundwork for a connection between topological phases and tensor network methods, showing that important details of a topological phase, such as the braiding statistics of the quasiparticle excitations, could be extracted from the ground state wavefunction of the system.  

[Levin and Wen](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.96.110405) and [Preskill and Kitaev](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.96.110404) concurrently discovered that in gapped topological phases of matter, the area law for entanglement gains an additional, _topological_ contribution. This topological entanglement entropy (TEE) was eventually shown to be a partial classification of topological phases, as it vanishes for noninteracting topological phases such as Chern insulators or time-reversal invariant topological insulators. However, [Haldane and Li](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.101.010504) later realized that the _entanglement spectrum_ can encode properties of the edge modes the system and thereby provide more avenues for tensor network methods to be applied to diagnose and classify topological phases. 

We will review the strategy behind a series of applications based on the foundations mentioned above, looking at how tensor networks can shed light on the complicated physics of fractional quantum Hall states. 

* Cincio and Vidal paper sketch?
* Zaletel flux attachment scheme
* Application to FQHE Zaletel paper


