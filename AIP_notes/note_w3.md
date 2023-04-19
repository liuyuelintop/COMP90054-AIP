# Week3 How to describe arbitrary search problems

## Background
<span style="color:red"></span>
Motivation:
<span style="color:red"> How to develop systems or "agents" that can make decisions on their own? </span>

3 Approaches to solve tbe conrtrol problem:
- Programming based (hard code)
  - pros: domain-knowledge easy to express
  - cons: cannot deal with situations not anticipated by programmer 
- Learning-based (ML, DL)
  - pros: does not require much knowledge in principle
  - cons: in practice, hard to know which features to learn, and is slow
- **<span style="color:red">Model-based</span>**: Specify problem by hand, derive control automatically.
  - <span style="color:blue">pros: Powerful, Quick, Flexible & Clear, Intelligent & domain-independent</span> 
  - <span style="color:red">cons: need a model; computationally intractable</span>
    - Efficiency loss: Without any domain-specific knowledge about Chess, you don't beat Kasparvo..

**How to define a control problem in a Model?**
> actions, initial situation, goals, and sensors
## Models
### Basic State Model: <span style="color:red">**Classical Planning Model**</span> 
- finite and discrete state space $S$
- a <span style="color:blue">known initial state </span> $s_0 \in S$
- a set $S_G \subseteq S$ of goal states
- actions $A(s) \subseteq A$ applicable in each $s \in S$
- a <span style="color:blue">deterministic transition function</span>  $s' = f(s,a)$ for $a \in A(s)$
- positive action costs <span style="color:blue">$c(a,s)$</span>
- A **solution** is a sequence of applicable actions that maps $s_0$ into $S_G$, and it is **optimal** if it minimizes **sum of action costs**. 

### Uncertainty but No Feedback: Conformant Planning
- finite and discrete state space $S$
- a <span style="color:blue">set of possible initial state </span> $S_0 \in S$
- a set $S_G \subseteq S$ of goal states
- actions $A(s) \subseteq A$ applicable in each $s \in S$
- a <span style="color:blue">non-deterministic transition function</span>  $F(a,s) \subseteq S$ for $a \in A(s)$
- positive action costs <span style="color:blue">$c(a,s)$</span>
- A **solution** is an **action sequence** but must achieve the goal for **any possible initial state and transition**.

### Planning with **Markov Decision Planning(MDP)**
- a state space $S$
- <span style="color:blue">initial state </span> $s_0 \in S$
- a set $G \subseteq S$ of goal states
- actions $A(s) \subseteq A$ applicable in each $s \in S$
- <span style="color:blue">transition probabilities </span>$P_a(s'|s)$ for $s \in S$ and $a \in A(s)$
- positive action costs <span style="color:blue">$c(a,s) > 0$</span>
- **Solutions** are **functions(policies)** mapping states into actions
- **Optimal** solutions *minimize **expected cost*** to goal

### Partially Observable MDPS (POMDPs)
- states $s \in S$
- actions $A(s) \in A$
- <span style="color:blue">transition probabilities </span>$P_a(s'|s)$ for $s \in S$ and $a \in A(s)$
- <span style="color:blue">initial belief state</span> $b_0$
- <span style="color:blue">final belief state </span>$b_f$
- <span style="color:blue">sensor model</span> given by probabilities $P_a(o|s), o \in Obs$
- **Belief states** are probability distributions over $S$
- **Solutions** are policies that map belief states into actions
- **Optimal** policies minimize **expected** cost to go from $b_0$ to $G$
  
> If **actions deterministi**c && **initial location known**, planning problem is **classical**
>
> If **actions stochasti**c && **location observable**, problem is **MDP**
>
>If **actions stochastic** && **location partially observable**, problem is a **POMDP**.


<span style="color:red"> **Problems $\rightarrow$ Models $\rightarrow$ Algorithms** </span>

## Models, Languages, and Solvers

<span style="color:blue">A planner is a solver over a class of models</span>; 
 
 <span style="color:blue">Model description $\rightarrow$ Planner$\rightarrow$Corresponding controller</span>

### Classic Planning Language:
<span style="color:red">**STRIPS, PDDL**</span>
> PDDL复杂，但便于计算机理解

**STRIPS**

A problem in <span style="color:blue">STRIPS</span> is a tuple $P = <F, O, I, G>$
- F stands for set of all <span style="color:blue">atoms</span>(boolean vars), F can be called as Facts/Propositions, Fluents
  >atoms: 描述state得最小单元，例如at(x,y), coll(x), row(y), etc.
- O stands for set of all <span style="color:blue">operators</span> (actions)
- $I \subseteq F$ stands for <span style="color:blue">initial situation</span>
- $G \subseteq F$ stands for <span style="color:blue">goal situation</span>
  
Operators $o \in O$ represented by
- the <span style="color:blue">Add</span> list $Add(o) \subseteq F$
- the <span style="color:blue">Delete</span> list $Del(o) \subseteq F$
- the <span style="color:blue">Precondition</span> list $Pre(o) \subseteq F$

<img src="https://i.328888.xyz/2023/04/05/i8RvPq.jpeg" width ="80%"/>

<img src="https://i.328888.xyz/2023/04/05/i8BmJX.jpeg" width ="80%">
**PDDL**

<img src="https://i.328888.xyz/2023/04/05/i8cVp5.jpeg" width ="80%">
<img src="https://i.328888.xyz/2023/04/05/i8ciky.jpeg" width ="80%">
<img src="https://i.328888.xyz/2023/04/05/i8RuT3.jpeg" width ="80%">


**Algorithmic Problems in Planning**

Input: A planning task P.

>Satisficing Planning:
Output: A plan for P, or 'unsolvable' if no plans for exists.
>
>Optimal Planning:
Output: An optimal plan for P, or 'unsolvable' if no plans for exists
>
> <span style="color:red">Satisficing planning is much more effective in practice</span>
>
> Problems solving these problems are called (optimal) <span style="color:blue">planners, planning systems, or planning tools</span>.

**Decision Problems in Planning**

<span style="color:blue">PlanEx</span> is **PSPACE**-complete
>By PlanEx, we denote the problem of deciding, given a planning task P, whether or not there exists a plan for P. 
>
> -> <span style="color:red">Corresponds to satisficing planning.</span>


<span style="color:blue">PlanLen</span> is **PSPACE**-complete
>By PlanLen, we denote the problem of deciding, given a planning task P and an integer B (bound), whether or not there exists a plan for P of length at most B.
>
> -> <span style="color:red">Corresponds to optimal planning.</span>


<span style="color:red">**Blocksworld problem is hard**</span>
>the state space is typically exponentially large in the size

### Computaion: How to solve Strips planning problems?

**Key issue**: exploit two roles of language:
- <span style="color:blue">specifcation</span>: concise model description
- <span style="color:blue">computation</span>: reveal useful heuristic information (structure)
**Two traditional approaches**: <span style="background:yellow">search</span> vs. decomposition
- explicit <span style="color:blue">search</span>(more successful) of the state model $S(P)$ direct but not effective till recently
- <span style="color:blue">near decomposition</span> of the planning problem thought a better idea


<img src="https://i.328888.xyz/2023/04/05/i8prmz.jpeg" width="80%"/>

Question:
> **If planners** x, y **both compete in IPC'YY**, **and** x **wins**, **is** x **'better than'** y ?
> 
> Yes, but only on the IPC’YY <span style="background:yellow">benchmarks</span>, and only according to the <span style="background:yellow">criteria</span> used for determining a ‘winner’! On other domains and/or according to other criteria, you may well be better off with the ‘looser’.
>
> It’s complicated, over-simplification is dangerous. (But, of course, nevertheless is being done all the time).