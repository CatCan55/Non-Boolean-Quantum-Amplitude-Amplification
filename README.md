# Non-Boolean-Quantum-Amplitude-Amplification

This is a toy example of an adaptation by Prasanth Shyamsundar of Grover's algorithm in https://arxiv.org/pdf/2102.04975. Instead of amplifying correct solutions to a search by flipping the sign on correct solutions $e^{i\pi \cdot 1} = -1$ and preserving the sign on wrong solutions $e^{i\pi \cdot 0} = 1$, we allow $e^{i\pi x}$ for any x between 0 and 1, where when $x$ is closer to 1 solutions are amplified more (so $\cos(\pi x)$ is closer to -1) and when x is closer to 0 solutions are amplified less (so $\cos(\pi x)$ is closer to 1).

This is done by introducing an additional ancilla qubit. Then $2|\psi_0\rangle \langle\psi_0| - I$ is carried out on the tensor product, in between a tensor product of Hadamard with a unitary operator. The marker oracle is applied to odd iterations, and its adjoint is applied to even iterations.

## Step 1

In this step, we prep the circuit. We take the number of qubits to be 2, and we have the one ancilla qubit. We take the Hadamard gate on all the states, so that $A_0$ from the paper is $H$ tensor H here. Therefore, from Grover's algorithm, the diffuser part of the code involving $2|\psi_0\rangle \langle\psi_0| - I$ can be written using multi-controlled gates in Step 4. 

## Step 2

In this step, we define the two control gates to be used in the marker oracle. 

## Step 3

In this step, we define the marker oracle. We alternate applying U_phi and U_phi_adj, to remain within the span of three basis vectors, for the algorithm to work. For odd iterations we apply U_phi. For even iterations we apply U_phi_adj. We set up these two gates, calling them odd_gate and even_gate. The marking is done with the help of the ancilla qubit. See Section 3.2 of the paper.

## Step 4

This sets up the diffuser gate, using the multi-controlled phase operation. 

By comparison, in Grover's algorithm, the diffuser has the effect of staying within the span of two basis vectors, one spanning the correct-state subspace and one spanning the incorrect-state subspace. Then the effect of changing the phase of the correct-state vectors by -1 reflects the correct-states vector across the span of incorrect-states vector, and preserves the incorrect-states vector by marking that one by 1.

In Grover's algorithm, this is equivalently done either (1) with $2|\psi_0\rangle \langle\psi_0| - I$ or (2) with the multi-control Z gates, and NOT, CNOT gates. The former is the approach that works for general $A_0$ in the non-Boolean generalization, but both work when A_0 = H. In this code, we take the latter approach as $A_0$ is taken to be H. The non-Boolean adaptation therefore involves a .mcp multi-control phase command instead of the MCZ gate from Grover's algorithm.

## Step 5

In this step, we run the circuit for K = 3 iterations. The value of K is hard-coded into the program. One can take K to be given by Equation (74) in the paper, which would be K=1 in this case. Due to the periodic nature of the outcomes from iterations, K=3 also produces an answer close to the outcome we are looking for.

## Step 6

In this step, we measure the outcome, finding that states with the most negative cos(φ(x)) (x = 1, 2) are amplified and have high probability p, while states with cos(φ(x)) near 1 (x = 0, 3) are suppressed and have low probability p.

## How to run

This program can be opened in Colab and all cells run. num_qubits is the number of qubits. The number of iterations K should be computed from Eq (74) in the paper and hard-coded. The choice of $g(x)$ selected was $\sin^2(x)$, but another function from $\{0,...,N-1\} \to [0,1]$ may be chosen. 

$A_0 = H$ was chosen in the code. If one wants to make another choice according to knowing what states should be preferred, and would like to prep the state space in that direction, then the diffuser needs to be coded in the more general form of Equation (19) in the paper.

## Reference:

Shyamsundar, P. (2021). *Non-Boolean Quantum Amplitude Amplification and Quantum Mean Estimation*. arXiv:2102.04975.

## Acknowledgements

I thank the Erdős Institute's Quantum Computing Bootcamp, under which this program was created.  

