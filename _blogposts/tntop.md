---

layout: blogpost
title: Tensor networks & topology
date: August 2, 2021
description: overview of tensor networks & their application to topological matter

---

## Tensor networks & topology 

In this post, we will summarize some of the basic ideas behind tensor network methods for simulating quantum matter and touch on some of the applications of these methods to diagnosing and studying topological phases of matter. 

### SVD and image compression

![image compression](/_img/image_compression.png) 

We’ll begin by discussing the seemingly unrelated topic of image compression. It turns out that both tensor network methods and image compression rely fundamentally on the singular value decomposition (SVD).

SVD factorizes a $$m \times n$$ matrix $$M$$ into a product of two unitary matrices and a diagonal matrix:
 
 $$M = U \Sigma V^\dagger$$

Here $$U$$ and $$V^\dagger$$ are both semi-unitary matrices, which are $$n \times k$$ and $$k \times m$$ respectively, and the matrix of singular values $$\Sigma$$ is diagonal and has rank $$k$$, which is also the rank of the matrix $$M$$.  

To compress an image, represented by a matrix $$I$$, we simply take the SVD of $$I$$ and decide how many singular values we’d like to keep around to represent the image. If we keep one singular value, for example let’s call it $$\sigma$$, then our compressed image can be constructed by multiplying $$\sigma$$ with the product of the first column of $$U$$ and the first row of $$V^\dagger$$. 

The more singular values we keep, the better an approximation to the original image we get. In the picture above, fifty singular values were kept in the compressed image. We can plot the singular values and see why compression is a reasonable thing to do:

![singular-values](/_img/singular_values_img.png) 

The singular values (squared) are plotted in a semi-log plot, and there is a huge drop off between the first few singular values and the rest. 

A remark: what we’re doing is also intimately related to dimensionality reduction and [principal component analysis](https://en.wikipedia.org/wiki/Principal_component_analysis), where SVD is used to compress a data set.


### Schmidt decomposition 

There is a useful parallel between the compression of images and the compression of _quantum states_ that relies on the singular value decomposition, and more deeply, on entanglement. We first need to introduce a concept called the Schmidt decomposition of a quantum state. 

We start by considering an arbitrary quantum state $$\psi$$ which we represent generically as

$$ \ket{\psi} = \sum\limits_{j_1, … , j_N} \psi_{j_1, … , j_N}  \ket{j_1, … , j_N}$$

Each $$j$$ represents a subsystem of the overall wavefunction, for example $$j \in \lbrace 0, 1\rbrace$$ could represent a single qubit. 

We can imagine cutting our overall system into two parts by grouping the subsystems together $$A = j_1, … , j_n$$ and $$B = j_{n+1}, … , j_N$$, represented visually in the figure below.

![schmidt decomposition](/_img/schmidt_pic.png) 

We can first group the quantum state in terms of pieces to the left and right of the cut:

$$\ket{\psi} = \sum\limits_{A,B} \psi_{AB} \ket{\psi_A} \otimes \ket{\psi_B}$$

This representation allows us to naturally apply an SVD of the matrix $$\psi_{A,B} =  U_A \Lambda V_B^\dagger$$, where $$\lambda_\alpha$$ are the singular values from the matrix $$\Lambda$$ and we define the states $$\ket{\alpha_{A}} =U_A \ket{\psi_A}$$ and $$\ket{\alpha_{B}} = V^\dagger_B \ket{\psi_B}$$. We have now arrived at the _Schmidt decomposition_ of our quantum state:

$$\ket{\psi} = \sum_{\alpha} \lambda_\alpha \ket{\alpha_A} \otimes \ket{\alpha_B}$$ 

The singular values are directly related to the entanglement between subsystems $$A$$ and $$B$$, and we can see this by considering the reduced density matrix for either subsystem (let’s take $$A$$ for example)

$$\rho_A = \Tr_B \ket{\psi}\bra{\psi} = \sum_\alpha \lambda^2_\alpha \ket{\alpha_A} \bra{\alpha_A}$$

We can now see that the entanglement entropy $$S = -\Tr(\rho^A \log \rho^A) = \sum_\alpha \lambda_\alpha^2 \log \lambda_\alpha^2$$ 

### DMRG and iDMRG

We now jump a little ahead to see a practical application of the entanglement-based truncation of quantum states in action: DMRG. This method was developed by Steve White

* DMRG from truncation of density matrix
* DMRG algorith and maybe examples
* Advantage of iDMRG for some systems

### Connection to topological matter

The tensor network methods we have looked at so far are relevant for one and some two dimensional systems and can provide us with information about the ground state wavefunction. Several works in the mid 2000s helped lay the groundwork for a connection between topological phases and tensor network methods, showing that important details of a topological phase, such as the braiding statistics of the quasiparticle excitations, could be extracted from the ground state wavefunction of the system.  

[Levin and Wen](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.96.110405) and [Preskill and Kitaev](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.96.110404) concurrently discovered that in gapped topological phases of matter, the area law for entanglement gains an additional, _topological_ contribution. This topological entanglement entropy (TEE) was eventually shown to be a partial classification of topological phases, as it vanishes for noninteracting topological phases such as Chern insulators or time-reversal invariant topological insulators. However, [Haldane and Li](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.101.010504) later realized that the _entanglement spectrum_ can encode properties of the edge modes the system and thereby provide more avenues for tensor network methods to be applied to diagnose and classify topological phases. 

We will review the strategy behind a series of applications based on the foundations mentioned above, looking at how tensor networks can shed light on the complicated physics of fractional quantum Hall states. 

* Cincio and Vidal paper sketch?
* Zaletel flux attachment scheme
* Application to FQHE Zaletel paper


