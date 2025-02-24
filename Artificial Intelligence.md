#core 

| Unit No. | Syllabus                                                                                                                                                                                                                                                                                                                                |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.       | AI Problems, Task Domains of AI, AI Techniques: search knowledge, abstraction. Introduction to Intelligent program and Intelligent agents.<br><br>**Problem Solving:** Basic Problem solving Method: state space search, problem characteristics, Production systems characteristics, issues in design of Intelligent search algorithm. |
| 2.       | **Heuristic search Techniques**: Hill climbing techniques, Best First search, A\* Search, Problem Reduction: AO\* Search, Constraint Satisfaction, Means-End Analysis.<br><br>**Game Playing**: Game Tree, Searching procedure Minimax, alpha-beta pruning.                                                                             |
| 3.       | **Knowledge Representation**: Knowledge Representation issues. Knowledge Representation using Predicate Logic: Unification, resolution. Rule based Systems:Forward versus backward reasoning, conflict resolution.<br><br>**Structured Knowledge Representation**: Semantic Nets, Frames, conceptual dependency, scripts.               |
| 4.       | **Programming Languages**: Fundamental and concepts of Programming languages like Prolog or Lisp.<br><br>Relationship of languages with Knowledge representation and inferences                                                                                                                                                         |
| 5.       | **Reasoning**: Handling uncertainty Non-Monotonic Reasoning, Probabilistic reasoning, use of certainty factors, fuzzy logic.<br><br>Learning Concept of learning, learning automation, genetic algorithm, learning by inductions, neural nets.                                                                                          |
| 6.       | **Applications:** Expert Systems: Architecture, Domain Knowledge, Knowledge Acquisition, Case Studies: MYCIN, RI, Natural language Processing: Syntactic, Semantic and Pragmatic Analysis, Robotics etc.                                                                                                                                |

---
# UNIT 1

Artificial intelligence (AI) : Simulation of human intelligence by machines.
- Reactive
- Limited Memory
- Theory of Mind
- Self-aware

**Agents and Environment**

Agent: Programs that perceive environment, makes decisions and takes actions to achieve a goal.
- Percept: current sensor input
- Percept Sequence: History
- Agent Function: rules and conditions
- Agent Program: Implementation


**Rational Agent**: AI agent that chooses best action
- Action selection
- Performance measure
- Designing performance measures

**Task Environments**: understand context and problem.
**PEAS**: Performance Environment Actuators Sensors

**Properties of Task Environment**
- Fully Observable vs Partially Observable vs Unobservable.
- Single Agent vs Multi Agent. (single player vs multiplayer) <-
- Deterministic vs Stochastic (next state findable).
- Episodic (independent tasks) vs Sequential. 
- Static vs Dynamic (changing environment).
- Discrete (finite actions) vs Continuous (driving car)
- Known (defined rules) and Unknown.

**Types of Agents:**
- Simple Reflex
- Model-based Reflex
- Goal-based
- Utility-based

**Simple Reflex Agents**
- Performs actions based on current percepts, history doesn't matter.
- Condition-Action rules
- Simple but limited.
- Eg: Airbags

![[Screenshot 2025-02-20 at 1.17.41 PM.png]]

**Model Based Reflex Agents**
- Handle Partial Observability.
- Internal State: Percept history to reflect unobserved environment.
- Updating Internal State:
	- How world evolves independent of my actions.
	- What my actions would do?
- Decision Making. Learn over time.
- Eg: Self Driving car

![[Screenshot 2025-02-20 at 3.12.04 PM.png]]

**Goal Based Agents**
- extension of model based reflex agents.
- Action decision: using internal model and goal information
- Action selection: might consider sequences of action.
- Eg: Automatic Vacuum Cleaner.

![[Screenshot 2025-02-20 at 3.23.00 PM.png]]

**Utility Based Agents**
- Acts to maximize utility function.
- Performance measure that compares different world states based on how "desirable" they are.
- Utility: How happy/satisfied agent is with state.
- Eg: Smart AC

![[Screenshot 2025-02-20 at 4.06.15 PM.png]]

![[Screenshot 2025-02-20 at 3.37.02 PM.png]]

**Characteristics of learning agent**
- Adaptable
- Memory
- Feedback Sensitivity
- Decision-Making Ability
- Exploration and Exploitation
- Generalization
- Performance Improvement Over Time
- Problem-Solving Skills

---
# UNIT 2

**Problem Spaces States Space Representation**
{ Initial State, Action(s), Result(s, a), Goal Test, Path Cost Function }

Benefits: Structure, Search, Optimization and Decision making, Clarity, Scalability.

**Search Strategies**
Systematic methods and approaches used to explore and find relevant information or solutions within a given search space or dataset. Parameters:
- Completeness.
- Time and Space Complexity.
- Optimality.

**Uninformed Search** (Brute Force Search | Blind Search | Exhaustive Search)
- Explore search space without any specific information / heuristics about problem.
- Explore nodes systematically using pre-defined algorithms or random.
- Simple to implement and understand.
- But inefficient due to lack on knowledge. Slow.
- Eg: Breath First Search, DFS, Uniform Cost Search.

**Informed Search** (Heuristic)
- Search strategies utilize domain-specific information or heuristics to guide the search towards more promising paths.
- Efficient. Fast.
- Heuristic Accuracy: incorrect information can lead to suboptimal or incorrect solutions.
- Eg: Hill Climbing, Best First Search, A\* Algorithm.

**Breath First Search**
- Uninformed.
- Level by level.
- FIFO Queue.
- Algorithm : push root, unvisited neighbors, dequeue.
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
- Uninformed
- Explore depth, then backtracks
- LIFO Stack.
- Algorithm: initial node, recursively.
- Advantage:
	- Memory efficient. fewer nodes in comparison to breath.
- Disadvantage:
	- Completeness not guaranteed: may get trapped in infinite loop or branches, if cycle.
	- Non-Optimal: As might solution at lower depth.
- TC : $O(b^m)$; $b$ is branching factor and $m$ is maximum depth of search tree.
- SC : $O(b^m)$; stores longest depth in memory.

**Depth-Limited Search**
- Extension on BFS.
- Expand graph based on cost.
- Algorithm : Using priority queue.
- Optimal: Uniform cost search guarantees lowest-cost path.
- TC and SC : high.
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
- Time complexity: $O(b^{b/2})$
- Space complexity: $O(b^{b/2})$

**Problems in uninformed search**
- Blind Exploration: even when we have information.
- Inefficient in complex spaces.

**Informed (Heuristic)**
Special search method to find more solutions more efficiently using knowledge, intuition and common-sense.

**Best First Search**
- Greedily chooses node with best heuristic value (most promising).
- Takes advantage of both BFS and DFS.
- Node with lowest $h(n)$ is evaluated first.
- $h(n)$ : estimated cost of cheapest path from state at node $n$ to goal state.
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
(S) -> (n) -> (G)

- g(n) is sum of actual cost from Start node to current node.
- h(n) is heuristic cost from n to G.
- Algorithm : using priority queue and evaluation function.
- Complete : if search space is finite and heuristic function is admissible (<= actual cost)
- Optimal : if heuristic function is admissible and consistent (monotonic)
- TC and SC : depends but can be exponential.

> revisit example

- *Condition of optimality*
	- Admissible heuristic : never overestimates the cost to reach goal. (optimistic). Eg: Straight line distance.
	- Consistency (monotonicity) : for every successor $n'$ of $n$ :
		- `h(n) <= cost(n -> n') + h(n')`
- Problem with A\*
	- So far, considered OR graphs i.e. single path to goal.

**AO\* Search Algorithm**
- AND-OR graph is useful for solving problems by decomposing them into a set of smaller problems, all of which must be solved.
- Solve in the bottom up fashion.
- Return cost of solving terminal node with edge cost to parent node. Add both costs if AND Arc, otherwise choose best of all in case OR.
- Advantage:
	- efficient due to use of heuristics.
	- Optimal, when heuristic function is admissible
- Disadvantage:
	- Can consume large amount of memory.
	- heavily dependent of heuristic function.
- Complete and optimal : if consistent and admissible.
- TC and SC : heavily dependent of heuristic. worst case : exponential.

**Hill Climbing Algorithm**
- Greedy local maxima but no backtracking.
- Iterative algorithm that starts with arbitrary (random) solution to a problem, then attempts to find better solution by making a change. If change produces a better solution, another incremental change is made to the new solution, until no better solution is found.
- Algorithm of simple hill climbing:
	- Start at a random point
	- Evaluation current position
	- Evaluation neighbors
	- Check if neighbors are better
	- Move to a better neighbor
	- Repeat, until no better neighbor
	- End at peak.
	
![[Screenshot 2025-02-24 at 11.50.06 AM.png]]

- Problems:
	- Local Maxima: algorithm gets stuck at local maxima, while a better global maximum exists.
	- Ridges: `/\/\/\/\` sequence of local maxima, very difficult to navigate using greedy.
	- Plateau and shoulder: Flat area
- Advantage:
	- Simple and easy
	- Less computation power required
	- Quickly finds solution if heuristic is well chosen.
- Disadvantage:
	- No Optimal solution guaranteed.
	- highly sensitive to initial state, can get stuck at local maxima
	- no search history, infinite loop possible.
	- can't deal with flat regions.

*Random-restart Hill climbing*
- To avoid local optima, can perform multiple runs of algorithm from different random initial states.
- Tabu search: maintain previously visited state, to avoid infinite loop.
- Local beam search: keeps track of K states until one of them reaches goal. Else repeat with best K successors.

**Means-End Analysis (MEA)**
- Strategic approach combining forward and backward reasoning to tackle complex AI problems.
- Reduces unnecessary exploration.
- Algorithm:
	- Break down problem
	- Address sub-problems
	- Integrate strategies. use forward and backward search to solve problem effectively.

![[Screenshot 2025-02-24 at 12.37.38 PM.png]]

- Operators:
	- Delete black dot
	- Move triangle out of circle
	- Expand triangle.

*Operator Subgoaling*
- For handling situations where direct action cannot be applied to current state
- Setup sub-goals that can modify current state to goal state.
- Algorithm:
	- Identify different
	- Setup sub-goals
	- Find operators
	- Apply operators
	- Iterate

**Water Jug Problem**
![[Screenshot 2025-02-24 at 12.51.43 PM.png]]

**Constraints Satisfaction Problem (CSP)**
- Consists of set of variables, domain for each variable, and set of constraints that allow specific combinations of value.
- Eg: Sudoku.
- Find values of variables that satisfy a sum operation. Domain $\in [0,9]$. Condition: values must be unique. Observation: carry can only be $1$ or $0$. Extra digit at sum can only be $1$.
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
