# Module 1.1: Predicate Specification

## 1. Domains and Sets
* $I$: Set of Invigilators; $I = \lbrace i_1, i_2, i_3, \dots \rbrace$ (Only CBCTs are considered invigilators)
* $J$: Set of Shifts; $J = \lbrace j_1, j_2, j_3, \dots \rbrace$
* $C$: Set of Campuses; $C = \lbrace \text{CS1}, \text{CS2} \rbrace$

## 2. Functions
* $Cap(j)$: Number of invigilators required for shift $j$; $Cap(j) \in \mathbb{Z}^+$

## 3. Predicates
* $\text{Assign}(i, j)$: Invigilator $i$ is assigned to shift $j$.
* $\text{Busy}(i, j)$: Invigilator $i$ is unavailable during shift $j$.
* $\text{Overlap}(j, k)$: Shifts $j$ and $k$ occur at the same time.
* $\text{AtCampus}(j, c)$: Shift $j$ takes place at campus $c$.
* $\text{Prefer}(i, c)$: Invigilator $i$ prefers to be at campus $c$.
---

## 4. Hard Constraints (First-Order Logic)

### 4.1 Shift Capacity
* **Formal Language:**
  $$\forall j \in J, \; \exists i_1, \dots, i_{Cap(j)} \in I : \left( \bigwedge_{1 \le a < b \le Cap(j)} i_a \ne i_b \right) \wedge \left(\forall h \in I,   \text{Assign}(h, j) \longleftrightarrow \bigvee_{m=1}^{Cap(j)} h = i_m \right)$$
* **Natural Language:** For every shift $j \in J$, there exist $Cap(j)$ distinct invigilators $i_1, \dots, i_{Cap(j)} \in I$, and an invigilator $i \in I$ is assigned to shift $j$ if and only if invigilator $i$ is one of these $Cap(j)$ invigilators.
* **Explanation (VN):** Mỗi ca thi phải có đủ và đúng chính xác số lượng giám thị được yêu cầu, không thừa không thiếu.

### 4.2 No Double-Booking
* **Formal Language:**
  $$\forall i \in I, \; \forall j, k \in J : \left( j \ne k \wedge \text{Overlap}(j, k) \wedge \text{Assign}(i, j) \longrightarrow \neg \text{Assign}(i, k) \right)$$
* **Natural Language:** For every invigilator $i \in I$ and every pair of distinct shifts $j, k \in J$, if shifts $j$, $k$ overlap and invigilator $i$ is assigned to shift $j$, then invigilator $i$ cannot be assigned to shift $k$.
* **Explanation (VN):** Một giám thị không thể trực hai ca thi trùng giờ nhau.

### 4.3 Availability
* **Formal Language:**
  $$\forall i \in I, \; \forall j \in J : \left( \text{Busy}(i, j) \longrightarrow \neg \text{Assign}(i, j) \right)$$
* **Natural Language:** For every invigilator $i \in I$ and every shift $j \in J$, if invigilator $i$ is busy during shift $j$, then invigilator $i$ cannot be assigned to shift $j$.
* **Explanation (VN):** Giám thị có việc bận thì không được phân công trực ca thi đó.
