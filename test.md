## 2. Predicate Specification (Req 1.1)
* **Predicates:** $\text{Assign}(i,j)$, $\text{Busy}(i,j)$, $\text{Overlap}(j,k)$, $\text{Consecutive}(j,k)$, $\text{AtCampus}(j,c)$, $\text{Prefer}(i,c)$[cite: 2, 3].
* **Hard Rules:**
  * **No Double-Booking:** An invigilator cannot be assigned to two distinct shifts that overlap in time[cite: 2, 3].
  * **Availability:** An invigilator cannot be assigned to any shift during which they are marked as busy[cite: 2, 3].
  * **Capacity:** Each exam shift must be assigned exactly its required quota of distinct invigilators[cite: 3].
  * **No Consecutive Shifts Between Different Campuses:** An invigilator cannot be assigned to two consecutive shifts that take place at different campuses due to travel time constraints.
