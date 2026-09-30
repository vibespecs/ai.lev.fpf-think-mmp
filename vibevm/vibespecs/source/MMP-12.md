# MMP.12 - Formulate an Inverse Problem and Choose Whether and How to Use Regularization: depth {#depth}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Depth sections of the pattern; the working sections are in the contract document of the same id. See LICENSE.md for the list of changes.

## MMP.12:5 - Archetypal Grounding {#archetypal-grounding}

### MMP.12:5.1 - Recover a split whose contrast is weakly observed {#recover-a-split-whose-contrast-is-weakly-observed}

Suppose two nonnegative loads x1 and x2 have exactly known total s=3. A second channel measures a small contrast:

`d=x1-x2; z=0.01*d+e; |e|<=0.02.`

All values are expressed in fixed normalized units. The recorded z is 0.03. The inverse relations are `x1=(3+d)/2` and `x2=(3-d)/2`, so nonnegativity gives -3<=d<=3. The error account gives 1<=d<=5; jointly, the compatible contrasts are 1<=d<=3.

If the question concerns the total or whether d is positive, this already answers it. A simulation that needs one nominal split must introduce a selection. Suppose its stated reconstruction requirement is to limit the contribution of channel error to at most 1 contrast unit, while accepting at most one-half shrinkage toward balanced loads. This is a modeling preference for the nominal input, not additional evidence that the loads are equal.

Use the objective

`J_lambda(d)=(0.01*d-0.03)^2 + lambda*d^2; -3<=d<=3.`

Its unconstrained minimizer, whenever it lies in that interval, is

`d_lambda=0.01*z/(0.0001+lambda).`

The data-error contribution is bounded by `0.01*0.02/(0.0001+lambda)`. Making it at most 1 requires lambda>=0.0001. The exact-data shrinkage fraction is `lambda/(0.0001+lambda)`; making it at most one-half requires lambda<=0.0001. These two declared requirements select lambda=0.0001.

The nominal result is d_lambda=1.5, hence (x1,x2)=(2.25,0.75). Its predicted contrast record is 0.015, leaving residual 0.015 within the supplied error bound. For this fixed strength, the interior reconstruction gain is 50, compared with 100 for direct inversion. Projection onto the admitted interval cannot increase that gain.

The bias matters. If the underlying contrast were d=1 and the error e=0.02, direct inversion would return 3 and this regularized rule would return 1.5. If the underlying contrast were d=3 with e=0, the same observed record would make direct inversion correct and the regularized rule would understate the contrast by 1.5. These are two constructed compatible cases, not an empirical accuracy comparison.

For a worst-case guarantee from these records, retain [1,3]. Its midpoint 2 has maximum absolute error 1 over that interval, while the selected nominal value 1.5 has maximum error 1.5. The midpoint is the better choice for that different criterion. Regularization is justified here by the declared response and shrinkage requirements, not by a claim that it improves every error criterion.

**Changed condition.** A new acquisition reports the same z=0.03 with supported error bound 0.002. The compatible interval is now [2.8,3]. Direct inversion has data-error contribution at most 0.2, already below the allowed 1. Choose the weakest penalty meeting that requirement: lambda=0 now suffices and introduces no shrinkage. It returns d=3 with the interval [2.8,3]; a receiver minimizing worst-case absolute error could instead use 2.9.

Keeping the old strength would return d=1.5 and residual 0.015, incompatible with the new error bound. The changed observation condition, not more accurate minimization of the old objective, changes the useful formulation.

### MMP.12:5.2 - A circulation selected away by minimum norm {#a-circulation-selected-away-by-minimum-norm}

Three stores exchange material around a directed cycle. Let the nonnegative transfers be a from the first to the second, b from the second to the third, and c from the third to the first. Their stock changes are

`F(a,b,c)=(c-a, a-b, b-c).`

Observed zero stock changes allow every (a,b,c)=(t,t,t) with t>=0. Minimizing a^2+b^2+c^2 selects t=0. The minimizer is unique, yet a circulation of one unit gives exactly the same records. Minimum norm has supplied a nominal no-circulation choice, not evidence that no transfer occurred.

A question about net stock change is already settled. A question about gross transported amount 3*t remains unresolved unless the subject account supplies another restriction or observation. If the stores can circulate material during unchanged stocks, using the minimum-norm answer as measured throughput would erase the quantity being sought.

### MMP.12:5.3 - An accumulated quantity with an unstable derivative {#an-accumulated-quantity-with-an-unstable-derivative}

In a continuous model on the normalized time interval [0,2*pi], accumulated activity is N(t), and its rate is r(t)=N'(t). Consider

`N(t)=2*t; N_k(t)=2*t + sin(k*t)/k`

for positive integers k. Their maximum difference is 1/k, tending to zero. Their rates are 2 and `2+cos(k*t)`, whose maximum difference remains 1. Both accumulated curves are nondecreasing. Thus nonnegativity of the rate does not remove this instability in the maximum norm.

A justified bound on rapid rate variation, or a penalty on changes in the rate, can suppress the oscillatory alternative. It also risks suppressing a real short surge. Specify which temporal detail the receiving use needs before selecting that structure.

If the use needs only the total over this interval, both curves give 4*pi. Recover that target from the endpoints without differentiating. For a fixed sampling interval a finite-difference inverse is continuous, but its error amplification grows as the interval shrinks; this differs from the discontinuity of the function-space inverse just exhibited.

## MMP.12:6 - Bias-Annotation {#bias-annotation}

The quadratic case makes sensitivity and shrinkage calculable. It does not make quadratic penalties appropriate for every unknown. A smoothness preference can remove discontinuities; a sparsity preference depends on the representation; a learned preference can lose features absent from its construction cases.

The method treats the subject grounds of additional structure as a separate contribution. Its mathematical examples establish consequences of stated premises, not the suitability of those premises for a particular physical or organizational situation. More consequential use can require stronger subject evidence or a validated target bound; ordinary use can stop at an already sufficient comparison.

## MMP.12:8 - Common Anti-Patterns and How to Avoid Them {#common-anti-patterns-and-how-to-avoid-them}

| Failure | Repair |
| --- | --- |
| A unique penalized minimizer is reported as an identified subject value. | Show which data-indistinguishable alternatives the penalty selected among; retain the selection premise. |
| A smaller residual is treated as a better reconstruction. | Compare propagated error and regularization bias for the required target, as in :5.1. |
| An old penalty is retained after the noise or forward relation changes. | Recalculate its discrepancy, sensitivity and lost target detail under the changed condition. |
| A smooth or learned reconstruction is used for a feature its construction suppresses. | Change the restriction or return the feature as unresolved; the rate surge in :5.3 shows the relevant loss. |
| A solver's convergence is offered as stability of recovery. | State the fixed computational problem solved and separately establish sensitivity or the noise-dependent limit. |

## MMP.12:10 - Architectural Rationale {#architectural-rationale}

The forward relation determines what the records respond to. The target determines which unresolved variations matter. Regularization determines which remaining variations the reconstruction discourages. Keeping these three contributions separate explains why one fitted answer can be useful for a nominal simulation yet inadequate as evidence about the subject.

This method extends compatible-case interpretation by constructing the recovery rule, choosing its strength and analyzing its induced loss. The distinction from computational approximation preserves the ability to solve the chosen equations accurately while still revising their recovery assumptions.

## MMP.12:11 - SoTA-Echoing {#sota-echoing}

**How should a needed reconstruction be stabilized at the available accuracy?** The selected line separates propagated error from regularization bias and chooses strength for their receiving use. The serious defaults are direct inversion or least-squares fitting, and the sufficient-bound route of C.16.IR. In :5.1, elementary calculations expose the direct gain of 100 and the selected gain of 50 at comparable effort, with shrinkage as the accepted cost. The bound wins when it settles the question; direct inversion wins after the tighter observation. **Adopt** this conditional choice in :4.2–4.5 rather than a default penalty. [Clason, *Regularization of Inverse Problems*, arXiv:2001.00617v2, Chapter 4, equation (26), and Chapters 6–7](https://arxiv.org/html/2001.00617v2) supplies the mathematical error decomposition and parameter-dependent recovery line, including iterative regularization. Its operator assumptions delimit those results; it does not justify a subject penalty. Reopen the choice when a simpler recovery or bound meets the same target conditions, or when changed error or model structure defeats the selected strength.

**When can newer learned reconstruction change that choice?** **Adapt** the distinction between reconstruction fit and recovery guarantees from [Bednarski and Roith, *Introduction to Regularization and Learning Methods for Inverse Problems*, arXiv:2508.18178v1, §§1.3–1.4, 2.3 and 3.2–3.3](https://arxiv.org/html/2508.18178v1). Its mathematical treatment is a best-known-line candidate for comparing classical and data-dependent regularization: training distributions and parameter rules matter to the resulting guarantee. This changes :4.3–4.5 by retaining the added structure and its recovery conditions when R is learned. A trained replacement is a serious alternative when a simple penalty loses important structure, but requires a target-specific comparison including its extra preparation cost.

[Hertrich et al., *Learning Regularization Functionals for Inverse Problems: A Comparative Study*, arXiv:2510.01755v1, §§5.1–5.5](https://arxiv.org/html/2510.01755v1) supplies bounded rival and failure evidence: its imaging comparisons show dependence on training, task and cost, and report attractive reconstructed geometry that differs from ground truth. **Reject** transferring an imaging ranking into a general reconstruction rule. Retain its action-changing lesson in :4.3: compare the actual required feature under applicable conditions. Reopen when a learned alternative preserves that feature better at justified total effort, or when a changed observation model or subject domain invalidates the comparison.


## MMP.12:End {#end}
