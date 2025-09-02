---
tags:
  - core
references:
  - "[[Operating System - 1]]"
date_created: 2025-09-02
date_modified: 2025-09-02
---
---
## **Memory Management in OS**

In multiprogramming, there are many processes. and those processes run in RAM. But how are those processes stored on RAM? Might be continuous, or non-continuous. Might leave some space empty in between. But we know that physical addressing of processes will be different.

For example, both process $P_1$ and $P_2$ of 16kb has a **logical address** from $0$ to $12800$ bits. But they will have different **physical addresses**. $P_i$ will have range $[R_i + 0, R_i + 12800]$.

