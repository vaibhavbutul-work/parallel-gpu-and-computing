# LABORATORY EXPERIMENT REPORT

**Course Title:** Parallel and Grid Computing (PGC)  
**Experiment Title:** Performance Analysis of Matrix Multiplication using Sequential and OpenMP Paradigms  
**Author / Repository Owner:** `vaibhavbutul-work`  
**Repository:** `parallel-gpu-and-computing`  
**Date:** September 2026  

---

## 1. Abstract

This laboratory experiment evaluates the performance of dense `4000 × 4000` matrix multiplication using sequential CPU execution and OpenMP shared-memory parallel execution. The sequential implementation was executed using one CPU thread, while the OpenMP implementation used 8 threads. Both implementations produced the verified mathematical result `C[0][0] = 4000.00`.

In the recorded runs, the sequential implementation required **166.734358 seconds**, while the OpenMP implementation required **40.215130 seconds** using 8 threads. Based on these measurements, OpenMP reduced the execution time substantially compared with the sequential implementation. The measured speedup is approximately **4.15×**.

The repository also contains MPI and CUDA source files under `src/`, but verified execution-time measurements for those implementations were not included in the supplied experiment results. Therefore, no MPI or CUDA performance numbers are claimed in this report.

---

## 2. Experimental Objectives

1. Implement dense `4000 × 4000` matrix multiplication using a sequential C program and an OpenMP parallel C program.
2. Verify numerical correctness by confirming `C[0][0] = 4000.00`, with all initialized matrix elements equal to `1.0`.
3. Measure execution time for the sequential and OpenMP implementations.
4. Calculate the OpenMP speedup relative to the sequential baseline.
5. Compare the behavior of single-threaded execution with shared-memory multi-threaded execution.
6. Organize the source code, scripts, images, and report in a GitHub repository.

---

## 3. System Architecture & Resource Allocation

| Paradigm | Environment | Compute Units | Memory Architecture | Compiler / Toolchain |
| :--- | :--- | :--- | :--- | :--- |
| **Sequential** | WSL2 Ubuntu | 1 CPU Thread | Shared System RAM | GCC `-O2` |
| **OpenMP** | WSL2 Ubuntu | 8 CPU Threads | Shared System RAM | GCC `-O2 -fopenmp` |
| **MPI** | Source included in repository | Not benchmarked in the recorded run | Distributed Memory | Open MPI |
| **CUDA** | Source included in repository | Not benchmarked in the recorded run | GPU VRAM | NVIDIA `nvcc` |

The sequential implementation allocates three `4000 × 4000` double-precision matrices and performs the conventional three-nested-loop matrix multiplication. The OpenMP implementation applies `#pragma omp parallel for` to distribute the outer loop across threads.

---

## 4. Empirical Data & Benchmarking Results

### 4.1 Performance Summary

| Computing Model | Resources | Execution Time (s) | Speedup vs Sequential | Verification `C[0][0]` |
| :--- | :--- | :---: | :---: | :---: |
| **Sequential Baseline** | 1 CPU Thread | **166.734358** | **1.00×** | **4000.00** |
| **OpenMP Shared Memory** | 8 CPU Threads | **40.215130** | **4.15×** | **4000.00** |
| **MPI Distributed** | Not benchmarked | — | — | — |
| **CUDA GPU** | Not benchmarked | — | — | — |

### 4.2 Speedup Calculation

The speedup is calculated as:

`Speedup = Sequential Time / Parallel Time`

For the recorded OpenMP run:

`Speedup = 166.734358 / 40.215130`

`Speedup ≈ 4.15×`

Therefore, the recorded 8-thread OpenMP implementation completed the matrix multiplication in approximately one-quarter of the sequential execution time.

---

## 5. Performance Visualizations

The experiment files are organized in the following repository structure:

1. `image/sequential.png` — sequential matrix multiplication terminal output.
2. `image/openmp.png` — OpenMP matrix multiplication terminal output.
3. `image/3_openmp_verification.jpeg` — OpenMP verification screenshot.
4. `image/4_htop_resource_monitor.jpeg` — resource-monitor screenshot.
5. `image/5_sequential_verification.jpeg` — sequential verification screenshot.
6. `image/execution_time_comparison.png` — execution-time comparison chart.
7. `image/speedup_comparison.png` — speedup comparison chart.
8. `image/overall_performance_dashboard.png` — performance dashboard.

The `script/` directory contains the benchmark automation, result parser, and plot-generation scripts.

---

## 6. Discussion & Technical Findings

### 6.1 Sequential Execution

The sequential implementation performs matrix multiplication using three nested loops. With a matrix size of `4000 × 4000`, the computation involves a large number of arithmetic operations and memory accesses. The recorded execution time was **166.734358 seconds**.

### 6.2 OpenMP Shared-Memory Execution

The OpenMP implementation parallelizes the outer matrix-multiplication loop. The recorded run used **8 threads** and completed in **40.215130 seconds**.

Compared with the sequential result, this corresponds to approximately **4.15× speedup**.

### 6.3 Parallelization Overhead and Scaling

The speedup is lower than the theoretical maximum of 8× for 8 threads. This is expected in a real shared-memory system because practical performance is affected by factors such as memory bandwidth, cache behavior, thread-management overhead, and CPU resource contention.

The result therefore demonstrates that increasing the number of threads does not automatically produce perfectly linear speedup.

### 6.4 MPI and CUDA Implementations

MPI and CUDA source files are included in the repository under `src/`. However, verified execution-time results for these implementations were not part of the supplied sequential/OpenMP experiment evidence. They are therefore not assigned performance values in this report.

---

## 7. Repository Organization

The experiment repository is organized as follows:

```text
parallel-gpu-and-computing/
│
├── image/
│   ├── openmp.png
│   ├── sequential.png
│   ├── speedup_comparison.png
│   ├── execution_time_comparison.png
│   ├── overall_performance_dashboard.png
│   └── verification/resource screenshots
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

## 8. Conclusion

The experiment demonstrates the performance benefit of shared-memory parallelism for large matrix multiplication. For the recorded `4000 × 4000` workload, the sequential implementation required **166.734358 seconds**, whereas the 8-thread OpenMP implementation required **40.215130 seconds**. This produced an observed speedup of approximately **4.15×**.

The experiment also demonstrates that practical parallel performance depends on system resources, memory behavior, and parallelization overhead, so speedup is not necessarily equal to the number of available threads.

MPI and CUDA implementations are included as part of the project source, but their benchmark results should be added only after running and verifying those implementations.
