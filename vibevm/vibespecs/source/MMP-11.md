# MMP.11 - Construct a Mathematical Model Family from Known Relations: depth {#depth}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Depth sections of the pattern; the working sections are in the contract document of the same id. See LICENSE.md for the list of changes.

## MMP.11:5 - Archetypal Grounding {#archetypal-grounding}

### MMP.11:5.1 - Construct a response from its known shape {#construct-a-response-from-its-known-shape}

A normalized input u lies in [0,1]. The subject account supports a nondecreasing response r with `r(0)=0` and `r(1)=1`. Its intermediate shape is unknown. Begin with these properties, rather than choosing a straight line as the only candidate.

Choose an integrable h with `h(u)>=0` almost everywhere and `H=integral_0^1 h(v) dv>0`. Define

`r(u)=integral_0^u h(v) dv / H`.

The endpoints follow by substitution. For `u2>=u1`, the difference is the nonnegative integral of h over [u1,u2], divided by H. Thus every member is nondecreasing. These curves are absolutely continuous. Every absolutely continuous nondecreasing response with these endpoints has such a representation using its almost-everywhere derivative, but a jump response is outside this family. The needed regularity must come from the question or remain a declared restriction.

For a small calculable family, use linear segments through (0,0), (1/4,q), (1/2,1/2) and (1,1). Their slopes are `4*q`, `2-4*q` and 1. They are nonnegative exactly when `0<=q<=1/2`. This is a construction of admissible candidates, not a conclusion from measurements alone.

Suppose observations establish only the three values at 0, 1/2 and 1. Every q in that interval agrees with them. The consequence `r(1/4)<=0.6` follows for this whole family; it also follows for every nondecreasing response with the given midpoint. There is no need to identify q for that question.

Now the receiving use asks whether `r(1/4)>0.3`. Candidates q=0.2 and q=0.4 satisfy the same observations and give opposite answers. Another repetition at the three old input values does not distinguish these ideal candidates. An observation near the disputed input may help; its precision and cost belong to that new question. Alternatively, a supported additional shape relation could narrow the family.

### MMP.11:5.2 - Retain an exchange balance without inventing its mechanism {#retain-an-exchange-balance-without-inventing-its-mechanism}

Two nonnegative amounts x and y exchange a conserved total N. The forward and reverse rates are unknown. Use locally Lipschitz nonnegative rate functions a(x,y) and b(x,y), defined on a neighborhood of the nonnegative states being used, and construct

`q=x*a(x,y)-y*b(x,y)`,

`x_dot=-q`, `y_dot=q`.

Adding the two equations gives zero change in x+y for every admitted a and b. At x=0, `x_dot=y*b(0,y)>=0`; at y=0, `y_dot=x*a(x,0)>=0`. With these regularity conditions the continuous-time solution preserves nonnegativity. These are properties of the coupled construction. The applicability of conserved exchange to the subject remains a premise.

Even complete knowledge of q need not identify the gross transfers. For any nonnegative locally Lipschitz h, define

`a_new=a+y*h`, `b_new=b+x*h`.

The two added contributions to q are `x*y*h` and `-y*x*h`, which cancel. The whole observed evolution is unchanged. This is an algebraic family of alternatives, not merely several successful numerical fits.

For a dimensionless instance, take a=b=1. The alternative h=1 gives `a_new=1+y` and `b_new=1+x`, yet both models have `q=x-y`. At x=2, y=1 they both predict `x_dot=-1`.

Change the question: a proposed intervention suppresses only the reverse transfer while leaving the forward rate law applicable. Under that causal premise, C.28.MR replaces the reverse contribution by zero. The first model gives `x_dot=-2`; the second gives `x_dot=-4` at the same state. Ordinary observations of x and y under the unchanged mechanisms cannot choose between these accounts. A prediction under the old operation can still be useful; the proposed intervention needs a contribution that distinguishes the mechanisms or a sufficient bound covering them.

For dimensional quantities, a and b have inverse-time units, while h has inverse-amount-inverse-time units. Restoring units prevents treating the added terms as arbitrary dimensionless corrections.

### MMP.11:5.3 - Construct probabilities while keeping boundary outcomes {#construct-probabilities-while-keeping-boundary-outcomes}

A report has three possible outcomes. Let `w_i>=0` and let their sum W be positive. Set `p_i=w_i/W`. Every candidate has nonnegative probabilities summing to one. Conversely, every probability vector on these outcomes is represented by choosing w=p. Thus this construction includes zero-probability outcomes.

The weights (0,1,3) and (0,2,6) both give probabilities (0,1/4,3/4). The parameter vector is redundant even if the probability vector becomes fully determined. There is no need to distinguish those weights when the receiving question uses only the law.

A strictly positive parameterization, such as exponentiating every finite unconstrained parameter before normalization, excludes zero probabilities. It can approximate a zero closely but cannot express it with finite parameters. If the subject account rules out the first outcome, retain that zero in the construction and normalize weights for the remaining outcomes. Whether a very small nonzero value would suffice depends on the receiving question.

The constructed p is a family member, not yet an estimate from data. MMP.7 composes it with selection, rounding or other recording behavior. The appropriate statistical method then determines what the observations support. Changing the recording procedure can change that inference without changing the underlying outcome family.

## MMP.11:6 - Bias-Annotation {#bias-annotation}

Familiar formulas can turn an assumed shape into an unnoticed restriction. Flexible fitting can conceal a different commitment: the selected inputs, architecture and loss still determine which functions can be obtained. Recover those choices when they affect the receiving result.

A respected subject law can also be applied outside its range or boundary. Preserve its grounds and allowed discrepancy. If no supported structural restriction is available, an unrestricted family can be a reasonable candidate for a bounded use; further structure must earn its place through the subject question.

## MMP.11:8 - Common Anti-Patterns and How to Avoid Them {#common-anti-patterns-and-how-to-avoid-them}

| Failure | Consequence | Repair |
| --- | --- | --- |
| Fit each contribution independently despite a shared identity | The fitted whole can violate the identity. | Build the shared quantity or joint condition into the family. |
| Treat a penalty as an enforced relation | A small fitting loss can conceal a consequential violation. | Match the construction and obtaining method to the allowed discrepancy. |
| Treat a finite fitted family as all admissible relations | A failure inside it becomes an unsupported impossibility claim. | State its restrictions and widen or bound the family when the question needs it. |
| Identify parameters when only a consequence is needed | Work is spent resolving distinctions that do not change use. | Apply the observation relation to the receiving consequence. |
| Transfer an observational fit to an intervention without modeling the mechanism change | Models agreeing on observed behavior can imply different intervention effects. | Construct the mechanism replacement and the alternatives it can distinguish. |

## MMP.11:10 - Architectural Rationale {#architectural-rationale}

Constructing the free part through the retained relations makes the reason for a property inspectable. A shared transfer preserves a total because the same quantity enters with opposite signs. A shape-constrained response preserves monotonicity because its increments are integrals of nonnegative values. Those reasons remain available when coefficients or learned functions change.

Separating function, representation and receiving consequence also permits economical inference. Many representations of the same function need not be distinguished. Functions that agree on the needed consequence may remain as alternatives. A new intervention can make a formerly irrelevant difference decisive.

The insertion point is therefore an architectural choice in the model. It determines what the adjustable contribution can change, which relations constrain it and which results still have the interpretation the work needs. A symbolic expression and a trained network can each participate in this construction when their mathematical role is recoverable.

## MMP.11:11 - SoTA-Echoing {#sota-echoing}

**How much of the relation should be left free?** The historical [SINDy work, Brunton, Proctor and Kutz (2016), Discussion and Appendix B](https://robotics.caltech.edu/wiki/images/a/a3/BPK_PNAS.pdf), binds sparse discovery to the chosen coordinates and function library. The [universal differential equations construction, section 2.3](https://arxiv.org/html/2001.04385v4), combines retained mechanisms with an adjustable function. Sections :4.1-4.3 adopt this choice of where freedom belongs. A small fixed family can be sufficient when its restrictions fit the question. The flexible construction trades additional representation and inference work for retaining variations the small family omits.

**How should a required relation survive fitting?** For the conservation question in :5.2, :4.2 selects a shared transfer with opposite signs over independently fitted change laws for x and y with only a finite conservation penalty. The latter can fit observations while violating the required total elsewhere. The shared construction preserves that total for every admitted choice of its rate functions. Accept the extra derivation and restriction to conserved exchange in return for that identity; obtain the subject grounds for conservation first. When the question allows a specified discrepancy, a penalty or simpler approximate relation can be sufficient at lower construction cost. Carry its discrepancy into the requested consequence rather than requiring the identity anyway. Direct constraints enforcing the relation remain another option under MMP.10.

**Where does the adjustable part enter?** [Dyad's model-discovery documentation](https://help.juliahub.com/dyad/stable/analyses/udes.html) supports component-level insertion before structural simplification. [Micluta-Campeanu and colleagues (2026), sections 2.1-2.2](https://arxiv.org/html/2603.15943v1), demonstrate post-simplification correction followed by optional reduction and symbolic replacement. Section :4.4 retains both placements, chosen by their effect on the needed relations. Their thermal application supplies one use, not the scope of this method.

**What does fitting resolve?** [Loman and Baker (2025), sections 3.1, 3.3, 3.5 and B.5](https://arxiv.org/html/2510.14140), distinguish functions, parameters and predictions. Section 3.1 also constructs an algebraic compensation between an unknown function and a mechanistic parameter that preserves observed dynamics. Adopt that construction of indistinguishable alternatives in :4.5; :5.2 adapts it to coupled directional rates. Their finite fitted-ensemble comparisons in :2.4 and Appendix B can reveal alternatives, but agreement of sampled fits does not prove uniqueness over the admitted family. Constructing two admissible alternatives with different receiving consequences already establishes the consequential ambiguity, without fitting an ensemble.

Revisit the chosen family when new subject knowledge changes its restrictions, a different observation changes what is distinguishable, a new use needs a formerly discarded difference, or another construction supplies the needed result at lower cost.


## MMP.11:End {#end}
