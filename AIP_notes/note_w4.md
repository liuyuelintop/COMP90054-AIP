# Week4 Generating Heuristic Functions
## Agenda
Motivation, **How to Relax: Informally, and Formally, and During Search**, Conclusion

**Relaxations**

<span style="color:red">**We're simplifying the problem and trying to solve the simplified problem to get an intuition on how hard is to solve the original problem**</span>

<img src="https://i.328888.xyz/2023/04/05/i8XQMd.jpeg" width = "80%">
<img src="https://i.328888.xyz/2023/04/05/i8X17V.jpeg" width = "80%">


## How to Relax Informally

**How to Relax Informally:**

- You have a problem $P$, whose perfect heuristic $h^*$
- You define a <span style="color:red">simpler problem</span> $P'$, whose perfect heuristic $h^{'*}$ can be used to <span style="color:red">estimate</span> $h^*$
- You define a transformation, r, that <span style="color:red">simplifies</span> instance from $P$ into instances $P'$.
- Given $\Pi \in P$, you estimate $h^*(\Pi)$ by $h^{'*}(r(\Pi))$
> Relaxation means to simplify the problem, and take the solution to the simpler problem as the heuristic estimate for the solution to the actual problem.

### Relaxing in Route-Finding
<span style="color:red"></span>
<span style="color:red">How to derive straight-line distance by relaxation?</span>
- $P$: Route fidnging
- $P'$: Route finding for birds
- Perfect heuristic $h^{'*}$ for $P'$: Straight-line distance
- Transformation r: Pretend you're a bird.
- Properties:
  - <span style="color:red">Native?</span> No: Birds don't do route-finding(it's equivalent to trivial maps with direct routes between everywhere.)
  - <span style="color:red">efficiently constructible?</span> Yes (pretend you're a bird)
  - <span style="color:red">fficiently computable?</span>e Yes, measure straight-line distance.

### Relaxation in the 8-Puzzle
Perfect heuristic $h^∗$ for $P$: Actions = “A tile can move from square A to square B if A is adjacent to B and B is blank.”
- How to derive the Manhattan distance heuristic?  $P^′$: Actions = “A tile can move from square A to square B if A is adjacent to B.”
- How to derive the Manhattan distance heuristic?  $P^′$: Actions = “A tile can move from square A to square B."
- $h^{′∗}$ (resp. r) in both: optimal cost in $P^′$ (resp. use different actions). 
- Here: Manhattan distance = 18, misplaced tiles = 8.
- Properties:
  - <span style="color:red">Native?</span> No: With the modified rules, it's not the "same puzzle" anymore.
  - <span style="color:red">efficiently constructible?</span> Yes(exhange action set) 
  - <span style="color:red">efficiently computable?</span> Yes (count mistitled ties/sum up Manhattan distances)


### Goal-Counting Relaxation in Australia
**<span style="color:red">Goal Counting is not admissible</span>** 可以解释 A1 Pacman 中使用 goal-counting 作为 $BA^{*}$ 的 heuristic 找不到最优解的现象了 ($BA^{*}$ expanded nodes大量减少，但不是最优解，因为 $h$ is not admissible； $h=0$ is admissible 的$A^{*}$, $BrFS$ 找到最优解)


<span style="color:red">Let’s “act as if we could achieve each goal directly:</span>
- Problem P: All STRIPS planning tasks.
- Simpler problem $P^{'}$: **All STRIPS planning tasks with empty preconditions and deletes**.
- Perfect heuristic $h^{′∗ }$for $P^′$: Optimal plan cost (= h∗).
- Transformation r: Drop the preconditions and deletes.
- Heuristic value here? 4.
- Properties:
  - <span style="color:red">Native?</span> Yes: Planning with empty preconditions and deletes is a special case of planning (i.e., a sub-class of $P$)
  - <span style="color:red">efficiently constructible?</span> Yes(drop preconditions and deletes) 
  - <span style="color:red">efficiently computable?</span> **No!** Optimal planning is still **NP**-hard in this case (MINIMUM COVER of goal set by addlists).

> → Optimal STRIPS planning with empty preconditions and deletes is still NP-hard! (Reduction
from MINIMUM COVER, of goal set by add lists.)
>
> → Need to approximate the perfect heuristic $h^{′∗}$ for $P^′$. Hence goal counting: just approximate
$h^{′∗}$ by number-of-false-goals.
## How to Relax Formally

### Properties

<span style="color:red">**Native, Efficiently constructable, Efficiently computable**</span>


**What Shall we do with the relaxation?**
- What if R is not efficiently constructible?
  - Either (a) approximate r, or (b) design r in a way so that it will typically be feasible, or (c) just live with it and hope for the best.
  - Vast majority of known relaxations (in planning) are efficiently constructible.
- What if R is not efficiently computable?
  - Either (a) approximate h′∗, or (b) design h′∗ in a way so that it will typically be feasible, or (c) just live with it and hope for the best.
  - Many known relaxations (in planning) are efficiently computable, some aren’t. The latter use (a); (b) and (c) are not used anywhere right now.

## How to Relax During Search

### **Goal-Counting**

<img src="https://i.328888.xyz/2023/04/06/i8qKgA.jpeg" width="80%"/>

> <span style="color:red">**Relaxed Problem**</span>
> - **Greedy best-first search:**
> - State s: AC; goal G: AD
> - Actions A: <span style="color:blue">add</span>. (<span style="color:red">no predictions</span>)
> - $h^{R}(s) = 1$
> - $\Pi^{'*} = ul(D)$


<img src="https://i.328888.xyz/2023/04/06/iIZ8pk.jpeg" width="80%"/>

> <span style="color:red">**Relaxed Problem**</span>
> - **Greedy best-first search:**
> - State s: BC; goal G: AD
> - Actions A: <span style="color:blue">add</span>. (<span style="color:red">no predictions</span>)
> - $h^{R}(s) = 2$
> - $\Pi^{'*} = drBA, ul(D)$


> <span style="color:red">**Relaxed Problem**</span>
> - **Greedy best-first search:**
> - State s: CC; goal G: AD
> - Actions A: <span style="color:blue">add</span>. (<span style="color:red">no predictions</span>)
> - $h^{R}(s) = 2$
> - $\Pi^{'*} = drBA, ul(D)$

> <span style="color:red">**Relaxed Problem**</span>
> - **Greedy best-first search:**
> - State s: DC; goal G: AD
> - Actions A: <span style="color:blue">add</span>. (<span style="color:red">no predictions</span>)
> - $h^{R}(s) = 2$
> - $\Pi^{'*} = drBA, ul(D)$


> <span style="color:red">**Relaxed Problem**</span>
> - **Greedy best-first search:**
> - State s: CT; goal G: AD
> - Actions A: <span style="color:blue">add</span>. (<span style="color:red">no predictions</span>)
> - $h^{R}(s) = 2$
> - $\Pi^{'*} = drBA, ul(D)$


### **Ignoring Deletes**

<img src="https://i.328888.xyz/2023/04/06/iIV9IV.jpeg" width="40%"/>

> <span style="color:red">**Real Problem**</span>:
> - Initial State I: AC; goal G: AD
> - Actions A: pre, add, <span style="color:red">del</span>
> - drXy, loX, ulX
>
> <span style="color:red">**Relaxed problem**</span>
> - State s: AC; goal G: AD
> - Actions A: <span style="color:blue">pre, add</span>
> - $h^{R}(s) = h^{+}(s) = 5$

> <span style="color:red">**Relaxed problem**</span>
> - State s: DC; goal G: AD
> - Actions A: <span style="color:blue">pre, add</span>
> - $h^{R}(s) = h^{+}(s) = 5$

<img src="https://i.328888.xyz/2023/04/06/iIfVqv.jpeg" width="40%"/>

> <span style="color:red">**Relaxed problem**</span>
> - State s: CT; goal G: AD
> - Actions A: <span style="color:blue">pre, add</span>
> - $h^{R}(s) = h^{+}(s) = 4$

### Questionaire
<img src="https://i.328888.xyz/2023/04/06/iIfjWJ.jpeg" width="80%"/>

## Summary

- Relaxations can be **native**, **efficiently constructible**, and/or **efficiently computable**. None of this is a strict requirement to be useful.

- During search, <span style="color:red">the relaxation is used only inside the computation of the heuristic function on each state</span>; the relaxation does not affect anything else. (This can be a bit confusing especially for native relaxations like ignoring deletes