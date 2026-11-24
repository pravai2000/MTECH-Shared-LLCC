# Optimal Configuration for Shared Last-Level Cache in a Multi-Processor System

M.Tech project report, Department of Electrical Engineering, Indian Institute of Technology Madras (June 2020).

**Author:** Pravin Vaidya
**Guide:** Prof. Janakiraman Viraraghavan

**Report:** [MTech_Project_Report.pdf](MTech_Project_Report.pdf) (36 pages)

## Summary

In NoC-based MPSoCs with directory-based cache coherency, the number of memory-carrying nodes is limited by pin count. Last-level-cache (LLC) traffic to memory (reads, writes, evictions) therefore creates a bottleneck and hotspots at the memory nodes.

This project proposes a **distributed shared LLC**. The total LLC is split into equal segments, each serving a matching equal segment of DDR. Every processor node is linked to all of the cache segments. The aim is better cache sizing and shorter round-trip times.

## What was done

- **Simulation setup in gem5 (full-system mode).** A Python script wires together the CPU, L1, L2, DDR and NoC. ARM TLM models are used for the CPU, L1 and DDR. Two L2 TLM models were written: a reference L2 and one implementing the proposed architecture.
- **Benchmarks.** PARSEC multithreaded benchmarks (Swaptions, Ferret, BlackScholes) were cross-compiled and run on a Linux boot image with 2, 3 and 4 threads.
- **Comparison.** Both configurations were run for roughly the same simulated time. They were compared on **L2 average miss latency**, parsed from the gem5 `stats.txt` output.
- **RTL implementation.** The cache was coded in Verilog and verified in simulation. It has conventional and phased set-associative variants and a state-transition design. It was also synthesized.

## Report contents

1. Introduction (scope and organization)
2. Description of the setup (simulator and benchmarks)
3. Cache module (design, synthesis, block diagrams, functional verification)
4. Benchmark results
5. Summary and conclusions

## Results

The proposed configuration showed lower L2 average miss latency than the reference in most of the PARSEC runs. The gain varies with the program and shrinks as the thread count grows. See Chapter 4 of the report for the full table.

## Tools

gem5, TLM models, PARSEC benchmarks, Verilog, and a synthesis flow.

## Note

This repository contains the report only. The simulation scripts and RTL are not included.
