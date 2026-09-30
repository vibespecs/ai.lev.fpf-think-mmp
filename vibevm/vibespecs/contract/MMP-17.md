# MMP.17 - Construct a Surrogate for Selected Model Responses {#root}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Working sections of the pattern; its depth sections live in the source document named by the last line. See LICENSE.md for the list of changes.

> **Type:** Method pattern
> **Status:** Usable, evolving
> **Normativity:** Normative within the stated use

## MMP.17:1 - Problem frame {#problem-frame}

**Use this when** repeated use of a model is too costly or cumbersome, and the next calculation needs only some of its responses. You may need values at many inputs, a probability of exceeding a limit, a field over a region, or a response used inside an inverse problem. Begin with one receiving question: which response must the replacement supply, over which inputs, and what error would change the answer?

A **surrogate** is a replacement constructed to reproduce selected responses of a source model. It may be an interpolation table, a constrained formula, a reduced representation of outputs, a learned function, or a correction to a cheaper model. The practical gain is a less costly response with a usable account of where substitution holds and where to return to the source.

This is a method of mathematical modeling. It applies to computational, physical, biological and organizational models; a differential equation or a neural network is one possible case. It governs the construction and use of a replacement, while the subject practice supplies the meaning and grounds of the source model. Agreement with that model and agreement with the world remain different questions.

Preparation requires functions, interpolation and an error comparison suited to the receiving calculation. The derivative branch uses elementary differentiation; the output-basis branch uses orthogonal projection and singular value decomposition. The stochastic branch requires expectation, variance and the meaning of interval coverage. For a learned replacement, CMP.7 supplies the learning rule and its further-use conditions, with CMP.6 supplying iterative computation when needed. A specialist can construct a harder approximation, but must return an evaluable replacement and the conditions under which its response can be substituted.

For a few inexpensive queries, evaluate the source or reuse already computed answers. If a prescribed numerical approximation already supplies the response and sufficient error control, CMP.8 may finish the work. Surrogate construction becomes useful when selecting the responses, cases and retained structure changes what can be obtained at affordable cost.

## MMP.17:2 - Problem {#problem}

A replacement can fit its construction cases and fail at the inputs or operations that matter next. Average accuracy can conceal a wrong threshold crossing, a lost dependence between outputs, or a derivative with the wrong sign. A source model can also be wrong in a way that its accurate surrogate faithfully reproduces.

The modeling problem is to construct a useful substitution without silently enlarging its promise: choose what to reproduce, obtain informative cases, build the replacement, and act on consequential discrepancies or lost structure.

## MMP.17:3 - Forces {#forces}

| Force | Tension |
| --- | --- |
| Selected response | Reproducing less can save work, while a later question may need something discarded. |
| Construction cost | More source evaluations can improve the replacement, but may consume the saving it was meant to provide. |
| Known structure | Conservation, bounds and symmetries restrict useful candidates; a convenient restriction can also exclude the needed response. |
| Local and broad use | Concentrating cases near a decision can improve that answer while leaving other inputs poorly represented. |
| Several error sources | Source computation, surrogate approximation and uncertain source premises can each limit use and require different repairs. |
| Continued use | Reuse makes construction worthwhile, but changed inputs or questions can invalidate the substitution. |

## MMP.17:4 - Solution {#solution}

Construct the replacement around the response that another calculation or person will use. Carry the source conditions into that substitution, and refine only where the remaining difference matters.

### MMP.17:4.1 - Select the response and the input region {#select-the-response-and-the-input-region}

Let \(M\) be the source model and let \(Q\) extract the required response. Write the target as

\[
r(x)=Q(M(x)),\qquad x\in D,
\]

where \(x\) contains the inputs and \(D\) is the intended region of use. The input may be a number, a vector, a history, a function or a discrete configuration. State enough of its meaning to distinguish materially different conditions. If the same listed input gives different deterministic responses because a regime or previous state was omitted, restore that input before fitting a function.

Choose \(Q\) from the receiving operation. A mean, a tail probability and an entire probability law are different targets. So are a field value, its spatial derivative and a quantity integrated over that field. For a random source output \(Y_x\), a mean surrogate targets \(\mathbb E[Y_x]\); reproducing individual draws or their distribution requires another construction.

Determine how response error affects the receiving result. For a comparison with a limit, the distance to the limit matters. For a ranking, the gap between alternatives matters. If the receiver will differentiate, iterate or invert the response, include the corresponding sensitivity or structural requirement. A low average value error does not select these requirements for the practitioner.

### MMP.17:4.2 - Obtain construction cases that can distinguish useful replacements {#obtain-construction-cases-that-can-distinguish-useful}

Reuse source results whose inputs, output meanings and computation are compatible with the target. Choose further cases to expose consequential variation: the region the receiver will visit, boundaries or changes of regime, and places where plausible replacements disagree about the receiving answer.

For a scalar interval, an initial set of endpoints and interior points may suffice. For many inputs, a full grid can be unaffordable; use known structure to reduce the varying inputs, or distribute a finite set across the relevant region before concentrating additional cases. A design concentrated near one operating point supports a local construction unless another argument supports wider use.

Each case supplies an input and the selected source response. If the source response is itself approximate, carry its error into the construction. For a stochastic source, use MMP.7 to identify how the runs were obtained: repetitions, dependence, shared random inputs and selection can change what their averages or fitted probabilities estimate. MMP.13 supplies the uncertainty result needed from those runs.

Choose case placement and assessment together. Cases used to fit, select or repeatedly tune the replacement are construction cases. If the further-use claim depends on held-out performance, retain assessment cases suited to that use and do not count their later reuse for tuning as untouched assessment. For trajectories, repeated runs or grouped inputs, the unit that must be held out follows the claim; randomly separating nearby points does not by itself test a new trajectory or regime.

A query to the source model adds information about that model's response. An observation of the world may also challenge the model. Keep those contributions separate. Use existing bounds or observations when they already answer the question; another experiment is not an entry condition for constructing a surrogate.

### MMP.17:4.3 - Construct an evaluable replacement with the needed structure {#construct-an-evaluable-replacement-with-the-needed-structure}

Start with a representation that can express the required response at the available construction cost. Use MMP.11 to preserve justified relations and to expose what remains adjustable.

For ordered scalar cases \((x_i,r_i)\), one complete construction is piecewise linear interpolation:

\[
\widehat r(x)
=\frac{x_{i+1}-x}{x_{i+1}-x_i}r_i
+\frac{x-x_i}{x_{i+1}-x_i}r_{i+1},
\qquad x_i\leq x\leq x_{i+1}.
\]

The rule supplies a response between distinct neighboring inputs. It needs no iterative training. Its adequacy between the cases still depends on the response's variation and the receiving tolerance.

For a field or a large output vector, one can instead construct

\[
\widehat y(x)=y_0+\sum_{j=1}^{k} a_j(x)\phi_j.
\]

Here \(y_0\) and the retained output shapes \(\phi_j\) come from known structure or computed cases. For example, take \(y_0\) as the mean case vector, stack the centered case vectors as columns, retain selected left singular vectors of that matrix, and project each centered case onto those orthonormal vectors. Then interpolate or learn the coefficient functions \(a_j(x)\) from the inputs and the computed coefficients. A small reconstruction error over sampled fields can still discard a localized feature that controls the receiver's maximum or threshold. If only \(Q(y)\) is needed, compare approximating that response directly with reconstructing the full field.

When a cheap model \(L\) already follows much of the response, construct a correction from paired cases:

\[
d_i=r(x_i)-L(x_i),\qquad
\widehat r(x)=L(x)+\widehat d(x).
\]

Pair the same inputs and corresponding outputs. This construction still evaluates \(L\) at each new input. It is useful when the discrepancy is easier to approximate than the whole response; if the cheap model misses the consequential regime, adding many cheap cases may help little.

For a learned function, supply CMP.7 with the target, construction cases, function family and loss that reflects the required response. Obtain its effective fitting procedure through CMP.6 or another suitable computation. Writing an objective without a way to obtain and evaluate its candidate leaves the replacement unfinished. Optimization progress, fit on construction cases and accuracy at further inputs are separate results.

Preserve a justified relation by construction when possible. If two delivered quantities must sum to an input \(d\), construct one and define the other as \(d-\widehat q_1\), while also enforcing any required nonnegativity or capacity limits. A small penalty for violating a relation permits violations; it does not implement the relation as an identity.

### MMP.17:4.4 - Locate errors and losses that change the receiving use {#locate-errors-and-losses-that-change-the-receiving-use}

Compare the replacement with the source in the quantities the receiver consumes. A deterministic bound, an empirical error on selected cases and a statistical interval support different conclusions.

When bounds are available in the same response metric, propagate them. For example, if interpolation of accurate case values differs from \(r\) by at most \(e_{\mathrm{int}}\), and each supplied case value has error at most \(e_{\mathrm{case}}\), convex linear interpolation has error at most \(e_{\mathrm{int}}+e_{\mathrm{case}}\). Other fitting rules need their own propagation: a poorly conditioned fit can amplify errors in its cases. CMP.8 supplies that numerical approximation and conditioning work.

For a scalar test \(r(x)\leq b\), a justified bound \(e(x)\) gives an immediate rule:

- if \(\widehat r(x)+e(x)\leq b\), the bound supports the test;
- if \(\widehat r(x)-e(x)>b\), the bound rules it out;
- otherwise the replacement leaves this test unresolved.

An observed maximum error at finitely many cases is not automatically a bound over \(D\). A statistical coverage result retains its sampling and calibration conditions and its pointwise, marginal or simultaneous meaning. A fitted uncertainty indicator can guide the next query without supplying such a result.

Test lost operations as well as values. On \([0,1]\), \(r(x)=x\) and \(\widehat r(x)=x+0.01\sin(1000x)\) differ in value by at most \(0.01\). Yet \(r'(x)=1\), while \(\widehat r'(\pi/1000)=-9\). If a receiver follows the derivative, this substitution can reverse the proposed direction. Include derivative information or a justified monotone family when that operation matters, or keep the source calculation for it.

A discrepancy with the source calls for examination of case coverage, representation or fitting. A discrepancy with observations can instead require MMP.14 to revise the source or its observation model. Agreement with the source cannot close that second question.

### MMP.17:4.5 - Refine, combine or return where the difference matters {#refine-combine-or-return-where-the-difference-matters}

Choose the next change from the unresolved receiving result. With piecewise interpolation and a bound on curvature, subdivide intervals whose error bound can change that result. With an empirical construction, inspect informative new source cases, a different family or a local correction. Adding cases everywhere can cost more than repairing the affected region.

For adaptive case selection, make a finite candidate set in the allowed region, compare its points by the expected relevance of their unresolved responses and an error or disagreement indicator, and query the chosen source cases. Retain coverage of plausible unexplored regimes; a confident but misspecified replacement can otherwise prevent its own correction. Refit after adding the cases and assess the changed replacement under the conditions needed for the claim. The indicator is a reason to investigate a point, not evidence that the source response there has already been obtained.

A useful combination may keep the source near a threshold or regime boundary and use the surrogate elsewhere. It may keep a cheap model with a learned correction, or different replacements for different response questions. Make the selection condition usable by the caller. When a query is outside the supported region or the needed error control is unavailable, call the source if it can answer, restrict the claim, or return the unresolved response.

Compare total effort: case generation, fitting, checking, each later evaluation, and repairs after relevant changes. A source call can finish a single difficult query more cheaply than improving a reusable approximation. Stop when the receiving question has sufficient support at acceptable cost. Use the existing FPF choice and improvement methods when several worthwhile replacements or refinements remain; this construction does not require one universal best surrogate.

### MMP.17:4.6 - Carry the substitution into continued use {#carry-the-substitution-into-continued-use}

Make the evaluation rule, input meanings and region, selected responses, and consequential limits available with the replacement. The receiver must be able to obtain its response and recognize when the fallback applies. A function with its conditions in the surrounding model may suffice.

When the surrogate enters an inverse problem or an uncertainty calculation, propagate its approximation in the observation metric and into the requested conclusion. A small forward-response error can matter greatly along a poorly resolved direction. MMP.12 supplies the ambiguity and regularization analysis; MMP.13 supplies the qualified inference and uncertainty. Treating the replacement as an exact likelihood or forward relation can give a tighter answer than its construction supports.

Reopen the construction when the input region, source assumptions or receiving operation changes. A new question about an intervention may need causal identification or a mechanism supplied by the subject practice, even if the old predictions remain accurate. A new request for explanation needs the relevant relations, not only the same output number. Use C.2.8 to distinguish the structure a reader can recover and EXD to construct an explanation from a supplied subject account. A compact surrogate may expose useful structure, but compactness and predictive fit do not establish that contribution.

## MMP.17:7 - Conformance Checklist {#conformance-checklist}

Use these questions when relying on or passing on the replacement. The answers can remain in the model and its explanation.

| Check | Required content |
| --- | --- |
| Target | The source, selected responses, receiving operation and input region are recoverable. |
| Cases | Their obtaining conditions and any source-computation or sampling uncertainty fit the construction. |
| Construction | The representation and obtaining rule produce an evaluable replacement; justified coupled constraints are retained. |
| Consequential error | The error comparison addresses the receiving result and states whether its grounds are a bound, empirical comparison or statistical result. |
| Lost structure | A required derivative, dependence, regime or explanatory relation has not been inferred from value fit alone. |
| Continued use | The caller can identify unresolved queries and use the supported refinement, restriction or source return. |
| Effort | Construction and continued-use costs justify the substitution for the intended work. |

## MMP.17:9 - Consequences {#consequences}

Selected responses can become cheap enough for repeated comparison, simulation or inference. Known constraints can remain usable even when most of the source calculation is replaced, and a local source return can resolve the few queries that remain difficult.

The saving comes with a narrower promise and construction cost. Different responses may need different replacements. A changed question can reuse the cases while changing the response construction, as in the tail-probability example, or require a changed source account, as in the unavailable-channel example.

## MMP.17:12 - Relations {#relations}

- **MMP.11** supplies families constrained by known relations; MMP.17 consumes them to reproduce selected source responses.
- **MMP.7 and MMP.13** supply the obtaining law and qualified inference for stochastic construction cases. **MMP.12** supplies ambiguity, stability and regularization when the replacement enters an inverse problem.
- **MMP.14** finds and repairs predictive discrepancies that can require a changed source model; a surrogate-to-source discrepancy can often be repaired within the present construction.
- **CMP.7, CMP.6 and CMP.8** supply, respectively, a learning rule with further-use conditions, iterative computation where needed, and numerical approximation or error propagation. None selects the receiving model response on behalf of the practitioner.
- **C.2.8 and EXD** distinguish recoverable structure and explanatory work from predictive agreement. **C.28.MR** supplies intervention consequences inside a stated causal model; agreement of surrogate outputs does not identify that model.
- **C.11/C.11.CRC** compare worthwhile choices and contributions; **C.18** governs retention and Pareto-front claims; **G.5** declares a selected set when that is the needed result. **E.22/E.23** frame and conduct improvement. MMP.17 supplies the candidate replacements and their response/error/cost consequences, not another portfolio or improvement method.


## Dependencies {#dependencies}

- @fact:DEPENDS-ON Dependencies (as published): spec://ai.lev/fpf-think-mmp/contract/MMP-11#root for retained structure; spec://ai.lev/fpf-think-cmp/contract/CMP-7#root/.6 for learning and updates; spec://ai.lev/fpf-think-mmp/contract/MMP-14#root for consequential mismatch; spec://ai.lev/fpf-think-mmp/contract/MMP-18#root for coupled use. @status:spec/done
- @fact:REFERENCED-BY Referenced by (computed from the Tables of Contents): spec://ai.lev/fpf-eng-syse/contract/SYSE-49#root @status:spec/done

#source spec://ai.lev/fpf-think-mmp/source/MMP-17
