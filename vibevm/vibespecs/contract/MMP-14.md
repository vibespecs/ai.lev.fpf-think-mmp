# MMP.14 - Find and Repair a Mathematical Model's Failed Predictions {#root}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Working sections of the pattern; its depth sections live in the source document named by the last line. See LICENSE.md for the list of changes.

> **Type:** Method pattern
> **Status:** Usable, evolving
> **Normativity:** Normative within the stated use

## MMP.14:1 - Problem frame {#problem-frame}

Use this pattern when a mathematical model's predictions leave a consequential feature of the available observations unexplained, or when a proposed use makes such a discrepancy worth examining. A model may reproduce an overall average while missing conditional responses, bursts, extremes or the records that a selection rule actually permits.

Start with one needed prediction and a feature whose failure would change its use. For overload, compare relevant tails or sequences, not only the fitted mean. Construct that feature under the model on comparable records. The first result can be a localized discrepancy, a repaired calculation, or a sufficient reason to retain a narrower use.

The principal result is a changed model, the assumption changed, and the consequence that must be recalculated. A supported restriction of use or an unresolved choice between repairs can also be the useful result. A small residual is not a certificate of adequacy; a nonzero residual is not automatically a model failure.

This is model criticism within mathematical modeling. MMP.7 supplies the recording law, MMP.11 the available model family, and MMP.13 inference within a stated model. Here the work constructs and interprets comparisons that can change that model. A physical, biological, economic or other subject method supplies the meaning and admissibility of the proposed repair. Predictive improvement alone identifies neither a causal mechanism nor an intervention effect.

Do not reopen an adequate application merely to run a standard collection of diagnostics. An established calculation, bound or checked prediction may already suffice under unchanged conditions. C.11.DUA selects further checking when its possible outcomes can change the answer, claim or warranted use. New observations, model enlargement and simulation are not routine prerequisites.

## MMP.14:2 - Problem {#problem}

An optimizer can improve fit without repairing the needed prediction. A model can fail a broad diagnostic while retaining a sufficient narrower answer. Apparent disagreement can also come from comparing latent quantities with selected records, numerical approximation, or ordinary model-permitted variation.

Even a real discrepancy rarely names its cause. Large residuals might reflect a missing predictor, varying noise, dependence, selection or an erroneous observation. Wholesale replacement hides the changed assumption; making every observed feature look ordinary can fit chance patterns.

The working problem is to construct a comparison that can expose the relevant mismatch, trace it to a revisable part of the model, and establish what the revision changes without treating reused data or simulated agreement as new external evidence.

## MMP.14:3 - Forces {#forces}

| Force | Consequence for the method |
| --- | --- |
| Intended use versus overall fit | The discrepancy must retain distinctions on which the receiving prediction depends. |
| Sensitivity versus ordinary variation | A useful diagnostic can reveal systematic failure without declaring every unusual observation erroneous. |
| Localization versus ambiguity | A pattern of failure narrows repairs but often does not uniquely identify the defective assumption. |
| Adaptation versus evaluation | Data used to choose a repair cannot also supply an untouched assessment of that choice. |
| Flexibility versus retained structure | A repair must preserve needed constraints and account for the additional estimation or regularization it introduces. |
| Assurance versus effort | Use available comparisons first; acquire more evidence only for a consequential unresolved claim. |

## MMP.14:4 - Solution {#solution}

**Choose a consequential discrepancy → construct comparable predictions → locate the mismatch → change the implicated assumption → recalculate and compare the consequence → return the warranted use.**

### MMP.14:4.1 - Choose the prediction and the discrepancy together {#choose-the-prediction-and-the-discrepancy-together}

State the receiving quantity and conditions: a response at specified inputs, a probability of exceeding a limit, a distribution of recorded counts, or a forecast for a given horizon and group. Name the relevant observational unit. A message, a batch of messages and a whole operating period support different comparisons.

Recover the model and its observation law. Retain units, inputs, initial conditions, exposure, recording rules and material dependence. Separate unknown parameters from assumptions such as constant response, independent errors or complete recording.

Choose a discrepancy \(D\) that responds to a failure relevant to this use. For example:

- Conditional bias can be exposed by mean residuals within relevant input ranges, rather than a mean over all inputs.
- A tail count \(D(y)=\sum_i 1\{y_i>u\}\) asks whether the model accounts for excursions beyond the consequential level \(u\).
- A run length or \(D(r)=\sum_{i=2}^n r_i r_{i-1}\), with residuals in their actual order, can expose dependence hidden by a histogram.
- A distribution of recorded categories can reveal that predictions concern unfiltered events while observations concern selected records.

A conditional plot, a few statistics or a direct bound can suffice. Explain which repair would change the feature. A statistic that fitting nearly forces to agree, such as the mean in a fitted constant-mean model, usually contributes little to detecting omitted structure.

The user needs the target, conditional distributions or bounds, and the comparison's construction. Obtain a missing calculation from a mathematically qualified collaborator: for example, a record generator and a discrepancy's reference distribution. A human or AI participant may supply it; recover the subject assumptions and interpretation before using its output.

### MMP.14:4.2 - Generate the comparison the question requires {#generate-the-comparison-the-question-requires}

Compare quantities with the same meaning. Replicated physical states are not yet rounded, censored or selected records. Carry them through MMP.7's recording law.

For a **posterior predictive comparison**, obtain joint parameter draws from MMP.13 and generate records conditionally:
\[
 \theta^{(s)}\sim\pi_M(\theta\mid y,x),\qquad
 y^{\mathrm{rep},(s)}\sim p_M(y^{\mathrm{rep}}\mid x,\theta^{(s)}).
\]
Here \(M\) names the model and \(x\) the retained input and recording conditions. Compare \(D(y)\) with \(D(y^{\mathrm{rep},(s)})\). If the discrepancy depends on parameters, calculate \(D(y,\theta^{(s)})\) and \(D(y^{\mathrm{rep},(s)},\theta^{(s)})\) at the same draw.

Decide what repeats. New observations for existing groups with their inferred effects differ from new groups with regenerated effects. Retain or regenerate effects according to the questioned prediction. Do not independently redraw an effect that should be common to an entire batch.

A **non-Bayesian comparison** can use a specified parameter value, an exact conditional reference distribution that eliminates a nuisance parameter, or a fitted-model simulation. State which is used. When the reference concerns a statistic of a fitted procedure, reproduce the fitting step on each simulated dataset; a simulation that holds its fitted coefficients fixed generally answers a different question. A parametric bootstrap may approximate a reference distribution, not make its calibration exact.

For a **held-out comparison**, construct the forecast without using the records being predicted to fit, tune or select that forecast. Keep preprocessing inside the corresponding training operation. Choose the withheld unit and allowed information for the receiving prediction: new observations in an existing group, a whole new group, or a future block with a specified horizon. A convenient random split does not by itself establish future or new-group performance. An alternative split needs an argument that its bias and variability suffice for the intended conclusion.

Write a held-out predictive law as \(Q_M(y_H\mid y_T,x)\), where \(T\) is the available training information and \(H\) the withheld portion. Compare the models on the same \(H\), target and scoring convention. Use a joint block prediction when the question depends on within-block dependence. Pointwise scores can still answer a declared marginal prediction question; they do not test all joint behavior.

Exact enumeration or algebra may replace simulation. If a deterministic prediction and an observation each have established error bounds, compare their admissible ranges. Disjoint ranges expose an incompatibility under those bounds; overlapping ranges do not prove the model.

### MMP.14:4.3 - Interpret the difference at the comparison's actual strength {#interpret-the-difference-at-the-comparison-s-actual-strength}

Inspect where discrepancies occur, not just whether one aggregate score changes. Compare direction, size, input region and persistence with the variations that the reference construction permits.

A posterior predictive tail fraction describes a conditional comparison under the fitted model. It is not generally a frequentist p-value with a uniform null distribution. An exact conditional tail probability, a fitted bootstrap approximation and a held-out loss have different interpretations. None is the probability that the model is false.

Account for the construction's resolution when it can change the result. Zero exceedances in finitely many simulations does not establish a zero tail probability. Approximation error, poor sampling or an inaccurate held-out calculation can create an apparent discrepancy. CMP.8/.9 supply the relevant numerical error account. Checking recovery on data generated by the model can expose computational faults; success there does not establish the model's correspondence with the subject.

A pattern found after searching many views remains a useful clue, but its nominal tail area is not automatically calibrated for that search. If a repeated-error guarantee matters, account for the selection or use a suitable untouched comparison. Exploratory diagnosis need not claim that guarantee.

A discrepancy can warrant restricted use, examination of one component, or rejection of a prediction. Failure to expose one means only that this check, at this resolution, has not exposed it.

### MMP.14:4.4 - Change the part that explains the consequential mismatch {#change-the-part-that-explains-the-consequential-mismatch}

First trace the disputed prediction through its calculation and observation meaning. A wrong unit, event label, numerical solution or censoring convention can require correction without changing the underlying subject relation.

Then formulate a small number of plausible revisions. Show the changed mathematical component and why it can affect the discrepancy:

| Located feature | Possible construction to examine |
| --- | --- |
| Residual means vary with an omitted input | Replace \(m_0(x)\) by \(m_0(x)+b\,h(x)\), with a subject-admissible function \(h\); estimate \(b\) and recalculate the relevant conditional response. |
| Dispersion varies by input while the mean remains adequate | Replace constant error scale by a positive function \(s(x)\); compare conditional spread and the receiving tail probability. |
| Residual sequences have dependence absent from the model | Replace independent errors by a specified covariance or a recurrence such as \(e_t=\rho e_{t-1}+\eta_t\); derive the resulting block or horizon prediction. |
| Available records exclude outcomes the prediction includes | Change the recording or selection component using the established inclusion rule; predict the retained records, keeping the latent law separately visible. |

These are candidates, not conclusions from the symptom alone. Do not delete observations or inflate noise until everything passes. Several changes can reproduce the feature; use subject knowledge and existing discriminating observations to choose, retain conditional alternatives, or return the missing distinction.

Use MMP.11 to preserve support, constraints and known relations when extending the family. Use MMP.13 to infer the revised unknowns; MMP.12 supplies a justified restriction when added flexibility makes recovery unstable. Changed priors, constraints or noise laws can change the answer without adding information to the records.

If the remaining difference is worth a new observation, return the distinguishing prediction and feasible-design question to the applicable observation-design and subject methods. A predictive repair does not identify an intervention effect; obtain the required causal assumptions and identification separately when that is the receiving question. A narrower supported use can finish without either continuation.

### MMP.14:4.5 - Recalculate the consequence and examine the repair {#recalculate-the-consequence-and-examine-the-repair}

Recalculate the original discrepancy and the receiving quantity under the revision. Adding a term to an equation leaves both questions unfinished. Show what changes and what remains unchanged.

Compare with the previous model and a serious sufficient alternative on the same available basis. A simpler model can be preferable when its retained result suffices and the added component contributes only estimation noise or cost. A better average score can coexist with a worse consequential tail or subgroup prediction; inspect that conflict directly.

Distinguish **repair construction** from **assessment of the repaired prediction**. Reproducing the data that motivated the revision shows what the revision accommodates. An untouched set of suitable existing records can assess a forecast fixed before those records are inspected. When repeated tuning consumes that set, it becomes part of development. If the needed performance claim concerns the whole adaptive procedure, its assessment must include that adaptation, for example through a suitable outer split; it is not a test of one retrospectively selected fit.

Fresh observations are not the only useful continuation. Recalculate with available held-out records, derive the affected consequence, retain a conditional result or restrict use. C.11.DUA determines whether resolving the remaining limitation is worth its cost. Do not describe an unperformed comparison as successful.

### MMP.14:4.6 - Return the model and its changed use {#return-the-model-and-its-changed-use}

Return the changed relation or distribution, retained assumptions, relevant comparison, and consequence to use or recalculate. Include ambiguity where it affects use. A short explained calculation can suffice.

For a methodological use, return which discrepancy reveals the omitted distinction, how to produce comparable predictions, and which component to reconsider. For an unresolved subject use, identify the missing contribution instead of a generic demand for more data.

Recognition starts with a consequential disagreement. Assurance depends on the claim: algebra establishes a recalculated consequence; a computational check establishes its numerical execution; an appropriate comparison with observations supports the bounded subject use. Reopen when the target, regime, recording law, relevant evidence or consequential error requirement changes.

## MMP.14:7 - Conformance Checklist {#conformance-checklist}

- The questioned prediction and a discrepancy that can change its use are recoverable.
- Observed and predicted quantities share the relevant inputs, recording meaning, unit and dependence conditions.
- The replication, conditioning or withholding construction supports the interpretation actually claimed.
- Computational error and ordinary model-permitted variation have not been silently treated as subject-model failure.
- A proposed repair names the changed mathematical component and its subject basis; unresolved alternatives remain visible where consequential.
- The receiving consequence has been recalculated, and the role of data reused during repair is stated where it limits assessment.
- The result gives a warranted use, restriction or missing contribution, without imposing new evidence acquisition on a sufficient existing answer.

## MMP.14:9 - Consequences {#consequences}

The practitioner can replace “the model fits badly” with a calculable failed prediction and an explicit revised assumption. Downstream users can see which consequence changes, which remains sufficient, and which use is unsupported.

Comparable predictions cost work. Adaptive repair consumes assessment information, and extra parameters can weaken estimation. Improving one feature can leave another failure unresolved. Retain the use boundary without demanding exhaustive criticism of every model.

## MMP.14:12 - Relations {#relations}

- **B.5.TC / B.5.RR:** align accounts and revise dependent reasoning; this method supplies the model-criticism constructions.
- **MMP.7:** constructs the law of recorded data used for comparable predictions and repairs to selection or measurement assumptions.
- **MMP.11 / MMP.10:** supply admissible model families and constraint formulations when the failed prediction requires a changed relation.
- **MMP.13 / MMP.12 / C.16.IR:** supply inference, regularized recovery and the limits of what records resolve; a repaired fit does not remove those limits.
- **CMP.8 / CMP.9 / MATH.20:** obtain predictions and discrepancy calculations with the relevant numerical error or bound.
- **Causal-identification and observation-design methods:** receive the unresolved causal effect or distinguishing-observation question when it matters. Obtain these contributions from a suitable subject source or collaborator.
- **C.11.DUA and the subject method:** select worthwhile checking and establish the subject meaning of a repair. The receiving practice uses the revised prediction or restriction.


## Dependencies {#dependencies}

- @fact:DEPENDS-ON Dependencies (as published): spec://ai.lev/fpf-think-mmp/contract/MMP-7#root/.11/.13 for comparable predictions; spec://ai.lev/fpf-spec/contract/B-5-RR#root for affected revision; spec://ai.lev/fpf-think-cmp/contract/CMP-8#root/.9 for numerical error; spec://ai.lev/fpf-spec/contract/C-11-DUA#root for worthwhile further checking. @status:spec/done
- @fact:REFERENCED-BY Referenced by (computed from the Tables of Contents): spec://ai.lev/fpf-think-mmp/contract/MMP-13#root, spec://ai.lev/fpf-think-mmp/contract/MMP-17#root @status:spec/done

#source spec://ai.lev/fpf-think-mmp/source/MMP-14
