# COMP90054 AI Planning for Autonomy

# week1
## lecture 1
prerecorded videos
## lecture 2
introduction

| Staff | Contact |
|---|---|
|Nir Lipovetzky| nir.lipovetzky@unimelb.edu.au|
|Tim Miller|tmiller@unimelb.edu.au|
|Guang hu(head tutors)|ghu1@student.unimelb.edu.au|

### Assignments
- Individual early project: Search,
- Small Individual  project: Modeling a planning problem,
- Mid Semester Test: short Quiz
- Final group project in the form of a competition

### Pacman Competition
Hall of Fame (best 8 teams each year will compete with best teams
2016-present, forever!) 
: https://sites.google.com/view/pacman-capture-hall-fame/

###  What is Artificial Intelligence?
- **An engineering standpoint**
  - The science of making machines do things that would require intelligence if done by
humans. (M. Minsky)
- **A Rational perspective**
  - The branch of computer science that is concerned with the automation of intelligent
behavior. (Luger and Stubblefield) -
  - Intelligent behavior: make ‘good’ (rational) action choices
  - Are humans ‘rational’ agents? We often make mistakes; we are not all chess
grandmasters even though we may know all the rules of chess.

### Rational Agents

**Agents**:
- Perceive the environment through sensors (!percepts).
- Act upon the environment through actuators (!actions).
- Examples? Humans, animals, robots, software agents (softbots), . . .

**Rational Agents . . . do ‘the right thing’!**
- do the right thing: Rational agents select their
actions so as to maximize a performance measure.
- What’s the performance measure of an autonomous vacuum cleaner? m2 per
hour, Level of cleanliness, Energy usage, . . .

**TRY to do ‘the right thing’!**
- The hypothetical best case (‘the right thing’) is often unattainable.
- The agent might not be able to perceive all relevant information. (Is there dirt
under this bed?)

**Rationality vs. Omniscience:**
- An omniscient agent knows everything about the enviroment, and knows the
actual effects of its actions.
- A rational agent just makes the best of what it has at its disposal, maximizing
expected performance given its percepts and knowledge.
- Example? I check the traffic before crossing the street. As I cross, I am hit by a
meteorite. Was I lacking rationality?
Mapping your input to the best possible output
<span style="color:red">**Performance measure x Percepts x Knowledge -> Action** </span>.

**What Does AI Do?**

|   | Humanly | Rationally | |
|---|-------|-------|------|
|  Thinking |  Systems that think like humans Systems(Cognitive Science)|Systems that think rationally (Logics: Knowledge and Deduction)|
|Acting    |   System that act like humans(Turing test)    | **Systems that act rationally**(How to make good action choices) |

A central aspect of intelligence (and one possible way to define it) is the **ability to act successfully** in the world

### AI history

#### 60’s, 70’s, and 80’s
Theories as Programs, 

Methodology Problem:
**Theories expressed as programs cannot be proved wrong: when a program fails,
it can always be blamed on ‘missing knowledge’**

- narrow the domain (expert systems)
  - problem: lack of generality
- accept the program is just an illustration, a demo
  - problem: limited scientific value
- fill up the missing knowledge (intuition, commonsense)
  - problem: not successful so far

#### AI Winter: the 80’s
The knowledge-based approach reached an impasse in the 80’s, a time also of
debates and controversies: 

**Good Old Fashioned AI** is ‘rule application’ but intelligence is not (Haugeland)

#### AI 90’s - 2020
Formalization of AI techniques and increased use of mathematics. Recent issues of
AIJ, JAIR, AAAI or IJCAI shows papers on:
1. SAT and Constraints
2. Search and Planning
3. Probabilistic Reasoning
4. Probabilistic Planning
5. Inference in First-Order Logic
6. Machine Learning
7. Natural Language
8. Vision and Robotics
9. Multi-Agent Systems

Areas 1 to 4 often deemed about techniques, but more accurate to regard them
as **models and solvers**.

[![dieMo.png](https://i.328888.xyz/2023/03/05/dieMo.png)](https://imgloc.com/i/dieMo)
[![diE7A.png](https://i.328888.xyz/2023/03/05/diE7A.png)](https://imgloc.com/i/diE7A)
[![di7wc.png](https://i.328888.xyz/2023/03/05/di7wc.png)](https://imgloc.com/i/di7wc)
[![digYJ.png](https://i.328888.xyz/2023/03/05/digYJ.png)](https://imgloc.com/i/digYJ)
[![diXGt.png](https://i.328888.xyz/2023/03/05/diXGt.png)](https://imgloc.com/i/diXGt)
[![dipfP.png](https://i.328888.xyz/2023/03/05/dipfP.png)](https://imgloc.com/i/dipfP)

## Summary: AI and Automated Problem Solving
- A research agenda that has emerged in last 20 years: solvers for a range of
intractable models
- Solvers unlike other programs are general as they do not target individual
problems but families of problems (models)
- The challenge is computational: how to scale up
- Sheer size of problem shouldn’t be impediment to meaningful solution
- Structure of given problem must recognized and exploited
- Lots of room for ideas but methodology empirical
- Consistent progress
  - effective inference methods (derivation of h, conflict-learning)
  - islands of tractability (treewidth methods and relaxations)
  - transformations (compiling away incomplete info, extended goals, . . . )

--- 

# week2
## tutorial

**Problem Set 01**

- Overview of this subject
- Review on the State-Space Model
- Review on the Blind Search algorithms

![dwaAy.png](https://i.328888.xyz/2023/03/06/dwaAy.png)

### Overview
![dwQh8.png](https://i.328888.xyz/2023/03/06/dwQh8.png)


### State-Space model
![dwqZZ.png](https://i.328888.xyz/2023/03/06/dwqZZ.png)

- p = <S, s0, SG, A, T, c>

- s = {s1, s2, s3} 

- s0 = s1

- SG = {s3}

- A -> A(s) = {a1}

- A = {A(s1) = {a,c}, A(s2)={a,b}, A(s3) = {d,b}}

- T(s,a) = s'

- T(s,a) = {T(s1,a) = s2, T(s1,c)=s3, T(s2,a)=s3, T(s2,b) = s1, T(s3,d)=s1, T(s3,b)=s2}
c(a) =3 , c(b) =2, c(c) = c(d)=1

### Blind Search
- BFS 
  - Data Structure of implementation BFS: Queue (FIFO)
  - ![dwvHk.png](https://i.328888.xyz/2023/03/06/dwvHk.png) 
  - ![MCheC.jpeg](https://i.328888.xyz/2023/03/18/MCheC.jpeg)
  - Don't want to check during generating the node, check during expanding the node.
- DFS 
  - Data Structure of implementation DFS: Stack (FILO)
  - ![dwLkU.png](https://i.328888.xyz/2023/03/06/dwLkU.png)
  - [![MCw2d.jpeg](https://i.328888.xyz/2023/03/18/MCw2d.jpeg)](https://imgloc.com/i/MCw2d)
- ID

|     | Complete | Optimal | Time | Space  |
|-----|----------|---------|------|--------|
| BFS |     yes     | yes (when uniform cost)        | O(b^d)     | O(b^d)       |
| DFS |     no: could have loop    |    no     |    O(b^D) |   O(b * D)     |
| ID: Iterative Deepening  |     yes     |    yes     |  O(b^d)    |   O(b * d)     |

Complete: can find the solution if the solution exists

D: depth limit

**IDS example**:

![h2Aoq.gif](https://i.328888.xyz/2023/03/07/h2Aoq.gif)

---
## MX平时班2
Quick Overview
- Blind Search
  - only used the basic information
  - E.g.: DFS, BRFS, Dijkstra, IDS
  - Pros: Easy to implement;
  - Cons: "Blind"; Less effective
- Heuristic(Informed) Search
  - TOgether with the heuristic function
  - R.G.: BFS, A*, WA*, Enforced Hill Climbing
  - Pros: More effective in practice;
  - **Cons: How to find a good heuristic function?**

### Uniform Cost Search(Dijkstra):  $cost \geq 0$
- Expand nodes by the **best $g(\sigma)$** in the list; Using Priority Queue$O(log(n)) \ll O(n)$
- Completeness?  Y
- Optimality?  Y
  me Complexity: $|n| * |E|$, 点 x 边
- Space Complexity: $|n|$

<img src="https://i.328888.xyz/2023/03/13/vgMe8.jpeg" alt="vgMe8.jpeg" border="0" width = "70%"/>


  
### heuristic search

Heuristic Function

<span style="background-color:yellow">Heuristic function **h** estimates the cost of the path to the goal</span>; search gives a preference to explore states with small **h**

Heuristic value(h-value)
> $h(s) \in R_0^+  \cup \ \{\infty\}$

Remaining Cost 

<span style="background-color:yellow">**h\*(s)** is the remaining cost of an optimal plan fo s, or $\infty$ if there exists no plan for **s**</span>

h*(s)是一个假象值，抽象出来的

Search performance depends crucially on <span style="color:red">"how well h reflects h*"</span>. This is informally called the <span style="color:blue">informedness</span> or <span style="color:blue">quality</span> of h
#### **Properties**

**Definition**
- <span style="color:blue">**safe**</span>
  > $if\  h^*(x) = \infty for\  all\  s \in S\ with\ h(s) =\infty$
  >
  >if solution exists in state s, then $h(s)< \infty$
- <span style="color:blue">**goal-aware**</span>
  > $if\ h(s) = 0\ for\ all\ goal\ states\ s \in S^G$ 
- <span style="color:blue">**admissible**</span> -- <span style="color:red">Very important!!</span>
  > $if\ h(s) \leq h^*(s)\ for\ all\ s\ \in s$
- <span style="color:blue">**consistent**</span>
  > $if\ h(s) \leq h'(s) + c(a)\ for\ all\ transitions\ s \stackrel{a}{\rightarrow} s'$
  >
  >$h(s)-h(s') \leq c(a)$
  

Dominance
  > $\forall s, h(s) \geq g(s), where\ g\ and\ h\ are\ admissible\ heuristics$

Proposition
- Consistent + Goal-aware -> Admissible
- Admissible -> Goal-aware + Safe
Informedness(Quality)
  - how ell h reflects h*?
    - h = h*
    - h = 0
  - Trade-off between informedness and computational complexity
  
### Heuristic Search Algorithm
- **Systematic search**
  - Greedy best-first search (Popular satisficing planning)
  - Weighted A*(Popular satisficing planning)
  - **A\*(Popular optimal planning)**
  - IDA* (optimal but not popular)
- **Local Search**
  - Hill-Climbing
  - Enforced hill-climbing(Popular satisficing planning)
  
Greedy Best-First Search(Greedy BFS)
- Expand nodes by the **best h(s)** in the list; Using Priority Queue
- Completeness? For **Safe** heuristic, Yes
- Optimality? No

A Star(A*): * 代表 optimal
- Expand nodes by the best f(s) in the list; Using Priority Queue
  - f(s) = g(n) + h(s), $h(s) \leq h^*(s)$
  - Generated nodes: Nodes inserted into open at some point. --push
  - Expanded nodes: Nodes $\sigma$ popped from open for which the test against closed and distance succeeds.
  - Re-expanded nodes: Expanded nodes for which $state(\sigma) \in closed\ upon\ expansion$(also called re-opened nodes) 
    - best g(s), $g(n) \leq  best\ g(s)$
- Completeness? For **safe** heuristics, Yes
- Optimality? For **admissible** heuristics, Yes

Weighted A Star(WA*)
- Expanded ndoes by the best g(s) + w*h(s) in the list; Using Priority Queue
- The weight $w \in R_o^+$ is an algorithm parameter
  - For W = 0, weighted A* behaves like uniform-cost search
  - For W = 1, weighted A* behaves like A*
  - For $W \rightarrow \infty$, weighted A* behaves like greedy best-search
    - $w(\frac{1}{w}g(s) + h(s))$, $w\rightarrow \infty, \frac{1}{w} \rightarrow0$ 
  - if 0 < w < 1, still optimal, $f(s) = g(n)+w*h(s) = g(n)+ h'(s) \leq g(n) + h^*(s)$, still A*
  - For W > 1, weighted A* is **bounded suboptimal**: if *h* is admissible, then the solutions returned are at most a factor W more closely than optimal ones.

Iterative Deepning A*(IDA*)
- DFS with limit of f(s) = g(n)+h(s), increase the limit to the next threshold.
- h(s) -> admissible, IDA* -> optimal

Hill-Climbing (HC)
- Expand nodes by the best $h(\sigma)$ from the successors
- Local minima problem
- Completeness? No
- Optimality? No
  
Enforced Hill-Climbing(EHC)
- Expand nodes by using *BFS* to find the smaller $h(\sigma)$
- Local and Systematic
- Completeness? For **goal-aware** heuristics, Yes
- Optimality? No

---
### Prehandout-07
Search Terminology

> <span style="color:blue">Search node n</span>: Contains a state reached by the search, plus information about how it was reached
>
> <span style="color:blue">Path Cost g(n)</span>: The cost of path reaching n.
>
> <span style="color:blue">Optimal cost g*</span>: The cost of an optimal solution path. For a state s, g*(s) is the cost of a cheapest path reaching s.
>
> <span style="color:blue">Node expansion</span>: Generating all successors of a node, by applying all actions applicable to the node's state *s*. Afterwards. the ststa *s* itself is also said to be expanded 
>
> <span style="color:blue">Search Strategy</span>: Method for deciding which node is expanded next.
>
> <span style="color:blue">Open list</span> : Set of all nodes that currently are candidates for expansion. Also called <span style="color:blue"> frontier </span>
>
> <span style="color:blue">Closed list</span>: Set of all states that were already expanded. Used only in <span style="color:red">graph search</span>, not in <span style="color:red">tree search</span>. Also called <span style="color:blue">explored set</span>.

<span style="color:blue">Completeness</span>: Is the strategy guaranteed to find a solution when there is one? 

<span style="color:blue">Optimality</span>: Are the returned solutions guaranteed to be optimal?

Heuristic Functions performance depends on **informedness** and **computational overhead**.

[![MlFUw.jpeg](https://i.328888.xyz/2023/03/18/MlFUw.jpeg)](https://imgloc.com/i/MlFUw)
[![MlzKz.jpeg](https://i.328888.xyz/2023/03/18/MlzKz.jpeg)](https://imgloc.com/i/MlzKz)
[![MleXq.jpeg](https://i.328888.xyz/2023/03/18/MleXq.jpeg)](https://imgloc.com/i/MleXq)
[![MlECb.jpeg](https://i.328888.xyz/2023/03/18/MlECb.jpeg)](https://imgloc.com/i/MlECb)