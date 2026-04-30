# 🔥 High-Performance Grid-Based Environmental Spread Modeling

### Using Multithreaded CPU Parallelism (OpenMP)

## 📌 Overview

This project implements a **forest fire spread simulation** on a 2D grid using **C++ and OpenMP**. It demonstrates how shared-memory parallelism can significantly improve performance for computationally intensive grid-based problems.

Each cell in the grid evolves based on its neighbors over discrete time steps, making the problem ideal for parallel execution.

---

## 🎯 Objectives

* Implement a **sequential baseline simulation**
* Develop a **parallel version using OpenMP**
* Compare performance across:

  * Grid sizes: `200×200`, `400×400`, `600×600`
  * Thread counts: `1, 2, 4, 8`
* Analyze:

  * Execution time
  * Speedup
  * Parallel efficiency

---

## ⚙️ Tech Stack

* **Language:** C++17
* **Parallelism:** OpenMP
* **Compiler:** g++ (`-fopenmp`)
* **Timing:** `std::chrono`
* **Environment:** Kali Linux

---

## 💻 Execution Environment

* Implemented and executed on **Kali Linux**
* CPU utilization verified using **htop**
* Parallel execution confirmed across multiple cores (up to ~85% CPU usage)

---

## 🔥 Simulation Model

### Cell States

* `0 → EMPTY`
* `1 → TREE`
* `2 → BURNING`

### Update Rules

1. Burning → Empty
2. Tree + Burning neighbor → Burning
3. Tree (no burning neighbor) → Tree
4. Empty → Empty

* Fire starts at **top-center of the grid**
* Simulation runs for **200 steps**

---

## ⚡ Parallelization Strategy

```cpp
#pragma omp parallel for collapse(2) schedule(static)
```

* `collapse(2)` → Improves load balancing across threads
* `static scheduling` → Efficient due to equal work per cell

---

## 📊 Performance Results

| Grid Size | Threads | Speedup |
| --------- | ------- | ------- |
| 200×200   | 8       | ~2.51×  |
| 400×400   | 8       | ~3.33×  |
| 600×600   | 8       | ~3.47×  |

### Key Insights

* Larger grids achieve better parallel efficiency
* Speedup is **sub-linear** due to overhead
* 1-thread parallel ≈ sequential (expected behavior)

---

## ▶️ How to Compile & Run

### Compile

```bash
g++ -O2 -fopenmp fire_simulation_openmp.cpp -o run
```

### Run

```bash
./run
```

---

## 📂 Project Structure

```
.
├── src/
│   └── fire_simulation_openmp.cpp
├── report/
│   ├── Project_Report_ANU.pdf
│   └── Project_Report_ANU.tex
├── presentation/
│   └── Project_Presentation_Anu.pptx
├── results/
│   ├── output.txt
│   └── htop.png
├── README.md
```

---

## 🚀 Future Improvements

* GPU acceleration (CUDA / OpenCL)
* Distributed version using MPI
* Improved memory layout (1D array)
* Probabilistic fire spread model

---

## 👥 Authors

* Anushka Gupta
* Apurv
* Ishwanpreet Kaur
* Vibhav Garg

---

## 📌 Conclusion

This project demonstrates that **OpenMP-based parallelism** is highly effective for grid-based simulations, achieving up to **~3.47× speedup** on CPU systems. It highlights scalability behavior and practical limitations like thread overhead and Amdahl’s Law.
