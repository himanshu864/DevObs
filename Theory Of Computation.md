#core

**Finite Automata**: Abstract Machine to recognise patterns in strings of symbols by observing changes in state in response to external inputs.

Consists of finite set of state and set of transition.
Take input string and checks if it's part of a grammar.

**Deterministic FA**:
> `(Q, ∑, ð, S, F)`
>  Q : finite non empty states
>  ∑ : finite input alphabets
>  ð : transition function ; `ð : (Q x ∑ -> Q)`
>  S : initial state
>  F : set of final states

**Non - DFA**:
> `(Q, ∑, ð, S, F)`
>  ð : transition function ; `ð : (Q x ∑ -> 2^Q)`

- Easier to design
- Incomplete
- No dead state
- Every DFA is NFA, but not vice-versa
- Same language accepting power. Recognise regular language

Theoretical machine allows set of possible moves. Hence, different results for same transition.

### Convert NFA to DFA
- Initial State and input alphabets remain the same
- Make *transition* *table* and consider *union* as new states
- All states with NFA final states will be final state here,

![[Screenshot 2024-09-24 at 12.34.45 PM.png]]
![[Screenshot 2024-09-24 at 12.34.59 PM.png]]

**NFA with Epsilon Move (€ - NFA)**: Null - NFA
- allows transition of empty string. (null - transition)

> `(Q, ∑, ð, S, F)`
> ð : transition function ; `ð : (Q x (∑ U €) -> 2^Q)`

- *Null Closer (€\*)* : set of all states which are zero distance from state Q.

### Convert €-NFA to NFA
> ð(q, a) = €-closure[ ð[€-closure(q) , a] ]

- Make transition table for states
- To find ð(q, a) for a state Q.
	- Find null closer of state `Q`
	- Find transition of null closers on `a`
	- again find null-closer for result states.
	- Or simply use common sense to check where can `Q` go using only one `a`
- Do the same for all states.

![[Screenshot 2024-09-24 at 1.23.22 PM.png]]
To convert transition table to state. Read that ð(A, 0) goes to A, B, and C. and so on.

Note:
- €-closure(ø) = ø
- No change in initial state
- no change in total no. of states
- All states will be final state in resulting NFA whose €-closure contains at least one final state in initial €-NFA

### Moore Machine
- No final state or dead state. Generates output
- Moore and Mealy equivalent in power

> `(Q, ∑, O, δ, λ, q0)`
>  Q: set of finite states  
>  ∑: input alphabets
>  O: output alphabet  
>  δ: transition function where `Q × ∑ → Q`
>  λ: output function where `Q → O`
>  q0: initial state

- *Output is associated with state*
- Responds to null-string
- *Asynchronous*. Input - n. Output - n + 1

![[Pasted image 20240924140030.png]]
![[Pasted image 20240924135508.png]]
**To Construct Moore Machine from Transition Table**
1. Start at initial state
2. Generate output
3. Transition to next state and output
4. Repeat step 3

### Mealy Machine
> `(Q, ∑, O, δ, λ, q0)`
>  λ: output function where `Q x ∑ → O`

- *Output is associated with transition*
- doesn't respond to empty string
- *Synchronous*
![[Pasted image 20240924140347.png]]
![[Pasted image 20240924140354.png]]

### Convert Moore to Mealy
- Push output of state onto incoming transition
- same no. of states
### Convert Mealy to Moore
- push output from transitions to upcoming state.
- Since same states with have different transition outputs, *split states*.
- No. of states will increase

## Minimization of FA
To eliminate all non-productive state and achieving a *unique* DFA of that language.
- *Don't* remove *dead* states since completes system
- Remove all *unreachable* states (from initial state)
- Group all final and non-final states into two sets
- Connect all transitions from set to set
- Keep separating states who act differently from other states in same set
- Finally remove all *equal* *states*, who act the same way in the same.
- Remove a state by removing it's outgoing transition and self looping incoming transitions

### Myhill-Nerode Theorem
Table Filling Method: Minimization of DFA
![[Pasted image 20240924151940.png]]
1. Draw table for all pairs of states
2. Mark all pairs where one of the states is final and other one is non-final
3. Mark all unmarked pairs [P, Q] where [δ(P, a), δ(Q, a)] is marked
4. Combine all unmarked pairs into single states

# Regular Expression
- R = a + b denotes L = {a, b}
- R = a.b denotes L = {ab}
- R = a$^*$ denotes L = {€, a, aa, aaa, ...} - Kleene's Closure
- R = (a + b)$^3$ denotes L = {aaa, aab, aba, ... , bbb}
- R = {a + b}$^*$ denotes L = {a, b}* i.e. {€, a, b, aa, ab, bab, ...}

> a$^+$ = a.a$^*$
> Positive closure

#### Arden's Theorem
Mechanism for constructing R.E from FA
- Write down all expressions for every state of DFA using incoming transitions
- For **R = Q + RP**, If P 
	- is free from Null. **R = QP$^*$**. Unique Solution
	- contains Null. Infinite solutions
- Solve expressions

# Pumping Lemma
Used to prove irregularity of language

For any regular language L, there exists an integer n, such that for all Z ∈ L with |Z| ≥ n, there exists u, v, w ∈ Z$^*$, such that Z = uvw and
- |uv| ≤ n
- |v| ≥ 1
- for all i ≥ 0 : uv$^i$w ∈ L

If any i exists where uv$^i$w doesn't belong to L, the language is irregular.

### Decision Properties
1. **Emptiness** : (if accepts any string. Final state exists)
2. **Non** **Emptiness**:
	- Remove all unreachable states
	- If resulting machine contains even one final state. FA is non-empty
	- Otherwise FA is empty.
1. **Finiteness**
2. **Infiniteness**: (if contains any loop)
3. **Membership**: (property to verify if string is accepted by FA or not)
4. **Equality**: (if two FA accept same language. i.e. same Minimal FA)

### Grammar
- Mathematical Model for generating language
> `(Vn, T, P, S)`
> Vn : Variable : Non-terminal : A, B, C ...
> T : Terminals : a, b, c ...
> P : Production Rules : finite set of rules whose elements are α → β | α, β ∈ Vn U T
> S : Special Start Symbol

### Chomsky's Classification of Grammar
1. **Type 0**: Unrestricted / Phase structured / recursively enumerable grammar
	- No restriction.
	- Accepted by Turing machine
> α → β
> α  = (Vn U T)$^*$ Vn (Vn U T)$^*$
> β  = (Vn U T)$^*$

2. **Type 1**: Context sensitive Grammar
	- Accepted by Linear Bounded automata
> α → β
> α  = (Vn U T)$^*$Vn(Vn U T)$^*$
> β  = (Vn U T)$^*$
> |α| ≤ |β|

1. **Type 2:** Context Free Grammar (CFG)
	- accepted by push down automata
	- Only one terminal on LHS
> α → β
> α  = Vn
> β  = (Vn U T)$^*$
> |α| = 1

4. **Type 3**: Regular Grammar
	- generated by regular language, and accepted by finite automata
	- Left Linear or Right Linear
> α → β
> |α| = 1
> A -> aA | a
> A -> Aa | a

#### Ambiguous Grammar
Type 2 or above
- CFG is ambiguous if there exist more than one derivation tree for any string.
Example: S -> aS / Sa / a
- CFG will both left and right recursion is bound to be ambiguous

**Simplification / Minimization of CFG**
- Removal of Null-production
- Removal of Unit-production
- Removal of Useless-production: unreachable and dead
