# Week5 Delete Relaxation Heuristics

## Agenda
- Motication
- The Delete Relaxation
- The Additive and Max Heuristics
- Relaxed Plans
- Conclusion

## Delete Relaxing

<span style="color:red">"**What was once true remains true forever**"</span>

**Delete relaxation**
- Strategy: Ignore the **del** p of actions
- "<span style="color:red">+</span>" super-script = deleted relaxed. e.g. $h^+$, $a^+$
- Delete Relaxation is <span style="color:red">**Admissible**</span>: $h(s) \leq h^*(s)$
- used during search: e.g. combine $h^+$ and Greedy BFS
- In TSP problem, when the cost is not uniform for each edge -> minimum spanning tree problems -> isn't efficiently computable 
  > Minimum Spanning Tree Introduction: https://www.youtube.com/watch?v=KsobpcI3dN0

## Additive and Max Heuristics
<span style="color:red">**把所有的 fluents/atmos 作为横坐标， 纵坐标为迭代次数， 不断基于当前state去发现可以更新的值。直到两次迭代的值没有发生变化时停止.**</span>

- $h^{max}$ is **Optimistic**, while $h^{add}$ is **Pessimistic**
- Both max and additive heuristics are **safe** and **goal-aware**, which means that they return zero for goal states and infinity for dead-end states

### $h^{max}$
- The $h^{max}$assigns to each node the maximum value of its predecessors
- <span style="color:red"> **$h^{max}$ is admissible** </span>
- <span style="color:blue">$h^{max} = max(predecessors) + cost$</span>
    > The max heuristic is admissible and consistent, which means that it never overestimates the true cost and it satisfies the triangle inequality. 
    > However, the max heuristic is often very pessimistic and uninformative, as it ignores the possibility of achieving multiple goals or preconditions with one action

### *$h^{add}$*
- Algorithm: Bellman-Ford variant
- $h^{add}$ assigns to each node the sum of the values of its predecessors
- <span style="color:red"> **$h^{add}$ is not admissible** </span>
- <span style="color:blue">$h^{add} = \sum(predecessors) + cost$</span>
    > The additive heuristic is not admissible or consistent, which means that it may overestimate the true cost and it may violate the triangle inequality
    > However, the additive heuristic is usually much more informative and realistic than the max heuristic, as it accounts for the positive interactions between actions and goals

### **Parcel problem**
<img src="https://i.328888.xyz/2023/04/19/i6s2MC.jpeg" width ="80%"/>



## Best-Supporter Functions

- Strategy: Based on $h^{max}$ and $h^{add}$, to find the cheapest achiever.
- $h^{FF} \geq h^+$, $h^+ \leq h^{FF}$; $h^{FF}$ is **not admissible**
- 直到两次迭代状况一样才停止

