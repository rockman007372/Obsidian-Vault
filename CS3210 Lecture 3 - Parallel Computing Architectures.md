---
tags:
  - toProcess
course: cs3210
type: lecture
date: 2024-08-26 Monday
---

## Notes

We have parallelism in both single and multiple-core processsors

##### Single core
Bit-level parallelism:
- increasing the word size
- word size may mean:
	- unit of transfer btw processor n mem
	- mem addr space capacity
	- integer size
	- single precision floating point number size

Instruction-level parallelism:
- pipelining (time):
	- split instructions into multiple stages (Fetch, decode, execute, writeback)
	- multiple instruction can happen at the same time at diff stages in the same clock cycle (provided there is no data/control dependencies)
- superscalar (space)
	- allow multiple **independent** instructions to be executed in parallel on execution units (ALU)
	- structurally complicated (bigger data cache for more ins, ...)
	- SIMD (single instruction, multiple data)

Thread-level:
- Multiple execution contexts (diff registers, stack pointers....)
- Can run one scalar ins per clock from one of the hardware threads
- Hyper-threading/simultaneous multithreading (SMT): share same ALU, diff contexts

Processor-Level Parallelism:
- each process/thread has an independent context mapped to multiple processor cores

Instruction stream:
Data stream:

Single Instruction Single Data (SISD)

Single Instruction Multiple Data (SIMD): multiple ALU

Multiple Instruction Single Data (MISD): does not exist

Multiple Ins Multiple Data (MIMD): modern model for multiprocressor

##### MultiCore Architecture

Hierarchical design: 
- multiple cores share multiple caches
- L1, L2, L3 cache

Pipelined design:
- Data elements processed by multiple cores in a pipeline

Network-based design

##### Memory Organization

Distributed memory:
- independent computers connected to other computers

Shared memory:
- parallel threads access mem through shared mem provider
- must deal w cache coherence: must update local cache if global mem change ⇒ overheads
- UMA (Uniform access time): every processor takes the same time to access shared mem
- NUMA (Non-uniform accesss time): accesing local mem is faster than remote mem in another socket?

Hybrid





## Summary

1. Processor architecture
2. Flynn's Parallel Architecture Taxonomy
3. Architecture of multicore processor
4. Memory org: 
	1. distributed-memory
	2. shared memory
	3. hybrid

## Questions/Cues

