# Module 1: Logic Specification & Feasibility Checking

## 1. Overview
Translates invigilator assignment rules into First-Order Logic (FOL), encodes them into CNF to check feasibility (SAT/UNSAT Core) using Z3/python-sat, and builds the Logic-to-LP bridge table for Module 2[cite: 1].

## 2. Predicate Specification (Req 1.1)
* **Predicates:** $Assign(i,j)$, $Busy(i,j)$, $Overlap(j,k)$, $Consecutive(j,k)$, $AtCampus(j,c)$, $Prefer(i,c)$[cite: 1].
* **Hard Rules:**
  * **No Double-Booking:** $\forall i, j \neq k: (Overlap(j,k) \land Assign(i,j) \rightarrow \neg Assign(i,k))$[cite: 1]
  * **Availability:** $\forall i, j: (Busy(i,j) \rightarrow \neg Assign(i,j))$[cite: 1]
  * **Capacity:** $\forall j: \exists^{=k} i \, (Assign(i,j))$[cite: 1]
  * **No Consecutive Shifts Between Different Campuses:** $\forall i, j, k, c_1 \neq c_2: (Consecutive(j,k) \land AtCampus(j,c_1) \land AtCampus(k,c_2) \land Assign(i,j) \rightarrow \neg Assign(i,k))$

## 3. CNF & SAT Checking (Req 1.2)
* **Encoding:** Converts FOL formulas and cardinality constraints into CNF over binary variables $x_{ij}$[cite: 1].
* **Results:** Runs SAT solver on Toy Instance & Data Slice; outputs a Satisfying Model (FEASIBLE) or Minimal UNSAT Core (INFEASIBLE)[cite: 1].

## 4. Logic-to-LP Bridge Table (Req 1.3)
| Logic Rule | CNF Clause | LP Inequality |
| :--- | :--- | :--- |
| **Availability:** $Busy \rightarrow \neg Assign$[cite: 1] | $(\neg x_{ij})$[cite: 1] | $x_{ij} = 0$[cite: 1] |
| **No Overlap:** $Assign_j \Rightarrow \neg Assign_k$[cite: 1] | $(\neg x_{ij} \lor \neg x_{ik})$[cite: 1] | $x_{ij} + x_{ik} \le 1$[cite: 1] |
| **No Campus Jump:** $Consecutive \land c_1 \neq c_2 \Rightarrow \neg (Assign_j \land Assign_k)$ | $(\neg x_{ij} \lor \neg x_{ik})$ | $x_{ij} + x_{ik} \le 1$ |
| **Capacity:** Exactly $k$ invigilators[cite: 1] | Pseudo-Boolean[cite: 1] | $\sum_i x_{ij} = k$[cite: 1] |
