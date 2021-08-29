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

We’ll begin by discussing the seemingly unrelated topic of image compression. It turns out that both tensor network methods and image compression rely fundamentally on the singular value decomposition (SVD). SVD factorizes a $$m \times n$$ matrix $$M$$ into a product of two unitary matrices and a diagonal matrix:
 
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
 <img src="{{site.url}}/_img/arealaw.png" alt="area law" width="700" height="auto"/>
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

$$\psi_{j_1, … , j_N} = \sum\limits_{\alpha_1}^{\chi_1} U_{j_1, \alpha_1} \Sigma_{\alpha_1, \alpha_1} (V^\dagger)_{\alpha_1, (j_2,    … , j_N)} \equiv \sum\limits_{\alpha_1}^{\chi_1} U_{j_1,\alpha_1} \psi_{\alpha_1, j_2, … , j_N}$$

The result is the familiar $$U, V^\dagger$$ and $$\Sigma$$ matrices where the latter contains the non-zero singular values (there are $$\chi_1$$ of them). It is more convenient to view  the $$U$$ matrix here as a collection of $$d$$ row vectors with entries $$A^{j_1}_{\alpha_1} = U_{j_1,\alpha_1}$$. Continuing on, we can again reshape the object $$\psi_{\alpha_1, j_2, … , j_N} \rightarrow \psi_{(\alpha_1 j_2), (j_3, … , j_N)}$$ and perform an SVD:

$$\psi_{j_1, … , j_N} = \sum\limits_{\alpha_1}^{\chi_1}\sum\limits_{\alpha_2}^{\chi_2} A^{j_1}_{\alpha_1} U_{(a_1 j_2), (j_3, … , j_N)} \Sigma_{\alpha_2, \alpha_2} (V^\dagger)_{a_2, (j_3, …, j_N)}= \sum\limits_{\alpha_1}^{\chi_1}\sum\limits_{\alpha_2}^{\chi_2} A^{j_1}_{\alpha_1} A^{j_2}_{\alpha_1, \alpha_2} \psi_{(a_2 j_3),(j_4, … , j_N)}$$

We can continue this process to build the state entirely out of $$A$$ tensors and graphically this looks like:

<p align="center">
 <img src="{{site.url}}/_img/leftcanonicalform.png" alt="left canonical form" width="400" height="auto"/>
</p> 

The above form is referred to as “left canonical form” as the matrices that build our MPS were built from the $$U$$ type matrices in SVD. If we were to cut our MPS in to two parts $$A$$ and $$B$$, with

$$\ket{\alpha_l}_A = A^{j_1}A^{j_2} \cdots A^{j_l} \ket{j_1, j_2, … , j_l} \;\;\&\;\; \ket{\alpha_l}_B = A^{j_{l+1}} \cdots A^{j_N} \ket{j_{l+1},… , j_N} $$

Then the overall state can be expressed in a SD-like form:

$$\ket{\psi} = \sum\limits_{\alpha_l} \ket{\alpha_l}_A \ket{\alpha_l}_B$$

This unfortunately is not equivalent to the SD, as the $$A$$ matrices are left-normalized (due to the fact that $$U^\dagger U = I \neq U U^\dagger$$), which leads to the statement that the left states $$ \lbrace \ket{\alpha_l}_A \rbrace$$ form an orthonormal basis but the right states do not. We would run into similar issues with the “right canonical form”, where the chain of SVD is started from the $$N$$-th site and the MPS matrices $$B^{j_i}$$are built from the right-unitary SVD matrices $$V^\dagger$$. There the right states would form an orthonormal basis, but not the left states. 

There is a simple fix, however, to actually identify our MPS with a SD and to thereby have direct access to engtanglement information, and that is to use a mixed canonical form:

$$\ket{\psi} = \sum\limits_{j_1, … , j_N} A^{j_1} \cdots A^{j_l} \Sigma B^{j_{l+1}} \cdots B^{j_N} \ket{j_1, … , j_N}$$

If we now split this state into two subsystems $$A$$ and $$B$$, with $$A$$ including all sites up to $$l$$ and $$B$$ representing the sites $$l+2$$ onwards, the state now takes the form of a SD:

$$ \ket{\psi} = \sum\limits_{\alpha_l} \sigma_a \ket{\alpha_l}_A \ket{\alpha_l}_B$$

where the Schmidt values $$\sigma_a$$ are the entries of the $$\Sigma$$ matrix. The families of states representing each subsystem are orthonormal in this case by construction. In this sense, we can directly relate MPS to the SD, and hence we can also consider the entanglement-based truncation of MPS. In the mixed canonical form, we can consider throwing away subleading Schmidt values $$\sigma_a$$ and approximating our MPS. The number of singular values kept is referred to as the _bond dimension_, and the overall bond dimension for any tensor network is the maximum bond dimension for any individual site. 

### DMRG and iDMRG

We now briefly want to sketch the density matrix renormalization group (DMRG) algorithm for finding the ground state properties of quantum systems. In view of MPS, the DMRG algorithm can be thought of as variationally minimizing the ground state energy over the space of MPS--in other words, we want to find the MPS $$\ket{\psi}$$ such that

$$\frac{\bra{\psi} \hat{H} \ket{\psi}}{\braket{\psi}}$$

is minimized. In order to do so, we first quickly introduce a compatible tensor network representation of the Hamiltonian, the matrix product operator (MPO) form, which will allow us to work with our MPS more easily. As in the definition of MPS, we can appeal to a general definition an operator $$\hat{O}$$ to motivate a similar representation:

$$\hat{O} = \sum\limits_{j_1,...,j_N, j'_1,...,j'_N} c_{(j_1,...,j_N)(j'_1,...,j'_N)} \ket{j_1, ... , j_N} \bra{j'_1, ... , j'_N}$$

We can decompose the coefficients in a similar way to how we did with the coefficients of a quantum state, but first grouping pairs $$ c_{(j_1,...,j_N)(j'_1,...,j'_N)} \rightarrow  c_{(j_1 j'_1),...,(j_N j'_N)}$$ and having the double index $$j_i j'_i$$ take the role of a single index for an MPS. Ultimately it can be shown that any operator can be expressed in the following MPO representation:

$$\hat{O} = \sum\limits_{\bf j,j'} v^L W^{j_1 j'_1} \cdots W^{j_N j'_N} v^R \ket{\bf j} \bra{\bf j'}$$

The coefficients $$W^{j_i j'_i}$$ in our MPO play the role of the tensors in an MPS and the vectors $$v^L, v^R$$ determine the boundaries of the MPO. Now to find the energy of some MPS $$\ket{\psi}$$ with a hamiltonian $$H$$ in MPO form, we arrive at the  diagram below

<p align="center">
 <img src="{{site.url}}/_img/mpsmpoenergy.png" alt="left canonical form" width="700" height="auto"/>
</p> 

The top and bottom tensors are our state $$\ket{\psi}$$ (with $$\bra{\psi}$$ on the bottom) and the Hamiltonian in MPO form is in the middle, with all external legs fully contracted to give us the energy. Now the goal is to variationally minimize the energy to find the ground state MPS of the Hamiltonian in an efficient way through DMRG. The tensor diagram above is a good lead-in to the general procedure: we want to optimize the energy _locally_ by working with two sites at a time and moving through the whole chain. The most computationally costly aspect of DMRG is this two-site optimization, where the two site wavefunction, encoded in $$\Theta$$, is updated to be the ground state of the effective two-site Hamiltonian. Once the new state $$\tilde{\Theta}$$ is found, we can do an SVD to break it up and get back to a mixed canonical MPS. 

<p align="center">
 <img src="{{site.url}}/_img/dmrgupdate.png" alt="dmrg update process" width="700" height="auto"/>
</p> 

This is the two-site update version of DMRG. There is also a version where only one site is updated at a time, and the two methods have various tradeoffs and individual advantages when applied to various systems (for an overview, see )

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

