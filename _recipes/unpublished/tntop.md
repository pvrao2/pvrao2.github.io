---

layout: blogpost
title: Tensor networks & topology
date: August 2, 2021
description: overview of tensor networks & their application to topological matter

---

## Tensor networks & topology 

In this post, we will summarize some of the basic ideas behind tensor network methods for simulating quantum matter and touch on some of the applications of these methods to diagnosing and studying topological phases of matter. 

### SVD and image compression

<p align="center">
<img src="{{site.url}}/_img/image_compression.png" alt="image compression" width="500" height="auto"/>
</p>

We’ll begin by discussing the seemingly unrelated topic of image compression. It turns out that both tensor network methods and image compression rely fundamentally on the singular value decomposition (SVD).

SVD factorizes a $$m \times n$$ matrix $$M$$ into a product of two unitary matrices and a diagonal matrix:
 
 $$M = U \Sigma V^\dagger$$

Here $$U$$ and $$V^\dagger$$ are both semi-unitary matrices, which are $$n \times k$$ and $$k \times m$$ respectively, and the matrix of non-zero singular values $$\Sigma$$ is diagonal and has rank $$k$$, which is also the rank of the matrix $$M$$.  We can now introduce a basic “tensor network” diagram for SVD, where each open leg in the diagram represents a free index and connecting edges represent contractions (for a more concrete introduction to the visual notation [see](https://arxiv.org/abs/1805.00055)), 


<p align="center">
 <img src="{{site.url}}/_img/SVD.png" alt="SVD" width="600" height="auto"/>
</p> 

To compress an image, represented by a matrix $$I$$, we simply take the SVD of $$I$$ and decide how many singular values we’d like to keep around to represent the image. If we keep the first singular value, for example let’s call it $$\sigma$$, then our compressed image can be constructed by multiplying $$\sigma$$ with the product of the first column of $$U$$ and the first row of $$V^\dagger$$. 

The more singular values we keep, the better an approximation to the original image we get. In the picture above, fifty singular values were kept in the compressed image. We can plot the singular values and see why compression is a reasonable thing to do:

<p align="center">
 <img src="{{site.url}}/_img/singular_values_img.png" alt="singular values" width="450" height="auto"/>
</p> 

The singular values (squared) are plotted in a semi-log plot, and there is a huge drop off between the first few singular values and the rest. 

A remark: what we’re doing is also intimately related to dimensionality reduction and [principal component analysis](https://en.wikipedia.org/wiki/Principal_component_analysis), where SVD is used to compress a data set.


### Schmidt decomposition 

There is a useful parallel between the compression of images and the compression of _quantum states_ that relies on the singular value decomposition, and more deeply, on entanglement. We first need to introduce a concept called the Schmidt decomposition of a quantum state. 

We start by considering an arbitrary quantum state $$\psi$$ which we represent generically as

$$ \ket{\psi} = \sum\limits_{j_1, … , j_N} \psi_{j_1, … , j_N}  \ket{j_1, … , j_N}$$

Each $$j$$ represents a subsystem of the overall wavefunction, for example $$j \in \lbrace 0, 1\rbrace$$ could represent a single qubit. 

We can imagine cutting our overall system into two parts by grouping the subsystems together $$A = j_1, … , j_n$$ and $$B = j_{n+1}, … , j_N$$, represented visually in the figure below.


<p align="center">
 <img src="{{site.url}}/_img/schmidt_pic.png" alt="schmidt picture" width="400" height="auto"/>
</p> 

We can first group the quantum state in terms of pieces to the left and right of the cut:

$$\ket{\psi} = \sum\limits_{A,B} \psi_{AB} \ket{\psi_A} \otimes \ket{\psi_B}$$

This representation allows us to naturally apply an SVD of the matrix $$\psi_{A,B} =  U_A \Lambda V_B^\dagger$$, where $$\lambda_\alpha$$ are the non-zero singular values from the matrix $$\Lambda$$ — there are $$\chi$$ of them this is called the Schmidt rank. We define the states $$\ket{\alpha_{A}} =U_A \ket{\psi_A}$$ and $$\ket{\alpha_{B}} = V^\dagger_B \ket{\psi_B}$$. We have now arrived at the _Schmidt decomposition_ of our quantum state:

$$\ket{\psi} = \sum_{\alpha}^\chi \lambda_\alpha \ket{\alpha_A} \otimes \ket{\alpha_B}$$ 

The singular values are directly related to the entanglement between subsystems $$A$$ and $$B$$, and we can see this by considering the reduced density matrix for either subsystem (let’s take $$A$$ for example)

$$\rho_A = \Tr_B \ket{\psi}\bra{\psi} = \sum_\alpha \lambda^2_\alpha \ket{\alpha_A} \bra{\alpha_A}$$

We can now see that the entanglement entropy is directly related to the singular values as 

$$S = -\Tr(\rho^A \log \rho^A) = \sum_\alpha \lambda_\alpha^2 \log \lambda_\alpha^2$$

The spectrum of the density matrix is referred to as the entanglement spectrum $$\lbrace \epsilon_\alpha \rbrace$$, which we will revisit. 

### Entanglement: area versus volume laws

We now add some important context to the Schmidt decomposition of quantum states. 

*  For a gapped local Hamiltonian in 1D, the ground state obeys an area law with entanglement entropy: scales with the _area_ of cut and not _volume._
* In terms of the Schmidt decomposition, we see that an area law state will have decreasing Schmidt values rather than constant ones.

<p align="center">
 <img src="{{site.url}}/_img/arealaw.png" alt="area law" width=“700” height="auto"/>
</p> 

As we see in the figure above from the [review paper](https://arxiv.org/abs/1805.00055) by Hauschild and Pollmann, we can think of the area law states as a special corner of the overall Hilbert space. The figure on the right compares the Schmidt values of the ground state of the transverse field Ising model versus a random state for $$N=16$$ spins - we can see that for this gapped ground state, the Schmidt values decay rapidly.

This brings to mind the example of image compression where the first few singular values contained most of the important information, and we were able to truncate our image. In this case, we can imagine truncating the quantum state to keep only $$\tilde{\chi} < \chi$$ Schmidt values:

$$|| \psi - \sum\limits_\alpha^\tilde{\chi} \lambda_\alpha \ket{\alpha_A} \otimes \ket{\alpha_B}|| < \epsilon$$ 

For an area law state, for all $$\epsilon > 0$$, we can achieve the relation above for a finite $$\tilde{\chi}$$, where above the norm is the Frobenius norm. Though the area law states are only rigorously linked (see [here](https://arxiv.org/pdf/1301.1162.pdf) and [here](https://arxiv.org/abs/0705.2024)) to ground states of gapped local Hamiltonians in 1D, if we are able to map a pseudo 2D problem to a 1D problem, the same considerations will apply. 

The density matrix renormalization group (DMRG)  [developed by](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.69.2863)  Steve White was originally developed with this in mind, successively truncating the quantum state based on the entanglement spectrum (Schmidt values) of the density matrix. We will consider a compatible formulation that came later based on matrix product states. 

### Matrix product states (MPS)

A matrix product state $$\ket{\psi}$$ is one that can be written as 

$$\ket{\psi} = \sum\limits_{j_1, … , j_N} \sum\limits_{\alpha_1, … , \alpha_N} M^{[1] j_1}_{\alpha_1 \alpha_2} M^{[2] j_2}_{\alpha_2 \alpha_3} … M^{[N] j_N}_{\alpha_N \alpha_{N+1}} \ket{j_1, … , j_N}$$

Each matrix $$M^{[i] j_i}$$ is an $$\chi_i \times \chi_{i+1}$$ dimensional matrix (which represent the dimension of the lower indices $$\alpha_i$$). There’s an inherent ambiguity in the definition of MPS, as we can always insert an invertible matrix between any of the two matrices and recoup the same overall state. It turns out that there is a _canonical form_ of MPS that will allow us to make contact with the Schmidt decomposition of quantum states seen earlier.  Let’s introduce this canonical form by considering a generic state on a lattice of $$N$$ sites, with degrees of freedom $$j_i$$ (each of dimension $$d$$) on each site, this reads:

$$\ket{\psi} = \sum\limits_{j_1, … , j_N} \psi_{j_1, … , j_N} \ket{j_1, … , j_N}$$ 

into an MPS in a specific way, starting by considering the tensor $$\psi_{j_1,…,j_N}$$ as a matrix with indices $$j_1$$ and the composite index $$(j_2, … , j_N)$$, 

<p align="center">
 <img src="{{site.url}}/_img/canonicalform1.png" alt="" width="550" height="auto"/>
</p> 

We have performed an SVD here on the matrix $$\psi_{j_1, (j_2, … , j_N)}$$ and find:

$$\psi_{j_1, … , j_N} = \sum\limits_{\alpha_1}^{\chi_1} U_{j_1, \alpha_1} \Sigma_{\alpha_1, \alpha_1} (V^\dagger)_{\alpha_1, \bf{j}} \equiv \sum\limits_\alpha_1^\chi_1 U_{j_1,\alpha_1} \psi_{\alpha_1, j_2, … , j_N)}$$

The result is the familiar $$U, V^\dagger$$ and $$\Sigma$$ matrices where the latter contains the non-zero singular values (there are $$\chi_1$$ of them). It is more convenient to view  the $$U$$ matrix here as a collection of $$d$$ row vectors with entries $$A^{j_1}_{\alpha_1} = U_{j_1,\alpha_1}$$. Continuing on, we can again reshape the object $$\psi_{\alpha_1, j_2, … , j_N)} \rightarrow \psi_{(\alpha_1 j_2), (j_3, … , j_N)$$ and perform an SVD:

$$\psi_{j_1, … , j_N} = \sum\limits{\alpha_1}^{\chi_1}\sum\limits_{\alpha_2}^{\chi_2} A^{j_1}_{\alpha_1} U_{(a_1 j_2), (j_3, … , j_N) \Sigma_{\alpha_2, \alpha_2} (V^\dagger)_{a_2, (j_3, …, j_N)= \sum_\limits{\alpha_1}^{\chi_1}\sum\limits_{\alpha_2}^{\chi_2} A^{j_1}_{\alpha_1} A^{j_2}_{\alpha_1, \alpha_2} \psi_{(a_2, j_3),(j_4, … , j_N)}$$

<p align="center">
 <img src="/_img/leftcanonicalform.png" alt="left canonical form" width="400" height="auto"/>
</p> 

The above form is referred to as “left canonical form” — if we started chain of SVD from the right, we could alternatively reach the “right canonical form”, and working from both ends and keeping at least one matrix of singular values around would yield a “mixed canonical form”. 

### DMRG and iDMRG

* DMRG from truncation of density matrix
* DMRG algorithm and maybe examples
* Advantage of iDMRG for some systems

### Connection to topological matter

The tensor network methods we have looked at so far are relevant for one and some two dimensional systems and can provide us with information about the ground state wavefunction. Several works in the mid 2000s helped lay the groundwork for a connection between topological phases and tensor network methods, showing that important details of a topological phase, such as the braiding statistics of the quasiparticle excitations, could be extracted from the ground state wavefunction of the system.  

[Levin and Wen](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.96.110405) and [Preskill and Kitaev](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.96.110404) concurrently discovered that in gapped topological phases of matter, the area law for entanglement gains an additional, _topological_ contribution. This topological entanglement entropy (TEE) was eventually shown to be a partial classification of topological phases, as it vanishes for noninteracting topological phases such as Chern insulators or time-reversal invariant topological insulators. However, [Haldane and Li](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.101.010504) later realized that the _entanglement spectrum_ can encode properties of the edge modes the system and thereby provide more avenues for tensor network methods to be applied to diagnose and classify topological phases. 

We will review the strategy behind a series of applications based on the foundations mentioned above, looking at how tensor networks can shed light on the complicated physics of fractional quantum Hall states. 

* Cincio and Vidal paper sketch?
* Zaletel flux attachment scheme
* Application to FQHE Zaletel paper

