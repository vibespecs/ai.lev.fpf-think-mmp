# MMP.12 - Formulate an Inverse Problem and Choose Whether and How to Use Regularization {#root}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Working sections of the pattern; its depth sections live in the source document named by the last line. See LICENSE.md for the list of changes.

> **Type:** Method pattern
> **Status:** Usable, evolving
> **Normativity:** Normative within the stated use

## MMP.12:1 - Problem frame {#problem-frame}

Use this pattern when you can predict records from a proposed state or model, but recovering the needed unknown from the records is ambiguous or too sensitive to their errors. A mixture can reveal its total while scarcely distinguishing its components. Accumulated activity can be known much more reliably than its instantaneous rate. You need to decide what can be recovered and what additional structure a usable reconstruction would impose.

Begin with the quantity the next use needs. Write how a candidate unknown would produce the recorded result, then vary the unknown in a direction that changes that quantity. If the records remain unchanged, that distinction is unidentified. If they change only slightly, calculate how their uncertainty affects recovery. Introduce regularization only when the remaining task warrants its extra assumptions.

**Regularization** constructs a controlled reconstruction by restricting candidates or discouraging selected variations. Its practical gain is a usable answer whose dependence on that restriction is visible. It can suppress error amplification while also suppressing real detail. The result may be a conditional estimate, a sufficient target bound, or a reason the requested reconstruction needs another contribution.

This is the inverse-formulation branch of mathematical modeling. It constructs the reconstruction problem and the added structure that shapes its answer. Statistical inference supplies probability claims when needed; computational methods obtain solutions to the stated problem. The examples use linear equations, norms and elementary differentiation. More difficult operators require suitable mathematical preparation or a collaborator who can supply their inverse and stability analysis. A person or AI participant still needs the subject grounds for the forward relation and the proposed restriction.

Use an adequate direct inverse when its propagated error is acceptable. If an available range or comparison already settles the receiving question, return it through C.16.IR without reconstructing every unknown. Solver implementation alone calls for the corresponding computational method.

## MMP.12:2 - Problem {#problem}

Matching the data can select the wrong kind of answer. Several unknowns may produce the same records, or the best fit may follow noise in a direction the observations barely constrain. More accurate solution of those fitting equations can make the reconstruction more extreme.

Additional structure can help, but it changes the grounds of the answer. A small norm favors small unknowns in a chosen representation. A smoothness penalty favors slow variation. A learned penalty favors features represented by its training and construction. Each can remove a feature the receiving question needs.

The problem is to formulate recovery so that the required target, observation relation, error account and added selection are distinguishable, and then to determine which improvement and loss the regularization produces.

## MMP.12:3 - Forces {#forces}

| Force | Tension |
| --- | --- |
| Needed target and full reconstruction | A stable total or comparison can be sufficient even when individual components are unresolved. |
| Fit and sensitivity | Exact fitting retains recorded detail, including errors amplified by inversion. |
| Additional structure and lost alternatives | A restriction can make recovery usable while excluding a consequential subject case. |
| Strong regularization and bias | Suppressing weakly observed variation reduces sensitivity but can systematically displace the target. |
| Mathematical recovery and computation | Solving the selected objective accurately does not establish that it recovers the subject quantity accurately. |

## MMP.12:4 - Solution {#solution}

Construct the forward relation for the requested target, locate the consequential loss of distinction or amplification, and choose the smallest justified restriction that changes that difficulty. Formulate its strength together with the error account. Return the target with the dependence and loss introduced by that choice.

### MMP.12:4.1 - Construct the forward relation from the modeled situation {#construct-the-forward-relation-from-the-modeled-situation}

Name the unknown x, the target q=T(x), and the records y. The unknown may be a parameter vector, a function or a collection of relations. State its domain and the units and scales used to compare changes. A target can be a total, a value at one time or a threshold; it need not be x itself.

Follow a candidate x through the modeled process and recording operation. Write the resulting ideal record as F(x,z), where z contains influential unknowns that are not the target. Keep known inputs fixed and retain shared unknowns across records. MMP.11 constructs a missing model family; C.16.MR supplies a missing measurement relation. If probabilities matter, MMP.7 constructs the recording law.

For an additive bounded-error account, one possible formulation is

`y_delta = F(x,z) + e, with ||e||_Y <= delta.`

Here delta bounds error in the chosen record norm. Use this form only when the recording procedure supports additive error. For an implicit forward relation, retain its equations and jointly unknown outputs rather than forcing it into a single-valued map. A likelihood from MMP.7 can instead supply the data discrepancy appropriate to a probabilistic account.

Include consequential uncertainty in calibration and in the forward approximation. A fixed but unknown offset remains an unknown; setting it to zero can make recovery appear better determined. A noise bound and a standard deviation have different meanings and support different conclusions.

### MMP.12:4.2 - Locate the part that needs regularization {#locate-the-part-that-needs-regularization}

Use C.16.IR's compatible cases or sufficient bounds to establish what the current records and premises resolve. Reuse that result. This pattern adds the construction of a recovery rule and analysis of the rule's sensitivity.

For a linear relation y=A*x, a change h with A*h=0 is invisible to the records. If both x and x+h are admitted and T(x+h) differs from T(x), full recovery of that target needs another premise. If T is unchanged, the invisible direction may be irrelevant to the current use. For unknown influences, vary x and z jointly.

Next examine changes that are visible but weak. In finite dimensions, after meaningful scaling, singular values of A describe the response to orthogonal input directions. A small nonzero singular value sigma means that direct inversion multiplies the corresponding record error by 1/sigma. Estimate the effect on T, not merely on an unnecessarily detailed reconstruction. For nonlinear models, a derivative can reveal local weak directions; it does not establish global uniqueness or exclude another branch.

Distinguish poor conditioning from a discontinuous inverse. An invertible finite matrix has a continuous inverse, although its error amplification may be unacceptable. In a function-space problem, data changes tending to zero can produce target changes that do not tend to zero. The spaces and norms determine this claim; :5.3 gives an explicit example. Refining a finite discretization can expose progressively larger amplification.

If the supported target bound is already sufficient, stop. If the premises are inconsistent, return to their diagnosis through C.16.IR. A penalty cannot make an incompatible observation account true.

### MMP.12:4.3 - Turn the added structure into a reconstruction problem {#turn-the-added-structure-into-a-reconstruction-problem}

State why particular alternatives should be excluded or discouraged. A known nonnegative quantity can justify a hard domain restriction. A supported slowly varying response can justify discouraging rapid changes. A reference state can justify penalizing departure from it. When the structure is only a preference for selecting one nominal model, say so; the selected model then remains one conditional representative.

A useful variational formulation is

`(x_lambda,z_lambda) in argmin over (x,z) in C of D(F(x,z),y_delta) + lambda*R(x,z).`

C contains the hard conditions. D measures discrepancy in records. R is the regularizer: the quantity whose increase discourages a candidate. The parameter lambda controls its weight. Explain each term's subject meaning and scaling. Adding squared errors with different units, or changing units without changing the weights, changes the problem.

Choose R by deriving which variations it penalizes. For a quadratic example,

`R(x) = ||L*(x-x0)||^2.`

The reference x0 and operator L determine the preference. L=I penalizes distance from x0; a difference operator penalizes changes between neighboring values. The latter permits constant shifts unless another condition fixes them. A sparsity penalty is appropriate only when concentrating the unknown in relatively few components fits the intended representation and subject question.

For a finite, unconstrained real linear problem with scaled squared discrepancy, differentiating the quadratic objective gives

`(A^T*A + lambda*L^T*L)*x = A^T*y_delta + lambda*L^T*L*x0.`

For lambda>0 this has a unique minimizer when the null spaces of A and L intersect only at zero. Thus adding a penalty does not by itself guarantee unique recovery. Constraints and nonlinear or nonconvex choices require their own existence, uniqueness and obtaining arguments.

An alternative is to minimize R subject to a justified discrepancy ceiling. This makes the acceptable fit explicit. It can agree with a penalized formulation for suitable parameters, but the correspondence must be established for the problem being used.

A learned regularizer is another way to construct R. Its training examples and training objective supply additional structure, whose relevance to the current subject and observation conditions must be justified. Compare it with the simpler available restriction on the same required target and with its training and obtaining costs included. A visually plausible or numerically precise reconstruction can still lose the feature the target asks for.

### MMP.12:4.4 - Select strength from the required sensitivity and tolerated loss {#select-strength-from-the-required-sensitivity-and-tolerated-loss}

Work out how the added structure changes recovery before choosing its numerical strength. For L=I, x0=0 and one nonzero singular direction, quadratic regularization replaces division by sigma with multiplication by

`sigma/(sigma^2 + lambda).`

This reduces noise amplification. With exact data, it also multiplies the true component by `sigma^2/(sigma^2+lambda)`, shrinking it toward zero. A component invisible to A is selected through the regularizer, not recovered from the records.

Choose lambda using the error account and the receiving use. A bound on acceptable noise amplification, together with a bound on tolerated shrinkage, can determine an interval of useful values. Section :5.1 computes such a choice. A supported discrepancy level can instead guide a parameter search: compare each candidate's residual with the level warranted by the observation and model errors. An empirical choice rule needs evidence appropriate to its own claim; fitting the available records best is not a general parameter-selection argument.

Evaluate both sides of the trade-off. Compare the changed target when the data are perturbed within their error account and when the reference, penalty or strength changes within its justified range. Return consequential dependence rather than hiding it behind one selected value. A few numerical trials can reveal a failure; they establish a bound only when an argument covers the claimed variation.

If no supported strength gives the needed sensitivity and tolerable loss, narrow the target or return the missing contribution. A stronger penalty can make outputs nearly constant while leaving them useless for the question.

### MMP.12:4.5 - Separate recovery error from solving error {#separate-recovery-error-from-solving-error}

For a linear reconstruction rule H_lambda and exact data y, the triangle inequality separates two contributions:

`||H_lambda*y_delta - x_target|| <= ||H_lambda*(y_delta-y)|| + ||H_lambda*y - x_target||.`

The first is propagated data error; the second is the displacement caused by the reconstruction rule even with exact data. Choose x_target explicitly: an identified true unknown, a specified minimum-norm solution, or another admitted target. Those are different claims. Numerical approximation adds its own contribution, which MATH.20 and CMP.8 can bound.

For a fixed regularization strength, establish only the stability supported by the formulation. A unique minimizer in a general nonlinear problem is not automatically a quantitative stability bound. If the claim concerns recovery as noise tends to zero, specify how strength and any discretization change with that noise. Fixed-strength bias may persist. Classical regularization analysis supplies conditions for this limit; the existence of a penalty is insufficient.

Keep that limit separate from iterations of a solver converging at fixed data and strength. The solver can converge to the exact minimizer of a biased problem. Conversely, early stopping can itself be a regularization choice when its stopping rule has an appropriate noise-dependent justification. Additional iterations then need not improve the subject reconstruction.

For ordinary finite use, obtain only the error or settled distinction the receiver needs. A limiting theorem need not be proved anew when an applicable result and a sufficient finite bound are available.

### MMP.12:4.6 - Return the useful target and the choice it depends on {#return-the-useful-target-and-the-choice-it-depends-on}

Return T(x_lambda) with the forward relation, consequential error assumptions and added restriction needed to interpret it. State what remains unresolved and how much the target changes under the relevant data and regularization variations. Preserve a compatible range when it is needed alongside a nominal reconstruction. A penalty-selected point alone supplies neither a confidence interval nor a posterior distribution.

Regularization changes the grounds for selecting an answer; it creates no new observation from the old records. When a different premise, observation relation or target would remove the difficulty, name that contribution. Further computation helps only if the remaining problem is computational.

A person or AI can propose the formulation, calculate the example and compare alternatives. The needed subject relation and mathematical argument must still be available from a competent participant or established result. When they are missing, return the precise question they must answer. B.5.RR carries a changed premise through the reasoning; B.5.MPC.R helps coordinate a revision spanning subject, mathematical and computational contributions.

A methodological use can take the same result back to a working method: for example, replace an unstable instantaneous-rate target by a sufficient interval total, or revise how records are obtained when a needed distinction remains invisible. Such a change is selected for the original use, not made compulsory by the presence of an inverse problem.

## MMP.12:7 - Conformance Checklist {#conformance-checklist}

- The target and forward relation are recoverable, including consequential unknown influences, units and record-error assumptions.
- Indistinguishable alternatives and error amplification are distinguished; a sufficient target is used without demanding full recovery.
- Each hard restriction or penalty has a subject justification or an explicit nominal-selection purpose. Its excluded or discouraged variation is identifiable.
- The strength choice exposes both sensitivity reduction and target loss. A changed observation condition is carried through that choice.
- Existence, uniqueness, stability, vanishing-noise recovery and solver convergence are claimed only at the scope established for the formulation.
- The returned target retains consequential dependence on added structure and the uncertainty needed for its receiving use.

## MMP.12:9 - Consequences {#consequences}

The practitioner obtains a reconstruction problem with visible reasons for its additional structure. Some questions become cheaper because a stable total or bound replaces full reconstruction. Others gain a useful nominal estimate at the cost of explicitly accepted bias.

The formulation also locates a failed use: unsupported regularity, an unresolved invisible direction, an inadequate forward relation or insufficient numerical control call for different contributions. Increasing regularization or computation indiscriminately does not resolve them.

## MMP.12:12 - Relations {#relations}

- **Uses MMP.11** to construct the model family from which the forward relation is assembled, and **MMP.7** when a probability law of records is needed.
- **Uses C.16.MR** for a missing measurement relation and **C.16.IR** for compatible alternatives and sufficient target bounds. Adds regularized formulation, strength selection and analysis of induced sensitivity and loss.
- **Uses MATH.20** for error and target bounds. **CMP.6 and CMP.8** supply an iterative obtaining method or controlled approximate computation for the selected problem.
- **Supplies statistical inference** with the target, observation account and unresolved dependence on added assumptions when an estimate's probability or uncertainty is needed. **Supplies observation design** with the distinctions an additional observation would need to resolve.
- **Returns to B.5.RR and B.5.MPC.R** when the required result changes the mathematical, subject or computational contribution. Method Engineering can use that result when revising how a working method obtains or uses observations.


## Dependencies {#dependencies}

- @fact:DEPENDS-ON Dependencies (as published): spec://ai.lev/fpf-spec/contract/C-16-IR#root for compatible cases; spec://ai.lev/fpf-think-mmp/contract/MMP-11#root/.7 for the forward and recording relations; spec://ai.lev/fpf-think-mmp/contract/MMP-13#root for inferential uncertainty; CMP for solving the formulated problem. @status:spec/done
- @fact:REFERENCED-BY Referenced by (computed from the Tables of Contents): spec://ai.lev/fpf-think-mmp/contract/MMP-13#root @status:spec/done

#source spec://ai.lev/fpf-think-mmp/source/MMP-12
