# Qiskit simulation container

Apptainer image with Qiskit 2.5 and its addons, for simulation only.
Qiskit Aer 0.17.2 is built from source with CUDA 12.6, so it runs on NVIDIA GPUs.

## Files

| File | Content |
|---|---|
| `qiskit.def` | Apptainer definition file |
| `build.sh` | Build command (Slurm batch script) |
| `qiskit.sif` | Built image |
| `tutorials/` | Jupyter notebooks for each package |

## Build

```bash
apptainer build --fakeroot qiskit.sif qiskit.def
```

Or submit `build.sh` with `sbatch build.sh`.

- The build needs internet access and about 30 minutes (most of it compiles Aer).
- No GPU is needed for the build.
- The image is about 8 GB.
- At the end, `%test` checks that Aer has GPU support and that a noisy simulation works.

## Run

```bash
# CPU
apptainer exec qiskit.sif python script.py

# GPU (--nv makes the host NVIDIA driver available)
apptainer exec --nv qiskit.sif python script.py
```

Check the GPU build:

```bash
apptainer exec --nv qiskit.sif python -c "from qiskit_aer import AerSimulator; print(AerSimulator().available_devices())"
```

The output `('CPU', 'GPU')` means that Aer has GPU support.
To check that a GPU is present, run a circuit with `AerSimulator(device="GPU")`.

## Main packages

| Package | Version |
|---|---|
| qiskit | 2.5.2 |
| qiskit-aer (GPU build) | 0.17.2 |
| qiskit-fermions + ffsim | 0.2.0 + 0.0.80 |
| qiskit-addon-aqc-tensor, -mpf, -opt-mapper | 0.3.1, 0.3.0, 0.1.0 |
| qiskit-addon-utils, -sqd, -cutting, -obp | 0.4.0, 0.14.0, 0.10.0, 0.3.0 |
| qiskit-algorithms, qiskit-machine-learning | 0.4.0, 0.9.1 |
| mthree, qiskit-experiments | 3.0.0, 0.14.2 |
| torch | 2.14.1 (CUDA 12.6) |

Python 3.10, Ubuntu 22.04, base image `nvidia/cuda:12.6.3-devel-ubuntu22.04`.

## Build notes

- `qiskit-aer-gpu` 0.15.1 from PyPI does not work with Qiskit 2.x, so Aer is built from source,
  following the [Aer build instructions](https://github.com/Qiskit/qiskit-aer/blob/main/CONTRIBUTING.md).
- GPU targets: V100 (sm_70), A100 (sm_80), L40S (sm_89), H100 (sm_90).
- Aer needs nlohmann-json 3.1.1. Newer versions break noise models.
- The GPU build is installed under the name `qiskit-aer`, so `pip` does not replace it with the CPU wheel.
- `qiskit-ibm-runtime` is installed only as a dependency. Its fake backends are used as offline noise models.
