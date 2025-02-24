---
tags:
  - toProcess
course: CS3210
type: lecture
date: 2024-10-13 Sunday
---
# GPU

Overview: A GPU is built around the concept of **massive parallelism**, with thousands of **simple CUDA cores** spread across many **Streaming Multiprocessors (SMs)**. It leverages a **hierarchy of memory types** (registers, shared memory, caches, global memory) to balance speed and capacity. By organizing threads into blocks and grids and executing them in parallel, GPUs can achieve high throughput for computationally intensive tasks, making them ideal for workloads such as graphics rendering, scientific simulations, and machine learning.

Architecture:
- Multiple **Streaming Multiprocessors** (SM)
	- specialized processing unit
	- analogous to a CPU core but with more simplified control logic and designed to execute many threads simultaneously.
	- Contains a large number of **CUDA cores** 
		- actual compute units that execute individual threads
		- all cores execute the same instruction but on different data.
	- Contain a **Warp Scheduler**:  assigns a warp (groups of 32 threads) to the CUDA cores.
- Memory:
	- Hierarchical
	- Global
	- Shared
	- Registers
	- L1/L2 caches
	- Constant and texture mem

# CUGPU

CUGPU (CUDA GPU) =  **CUDA** (Compute Unified Device Architecture) technology + **GPUs** (Graphics Processing Units => enables general-purpose computing on GPUs, allowing the GPU to handle more than just graphics-related tasks.

Threads in a GPU are organized **hierarchically** to maximize parallelism. This organization allows **thousands of threads to execute concurrently**, enabling GPUs to handle highly parallel tasks.
### 1. Thread Organization Levels
The execution model in GPUs (especially CUDA-enabled ones) organizes threads into a multi-level hierarchy:
#### a. Thread:
- **Basic Execution Unit**: A thread is the smallest unit of execution, and each thread executes a kernel function (a function that runs on the GPU).
- **Parallelism**: Each thread has its own set of registers and can perform independent tasks, but threads usually work together on a shared task.

#### b. Warp:
- **Group of Threads**: Threads are grouped into units called warps, which typically consist of **32 threads** in NVIDIA's CUDA architecture.
- **SIMT Execution**: GPUs use a **Single Instruction, Multiple Threads** (SIMT) execution model, meaning all threads in a warp execute the same instruction at the same time, but on different data.
- **Efficiency Considerations**: If threads within a warp follow divergent execution paths (e.g., if statements with different conditions), this can reduce efficiency, as some threads will be idle while others are executing.

#### c. Thread Block (or CUDA Block):
- **Collection of Warps**: A thread block is a group of warps (and hence, threads) that are executed together. In CUDA, each block can contain up to **1024 threads**.
- **Shared Memory**: Threads in the same block can communicate and share data through **shared memory**, which is faster than global memory but limited in size.
- **Block Synchronization**: Threads within the same block can synchronize with each other using barriers (e.g., `__syncthreads()`), which allows them to coordinate computations.
	- Threads in different blocks cannot cooperate (til CC9.0)
- **Block Dimension**: Thread blocks can be organized in 1D, 2D, or 3D grids, depending on the problem being solved (e.g., a 3D block for image processing or 1D for simple list computations).
- Hardware can schedule blocks to any SM => a kernel scales across any number of parallel mutiprocessors

#### d. Grid:
- **Collection of Thread Blocks**: A grid is a collection of thread blocks that are executed independently. The number of blocks and threads within each block is determined at kernel launch.
- **Global Memory**: All blocks in a grid can access the **global memory** (slower than shared memory) and work on different parts of a dataset.
- **No Synchronization Between Blocks**: Blocks in different grids or even within the same grid cannot directly synchronize or communicate with each other, but they can write to global memory to pass data between them if needed.

### 2. Execution Model
The GPU execution model focuses on organizing and scheduling threads in a way that maximizes parallel efficiency. Here’s how it works:

- **SIMT (Single Instruction, Multiple Threads)**: Each warp of 32 threads executes the same instruction on different pieces of data, taking advantage of data parallelism. However, when some threads within a warp diverge (e.g., due to conditionals), they may execute serially, leading to reduced efficiency (known as **warp divergence**).
- **Occupancy**: The GPU tries to maximize the number of threads in flight by launching multiple warps simultaneously. This depends on the available registers, shared memory, and the number of blocks/threads. Higher occupancy often leads to better performance because more threads can be executed concurrently while others are waiting for memory or instructions.

### 3. Memory Hierarchy and Thread Access
The way threads access memory is crucial to performance. GPU memory is organized into several levels:

![[Pasted image 20241013145001.png]]
#### a. Register Memory:
- Each thread has access to its own registers. Registers are the fastest type of memory but are limited in number. If a thread uses too many registers, it can reduce the total number of threads that can run concurrently (affecting occupancy).

#### b. Shared Memory:
- Shared memory is accessible by all threads **within a thread block** and is faster than global memory. It allows threads within the same block to exchange data efficiently. It's typically used for inter-thread communication and temporary storage.

#### c. Global Memory:
- This is the largest but slowest memory available on the GPU. All threads can access global memory, but accessing it involves higher latency (400-800 cycles). Therefore, threads should minimize global memory access or use techniques like **memory coalescing** (ensuring threads access contiguous memory locations to optimize access).

#### d. Constant and Texture Memory:
- These are special types of memory optimized for certain types of read-only access patterns. Constant memory is cached and well-suited for broadcasting the same data to many threads. Texture memory is used for spatially localized memory access patterns, such as in image processing.

### 4. Thread Scheduling
The GPU schedules threads dynamically to ensure that computation resources (like CUDA cores) are maximally utilized:

- **Warp Scheduling**: The GPU schedules warps rather than individual threads. Multiple warps can be active on a single **Streaming Multiprocessor** (SM), and when one warp is waiting (for memory or computation), another can be executed.
- **Latency Hiding**: GPUs hide memory access latency by switching between warps, allowing the GPU to stay productive even when some warps are waiting for data from global memory.

### 5. Streaming Multiprocessors (SMs)
At the hardware level, GPUs are composed of **Streaming Multiprocessors (SMs)**. Each SM can execute multiple warps concurrently, and they include:
- **CUDA Cores**: Responsible for executing individual threads.
- **Warp Schedulers**: Manage the execution of warps on the SM.
- **Memory Units**: Each SM has access to shared memory and registers.

### 6. Practical Example
Let’s take an example where a kernel is launched with 256 threads per block, and the grid has 1000 blocks:
- A total of **256,000 threads** are created.
- These threads are divided into **1000 blocks**, with each block containing **256 threads**.
- These blocks are then distributed across the available **SMs**, and each SM schedules multiple warps (32 threads per warp) for execution.
  
### Summary of Thread Hierarchy:
1. **Grid**: A collection of thread blocks.
2. **Thread Block**: A collection of threads, with shared memory and synchronization abilities.
3. **Warp**: A group of 32 threads that execute together in a SIMT fashion.
4. **Thread**: The basic execution unit that performs computations.

This hierarchical structure allows GPUs to scale to handle massive parallel workloads effectively.

## Questions

1. Type of warp parallelism

- **Warp Parallelism within an SM**: Warps interleave execution => **warp scheduling** 
    
- **Warp Parallelism across SMs**: Since the GPU has multiple SMs, warps can indeed be running **truly in parallel** on different SMs. For example, if a GPU has 80 SMs, 80 warps could be running at the same time, with each SM executing one or more warps simultaneously. 


