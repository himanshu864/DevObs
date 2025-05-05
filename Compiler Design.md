#core 

![[Screenshot 2025-02-28 at 10.14.57 AM.png | 600]]

---

***Compiler*** is a software that translates high level language into low level machine code (for processor).

# UNIT 1

## Language Processing System (LPS)

1. **Preprocessor** → strips/expands directives → **pure source code (HLL)**
2. **Compiler** → transforms source to assembly/machine code in several phases (lex, parse, semantic checks, IR, optimization, code generation) → **assembly code** (or directly object code)
3. **Assembler** → translates assembly to **object code** (multiple relocatable m/c)
4. **Linker** → merges object files/libraries, resolves symbols → **executable** (single m/c)
5. **Loader** → places executable into memory, prepares to run. -> **.exe**

**Preprocessors**
Handles directives before compilation. (`#include`, `#define` in C/C++)

  1. Macro expansion (`#define` → inline code/text).  
  2. File inclusion (`#include` → copy/paste file content).  
  3. Conditional compilation (`#ifdef`, `#if`, etc.).

No computation only substitution.

---
## Compiler vs Interpreter

Files are in HDD. Compilers/interpreter in Main memory (RAM). And CPU handles execution.

**Compiler**

- Converts full source code into machine code (e.g., generates a **.exe** file).
- **.exe** runs independently without the compiler or source code.
- Faster execution post-compilation.
- Requires more space.
- Detects errors at compile-time (no execution).
- Typically platform-specific.
- C/C++.

**Interpreter**

- Executes code line-by-line; no standalone output file.
- Requires source code and interpreter at runtime.
- Slower execution due to on-the-fly translation.
- Detects errors during execution (previous lines have been executed).
- More portable across platforms if a compatible interpreter is available.
- Javascript (browser).

---
## Phases of Compiler

![[Pasted image 20250228115945.png]]

**1. Lexical Analysis**  
- Converts a stream of characters (pure HLL i.e. $x = y + z * 60$) into a stream of *tokens* using DFAs.
- All identifiers are stored in a symbol table after tokenization.

**2. Syntax Analysis**
- Parses tokens and builds a parse tree/AST (abstract syntax tree) using grammar rules.

**3. Semantic Analysis**
- Checks semantic rules (types, scopes, and context) to construct a semantically verified parse tree.
- Semantic Rules:
	1. Type checking.
	2. Undeclared variable detection.
	3. Multiple declaration prevention.
- Uses the symbol table to analyze in a bottom-up fashion.

**4. Intermediate Code Generation**
- Translates the AST into a platform-independent *IR* (Intermediate Representation).
- E.g., generates three-address code (TAC).

**5. Code Optimization**
- Refines the IR by eliminating redundancies and improving performance.
- Produces an optimized version of TAC.

**6. Target Code Generation**
- Converts the optimized IR into assembly/machine code (e.g., produces an executable).

> [!Note]
> These phases/functions do not run sequentially. Like code snippets, they are called upon whenever needed.

**Error Handling:**
Detects invalid or unrecognized sequences and flags errors early in the compilation process.

**Symbol Table Integration:**
Identifiers encountered during scanning are stored in a symbol table along with metadata (such as type and scope). This aids later phases in semantic analysis.

---
## Lexical Analyzer

- **Lexemes:** The actual sequences of characters that form meaningful units (e.g., `x`, `+`, `60`).
- **Tokens:** Pairs or tuples typically represented as `<token_type, token_value>` (e.g., `<id, 1>`, `<operator, +>`).
- **Patterns:** Defined using regular expressions that specify the format of each token type (identifiers, numbers, keywords, etc.).

1. Converts a raw stream of characters from the source code into a structured stream of tokens, which are easier for the parser to handle.
2. Tokens include *identifiers* (variables, function names), operators (`+`, `=`), keywords, symbols, literals, and constants (e.g., int, float).
3. LA eliminates comments and white spaces from program.
4. Gives error message by providing row no. and column no.

**Process Flow Example:**
- Source Code: `x = y + z * 60`
- Lexical Analysis: Reads characters, identifies lexemes (`x`, `=`, `y`, `+`, `z`, `*`, `60`).
- Generates tokens: `<id,1>`, `<assign>`, `<id,2>`, `<operator, +>`, `<id,3>`, `<operator, *>`, `<constant, 60>`.
- Stores identifiers (`x`, `y`, `z`) in the symbol table with `S.No, variable_name, type`.

### Count no. of tokens

1. LA uses DFA to perform tokenization.
2. During tokenization, LA always prioritizes *longest matching*.
3. Doesn't care for syntax or semantic errors.

Example of tokens
```
int
main
{
"adsf asdf2343529 f"
93
i
=
0
;
return
)
,
++
<=
**c -> 3 tokens
in t -> 2 tokens
in/*comment line*/t -> same as above
=== -> 2 tokens
"hello -> token error
```

---
## Ambiguous Grammar

A grammar is ambiguous if a string can have multiple valid derivation trees (via LMD or RMD).
Example:
- `E -> E + E | id`
- The string `id + id + id` can be parsed in two different ways using only leftmost derivation.

### Ambiguous to Unambiguous Grammar

Ensure a single, unique parse tree by enforcing operator *precedence* and *associativity*.

We need to process operators with higher precedence and associativity first. i.e. should be lower down the parse tree.

Eg: for `E -> id + id + id`

```
E -> E + E  | id    # is ambiguous
E -> E + id | id    # unambiguous

Left recursive grammar since '+' operator has L->R associativity
```

||ly for `E -> id + id * id`

```
E -> id + T | T
T -> T * id | id

Right recursive since '*' operator has higher precedences
```

### Remove left recursion

Eg: `L -> L + S | S`

Becomes
```
L -> SA
A -> +SA | E
```

### Removing left factoring

Eg: `A -> aB1 | aB2 | aB3`

Becomes
```
A -> AB
B -> B1 | B2 | B3
```

Just take common prefix.

---

# UNIT 2

## Parser (Syntax Analysis)

Transforms the stream of tokens into a structured, hierarchical parse tree or AST that represents the program's grammatical structure.

- **Top-Down Parsing:**
	- Uses recursive descent or LL(1) methods.
	- Starts with the start symbol and breaks down the input via productions.
	- Simple to implement but may require grammar modifications (e.g., eliminating left recursion).
	
- **Bottom-Up Parsing:**
	- Uses shift-reduce techniques like LR, SLR, LALR, or LR(1).
	- Starts with the input tokens and reduces them to the start symbol.
	- Handles a wider range of grammars with fewer modifications.

None accept ambiguous grammar.

![[Pasted image 20250228163405.png]]

#### LL(1)
- First L represents: reading left to right.
- Second L represents: LMD.
- (1) is for processing one token at a time.

#### Top-Down
- Derive word from start.
- Replace $\alpha$ with $\beta$.
- Hard to choose between $\beta$.
- LMD

#### Bottom-Up
- Derive start from word.
- Replace $\beta$ with $\alpha$.
- RMD in reverse.

#### Recursive Descent Parser

- **Top-Down Approach:** Implements each non-terminal as a recursive function.
- **Structure:** Functions call one another based on grammar rules.
- **Applicability:** Works well for LL(1) grammars (no left recursion, clear first sets).
- **Limitations:** Cannot handle left-recursive grammars without modifications; may require backtracking for ambiguous rules.

---
## First and Follow

#### FIRST Set

The set of terminals that can appear as the first symbol in some string derived from a non-terminal.
Build bottom to top.

1. **For a Terminal:**  
   - **Rule:** If X is a terminal, then **FIRST(X) = { X }**.

2. **For a Nonterminal:**  
   - **Rule:** If X is a nonterminal, then **FIRST(X)** is the set of terminals that begin the strings derivable from X.
   - **Procedure:**  
     - For every production **X → Y₁ Y₂ ... Yₙ**:
       - Add all symbols in **FIRST(Y₁)** (except ε) to **FIRST(X)**.
       - If **FIRST(Y₁)** contains ε, then include **FIRST(Y₂)** (except ε).  
       - Continue this process until you reach a Yᵢ that does not derive ε, or you have processed all symbols.
       - If all Yᵢ (i = 1 to n) derive ε, then add ε to **FIRST(X)**.

3. **For the Empty String:**  
   - **Rule:** If a nonterminal can derive the empty string (ε), then ε is included in its **FIRST** set.

#### FOLLOW Set

The first of what's immediately after every non-terminal's occurrence.
Build top to bottom.

1. **Start Symbol:**  
   - **Rule:** For the start symbol S, add the end-of-input marker `$` to **FOLLOW(S)**.

2. **For Productions:**  
   - **Rule:** For *every* production **A → αBβ**:
     - Add all non-ε symbols in **FIRST(β)** to **FOLLOW(B)**.
     - If **β** can derive ε (i.e., **FIRST(β)** contains ε) or if B is at the end of the production, add **FOLLOW(A)** to **FOLLOW(B)**.

3. **For Productions Ending with a Nonterminal:**  
   - **Rule:** If a production is of the form **A → αB** (i.e., B is the last symbol), then add **FOLLOW(A)** to **FOLLOW(B)**.

---
## LL(1) Parser

A top-down parser that scans input Left-to-right, produces a Leftmost derivation, and uses 1-token lookahead.

**Grammar Requirements:**
- Must be free of left recursion.
- Should be left-factored to avoid ambiguity.

**Building the LL(1) Parsing Table:**
- **For each production A → α:**
	- For every terminal a in **FIRST(α)**, add A → α to table entry M[A, a].
	- If ε ∈ **FIRST(α)**, then for every terminal b in **FOLLOW(A)**, add A → α to M[A, b].
	- Keep putting $\epsilon$ on right hand side as long as NULL and add firsts.
	- Include M[A, $] if ε ∈ **FIRST(α)** and $ ∈ **FOLLOW(A)**.
- The table must have at most one production per cell; conflicts indicate the grammar is not LL(1).

![[Screenshot 2025-03-02 at 4.02.02 PM.png]]

**Parsing Process:**
- Initialize a stack with the start symbol and end marker `$`.
- Read the lookahead token.
- **If top of stack is:**
	- A terminal matching the lookahead: Pop it and advance the input.
	- A nonterminal: Consult the table; push the production’s right-hand side (in reverse order) if found.
	- An error if no matching entry exists.
- Repeat until the stack is empty and input is fully consumed.

![[Screenshot 2025-03-02 at 11.20.57 AM.png]]

**Error Handling:**
When a table entry is empty, report a syntax error and apply recovery strategies if needed.
**Advantages:**
Simple, efficient, and easy to implement for LL(1) grammars.
**Limitations:**
Only works with grammars that are LL(1); may require grammar modifications for others.

### Steps to Check if a Grammar is LL(1):

![[Screenshot 2025-03-01 at 11.42.29 AM.png | 500]]

---

## Bottom Up Parser
- Processes input left-to-right, constructing a rightmost derivation in reverse.
- Uses **shift** (push tokens onto a stack) and **reduce** (collapse symbols using grammar productions) operations.
- Typically driven by a parsing table (ACTION and GOTO) and a stack.
- Capable of handling more complex grammars than many top-down methods.
- Can work with left recursive and non-deterministic grammar. No backtracking.

## LR(0)

A type of bottom-up parsing that uses **LR(0) items**—productions with a dot indicating how much of the production has been seen (shifted).

**LR(0) Items**
- A production with a dot (·) indicating parsing progress.
- Example: For `A → BC`, items are:
  - `[A → · BC]`
  - `[A → B · C]`
  - `[A → BC ·]`

**closure(I)**
1. Start with a set of LR(0) items **I**.
2. For each item `[A → α · B β]` in **I**, add `[B → · γ]` for every production `B → γ`.
3. Repeat until no new items can be added (included added productions).

**goto(I, X)**
1. For each item `[A → α · X β]` in **I**, move the dot past **X** to form `[A → α X · β]`.
2. Collect all such items into a new set **J**.
3. Apply **closure(J)** to get **goto(I, X)**.

#### LR(0) Parsing Table Construction

- **Augment Grammar:**
	- Add $S' \to S$.
- **Build States:**
	- Start with $I_0 = closure({S' \to \cdot S})$.
	- For each state $I$, compute $goto(I, X)$ for every symbol $X$ to generate new states.
- **ACTION Table:** (contains shift and reduce operations over terminal)
	- If an item in $I$ is $A \to \alpha \cdot a \beta$, set ACTION[I, a] to "*shift* to $goto(I, a)$".
	- If an item in $I$ is $A \to \alpha \cdot$, for every terminal $t$, set ACTION[I, t] to "*reduce* by $A \to \alpha$".
	- For $I$ containing $S' \to S \cdot$, set ACTION[I, \$] to "accept".
- **GOTO Table:** (contains only shift operations over non-terminals)
	- For each nonterminal $B$, if $I$ has an item $A \to \alpha \cdot B \beta$, set GOTO[I, B] to $goto(I, B)$.
- **Conflict Check:**
	- Ensure each cell in the tables has only one action; multiple actions mean the grammar is not LR(0).

![[Screenshot 2025-03-02 at 12.09.18 PM.png]]

- **Initialize:**
    - Stack: [0]
    - Append $ to input.
- **Repeat until done:**
    1. Let current state = top of stack; current token = lookahead.
    2. **Shift (push):**
        - If ACTION[state, token] = "shift s":
            - Push token, then state s.
            - Advance input.
    3. **Reduce (pop):**
        - If ACTION[state, token] = "reduce by A → α":
            - Pop 2×|α| items (double length of RHS).
            - Let t = new top (number); push nonterminal A, then push *$GOTO[t, A]$.*
    4. **Accept/Error:**
        - If ACTION[state, $] = "accept": parsing succeeds.
        - Otherwise, if no valid action, signal error.
- **End:**
    - Parsing completes when the accept action is reached.

![[Screenshot 2025-03-02 at 2.51.52 PM.png | 600]]

> [!Note]
> Shift items together if same goto non-terminal.

---
## SLR(1) Parsing

SLR(1) (Simple LR with 1 lookahead) extends LR(0) by using FOLLOW sets to decide reduce actions.

**SLR(1) Parsing** is built the same way as **LR(0)** parsing, with one key difference.

For an item $A \to \alpha \cdot$, instead of *reducing* on all terminals, add a reduce action only for terminals in $\text{FOLLOW}(A)$.

> LR(0) $\in$ SLR(1) but not vice-versa.

> [!Tip]
**Inadequate State**: Any state where there exists either $S-R$ (shift-reduce) or $R-R$ conflict.

---
## CLR(1)

Most powerful LR Parser with *look ahead symbols*. Same as SLR(1) just calculate FOLLOW of each production at *runtime*.

- **Build Canonical LR(1) Items:**
    - Items are of the form $[A \to \alpha \cdot \beta, a]$, where $a$ is a lookahead.
    - **Closure:** For $[A \to \alpha \cdot B \beta, a]$, add $[B \to \cdot \gamma, b]$ for every production $B \to \gamma$ and each $b \in FIRST(\beta a)$. (find follow of first B, right next to dot which called it, and no other occurrence)
    - **Goto:** For each item $[A \to \alpha \cdot X \beta, a]$, shift the dot over $X$ to form $[A \to \alpha X \cdot \beta, a]$, then take closure. (carry previous follow)
	
Fill the table just like we did in SLR(1) just use calculated follow for reduction.

---
## LALR(1)

Minimized from of CLR(1). Less powerful. We merge same states with different look ahead symbols.

![[Screenshot 2025-03-02 at 5.56.48 PM.png]]

---
## Operator Precedence Grammar

An operator precedence grammar is a CFG where productions do not have adjacent nonterminals, allowing clear specification of precedence and associativity among terminal operators.

- **Precedence Relations:**
    
    - **Equal Precedence ($\doteq$):** Operators at the same level.
    - **Lower Precedence ($\lessdot$):** The left operator yields to the right operator.
    - **Higher Precedence ($\gtrdot$):** The left operator takes precedence over the right.
- **Parsing Mechanism:**
    
    - A parser uses a precedence table based on these relations to decide when to shift (read new input) or reduce (apply a production), especially for arithmetic expressions.
- **Advantages & Limitations:**
    
    - **Advantages:** Simple and efficient for expressions with defined operator hierarchies.
    - **Limitations:** Applicable only to grammars meeting specific constraints (e.g., no adjacent nonterminals, no ε-productions).