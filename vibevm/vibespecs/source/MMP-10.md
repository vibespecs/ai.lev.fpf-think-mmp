# MMP.10 - Construct and Revise a Mathematical Constraint Formulation: depth {#depth}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Depth sections of the pattern; the working sections are in the contract document of the same id. See LICENSE.md for the list of changes.

## MMP.10:5 - Archetypal Grounding {#archetypal-grounding}

### MMP.10:5.1 - Construct an unknown rule from requirements on its repetitions {#construct-an-unknown-rule-from-requirements-on-its-repetitions}

A device has three labeled modes A, B and C. The required rule changes the mode on every use and returns to the starting mode after three uses. The question is to construct a deterministic rule, with no additional internal state. The rule itself is the unknown object.

Let `S={A,B,C}`. Choose one output variable `p_i in S` for each input i. The requirements become `p_i != i` and `p_(p_(p_i)) = i` for every i. Function composition gives the meaning of the repeated application. MATH.1 constructs composable paths; MATH.5 extends an interpretation of their elementary steps to the compounds.

To express the rule by selected pairs instead, choose `r_ij in {0,1}`. Add `sum_j r_ij=1` for each row, `r_ii=0`, and, for all i,j,k, `(r_ij=1 AND r_jk=1) implies r_ki=1`. The row condition makes a function. The implication expresses the return after three uses: the first two selected transitions determine a required third.

Recover p by taking the unique selected column in each row. Conversely, p creates the table by selecting exactly its output pair in each row. These constructions are inverse. The triple-application requirement is therefore the same in both formulations, with MATH.7 carrying that relation. A rule A→B→C→A and its reverse both satisfy it.

There are precisely two such rules. From `p^3=id`, p is invertible with inverse `p^2`. Its cycles have lengths dividing three. Since a one-element cycle is forbidden, the three modes form one three-element cycle, with two possible orientations. This reasoning proves completeness; listing two examples alone would not.

Change the device to four modes, retaining the three-use return and no unchanged mode. A permutation of four elements cannot partition them into cycles all of length three, so no rule exists under these conditions. Change instead to a return after two uses. The conditions become `p_(p_i)=i` and `p_i!=i`; the indicator formulation requires symmetry `r_ij=r_ji`. It admits three pairings of four modes. Remove the former three-use implication: leaving it in the formulation would make the new, feasible requirement appear impossible.

The result is a rule that can be implemented and its stated scope: deterministic changes of the visible mode without hidden state. A proposal with additional state describes a different device and needs a new account of its operation.

### MMP.10:5.2 - Preserve existence while repairing a count {#preserve-existence-while-repairing-a-count}

An optional assignment gives each of two named requests either no selected option or one of options 0 and 1. Different requests may select the same option. This is a partial function from the two requests to `{0,1}`. Each request has three possibilities, so there are nine assignments.

Suppose the storage format gives each request two bits: d says whether an option is defined, and q gives its value when defined. When `d=0`, q is ignored. All sixteen four-bit records denote valid partial assignments. Every assignment has a record, so the representation can support an existence query with translated requirements.

It does not preserve the count. The empty assignment has four records, each of the four assignments defined on exactly one request has two records, and each of the four total assignments has one record. Thus `4 + 4*2 + 4 = 16`. Uniform selection among records gives probability `4/16` to the empty assignment and `1/16` to each total assignment, rather than the `1/9` obtained by uniform selection among assignments.

For a count or uniform assignment sample, one repair is the structural condition `d=0 implies q=0` for each request. There are now three admissible bit pairs per request and nine records, one per assignment. Another is a single variable with domain `{absent,0,1}` per request. If the sixteen-record storage representation must remain, group or weight its records using the multiplicities instead. To sample the nine assignments uniformly, give each record of an assignment with m records probability `1/(9*m)`. The probabilities of all m records then sum to `1/9` for that assignment. Thus each record of the empty assignment receives `1/36`, each record of a one-request assignment `1/18`, and each total-assignment record `1/9`. C.29.1 supplies the required correspondence; MMP.7 supplies a probability law when sampling is the intended operation.

The original existence use can remain sufficient. The new count or sampling question exposes the need for the additional construction. No change in the underlying possible assignments is intended.

### MMP.10:5.3 - Keep quantities and domain restrictions together {#keep-quantities-and-domain-restrictions-together}

A preparation requires one litre containing 35 percent solute by volume, using solutions A and B at 20 and 80 percent. Assume solute is conserved and component volumes add in this preparation. Those subject assumptions supply the relations. Let x and y be the respective volumes in litres; choose nonnegative real domains because the amounts can initially be divided freely.

The joint conditions are `x+y=1` and `0.2*x+0.8*y=0.35`. Substitution gives `x=0.75`, `y=0.25`. Both the total and solute requirements hold for those amounts. Separate bounds `0<=x<=1` and `0<=y<=1` would lose their required total.

Now only whole half-litre doses may be used. Change the representation to `x=m/2`, `y=n/2`, with nonnegative integers m and n. The volume equation becomes `m+n=2`. Its possibilities `(m,n)=(2,0),(1,1),(0,2)` give solute amounts 0.2, 0.5 and 0.8 litre. None supplies 0.35 litre. Rounding the former solution changes the preparation; it does not satisfy its original condition.

If the required concentration changes to 50 percent, one dose of each solution works. The subject relations and unit remain, while the requirement and feasible assignment change. If mixing changes volume or solute, obtain the replacement subject relation before revising its mathematical expression.

## MMP.10:6 - Bias-Annotation {#bias-annotation}

Tool familiarity can make scalar variables appear inevitable and conceal a different object or useful operation. Begin with the candidate object and its requirements. Compare representations when that comparison can change the answer or obtaining effort.

Compactness can hide duplicate records or omitted possibilities. Judge the representation by the requested result and the work needed to obtain it.

## MMP.10:8 - Common Anti-Patterns and How to Avoid Them {#common-anti-patterns-and-how-to-avoid-them}

| Failure | Why it changes the result | Repair |
| --- | --- | --- |
| Use separate bounds in place of a joint relation. | The same assignment can violate the lost total or coupling. | Retain the relation with its shared variables. |
| Number labels and use their arithmetic as a subject law. | Addition or order on the labels may describe no operation on the labeled objects. | Supply the intended operation or use names as names. |
| Read an empty restricted search as absence in the original problem. | Intended cases may lie outside the chosen bound or family. | Return the restricted conclusion or extend the representation. |
| Count records as objects after adding auxiliary fields. | Multiple records can describe one object and alter the count or sampling law. | Canonicalize, group or weight by the needed correspondence. |
| Keep a consequence of a replaced requirement. | It can remove the newly allowed cases, as in the changed rule in :5.1. | Re-derive the affected constraints. |

## MMP.10:10 - Architectural Rationale {#architectural-rationale}

Mathematical modeling often starts with choosing how possible objects will be expressed. The choice determines which restrictions must be added and which results can be recovered. Separating representation conditions, subject requirements and the operation on solutions makes revisions local: a changed requirement need not replace the representation, and a new representation need not change the intended possibilities.

An operation can itself be the unknown object. The finite-rule case therefore treats repeated action as a requirement on a function and uses composition to express it. The same organization applies to other structured objects, while their mathematics supplies the needed constructions and proofs. MATH.7 explains reversible transport after the maps are available; this pattern develops the modeling choice and construction of those expressions, including cases that need a many-to-one correspondence.

The connection to computation runs in both directions. A mathematical formulation supplies the problem a procedure must answer. The operations supported by a procedure can suggest a different expression of that problem. Meaning is retained through the representation conditions and answer interpretation, while performance is judged on the resulting work.

## MMP.10:11 - SoTA-Echoing {#sota-echoing}

The [MiniZinc Handbook 2.10.1, modeling and efficiency sections](https://docs.minizinc.org/en/stable/efficient.html) develops alternative models, derived constraints and interactions with solving methods. Adopt comparison of the resulting work; a smaller variable count alone does not settle it. A direct scalar formulation remains economical when its meaning is already clear.

[Akgun and colleagues, Conjure (2023), sections 2-4](https://www.ijcai.org/proceedings/2023/0765.pdf) separates representation selection from expression refinement and introduces structural constraints during refinement. Adopt this construction when structured objects would otherwise disappear into unexplained scalar choices. Conjure's finite combinatorial scope and model-selection heuristic remain specific to that approach. They do not establish a general best representation or performance guarantee.

The [Essence language reference, function and relation domains](https://conjure.readthedocs.io/en/latest/essence.html) makes such choices as partiality and cardinality explicit. This informs :4.2-4.3; its particular syntax is optional. The ordinary alternative is to express those conditions directly in a familiar mathematical notation.

For infinitely many possible objects, a finite parameterization needs its own coverage or approximation argument. Consider continuous nonnegative functions f on `[0,1]`, with `f(0)=f(1)=0` and integral one. An affine parameterization permits only the zero function after the endpoint conditions, so it fails. The quadratic `f(t)=6*t*(1-t)` satisfies every requirement. This authored countercase explains why the finite structured-model sources do not settle general parameterization. C.29.1 supplies the interpretation of a restriction; the relevant mathematical method supplies a suitable larger family or approximation.

To apply the formulation in another subject, obtain the relations and mathematical operations needed to express its requirements. Reconsider the representation when a new requirement, result kind or obtaining method changes what it needs to preserve or make affordable.


## MMP.10:End {#end}
