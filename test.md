## 1.1. Predicate Specification
This section defines the domains, functions, predicates, and hard constraints for exam invigilator assignment
* **Domains and sets:** $I$: Set of Invigilators, $J$: Set of Shifts, $C$: Set of Campuses
* **Functions:** $Cap(j)$
* **Predicates:** $\text{Assign}(i,j)$, $\text{Busy}(i,j)$, $\text{Overlap}(j,k)$, $\text{Consecutive}(j,k)$, $\text{AtCampus}(j,c)$, $\text{Prefer}(i,c)$].
* **Hard Rules:**
  * **Capacity:** Each exam shift must be assigned exactly its required number of distinct invigilators.
  * **No Double-Booking:** An invigilator can't be assigned to two distinct shifts that occur at the same time.
  * **Availability:** An invigilator can't be assigned to any shift during the time the invigilator is busy.
  * **No Consecutive Shifts Between Different Campuses:** An invigilator can't be assigned to two consecutive shifts that take place at different campuses due to travel time.
