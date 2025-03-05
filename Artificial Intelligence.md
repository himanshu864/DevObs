#core 

| Unit No. | Syllabus                                                                                                                                                                                                                                                                                                                                |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.       | AI Problems, Task Domains of AI, AI Techniques: search knowledge, abstraction. Introduction to Intelligent program and Intelligent agents.<br><br>**Problem Solving:** Basic Problem solving Method: state space search, problem characteristics, Production systems characteristics, issues in design of Intelligent search algorithm. |
| 2.       | **Heuristic search Techniques**: Hill climbing techniques, Best First search, A\* Search, Problem Reduction: AO\* Search, Constraint Satisfaction, Means-End Analysis.<br><br>**Game Playing**: Game Tree, Searching procedure Minimax, alpha-beta pruning.                                                                             |
| 3.       | **Knowledge Representation**: Knowledg[]()e Representation issues. Knowledge Representation using Predicate Logic: Unification, resolution. Rule based Systems:Forward versus backward reasoning, conflict resolution.<br><br>**Structured Knowledge Representation**: Semantic Nets, Frames, conceptual dependency, scripts.           |
| 4.       | **Programming Languages**: Fundamental and concepts of Programming languages like Prolog or Lisp.<br><br>Relationship of languages with Knowledge representation and inferences                                                                                                                                                         |
| 5.       | **Reasoning**: Handling uncertainty Non-Monotonic Reasoning, Probabilistic reasoning, use of certainty factors, fuzzy logic.<br><br>Learning Concept of learning, learning automation, genetic algorithm, learning by inductions, neural nets.                                                                                          |
| 6.       | **Applications:** Expert Systems: Architecture, Domain Knowledge, Knowledge Acquisition, Case Studies: MYCIN, RI, Natural language Processing: Syntactic, Semantic and Pragmatic Analysis, Robotics etc.                                                                                                                                |

---
# UNIT 1

## What is AI?

**Definition:** Simulation of human intelligence by machines.

**Applications:**
- **Mundane Tasks:** Perception (computer vision, speech recognition), natural language processing, common-sense reasoning, robot control, etc.
- **Formal Tasks:** Games (e.g., chess), mathematics (geometry, logic, calculus), and automated theorem proving.
- **Expert Tasks:** Engineering, design, fault finding, scientific analysis, medical diagnosis, finance, etc.

**Characterization of Intelligent systems**
- **Reactive** (no future knowledge)
- **Limited Memory** (informed decisions)
- **Theory of Mind** (personal AI that understands human emotions)
- **Self-aware** (futuristic with it's own emotions)

**Components of AI**
- **Learning:** Improving performance over time with data.
- **Reasoning:** Drawing conclusions and making inferences.
- **Problem-Solving:** Searching for solutions.
- **Perception:** Interpreting sensory inputs.
- **Language Understanding:** Processing and generating human language.

## Intelligent Agents

An **agent** is a program that perceives its environment, makes decisions, and acts to achieve its goals.

**Key Terms:**
- **Percept:** The current sensor input.
- **Percept Sequence:** The history of all percepts.
- **Agent Function:** Maps percept sequences to actions.
- **Agent Program:** The implementation of the agent function.

**Rational Agent:** Chooses the best action based on a **performance measure** and the task environment. Important considerations include:
- **Action Selection**
- **Performance Measures**
- **Designing Effective Performance Measures**

**Task Environments:** Defined by the context in which the agent operates. Use the **PEAS** framework:
- **Performance Measure**
- **Environment**
- **Actuators**
- **Sensors**

**Properties of Task Environments:**
- **Observability:** Fully observable vs. partially observable vs. unobservable.
- **Agents:** Single-agent vs. multi-agent environments (driving car).
- **Determinism:** Deterministic vs. stochastic (next state undeterminable).
- **Task Nature:** Episodic (independent tasks) vs. sequential.
- **Dynamics:** Static vs. dynamic (changing environment).
- **Structure:** Discrete (finite observations & actions) vs. continuous.
- **Knowledge:** Known (defined) vs. unknown rules.

## Types of Agents

**Simple Reflex Agents:**
- **Mechanism:** Respond based solely on the current percept (using *condition-action* rules).
- **Limitations:** Lack internal state (no history); may get stuck in loops.
- **Example:** Airbag system.

![[Screenshot 2025-02-20 at 1.17.41 PM.png]]

**Model-Based Reflex Agents:**
- **Mechanism:** Maintain an internal state to handle partial observability.
- **Capabilities:** Update the state based on percept history and learn over time.
- **Updating Internal State**:
	- How world evolves independent of my actions.
	- What my actions would do?
- **Example:** Self-driving car.

![[Screenshot 2025-02-20 at 3.12.04 PM.png]]

**Goal-Based Agents:**
- **Mechanism:** Use internal models plus goal information to plan actions.
- **Strategy:** Consider sequences of actions to reach the goal.
- **Example:** Automatic vacuum cleaner.

![[Screenshot 2025-02-20 at 3.23.00 PM.png]]

**Utility-Based Agents:**
- **Mechanism:** Choose actions to maximize a utility function (a measure of “happiness” or satisfaction).
- **Strategy:** Performance measures compare various world states and select the optimal one.
- **Example:** Smart air conditioning systems.

![[Screenshot 2025-02-20 at 4.06.15 PM.png]]

**Learning Agents:**

![[Screenshot 2025-02-24 at 8.57.53 PM.png]]

**Characteristics of a Learning Agent**
- **Adaptability:** Adjust behavior based on new data.
- **Memory:** Retain past experiences.
- **Feedback Sensitivity:** Use feedback to improve performance.
- **Decision-Making Ability:** Make effective choices in uncertain situations.
- **Exploration vs. Exploitation:** Balance trying new things and using known strategies.
- **Generalization:** Apply learned knowledge to new problems.
- **Performance Improvement:** Enhance problem-solving skills over time.

![[Screenshot 2025-02-20 at 3.37.02 PM.png]]

## Reasoning: Forward vs. Backward

- **Forward Reasoning (Data-Driven):**
    - Starts with available data and applies rules to infer conclusions.
    - Opportunistic approach.
    - Suitable for planning and control monitoring.
- **Backward Reasoning (Goal-Driven):**
    - Starts with a goal or hypothesis and works backward to find supporting facts.
    - Conservative approach.
    - Often used in diagnostic tasks.

| **Forward Reasoning**                 | **Backward Reasoning**                 |
| ------------------------------------- | -------------------------------------- |
| Data-driven                           | Goal-driven                            |
| Begins with available data            | Begins with the desired conclusion     |
| Explores all applicable rules         | Tests select rules to support the goal |
| Often used in planning and monitoring | Commonly used in diagnostic tasks      |

---
# UNIT 2

### State Space Search and Production System

**State space search** is a method used in AI to navigate through sequences of states in order to efficiently reach a goal state.

The **state space** represents all possible configurations or snapshots of the system (or problem) at any given time. Each state captures the values of all relevant variables.

A **production system** provides a structured framework for solving AI problems. It organizes the process of search and decision-making through a set of rules.

**Production rules** consist of pairs of conditions and actions, typically phrased as:  
  `If [condition] then [action]`.

**Representation of a State Space Search Problem**
A typical problem in state space search is defined by:
```
{ Initial State, Action(s), Result(s, a), Goal State, Path Cost Function }
```

> *Action(s)*: set of all possible actions for current state.
> *Result(s, a)*: state reached by performing action $a$ on state $s$.
> *cost(s, a)*: cost of performing action $a$ on state $s$.

**Benefits**
This structured approach enhances **clarity**, **scalability**, **optimization**, and supports effective **decision making** during the search process.

### Problem Characteristics

- **Decomposability:** Can the problem be broken into smaller, almost independent parts?
- **Reversibility:** Can you backtrack or revert actions?
- **Predictability:** Is the environment predictable?
- **Knowledge Requirement:** Is domain-specific knowledge required?
- **Human Interaction:** Is human intervention needed?
- **Solution Nature:** Is the solution a single state or a sequence (path) of states?
- **Relativity**: Is a solution's effectiveness determined by absolute criteria, or is it measured relative to other solutions?

## Search Strategies

Systematic methods and approaches used to explore and find relevant information or solutions within a given search space or dataset. Parameters:
- Completeness.
- Optimality.
- Time and Space Complexity.

### Uninformed (Blind) Search
(Brute Force Search | Blind Search | Exhaustive Search)

- Explore search space without any specific information / heuristics about problem.
- Explore nodes systematically using pre-defined algorithms or random.
- Simple to implement and understand.
- But inefficient due to lack on knowledge. Slow.
- Eg: Breadth First Search, DFS, Uniform Cost Search.

**Breadth First Search**
- Explore level by level using a FIFO queue.
- Advantages:
	- Guarantees finding the shortest path if one exists in an unweighted graph.
	- Closer nodes are discovered before moving to farther ones.
- Disadvantages:
	- Inefficient in terms of time and space for large search spaces.
	- Not suitable for scenarios where the cost or weight of edges is not uniform.
- Complete: if search space is finite.
- Optimal: if unweighted or uniformly weighted.
- Time complexity: $O(b^d)$; $b$ is branching factor and $d$ is depth of shallowed goal node.
- Space complexity: $O(b^d)$; Stores all nodes at lowest level.

**Depth First Search**
- Explore as deep as possible along one branch before backtracking (using a LIFO stack).
- Advantage:
	- Memory efficient. fewer nodes in comparison to breadth.
- Disadvantage:
	- Completeness not guaranteed: may get trapped in infinite loop or branches, if cycle. Use *Depth Limited Search* or *Iterative Deepening DFS* to remedy that. But again, not complete.
	- Non-Optimal: As might solution at lower depth.
- TC : $O(b^m)$; $b$ is branching factor and $m$ is maximum depth of search tree.
- SC : $O(b^m)$; stores longest depth in memory.

**Uniform Cost Search**
- Used for weighted tree/graph traversals.
- Expands the node with the lowest path cost (using a priority queue).
- Optimal: guarantees lowest-cost path.
- TC and SC : high. (backtracking)
- Time complexity: $O(b^d)$ but better than BFS.
- Space complexity: $O(b^d)$

**Bidirectional Search**
- Simultaneous BFS from start and goal state and then meet in middle.
- Advantage:
	- Faster Exploration
	- Reduce effective branching factor
- Disadvantage:
	- Increases memory requirements
	- Additional Overhead.
- Completeness.
- Optimality.
- Time complexity: $O(b^{d/2})$
- Space complexity: $O(b^{d/2})$

**Problems in uninformed search**
- Blind Exploration: even when we have information.
- Inefficient in complex spaces.

### Informed (Heuristic) Search

- Search strategies utilize domain-specific information or heuristics to guide the search towards more promising paths.
- Efficient. Fast.
- Heuristic Accuracy: incorrect information can lead to suboptimal or incorrect solutions.
- Eg: Hill Climbing, Best First Search, A\* Algorithm.

**Informed (Heuristic) Search**
Special search method to find more solutions more efficiently using knowledge, intuition and common-sense.
- *Heuristic Function $h(n)$*: gives estimation on cost of getting from node $n$ to goal state.

**Best First Search**
- Greedily chooses node with best heuristic value (most promising).
- Takes advantage of both BFS and DFS.
- Node with lowest $h(n)$ is evaluated first.
- Algorithm : Using priority queue based on $h(n)$. start root. end goal.
- Advance:
	- find solution without much exploration
	- less memory comparison to $A*$ etc.
- Disadvantage:
	- Not complete, might get stuck in infinite loop.
	- Not optimal, no guarantee, heavily depends on accuracy of heuristic value.
- TC and SC : Worst case - $O(b^d)$ . average very less.

**A\* Search**
- Combines advantage of both uniform cost search and best first search.
$$f(n) = g(n) + h(n)$$
> **g(n)** is sum of actual cost from start node to current node.
> **h(n)** is heuristic value of node n.

- Algorithm : using priority queue and evaluation function.
- Complete : if search space is finite and heuristic function is *admissible*.
- Optimal : if heuristic function is admissible and *consistent* (monotonic).
- TC and SC : depends but can be exponential.

*Condition of optimality*
- Admissible heuristic : never overestimates the cost to reach goal. (optimistic). Eg: Straight line distance.
- Consistency (monotonicity) : for every successor $n'$ of $n$ :
	- `h(n) <= cost(n -> n') + h(n')`
- Problem with A\*
	- So far, considered OR graphs i.e. single path to goal.

**AO\* Search Algorithm**
- AND-OR graph is useful for solving problems by *decomposing* them into a set of smaller problems, all of which must be solved.
- Solve in the bottom up fashion.
- Return cost of solving terminal node with edge cost to parent node. Add both costs if AND Arc, otherwise choose best of all in case OR.
- Advantage:
	- Efficient due to use of heuristics.
	- Optimal, when heuristic function is admissible
- Disadvantage:
	- Can consume large amount of memory.
	- Heavily dependent of heuristic function.
- Complete and optimal : if consistent and admissible.
- TC and SC : heavily dependent of heuristic. worst case : exponential.

**Hill Climbing Algorithm**
Greedy local maxima but no backtracking.

- Starts with an arbitrary solution and iteratively moves to a better neighboring state.
- **Algorithm**:
	1. Start at a random state.
	2. Evaluate the current state.
	3. Evaluate neighboring states.
	4. Move to a neighbor that improves the evaluation.
	5. Repeat until no better neighbor is found.
	
![[Screenshot 2025-02-24 at 11.50.06 AM.png]]

- **Problems**:
	- Local Maxima: algorithm gets stuck at local maxima, while a better global maximum exists.
	- Ridges: `/\/\/\/\` sequence of local maxima, very difficult to navigate using greedy.
	- Plateau and shoulder: Flat area
- **Advantage**:
	- Simple and easy
	- Less computation power required
	- Quickly finds solution if heuristic is well chosen.
- **Disadvantage**:
	- No Optimal solution guaranteed.
	- highly sensitive to initial state, can get stuck at local maxima
	- no search history, infinite loop possible.
	- can't deal with flat regions.
- **Variations:**
	- **Random-Restart Hill Climbing:** Repeatedly start from different random states to overcome local optima.
	- **Tabu Search:** Keeps a memory of visited states to avoid cycles.
	- **Local Beam Search:** Maintains _k_ states and explores the best successors from them.
	
**Means-End Analysis (MEA)**
- Strategic approach combining forward and backward reasoning to tackle complex AI problems.
- Reduces unnecessary exploration.
- Algorithm:
	1. Identify the differences between the current state and the goal.
	2. Set sub-goals to eliminate these differences.
	3. Select operators (actions) that reduce the difference.
	4. Apply these operators iteratively until the goal is reached.

![[Screenshot 2025-02-24 at 12.37.38 PM.png]]

*Operator Subgoaling*: Create intermediate goals when direct action toward the final goal isn’t possible.

Operators:
- Delete black dot
- Move triangle out of circle
- Expand triangle.

### Example Problems

**Water Jug Problem**
![[Screenshot 2025-02-24 at 12.51.43 PM.png]]

**Constraints Satisfaction Problem (CSP)**
- Consists of set of variables, domain for each variable, and set of constraints that allow specific combinations of value.
- Eg: Sudoku.
- *Crypt Arithmetic Problem:* Find values of variables that satisfy a sum operation. Domain $\in [0,9]$. Condition: values must be unique. Observation: carry can only be $1$ or $0$. Extra digit at sum can only be $1$.
- Solve using decision tree and backtracking.
- Eg: `SEND + MORE = MONEY` => `9567 + 1085 = 10652`

**8-Puzzle Problem**
- 3x3 grid with 8 clockwise numbered tiles and one empty space at the center.
- Can swap empty space with any adjacent tile (four directions)
- Can use BFS, DFS, A\* or other search space algorithm
- Can use manhattan distance or A\* to estimate cost using heuristic.
- Heuristic A\*:
	- g(n) is no. of moves taken so far
	- h(n) is no. of misplaced tiles
	- Greedily keep choosing state with lowest heuristic function.

**Minimax Algorithm**
- Search algorithm used in game playing to determine optimal sequence of moves for a player in zero-sum games (tic tac toe, chess, etc)
- Backtracking in DFS, where one player tries to maximize the utility and another tries to minimize it.
- Complete and Optimal
- TC and SC : $O(b^d)$
- Limitations: can be too slow for complex games with many possible moves.

**Alpha-Beta pruning**
- Alpha - best value that the maximizer currently can guarantee can that level or above.
- Beta - best value that the minimizer currently can guarantee can that level or above.
- Initially $\alpha = -\infty$ and $\beta = \infty$.
- Prune when $\alpha \ge \beta$.
- Maximum node updates $\alpha$ from children, and similarly minimum updates $\beta$.
- Efficient, complete, optimal, widely applicable.

**Branch and Bound**
- Systematically divides a problem into subproblems (branches) and evaluates each using a bound.  
- Find optimal solution in problems like traveling salesman, knapsack, and job scheduling.
- The bound estimates the best possible outcome from that branch, guiding the search toward promising solutions.
- If a branch's bound is worse than the best complete solution found so far, it is pruned (discarded).  
- It employs a search strategy (such as best-first search, BFS, or DFS) to explore the most promising branches first.  
- This method efficiently finds the optimal solution by avoiding unnecessary exploration of suboptimal branches.
