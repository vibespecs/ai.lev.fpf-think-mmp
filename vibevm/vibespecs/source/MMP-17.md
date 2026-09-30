# MMP.17 - Construct a Surrogate for Selected Model Responses: depth {#depth}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Depth sections of the pattern; the working sections are in the contract document of the same id. See LICENSE.md for the list of changes.

## MMP.17:5 - Archetypal Grounding {#archetypal-grounding}

### MMP.17:5.1 - Refine an interpolation only until it settles the comparison {#refine-an-interpolation-only-until-it-settles-the-comparison}

A repeated calculation needs the response \(r(x)\) of a costly reference model for \(0\leq x\leq1\). The present question is whether \(r(0.4)\leq0.3\). Available analysis of the reference model gives \(|r''(x)|\leq2\). Its accurate case values are \(r(0)=0\) and \(r(1)=1\).

The first surrogate is the line \(\widehat r(x)=x\). For linear interpolation on an interval of width \(h\), the curvature bound gives an error at most \(2h^2/8\). With \(h=1\), the response at \(0.4\) is therefore enclosed by \(0.4\pm0.25\). This interval crosses \(0.3\); the replacement has not answered the question.

Query the reference model at \(x=0.5\), obtaining \(r(0.5)=0.25\), and use the two half-intervals. In the first half, \(\widehat r(x)=0.5x\), so \(\widehat r(0.4)=0.2\). The bound is now \(2(0.5)^2/8=0.0625\), giving

\[
r(0.4)\in[0.1375,\,0.2625].
\]

The upper endpoint is below \(0.3\). One added case and a specified interpolation rule settle the comparison under the curvature premise. The three values alone would not justify the bound.

Now the receiving limit changes to \(0.18\). The same enclosure crosses that limit. For this one query, the practitioner returns to the reference model at \(0.4\), which gives \(0.16\), and can answer the stricter comparison. If many similar queries are expected, further subdivision may instead be worthwhile. There is no need to improve the surrogate over the entire interval to finish the single question.

These calculations establish agreement with the reference model under its stated smoothness and case-accuracy conditions. Whether that model's response represents the subject phenomenon remains a separate modeling question.

### MMP.17:5.2 - Correct a cheap allocation model, then change its regime {#correct-a-cheap-allocation-model-then-change-its-regime}

A network model returns delivered quantities \(q_1(d)\) and \(q_2(d)\) through two channels for demand \(2\leq d\leq4\). In the normal regime all demand is served, so \(q_1+q_2=d\). A cheap approximation splits it equally: \(L(d)=(d/2,d/2)\).

The source supplies \(q(2)=(1.2,0.8)\) and \(q(4)=(3,1)\). The first-channel discrepancies from \(L\) are \(0.2\) and \(1\). Linear interpolation of that discrepancy gives

\[
\widehat d_1(d)=0.4d-0.6,\qquad
\widehat q_1(d)=0.9d-0.6,\qquad
\widehat q_2(d)=d-\widehat q_1(d).
\]

At demand \(3\), the replacement returns \((2.1,0.9)\). It preserves total delivery and nonnegativity throughout the declared interval. Those properties follow from the construction; agreement between the cases has not yet been established.

The receiving question is whether the first delivery stays at or below \(2.25\) at demand \(3\). The provisional value \(2.1\) is only \(0.15\) below the limit, and there is no supported error bound for this interpolation. A source query at \(3\) returns \((2.4,0.6)\), ruling out the proposed limit. Add its discrepancy \(0.9\) and interpolate separately over \([2,3]\) and \([3,4]\). The new surrogate matches all three cases and preserves the balance. Further-input accuracy remains an empirical question or requires a separate bound.

Now channel 2 becomes unavailable. The normal-regime fit does not describe this input. Suppose the changed source account states that channel 1 serves all demand up to \(3\) units and any excess remains unserved. The needed output now includes unserved demand \(u\):

\[
q_1=\min(d,3),\qquad q_2=0,\qquad u=d-q_1.
\]

At demand \(4\), the result is \((3,0,1)\). The balance has become \(q_1+q_2+u=d\). This branch follows from the newly supplied operating rule, not from extrapolating the normal-regime cases. Its formula is already cheap enough to use; training another replacement adds no benefit here. The caller can retain the normal-regime surrogate for its supported questions and use this formula for the stated unavailable-channel regime.

### MMP.17:5.3 - Reuse stochastic cases when the requested response changes {#reuse-stochastic-cases-when-the-requested-response-changes}

A stochastic loss model returns either \(0\) or \(5\). Its source structure states that the probability \(p(x)\) of loss \(5\) is affine for \(0\leq x\leq1\); the two endpoint probabilities are unknown. All 2,000 runs in the construction are independent: 1,000 runs give 100 losses of \(5\) at \(x=0\), and another 1,000 give 300 at \(x=1\).

Fit the endpoint proportions and interpolate:

\[
\widehat p(x)=0.1+0.2x,\qquad
\widehat\mu(x)=5\widehat p(x)=0.5+x.
\]

The affine premise comes from the source structure, not from the two observed proportions. The mean surrogate is evaluable without rerunning the stochastic source.

At \(x=0.5\), the estimated mean is \(1\). A simple uncertainty calculation illustrates what must accompany that value. Each endpoint proportion has variance at most \(1/(4{,}000)\). Independence gives variance at most \(1/(8{,}000)\) for their average, an unbiased estimator of \(p(0.5)\) under the affine premise. Chebyshev's inequality therefore gives coverage of at least 95% for a half-width of \(0.05\) around that average. The resulting probability interval is \([0.15,0.25]\), and the corresponding mean interval is \([0.75,1.25]\). For a receiver using this 95% confidence procedure, the upper endpoint supports the mean-at-most-\(1.4\) comparison; it is not a deterministic bound. MMP.13 permits sharper uncertainty calculations when the receiving use needs them.

The receiver now asks whether \(\Pr(Y_{0.5}>4)\leq0.18\). The mean alone cannot answer: a constant loss of \(1\) has the same mean but a different tail. Here the retained two-point support supplies the relation \(\Pr(Y_x>4)=p(x)=\mu(x)/5\). Reuse the same cases and the probability surrogate; no new fit is needed. The interval \([0.15,0.25]\) crosses \(0.18\), so this uncertainty result leaves the new comparison unresolved.

The interval concerns the fixed input \(0.5\) under independent runs, the stated support and the affine probability law. It is not a simultaneous guarantee for all inputs, and it does not cover error in those source premises. A sharper inference, a useful bound, more runs or a qualified unresolved answer are different possible continuations; choose among them for the receiving question.

## MMP.17:6 - Bias-Annotation {#bias-annotation}

Convenient source cases can overrepresent smooth central behavior and miss a boundary, rare response or minority regime. Begin with the receiving consequence, then check whether the construction and assessment actually expose it.

A family with a smooth uncertainty indicator can understate error where all its members share the same missing structure. Source comparisons outside the currently attractive region can reveal that failure. The indicator's numerical precision does not strengthen its grounds.

Construction cost can be hidden by reporting only evaluation speed. Compare the reuse expected in this work, including source queries and repair, before attributing a practical saving.

## MMP.17:8 - Common Anti-Patterns and How to Avoid Them {#common-anti-patterns-and-how-to-avoid-them}

| Invited mistake | Repair |
| --- | --- |
| Declare success from small average error while a limit crossing is wrong. | Compare the response and error in the receiving operation, including the affected input region. |
| Treat an optimization objective as the constructed surrogate. | Supply the fitting procedure and the evaluator; inspect computational failure separately from inadequate cases or family. |
| Add cheap cases whose model misses the needed regime. | Examine the cheap-to-source discrepancy and compare correction with source-only construction at the same total effort. |
| Differentiate or invert a value surrogate without carrying its approximation. | Include the required operation in construction and error analysis, or keep the source for that operation. |
| Use the same cases repeatedly for tuning and claim untouched assessment. | Treat them as construction information and qualify the remaining further-use result. |
| Read a fitted interval as a guarantee against missing source structure. | Retain its conditions and return to source-model criticism or the subject account when those conditions change. |

## MMP.17:10 - Architectural Rationale {#architectural-rationale}

The response and the receiver's operation are chosen before the representation because they determine which differences matter. Reconstructing an entire model can waste effort; reproducing only a convenient summary can remove what the next operation needs. Selecting \(Q\) and \(D\) makes that trade-off actionable.

MMP.11 constructs families from known relations. MMP.17 adds the substitution question: which source responses to retain, which cases make their replacement informative, and where to refine or return when the replacement changes a receiving answer. CMP.7 and CMP.6 supply learning and computation when those are the chosen construction, while CMP.8 supplies numerical approximation control. The interpolation branch shows why a surrogate need not require a learner.

The source remains distinguishable from its replacement because a source call can repair approximation without repairing the model's account of the world. MMP.14 governs the latter discrepancy. Likewise, fast predictive use can coexist with a separate explanatory model; neither role earns the other's conclusions by sharing outputs.

## MMP.17:11 - SoTA-Echoing {#sota-echoing}

The practice question is how to obtain a reusable response at lower total effort without losing what the receiver must do with it. The selected answer is a response-specific construction with informative cases, retained structure, and refinement or source return where the receiving consequence remains unresolved. It does not select one model family for every input dimension, data budget and error claim.

**Adaptive construction versus a fixed case budget.** [Winovich et al., *Active operator learning with predictive uncertainty quantification for partial differential equations*, v4 (2026), §§2 and 5](https://arxiv.org/html/2503.03178v4) compares uncertainty-guided construction with alternatives that differ in accuracy and training cost. **Adapt** this experimental line in :4.2 and :4.5: target informative queries while counting the guidance cost. Fixed distributed cases remain a serious alternative when guidance is unreliable or expensive. The PDE experiments establish neither general superiority nor error bounds at arbitrary inputs. Reopen the choice when consequential errors escape the indicator or the cost balance changes.

**Combined models versus a single replacement.** [Brunel et al., *A survey on multi-fidelity surrogates for simulators with functional outputs: unified framework and benchmark* (2025), §§3 and 6.6](https://arxiv.org/html/2408.17075v2) compares correction, mapping and fusion; its benchmark has no universal winner. **Adopt** paired correction in :4.3 and **adapt** the comparison in :4.5: retain the cheap model when its discrepancy is easier to represent than the whole response at comparable total effort. Interpolation or single-source construction can otherwise win. The functional-output results inform this branch, not the method's domain boundary. Lost features or weak correspondence reopen the choice.

**Structural restriction versus expressive universality.** [Kovachki, Lanthaler and Mhaskar, *Data Complexity Estimates for Operator Learning*, v2, introduction and main results](https://arxiv.org/html/2405.15992v2) supplies a theoretical counterweight to choosing an expressive learner first. Their general operator classes can require exponentially many examples, while more restricted approximation classes permit better rates under their assumptions. **Reject** expressive capacity as sufficient grounds for affordable construction; **adapt** the consequence in :4.1–:4.3 by reducing the target and using justified structure before expanding the learner. The results concern specified classes and access models, not the sample count for an arbitrary engineering model. Reopen the restriction when it excludes a consequential response.

For the scalar bounded case in :5.1, interpolation already answers the needed comparison with one added case and a supplied curvature bound. An operator learner or statistical uncertainty model would add assumptions and construction work without improving that answer. For coupled outputs or large response families, the retained contemporary branches can instead justify their extra cost. That difference, rather than a universal ranking of algorithms, selects the branch.


## MMP.17:End {#end}
