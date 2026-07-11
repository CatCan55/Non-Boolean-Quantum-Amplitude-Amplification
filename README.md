# Non-Boolean-Quantum-Amplitude-Amplification

This is a toy example of an adaptation by Prasanth Shyamsundar of Grover's algorithm. Instead of amplifying correct solutions to a search by flipping the sign on correct solutions e^{i x pi x 1} and preserving the sign on wrong solutions e^{i x pi x 0}, we allow e^{i x pi x x} for any x between 0 and 1, where when x is closer to 1 solutions are amplified more and when x is closer to 0 solutions are amplified less.

This is done by introducting an additional ancilla qubit. Then 2|psi_0><psi_0| - I is carried out on the tensor product, in between a tensor product of Hadamard with a unitary operator. The marker oracle is applied to odd iterations, and its adjugate is applied to even iterations.
