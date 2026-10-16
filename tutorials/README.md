# Qiskit tutorials

Jupyter notebooks for the packages in the `qiskit.sif` container (see [`../README.md`](../README.md)).
Each notebook covers one package. All notebooks run on simulators only; no IBM Quantum account is needed.
The saved outputs come from one NVIDIA H100 GPU node on Bridges-2.

## Notebooks

| # | Notebook | Package | Topics | Documentation |
|---|---|---|---|---|
| 01 | [Quantum computing basics](01_qiskit_quantum_computing_basics.ipynb) | qiskit | Qubits, gates, measurement, entanglement, primitives, transpilation, teleportation, Grover, QFT | [docs](https://quantum.cloud.ibm.com/docs/en/guides) |
| 02 | [Aer simulation](02_qiskit_aer_simulation.ipynb) | qiskit-aer | Simulation methods, CPU and GPU, noise models, Aer primitives, performance options | [docs](https://qiskit.github.io/qiskit-aer/) |
| 03 | [Fermions](03_qiskit_fermions.ipynb) | qiskit-fermions, ffsim | Fermionic operators, Jordan–Wigner mapping, Hubbard and H₂ models, UCC/UCJ ansätze | [repo](https://github.com/Qiskit/qiskit-fermions), [ffsim](https://qiskit-community.github.io/ffsim/) |
| 04 | [Optimization mapper](04_qiskit_addon_opt_mapper.ipynb) | qiskit-addon-opt-mapper | Optimization models, QUBO/HUBO, Ising Hamiltonians, QAOA for MaxCut | [docs](https://qiskit.github.io/qiskit-addon-opt-mapper/) |
| 05 | [AQC-Tensor](05_qiskit_addon_aqc_tensor.ipynb) | qiskit-addon-aqc-tensor | Matrix product states, compression of Trotter circuits | [docs](https://qiskit.github.io/qiskit-addon-aqc-tensor/) |
| 06 | [Multi-product formulas](06_qiskit_addon_mpf.ipynb) | qiskit-addon-mpf | Trotter error, static and dynamic MPFs | [docs](https://qiskit.github.io/qiskit-addon-mpf/) |
| 07 | [Algorithms](07_qiskit_algorithms.ipynb) | qiskit-algorithms | VQE, VQD, QAOA, optimizers, gradients, amplitude and phase estimation, time evolution | [docs](https://qiskit-community.github.io/qiskit-algorithms/) |
| 08 | [Machine learning](08_qiskit_machine_learning.ipynb) | qiskit-machine-learning | Quantum kernels, QNNs, VQC, VQR, PyTorch models | [docs](https://qiskit-community.github.io/qiskit-machine-learning/) |
| 09 | [Addon utilities](09_qiskit_addon_utils.ipynb) | qiskit-addon-utils | Hamiltonian generators, Trotter circuits, circuit slicing, TREX, PEC | [docs](https://qiskit.github.io/qiskit-addon-utils/) |
| 10 | [Sample-based quantum diagonalization](10_qiskit_addon_sqd.ipynb) | qiskit-addon-sqd | SQD for N₂ with an LUCJ ansatz, configuration recovery | [docs](https://qiskit.github.io/qiskit-addon-sqd/) |
| 11 | [Circuit cutting](11_qiskit_addon_cutting.ipynb) | qiskit-addon-cutting | Gate and wire cutting, sampling overhead, automatic cut finding | [docs](https://qiskit.github.io/qiskit-addon-cutting/) |
| 12 | [Operator backpropagation](12_qiskit_addon_obp.ipynb) | qiskit-addon-obp | Backpropagation, truncation error budgets, depth reduction | [docs](https://qiskit.github.io/qiskit-addon-obp/) |
| 13 | [Readout mitigation (M3)](13_mthree.ipynb) | mthree | Readout calibration, mitigated distributions and expectation values | [docs](https://qiskit.github.io/qiskit-addon-mthree/) |
| 14 | [Qiskit Experiments](14_qiskit_experiments.ipynb) | qiskit-experiments | T1, T2, randomized benchmarking, tomography, readout characterization | [docs](https://qiskit-community.github.io/qiskit-experiments/) |

Start with 01 if you are new to quantum computing, then 02.
Each notebook lists its sources in the first cell and in a "References" section at the end.

## Run

Run one notebook on a GPU node:

```bash
cd tutorials
apptainer exec --nv ../qiskit.sif jupyter nbconvert --to notebook --execute --inplace 02_qiskit_aer_simulation.ipynb
```

- Without `--nv`, or on a CPU node, the notebooks still run; Aer then uses the CPU.
- Most notebooks run in under one minute. 03, 06 and 10 take 1–2 minutes.
- On shared nodes, set `OMP_NUM_THREADS` to the number of cores in your allocation.
