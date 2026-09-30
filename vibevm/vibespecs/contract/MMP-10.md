# MMP.10 - Construct and Revise a Mathematical Constraint Formulation {#root}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Working sections of the pattern; its depth sections live in the source document named by the last line. See LICENSE.md for the list of changes.

> **Type:** Method pattern
> **Status:** Usable, evolving
> **Normativity:** Normative within the stated use

## MMP.10:1 - Problem frame {#problem-frame}

Use this pattern when you know conditions that a possible object or situation must satisfy, but still need to express its possibilities mathematically. You may be looking for an arrangement, a quantity, a shape or a rule of action. Choosing variables already makes decisions: a number can express an amount, but an ordered list, a set of members and an unknown function permit different operations and different possible answers.

Start by describing one candidate object and what would make it admissible. Choose a way to represent it, then distinguish two kinds of condition: those needed for the representation to denote such an object, and those expressing the requirements on that object. This produces a mathematical problem that can be reasoned about or handed to an appropriate computational method.

The result consists of variables with their domains, joint conditions, the requested operation on their solutions and a way to interpret the answer. It can be enough to find one feasible case; another question may require all possible values, a preferred case or a count. The chosen representation must support that particular result.

You need to understand the objects and requirements in the original question, elementary logical conditions and the mathematics used to express them. A mathematical collaborator can construct the expressions while you resolve their intended meaning. When a suitable formulation already exists, use it. When the missing contribution is a physical relation, an observation law or a rule of change, obtain that relation through the relevant method before translating it. B.5.FM supplies the broader first-model construction; MMP.7 and MMP.9 develop observation and reduced-evolution constructions.

## MMP.10:2 - Problem {#problem}

A convenient variable can leave out the possibility that matters. A single interval cannot represent an activity that may pause. A membership bit cannot record repeated membership. Coefficients of a straight line cannot describe every continuous curve. These restrictions may be useful, but they change which cases the formulation can answer for.

Representation can also add possibilities. A table intended to describe a function can allow two values for one argument unless its conditions exclude that case. Extra fields can create several records of the same object. A calculation over those records can then answer a different counting or probability question.

The difficulty is to construct the mathematical expression of the intended possibilities, including their joint restrictions and the requested result. Solving the resulting equations addresses the problem only after that construction has been made.

## MMP.10:3 - Forces {#forces}

| Force | Consequence for the construction |
| --- | --- |
| Faithful possibilities and useful operations | A familiar representation may make calculation easy while excluding an intended case or hiding a useful relation. |
| Structured objects and scalar tools | A function, set or sequence may need several scalar variables and additional conditions to represent its structure. |
| Shared restrictions and local descriptions | Separate bounds on individual variables can lose a condition on their combination. |
| Simple answer and rich solution set | A single witness needs less from the representation than counting, sampling or claiming that no witness exists. |
| Reuse and changed requirements | A derived constraint that helped an earlier formulation may exclude valid cases after the requirement changes. |

## MMP.10:4 - Solution {#solution}

**Describe the possible object → choose its representation → derive the representation conditions → express the requirements and question → obtain and interpret a result → revise the affected construction.**

### MMP.10:4.1 - Recover what varies and what the question asks {#recover-what-varies-and-what-the-question-asks}

Describe a candidate before choosing scalar variables. Is it an amount, a collection, a sequence, an assignment, a function or another mathematical object? Which distinctions can change the answer? A set retains membership; a multiset also retains multiplicity; a sequence retains positions. Choose among them from the question.

Separate supplied quantities from unknowns. Among unknowns, distinguish what is to be inferred, what can be chosen and what can vary independently of that choice. If a choice uses an observation, specify when the observation becomes available; MMP.8 constructs the resulting information-dependent requirement. An unknown value does not become a freely selectable design variable merely by appearing in the same equation.

State the requested result. Existence asks whether at least one admissible object can be constructed. Inference asks what a quantity can be across admissible objects. Selection adds a preference among them. Counting and sampling depend on how individual objects are distinguished. Keep those requests separate while choosing the representation.

### MMP.10:4.2 - Construct variables that represent the object {#construct-variables-that-represent-the-object}

Choose an expression from which a candidate can be recovered. Give each variable a domain and any unit or reference point needed by its operations. A machine label ranges over names; arithmetic on the label requires a separate meaning. A count ranges over nonnegative integers; an amount may be divisible. State a finite bound when the task supplies one. Adding a bound solely to finish a search restricts the question to that bound.

For a structured object, compare representations by the operations you need. A function on a finite set can use one output variable for each input. Alternatively, a table of Boolean indicators can say which input-output pairs belong to its graph. The first expression makes function evaluation easy to state. The second makes some relations among pairs visible, but needs conditions to make the table a function. For a partial function, represent undefinedness as well as defined values.

Keep a shared quantity shared. If several equations use the same unknown offset, one offset variable must occur in all of them. Introducing a separate offset in each equation creates additional possibilities. Conversely, equating genuinely separate values can remove possibilities.

For a function or shape over an infinite domain, choosing finitely many coefficients also chooses a family. Identify that family and whether it expresses the intended possibilities or is a deliberate restriction. For example, the conditions on a continuous function may allow curved solutions even when no affine function satisfies them. A useful restricted family can be sufficient for finding a witness; failure inside it leaves the larger family unresolved.

### MMP.10:4.3 - Derive structural conditions and translate requirements {#derive-structural-conditions-and-translate-requirements}

Ask what must hold for a variable assignment to describe one candidate of the intended kind. With Boolean entries `r_ij` describing the graph of a total function, require `sum_j r_ij = 1` for every input i. For a partial function, replace this with `sum_j r_ij <= 1`; an all-zero row then means undefined at that input. For an injective function, additional conditions on columns express the extra requirement.

These conditions have different reasons. One value per input comes from choosing a total function. Injectivity comes from the particular problem, if it requires injectivity. Keep their reasons recoverable so that a later change from total to partial or from injective to unrestricted has a local repair.

Express the original requirements using the represented objects. Conjoin conditions that must hold for the same assignment. Use disjunction for allowed alternatives and implication when choosing an option imposes a condition. An implication alone supplies no timing; use time quantities or an explicit sequence when order matters. Preserve a coupled condition such as `x+y=1` rather than replacing it by separate bounds on x and y.

When a bijection between representations is established, MATH.7 supplies transport of operations, relations and compound expressions. For a representation with several records per object, C.29.1 supplies the more general correspondence. Use the decoding of a record to express the requirement on its object. If a condition is rewritten to fit the receiving notation, derive that expression from the original relation and the structural conditions. This is where a missing index, an undefined value or a lost alternative can change the formulation.

Additional constraints can expose consequences and help the obtaining method. Derive them from the retained requirements, and preserve that dependence. Fewer variables or more constraints do not alone establish a faster method; compare the actual resulting work when efficiency matters.

### MMP.10:4.4 - Make the answer correspond to the question {#make-the-answer-correspond-to-the-question}

Define how to recover the requested object or quantity from a satisfying assignment. Then work in both directions: represent an intended admissible case, and interpret an allowed assignment. Use the construction and its conditions to establish the reach of this correspondence. A small case can expose a mistake; a claim about every case needs the corresponding argument.

Match that reach to the requested result:

- To use a witness, its recovered object must satisfy the original requirements.
- To conclude that no intended object exists from inconsistency of the formulation, every intended object must have a representation in it.
- To infer all possible values, translate the quantity as well as the admissible cases; C.16.IR supplies the projection question.
- To optimize, translate the objective and preference as well as feasibility. Distinguish a bound from a value attained by an object.
- To count or sample objects, account for multiple representations of the same object. One representation per object is one solution; weighting or grouping representations can be another.

Auxiliary variables can change what a returned number means. Suppose a finite nonempty set of finish times `f_i` is determined by the other variables. Introduce a real auxiliary T used only in `T >= f_i` and the objective of minimizing T. Lowering T to `max_i f_i` then preserves feasibility, so at an attained optimum T equals the latest finish. If T must instead be an integer and the latest finish is 1/2, its minimum is 1. A merely feasible intermediate T can also exceed the latest finish. Recover the actual latest finish as `max_i f_i`; infer equality with T only when its domain and other conditions permit that lowering.

Choose an obtaining method for the constructed question. Manual substitution may suffice; another problem needs a numerical method, symbolic derivation or search. C.29.2 separates the required mathematical result from the procedure and its execution. Use that method's actual conclusion: finding no case within a time budget differs from establishing inconsistency. Preserve any restriction or approximation when returning the result to the original question through C.29.1.

### MMP.10:4.5 - Revise the formulation from the changed requirement {#revise-the-formulation-from-the-changed-requirement}

Locate the changed participant, domain, relation or requested result. Changing a supplied amount can retain the same representation. Allowing interruptions changes what an activity description must express. Changing a total function to a partial one changes structural conditions. Changing existence to counting can make duplicate records material.

Revisit constraints derived from the old requirement as well as the original formula. Reconstruct the affected expressions and answer interpretation, retaining the unaffected ones. If a solving tool cannot support the needed object, construct a suitable representation or choose another obtaining method; keep any deliberate restriction visible in the returned conclusion.

Stop with a usable formulation and interpretation, an adequate answer, or a named missing relation or operation. Choose further derivation, observation or computation according to what it can change in the work and its cost; C.11.DUA supplies that decision. When the formulated object is itself a working method, return its proposed change to ME for interpretation and use. The mathematical model supplies a reason for the change; the working method still has to be performed under its stated conditions.

## MMP.10:7 - Conformance Checklist {#conformance-checklist}

- Can the reader identify a candidate object before interpreting the variables, including what is supplied, unknown or selectable?
- Do domains, units, shared quantities and definedness express the intended possibilities?
- Which conditions make the representation denote an object, and which express requirements on it?
- Do conditions that must hold together refer to the same assignment? Are alternatives and conditional restrictions preserved?
- Can intended cases be represented and satisfying assignments be interpreted at the reach required by the question?
- Does the requested value, preference, count or probability survive the representation, including auxiliary values and duplicate records?
- What does the obtaining method actually establish, and which changed requirement reopens which construction?

## MMP.10:9 - Consequences {#consequences}

The mathematical problem becomes available for reasoning, computation and revision without leaving the interpretation of its variables implicit. A solver result can be returned as the arrangement, quantity or unresolved distinction that the work needs.

Constructing and maintaining a second representation has a cost. Direct formulation is often sufficient when the objects and their restrictions already have a clear expression. A structured intermediate formulation becomes useful when it preserves meaning across several receiving notations, helps revise requirements or exposes a calculation that the first representation hid. Any efficiency advantage depends on the resulting obtaining method.

## MMP.10:12 - Relations {#relations}

- **B.5.FM and B.5.TU:** construct a first account and connect a subject theory to the encountered problem. This pattern translates its candidate objects and conditions into a mathematical formulation.
- **MATH.1 and MATH.5:** construct composable paths and extend an assignment on elementary steps to compounds while preserving operations and equations. MATH.16 chooses a mathematical construction from the maps it must support. MATH.7 transports structure when the required bijections have been constructed.
- **C.29.1 and C.29.2:** supply correspondence, answer recovery and the separation of a mathematical result from its obtaining procedure and execution.
- **C.16.IR:** determines what a compatible set permits one to infer through projection and constancy of the requested quantity.
- **MMP.7 and MMP.8:** construct observation probabilities and information-dependent choices. A formulation's variables retain those probabilistic and temporal meanings.
- **MMP.9:** derives a reduced evolution law when retained quantities depend on eliminated contributions. The resulting law can supply relations used here.
- **C.11.DUA and E.22/E.23:** choose worthwhile further inquiry and organize evaluation and improvement of a formulation or its obtaining work.
- **ME:** uses the mathematical result when constructing or changing a working method. Its performance in the subject remains distinct from the formal properties of its description.


## Dependencies {#dependencies}

- @fact:DEPENDS-ON Dependencies (as published): spec://ai.lev/fpf-spec/contract/B-5-FM#root for initial formulation; spec://ai.lev/fpf-think-math/contract/MATH-1#root/.5 for construction and representation; spec://ai.lev/fpf-spec/contract/C-29-1#root for transferring results; spec://ai.lev/fpf-think-mmp/contract/MMP-11#root for unknown relations. @status:spec/done
- @fact:REFERENCED-BY Referenced by (computed from the Tables of Contents): spec://ai.lev/fpf-think-cmp/contract/CMP-4#root, spec://ai.lev/fpf-think-mmp/contract/MMP-11#root, spec://ai.lev/fpf-think-mmp/contract/MMP-18#root, spec://ai.lev/fpf-think-mmp/contract/MMP-19#root, spec://ai.lev/fpf-think-mmp/contract/MMP-8#root, spec://ai.lev/fpf-eng-ops/contract/OPS-10-2#root, spec://ai.lev/fpf-eng-ops/contract/OPS-11-1#root, spec://ai.lev/fpf-think-phy/contract/PHY-6#root @status:spec/done

#source spec://ai.lev/fpf-think-mmp/source/MMP-10
