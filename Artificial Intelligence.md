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
	- $h(n) \le cost(n \to n') + h(n')$
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
- Alpha - best value that the maximizer currently can guarantee at that level or above.
- Beta - best value that the minimizer currently can guarantee at that level or above.
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

---
# UNIT 3

Ability to reason -> Knowledge -> Intelligence

- **Logical agents**, also known as **knowledge-based agents**, are a type of AI agent that uses logic to reason about the world and make decisions.
- Knowledge-based agents initially contain some **Knowledge Base** i.e. background knowledge which is a set of **sentences** (also known as **axiom**). Each sentence is expressed in a language called *knowledge representation language*.
- We add new sentences to KB and query what is known through **Inferences**.

**Proposition** is a declarative sentence that is either true or false.

- **Premises** is a statement that supports conclusion (proposition). It is *always true*.
- **Argument**: If a set of premises (P) yield another proposition Q (conclusion).
- An argument is said *valid* if the conclusion Q can be derived from premises by applying rule of inference.
$$\{P_1 \ \wedge \ P_2 \ \wedge \ \dots \ \wedge \ P_n \} \ |- Q$$
- Propositional variables - $p, q, r, s$.
- **Compound propositions** - new mathematical statements, derived by combining one or more propositions.

1. **Negation**: NOT: $\neg P$
2. **Conjunction**: AND: $p \wedge q$
3. **Disjunction**: OR: $p \vee q$
4. **Implication**:
	- "if p, then q"
	- Is false only for $T \to F$, otherwise true.
	- $p \to q$; $p$ is called *hypothesis* (or premise) and q is called the *conclusion*.
	- $q \to p$ converse
	- $\neg p \to \neg q$ inverse
	- $\neg q \to \neg p$ contra positive
	- $p \to q \equiv \neg q \to \neg p$
	- $p \to q \equiv \neg p \vee q$
5. **Bi-conditional**:
	- "if p then q, and conversely"
	- $p \leftrightarrow q \equiv (p \to q) \wedge (q \to p)$
	- Is true when both $p$ and $q$ have same values, otherwise false.

- **Tautology / valid**: Proposition function which is "Always True".
- **Contradiction / Unsatisfiable**: "Always False".
- **Contingency**: which is neither tautology nor contradiction. $p \vee q$
- **Satisfiable**: at least one true.

**De Morgan's Law**
$$\neg (P \wedge Q) \equiv (\neg P \vee \neg Q)$$
$$\neg (P \vee Q) \equiv (\neg P \wedge \neg Q)$$

**Properties**
$$ (\alpha \wedge \beta) \equiv (\beta \wedge \alpha) \quad \text{commutativity of } \wedge $$
$$ (\alpha \vee \beta) \equiv (\beta \vee \alpha) \quad \text{commutativity of } \vee $$
$$ ((\alpha \wedge \beta) \wedge \gamma) \equiv (\alpha \wedge (\beta \wedge \gamma)) \quad \text{associativity of } \wedge $$
$$ ((\alpha \vee \beta) \vee \gamma) \equiv (\alpha \vee (\beta \vee \gamma)) \quad \text{associativity of } \vee $$
$$ \neg(\neg\alpha) \equiv \alpha \quad \text{double-negation elimination} $$
$$ (\alpha \to \beta) \equiv (\neg\beta \to \neg\alpha) \quad \text{contraposition} $$
$$ (\alpha \to \beta) \equiv (\neg\alpha \vee \beta) \quad \text{implication elimination} $$
$$ (\alpha \leftrightarrow \beta) \equiv ((\alpha \to \beta) \wedge (\beta \to \alpha)) \quad \text{biconditional elimination} $$
$$ \neg(\alpha \wedge \beta) \equiv (\neg\alpha \vee \neg\beta) \quad \text{De Morgan} $$
$$ \neg(\alpha \vee \beta) \equiv (\neg\alpha \wedge \neg\beta) \quad \text{De Morgan} $$
$$ (\alpha \wedge (\beta \vee \gamma)) \equiv ((\alpha \wedge \beta) \vee (\alpha \wedge \gamma)) \quad \text{distributivity of } \wedge \text{ over } \vee $$
$$ (\alpha \vee (\beta \wedge \gamma)) \equiv ((\alpha \vee \beta) \wedge (\alpha \vee \gamma)) \quad \text{distributivity of } \vee \text{ over } \wedge $$

## Well-found Formulas

A **sentence** (also called a _well-formed formula_) is defined inductively as follows:

1. Any propositional **symbol** $S$ is a sentence.
2. If S is a sentence, then $\neg S$ is also a sentence.
3. If S is a sentence, then $(S)$ is also a sentence.
4. If S and T are sentences, then each of the following is also a sentence:
    - $S \wedge T$
    - $S \vee T$
    - $S \to T$
    - $S \leftrightarrow T$

## Rules of Inference

- **Modus ponens**
$$P,\;P \to Q\;\therefore\;Q$$
- **Modus tollens**
$$\neg Q,\;P \to Q\;\therefore\;\neg P$$
- **Hypothetical syllogism**
$$P \to Q,\;Q \to R\;\therefore\;P \to R$$
- **Disjunctive syllogism**
$$P \vee Q,\;\neg P\;\therefore\;Q$$
- **Addition**
$$P\;\therefore\;P \vee Q$$
- **Simplification**
$$P \wedge Q\;\therefore\;P$$
- **Conjunction**
$$P,\;Q\;\therefore\;P \wedge Q$$
- **Resolution**
$$P \vee Q,\;\neg P \vee R\;\therefore\;Q \vee R$$

## Proposition Logic

**Disadvantages**
Too puny a language to represent complex environment in a concise way. That's where first order predicate logic comes in.

## First order predicate logic

**Universal Quantifiers** of a proposition function is the proposition that asserts

- P(x) is true for all values of x in the universe of discourse i.e. all possible values of x.
- $\forall_x \; P(x)$ i.e. for all values of x, P(x) is true.

**Existential Quantifiers** of a proposition function is the proposition that asserts

- P(x) is true for at least one value of x in the universe of discourse.
- $\exists_x \; P(x)$ i.e. for at least one value of x, P(x) is true.

**Negation**
$$\neg [\forall_x \; P(x)] \equiv \exists_x \; \neg P(x)$$
$$\neg [\exists_x \; P(x)] \equiv \forall_x \; \neg P(x)$$

> [!Tip]
> Read from left to right, when writing in first order predicate logic.

### Conjunctive Normal Form

A function is in CNF or clausal normal form if it is a conjunction of one or more clauses. (where clause is disjunction of literals). It is *AND of ORs*.

### Rules of Inference

Four different methods to deal with quantified sentences in first order logic.

1. **Universal instantiation / Universal specialization  / Universal elimination**
	- If "everyone likes ice cream", then "john likes ice cream".
	- The UI rule state that we can infer any sentence $P(c)$ by substituting a ground term $c$ (a constant within a domain x) from $\forall_x \; P(x)$ for any object in the universe of discourse.
	$$\frac{\forall_x \; P(x)}{P(c)}$$
2. **Existential instantiation**
	- "there exists a person who likes pizza" means "$c$ likes pizza".
	- This rule states that one can infer $P(c)$ from formula $\exists_x \; P(x)$ for a constant symbol $c$.
	$$\frac{\exists_x \; P(x)}{P(c)}$$
3. **Existential generalization / Existential introduction**
	- If "Priyanka got good marks in English", then "someone got good marks in English".
	- If there is some element $c$ in the universe of discourse which has a property $P$, then we can infer that there exists something in the universe which has a property $P$.
	$$\frac{P(c)}{\exists_x \; P(x)}$$
4. **Universal generalization / Universal introduction**
	- If "A byte contains 8 bits", so for all values of x "All bytes contain 8 bits".
	- If premise $P(c)$ is true for any arbitrary element $c$ in the universe of discourse, then we can have a conclusion as $\forall_x \; P(x)$
	$$\frac{P(c)}{\forall_x \; P(x)}$$
## Forward and Backward Chaining

| Forward Chaining                                                       | Backward Chaining                                                              |
| ---------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| Begins with what is known (basic facts)                                | Starts with a goal                                                             |
| Moves forward (applies rules to these facts to derive new conclusions) | Moves backward (checks if current knowledge proves goal)                       |
| **Data-driven**                                                        | **Goal-driven**                                                                |
| Adds Knowledge                                                         | Deduces necessities (conditions for goal)                                      |
| Stops when no further deductions can be made or goal is reached.       | Stops when it reaches beginning facts or rules, or goal is proven / disproven. |
| Bottom-up                                                              | Top-down                                                                       |
| **Modus Ponens** $(P \to Q) \wedge (P) \equiv Q$                       | **Modus Tollens** $(P \to Q) \wedge (\neg Q) \equiv \neg P$                    |
| Common in real-time systems and production rule system.                | Used in diagnostic systems.                                                    |

## Resolution

- Resolution in Al is a logical inference rule used to deduce new information or solve problems by **finding contradictions**.
- It involves converting logical statements into a standardized form called *clausal form*, which is a set of normalized logical expressions.
- ﻿﻿Contradictory pairs of clauses are identified, and through a process of unification and combination, new clauses are generated.
- ﻿﻿This process is repeated iteratively until either a contradiction is found (represented by an G empty clause) or no new information can be deduced.
- Resolution is particularly powerful in automated theorem proving and logic programming, such as in Prolog, where it's used to infer conclusions from given facts and rules.
- Eg: "all birds fly" and "tweety is a bird". Now we contradict that "tweety can't fly".

## Knowledge Acquisition

- Gathering expertise for use in expert systems, organizing it into structured formats like IF-THEN rules.
- Also refers to absorbing information into memory (knowledge base) and focusing on effective retrieval.
- Gather information via Introspection, Observation, Induction, Protocol analysis, Prototyping, Interviewing.

**Procedure**

- *Identification*: breaks down complex issues into parts
- *Conceptualization*: define key concepts
- *Formalization*: organize knowledge formally for programmatic use
- *Implementation*: code the structured knowledge
- *Testing*: check and validate system's functionality

## Knowledge Representation

Study of how knowledge can be represented in computer system to mimic human thought and reasoning.

- Facts: true information.
- Representation: formal expression of facts.

Ex: "Charlie is a dog" => logical representation $Dog(Charlie)$

**Characteristics**

- *Syntax and semantics*: clearly defined rules for structure and meaning.
- *Expressive capacity*: ability to convey all necessary domain knowledge.
- *Efficiency*: supports effective computing and reasoning.

### Techniques

- **Logic-based representation**
	- **Propositional Logic**: uses simple true or false statements
	- **Predicate Logic**: extends propositional logic with predicates that can express relations among objects and quantifiers to handle multiple entities.
	- Eg: "all humans are mortal" -> $\forall_x \; (Humans(x) \to Mortal(x))$
- ## **Semantic Network**
	- Graph structures used to represent semantic relations between concepts.
	- *Nodes* represent objects.
		- Circle (physical)
		- Ellipse (concept)
		- Rectangle (situation)
	- *Arcs / Edges* represent relations between them. (links, arrows)
	- *Link labels* specify relationships.
	- Popular in AI and NLP. It represents knowledge or support reasoning. Alternative of predicate logic.
	- Eg: "Socrates" is a "Human" and "Humans" are "Mortal".
	- **Components**
		1. **Lexical Components**: Nodes, links, labels.
		2. **Structural**: links or nodes (directed)
		3. **Semantic**: definition related to links or node.
		4. **Procedural**: constructor (creating new links) and destructor (removing new links)
- **Frame-based representation**
	- Uses data-structures called frames, which are similar to objects in OOPS.
	- Frames allow grouping of related properties and actions.
	- Eg: "Bird" has properties "has feathers" and "can fly" and actions like "Lay eggs".
- **Production Rules**
	- Consists of sets of rules in the form of IF-THEN constructs that are used to derive conclusions from given data.
	- Eg: IF hungry THEN eat food.
- **Ontologies**
	- Formal representations of set of concepts within a domain and relationships between those concepts. They are used to reason about entities within that domain and are often employed in semantic web applications.
	- Eg: In medical ontology, concepts like "symptom", "disease" and "treatment" might be related in ways that define what symptoms are commonly associated with a disease.
- **Bayesian Network**
	- Probabilistic models that represent a set of variables and their conditional dependencies via a directed acyclic graph (DAG). These are useful for handling uncertainty in AI applications.
	 - Example: A network might represent the probabilistic relationships between diseases and symptoms, allowing the system to infer disease probabilities given observed symptoms.
- **Neural Network**
	-  Although typically classified under machine learning, neural networks can represent complex relationships between inputs and outputs through learned weights and can effectively capture and model knowledge after training.
	- Example: A neural network trained on historical weather data might predict future weather conditions.

## Architecture of Knowledge Base System

KBS is a system that draws upon knowledge of human experts captured in knowledge base to solve problems that normally require human expertise.

**Components**
1. **Knowledge base**: centralized repository of information, organized facts, heuristics, etc.
2. **Inference Engine**: Acquires and manipulates knowledge from knowledge base to arrive at a particular solution.
3. **User Interface**: Enables user to interact with knowledge base.

## Knowledge Types

1. **Procedural knowledge** (Imperative)
	- Describes *how* to solve a problem
	- Rules, strategies, tasks, etc.
2. **Declarative Knowledge** (descriptive)
	- Describes *what* is known about a problem
	- Concepts, facts, objects, etc.
3. **Meta Knowledge**
	- Describes another knowledge
4. **Heuristic Knowledge**
	- Describes knowledge of some experts in a field. (rule of thumb)
	- Past experience, approaches, etc.
5. **Structural Knowledge**
	- Describes relationships between various concepts
	- Describes expert overall mental model of a problem.

## Frames

Collection of attributes or **slots** and associated values that describe some **real-world entity**.

- Uses data-structure (records) to represent the knowledge represented in semantic N/W.
- Each frame represents nodes as a class or an instance and each relation as slot.

**Attributes attached with each slot**

1. Instance - related slot with class
2. Definition - slot value
3. Default - slot default value
4. Domain - slot elements domain
5. Range - specifies class of which elements
6. Range constraints - logical expression $6 \lt i \lt 10$
7. To-compute - value of slot to be computed
8. Single-values - function returns single value
9. Inverse - slot inverse used in reasoning
10. Transfers-though - inheritance

**Reasoning actions that can be performed using frames**

1. *Relating the definition*: "is an inverse link" propagation of definition to relate all information.
2. *Inheritance*: inherited all values (including default) of slot.
3. *Legality of value*: range constraint.
4. *Consistency check*: verify slot value consistency before adding to frame. (domain)
5. *Maintaining consistency*: when one slot is updated its inverse should also be updated.
6. *Computation of value of slot*: to-compute transfers through.

## Baye's Theorem

Describes the probability of an event, based on prior knowledge of conditions that might be related to the event.

In Probability theory it relates the conditional probability and marginal probability of two random events.

> **Conditional Probability**
> $$P(H/E) = \frac{\text{number of times H and E occured}}{\text{number of times E occured}} = \frac{P(H \; \cap \; E)}{P(E)}$$

Calculate $P(B / A)$ with the knowledge of $P(A / B)$

> **Baye's Theorem**
> $$P(A/B) = \frac{P(B/A) \cdot P(A)}{P(B)}$$
> $P(A/B)$ is *Posterior* (prob. of A when B is true)
> $P(B/A)$ is *Likelihood* (prob. of evidence)
> $P(A)$ is *Prior probability* (prob. of hypothesis)
> $P(B)$ is *Marginal probability* (prob. of evidence)

**Applications**
- Robot / automatic machines
- Forecasting weather
- Monty Hall Problem

## Bayesian Belief Network

It is a probabilistic graphical model which represents a set of variables and their conditional dependencies using a DAG.

Consists of **DAG** and **table of conditional probabilities** (with effect of parent node).

- Node -> random variable (continuous or discrete)
- Arc / Directed arrows -> casual relationships or conditional probabilities among random variables.

To propagate a belief in Bayesian N/W, initial DAG is converted to undirected-graph in which arcs can be used to transmit probabilities of direction of evidence.

## Fuzzy Logic System

**Fuzzy Set Theory** - Mathematical tool for dealing with concepts used in natural language.

**Fuzzy Logic** - Multivalued logic that allows intermediate logic values to be defined between conventional equations. (resembles human reasoning involving possibilities b/w YES and NO).

Mathematical tool to represent uncertainty and vagueness.

**Characteristics**
- Exact reasoning is viewed as limited case of approximate reasoning.
- Everything is a matter of degree.
- Knowledge is represented as collection of variables.
- Any logical system can be fuzzified.

### Architecture

![[Pasted image 20250516231523.png]]

1. **Fuzzifier**
	- It transforms the system inputs, which are crisp numbers, into fuzzy sets. It splits the input signal into five steps.
		- LP - Large positive
		- MP - Medium positive
		- S - Small
		- MN - Medium negative
		- LN - Large negative
2. **Intelligence (Inference Engine)**
	- It simulates the human reasoning process by making fuzzy inference on the inputs and IF-THEN rules.
	- Determines matching degree of inputs w.r.t rules.
3. **Fuzzy Rule Base**
	- Set of rules and IF-THEN conditions provides by experts to help decision making.
4. **Defuzzifier**
	- It transforms the fuzzy set obtained by the inference engine into a crisp value.

## Membership function in Fuzzy Systems

**Degree of Truth:** Generalizes the classical “indicator” function (0 or 1) to a continuous scale $[0,1]$.
**Vagueness & Uncertainty:** Captures how strongly a given crisp input $x$ belongs to a fuzzy set $A$.
**Human‑style Reasoning:** Enables inference with partial truths (“somewhat hot,” “very tall,” etc.).

#### Mathematical Notation

A fuzzy set $A$ over universe $X$ is written as:
$$A = \{\, (x,\;\mu_A(x)) \mid x\in X \}$$
> $\mu_A: X \to [0,1]$ is the **membership function**
> $X$ is **membership space** (universe of discourse)
#### Key Features

For any fuzzy set $A$ with membership function $\mu_A(x)$:

| Feature                      | Definition                       | Notation                 |
| :--------------------------- | :------------------------------- | :----------------------- |
| **Support**                  | All $x$ with non‑zero membership | $\{x\mid \mu_A(x)>0\}$   |
| **Core**                     | All $x$ fully in the set         | $\{x\mid \mu_A(x)=1\}$   |
| **Crossover** (α‑cut at 0.5) | All $x$ where $\mu_A(x)=0.5$     | $\{x\mid \mu_A(x)=0.5\}$ |
| **Boundary**                 | Region between support and core  | $\{x\mid 0<\mu_A(x)<1\}$ |

![[Pasted image 20250517002441.png]]

**Types of Membership function**
![[Pasted image 20250517002459.png | 450]]

---
## Learning

- Learning is Specialized form of knowledge acquisition.
- fact 1 --> fact 2 --> conclusion.
- It is constructing or modifying representation of what is being experienced.

**Components of Learner system**

1. **Learning component** - (Main) Acquire knowledge, make changes/improvements to system depending on performance.
2. **Performance component** - Task is performed by choosing action to be taken.
3. **Problem Generator** - Suggests problems or actions that would lead to generation of new examples to improve learning.
4. **Critic** - gives feedback to the learner system.

**Learning can be achieved by**

- Taking advice
- observations
- examples
- direct instructions
- analyzing differences
- deduction
- explaining experience
- using relevant information
- correcting mistakes
- by recording cases

### Prologs

**Facts** - describe explicit relationship. eg: "megha is a girl"
**Rules** - defines implicit relationships. eg: "megha is a daughter of shaam if shaam is a father of megha"
**Queries** - by asking questions. eg: "is megha daughter of shaam?"

- Names of properties/relationships begin with lowercase letters.
- Relationships must appear at first.
- A period "." should end a fact.
- Objects also begin with lower case letters, digits or string.
- Eg: "color(pink, red)" is a clause

```prolog
:-  ==>  if or implied by
,   ==>  and / conjuction
;   ==>  or / disconjuction
/== ==> not equals to
? - ==> query
```

**Rules**
X is the father of Y if X is a parent of Y and X is a male.

```
father(X, Y) :- parent(X, Y) , male(X).
```

**Goals or Query**

 Is pizza a food ?
```
? - food(pizza).
```

## Conceptual Dependency

Conceptual dependency is a theory by schank , tells us about how to show the type of knowledge in events ,usually found in natural language sentences . shows knowledge in a way that : 

1. Helps make conclusions from the sentence 
2. Doesnt depend on the language of the sentence .

Conceptual primitives : determines the action taken to execute a statement 

1. ATRANS: Abstract transfer 
2. PTRANS : Physical transfer 
3. PROPEL ,MOVE ,INGEST , SPEAK etc

ex) man took a book from someone

Idhar p matlab person , o matlab object , atrans matlab ek abstract concept(book) ka transfer hua h

ADVANTAGE:
- Using these primitives involves fewer inference rules
- Many inference rules are alr present in conceptual dependency structure
- Holes in initial structure helps us to focus on points yet to be established 
DISADVANTAGE:
- Knowledge must be decomposed to low level primitives
- Difficult to find correct set of primitives 
- Lot of inference may still be required (despite being fewer than original)
- Requires lot of storage due to complex representations 

## Non-monotonic reasoning

## Confusion Matrix

## Neural Network

### Genetic Algorithm

![[Pasted image 20250517201443.png | 500]]

---
# IMPORTANT

- syllabus for AI  for end sem For clarification, solving/numerical type question for end sem can be taken from Propositional/Predicate Logic, Neural Networks.
- Small numerical from Genetic algorithms, probabilistic reasoning/certainty factors . 
- Rest Unit 3 part b, unit 4 and unit 6 will be covered as theoretical short note type questions.
 - 10-15 marks from midsem syllabus will be there in end sem.


