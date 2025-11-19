# 200-Node Multi Pickup-and-Delivery Instances

This repository contains **synthetic 200-node benchmark instances** for the multi pickup-and-delivery problem (MPD).  
They are constructed by systematically enlarging the original 100-node instances provided at:

> https://www.leandro-coelho.com/multi-pickup-and-delivery/

The goal is to offer larger yet structurally consistent test cases for scalability experiments, while remaining compatible with the original data format.

---

## 1. Origin of the data

These instances are derived from the benchmark set introduced by the original authors (see the above link for full details and the original files).  
Each original instance is characterised by three features:

- **Time-window type**:  
  - `N` – narrow local time windows at each pickup and delivery  
  - `L` – wider local time windows (more flexibility, but still per-node)  
  - `W` – no local windows; a single global time horizon is imposed

- **Request length**: number of pickup–delivery nodes per request  
  - `4` nodes per request  
  - `8` nodes per request  

- **Total number of nodes**:  
  - `25`, `35`, `50`, or `100`

For each combination of  
**(time-window type, request length, node count)**  
five distinct instance variants are provided in the original benchmark, giving a total of:

\[
3 \times 2 \times 4 \times 5 = 120 \text{ instances.}
\]

The 200-node instances in this repository are **synthetic extensions** of the original 100-node class.

---

## 2. Construction of the 200-node instances

To obtain larger test instances, we generated **synthetic 200-node datasets** by combining the existing 100-node benchmarks within each class.

- A **class** is defined by:
  - time-window type ∈ {`N`, `L`, `W`}
  - request length ∈ {`4`, `8`}
  - node count = `100`

For each such class:

1. Take the five original 100-node instances, denoted
   \[
   (f_0, f_1, f_2, f_3, f_4).
   \]

2. Form a deterministic **5-cycle of pairs**:
   - \((f_0, f_1)\)
   - \((f_1, f_2)\)
   - \((f_2, f_3)\)
   - \((f_3, f_4)\)
   - \((f_4, f_0)\)

3. For each pair, build a **single 200-node instance** by:
   - taking the union of their request sets, and  
   - **renumbering all nodes** to avoid ID collisions.

This yields **five 200-node instances per class**, and guarantees that:

- each original 100-node instance appears in **exactly two** merged 200-node instances;
- the resulting problems are larger but preserve the **structural characteristics** of their class;
- excessive duplication or artificial correlation between instances is avoided.

---

## 3. File naming convention

All 200-node instances are stored in the folder:

```text
instances_200/
