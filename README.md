# Parallel GPU and Computing — Matrix Multiplication Performance Analysis

## Overview

This repository contains my Parallel and Grid Computing (PGC) laboratory work for analyzing matrix multiplication performance using sequential CPU execution and OpenMP shared-memory parallelism.

The main workload is a **4000 × 4000 matrix multiplication**. The implementations use matrices initialized with `1.0`, so the expected verification value is:

```text
C[0][0] = 4000.00
```

The repository is organized into source code, benchmark/plotting scripts, experimental images, and the laboratory report.

---

## Objectives

- Implement dense matrix multiplication using a sequential CPU program.
- Implement matrix multiplication using OpenMP shared-memory parallelism.
- Verify the numerical result of the matrix multiplication.
- Measure execution time for sequential and OpenMP implementations.
- Calculate the observed OpenMP speedup relative to the sequential baseline.
- Store source code, benchmark scripts, results, and documentation in a reproducible repository structure.

---

## Experimental Setup

| Parameter | Sequential | OpenMP |
|---|---|---|
| Matrix size | 4000 × 4000 | 4000 × 4000 |
| CPU execution | 1 thread | 8 threads |
| Memory model | Shared system RAM | Shared system RAM |
| Compiler | GCC `-O2` | GCC `-O2 -fopenmp` |
| Expected result | `C[0][0] = 4000.00` | `C[0][0] = 4000.00` |

The experiment was performed in a WSL2 Ubuntu environment.

---

## Recorded Results

The verified runs in this repository produced the following results:

| Implementation | Threads | Execution Time | Speedup | Verification |
|---|---:|---:|---:|---:|
| Sequential | 1 | **166.734358 s** | **1.00×** | `4000.00` |
| OpenMP | 8 | **40.215130 s** | **4.15×** | `4000.00` |

### Speedup

The observed OpenMP speedup is calculated as:

```text
Speedup = Sequential Time / OpenMP Time
        = 166.734358 / 40.215130
        ≈ 4.15×
```

The 8-thread run therefore completed the recorded workload in substantially less time than the single-threaded baseline. The speedup is below the theoretical 8× limit because real systems are affected by memory bandwidth, cache behavior, scheduling overhead, and other resource contention.

---

## Source Code

The `src/` directory contains the matrix multiplication implementations:

```text
src/
├── matrix_sequential.c
├── matrix_openmp.c
├── matrix_mpi.c
└── matrix_cuda.cu
```

The sequential and OpenMP implementations are the implementations for which verified performance results are documented in this README.

MPI and CUDA source files are included as part of the project source structure. Their performance values are **not reported here unless they are independently executed and verified**.

---

## Benchmark and Plotting Scripts

The `script/` directory contains:

```text
script/
├── generate_plots.py
├── parse_results.py
└── run_benchmarks.sh
```

These files are used for benchmark execution, result processing, and performance visualization.

---

## Experimental Images

The `image/` directory contains the recorded outputs and visualizations:

```text
image/
├── 3_openmp_verification.jpeg
├── 4_htop_resource_monitor.jpeg
├── 5_sequential_verification.jpeg
├── execution_time_comparison.png
├── openmp.png
├── overall_performance_dashboard.png
├── sequential.png
└── speedup_comparison.png
```

These images provide terminal verification, resource-monitor evidence, execution-time comparison, speedup comparison, and the overall performance dashboard.

---

## How to Build and Run

### Sequential

Compile:

```bash
gcc -O2 src/matrix_sequential.c -o matrix_sequential
```

Run:

```bash
./matrix_sequential
```

### OpenMP

Compile:

```bash
gcc -O2 -fopenmp src/matrix_openmp.c -o matrix_openmp
```

Set the number of threads:

```bash
export OMP_NUM_THREADS=8
```

Run:

```bash
./matrix_openmp
```

The expected verification output includes:

```text
C[0][0] = 4000.00
```

---

## Repository Structure

```text
parallel-gpu-and-computing/
│
├── image/
│   ├── experimental screenshots
│   └── performance visualizations
│
├── script/
│   ├── generate_plots.py
│   ├── parse_results.py
│   └── run_benchmarks.sh
│
├── src/
│   ├── matrix_sequential.c
│   ├── matrix_openmp.c
│   ├── matrix_mpi.c
│   └── matrix_cuda.cu
│
└── LAB_REPORT.md
```

---

## Conclusion

The recorded experiment demonstrates the benefit of shared-memory parallelism for the 4000 × 4000 matrix multiplication workload. The sequential implementation took **166.734358 seconds**, while the 8-thread OpenMP implementation took **40.215130 seconds**, giving an observed speedup of approximately **4.15×**.

The project also keeps the source files, benchmark scripts, experimental evidence, and laboratory report together so that the work can be inspected and reproduced.

---

*Parallel and Grid Computing (PGC) Laboratory Experiment — 2026*
