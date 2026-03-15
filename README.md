Quantum DNA Encoding using Qiskit
        
This project demonstrates a quantum representation of DNA sequences using Qiskit.
The algorithm compresses DNA motifs, encodes nucleotide pairs into integers, and stores the sequence in a quantum circuit using index-value superposition.

The circuit is then optimized and evaluated under realistic quantum hardware noise using the FakeSherbrooke backend.

Overview

DNA sequences contain repeating structures called motifs.
This project performs the following steps:

Convert DNA string → nucleotide pairs

Detect repeating motifs

Compress motifs

Encode pairs into numeric symbols

Store the sequence in a quantum superposition

Optimize the circuit

Simulate noise using a real hardware noise model

Measure state fidelity

DNA Example

Input DNA:

ATGCGTACGTTAGCGTACGATCGTAGCTAGCTTGACGATCGTACGTTAGC

Pairs created:

AT GC GT AC GT TA GC GT AC GA TC GT AG CT AG CT TG AC GA TC GT AC GT TA GC
Encoding Scheme

Each DNA pair is encoded as an integer.

Pair	Value	Binary
AA	0	0000
AC	1	0001
AG	2	0010
AT	3	0011
CA	4	0100
CC	5	0101
CG	6	0110
CT	7	0111
GA	8	1000
GC	9	1001
GG	10	1010
GT	11	1011
TA	12	1100
TC	13	1101
TG	14	1110
TT	15	1111

Special symbol:

M1 → 16 (motif compression token)
Quantum Representation

The algorithm stores the sequence in a quantum state:

|index>|value>

Example:

|00000>|00011>  → AT
|00001>|01001>  → GC
|00010>|01011>  → GT

Where

index register stores position in the sequence

value register stores encoded pair

This creates a superposition over all indices.

Circuit Architecture

Total qubits used:

Total Qubits = index_qubits + value_qubits

Where

index_qubits = ceil(log2(sequence length))
value_qubits = 5

Operations used:

Hadamard (H) → index superposition

X gates → index conditioning

CCX (Toffoli) → controlled value encoding

Noise Simulation

To simulate real hardware behavior, we use

Fake backend:

FakeSherbrooke

This provides:

realistic gate errors

decoherence

readout noise

The circuit is simulated using:

AerSimulator(method="density_matrix")
Fidelity Measurement

We compare:

Ideal quantum state
vs
Noisy quantum state

Using:

state_fidelity()

Fidelity close to 1 means the encoded DNA state is preserved well under noise.

Circuit Metrics

The code outputs:

Total qubits

Circuit depth

CNOT count

SWAP count

Circuit diagram

These metrics help evaluate hardware feasibility.

Installation

Install dependencies:

pip install qiskit
pip install qiskit-aer
pip install qiskit-ibm-runtime
pip install numpy
Run the Code

Execute:

python quantum_dna_encoding.py

Expected outputs:

DNA pairs

Motif detection

Compressed sequence

Quantum state representation

Circuit depth (before & after optimization)

Fidelity

Circuit diagram

Example Output
Detected motif: ('GT','AC')

Symbol sequence:
[3,9,11,1,11,12,...]

Index qubits: 5
Value qubits: 5
Total qubits: 10

Circuit depth after optimization: 87

Exact state fidelity: 0.91
Applications

This research connects quantum computing with bioinformatics.

Possible applications:

Quantum DNA compression

Quantum genome indexing

Quantum pattern matching

Quantum biological data storage

Future Improvements

Possible extensions:

Quantum motif search using Grover's algorithm

Quantum sequence alignment

Variational quantum circuits for DNA analysis

Scaling to real genome datasets

https://drive.google.com/file/d/1E2dYtrUhObeQffKWKCLOrjYCj8aGJ12z/view?usp=sharing
