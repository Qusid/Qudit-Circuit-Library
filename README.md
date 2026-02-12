# Qudit Circuit Library

A Python library for building and simulating **qudit** quantum circuits using [Cirq](https://quantumai.google/cirq). Extends standard qubit gates to arbitrary dimension *d* for high-dimensional quantum computing.

## Features

- **Single-qudit gates**: X, Z, H (generalized Hadamard/QFT), Phase, U₈ (π/8-like)
- **Two-qudit gates**: CNOT, CZ
- **Utilities**: measurement, state vectors, probabilistic sampling
- **Example algorithms**: Deutsch–Jozsa (qubit & qudit), parity determination

## Installation

```bash
pip install cirq numpy sympy
```

## Quick Start

```python
import cirq
from qudity import quditXGate, quditHGate, quditCNOTGate

d = 3  # qutrits
q0 = cirq.LineQid(0, dimension=d)
q1 = cirq.LineQid(1, dimension=d)

circuit = cirq.Circuit(
    quditHGate(d=d).on(q0),
    quditHGate(d=d).on(q1),
    quditCNOTGate(d=d).on(q0, q1)
)
print(circuit)
```

## Gates

| Gate | Description | Notes |
|------|-------------|-------|
| `quditXGate(d, exponent)` | Generalized Pauli-X | Shift by `exponent` mod d |
| `quditZGate(d, exponent)` | Generalized Pauli-Z | Phase rotation |
| `quditHGate(d)` | Discrete Fourier transform | QFT for single qudit |
| `quditCNOTGate(d)` | Controlled-X | Target ← (target + control) mod d |
| `quditCZGate(d)` | Controlled-Z | Phase ω^(control·target) |
| `quditPhaseGate(d)` | Phase gate | d ≥ 3 prime |
| `quditU8Gate(d, gamma, z, eps)` | π/8-like gate | d prime, 12 invertible mod d |

## Examples

### Deutsch–Jozsa on qudits

See `Deutch.ipynb` for the Deutsch–Jozsa algorithm implemented both for qubits and qudits (e.g. qutrits).

### Parity determination

See `Parity_check.ipynb` for a parity-based algorithm using qutrits with generalized Hadamard and permutation gates.

## Project structure

```
.
├── qudity.py          # Core gate implementations
├── Deutch.ipynb       # Deutsch–Jozsa (qubit & qudit)
├── Parity_check.ipynb # Parity algorithm with qutrits
└── LICENSE            # MIT
```

## License

MIT © Siddhant Gupta
