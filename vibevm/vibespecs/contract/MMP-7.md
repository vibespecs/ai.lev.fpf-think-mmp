# MMP.7 - Construct a Probability Model of the Recorded Data {#root}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Working sections of the pattern; its depth sections live in the source document named by the last line. See LICENSE.md for the list of changes.

> **Type:** Method pattern
> **Status:** Usable, evolving
> **Normativity:** Normative within the stated use

## MMP.7:1 - Problem frame {#problem-frame}

Use this pattern when inference depends on how events, responses or quantities become records, and that procedure has not yet been expressed in the probability model. A feedback log may contain successes more often than failures. A timed trial can end before its event occurs. Several readings can share one calibration error. In each case, fitting a familiar distribution to the visible numbers can answer a different question from the one you intended.

Start with one possible event and follow what the observing procedure would record. Include the possibility that it leaves no record, reports an interval or shares an influence with another observation. Repeat for a contrasting event. These cases reveal what the mathematical outcome must contain before you choose its distribution.

The result is a probability law for the recorded outcome under stated assumptions, together with its relation to the quantity being inferred. It can supply a likelihood, a distribution of future records or a reason the intended inference remains ambiguous. This pattern develops probabilistic formulation within mathematical modeling. The subject practice supplies the meaning of the event, the observation procedure and plausible relations among quantities.

You need conditional probability and sums over alternatives; continuous cases also use densities and integration. A collaborator can supply those operations when you can describe the observation procedure and interpret the returned law. If an existing model already represents that procedure and answers the question, use it. When only compatible ranges are needed, C.16.IR can provide a sufficient answer without probabilities.

## MMP.7:2 - Problem {#problem}

The distribution of a subject property and the distribution of its records can differ. Selection changes which cases appear. Coarsening combines several possible values into one report. A common influence makes observations dependent. These transformations remain part of the inference even when a dataset presents every row in the same format.

A formula such as independent errors around a predicted value already makes choices about those transformations. If the choices are left implicit, more data and more accurate computation can reinforce a mistaken interpretation.

The difficulty is to construct the law of the observations from the modeled subject and its recording procedure, preserving the dependencies that matter to the question.

## MMP.7:3 - Forces {#forces}

| Choice | What changes in the inference |
| --- | --- |
| Target population and included cases | A result about reported cases may require a selection model before it describes the target population. |
| Retain or remove unobserved quantities | Keeping them can clarify construction; summing or integrating them out can simplify computation. |
| Separate and shared influences | Conditional independence can hold while observations remain dependent after a shared influence is removed. |
| Rich observation model and obtainable information | Extra parameters can represent real effects while leaving the desired answer less identifiable. |
| Probabilistic answer and sufficient conditional answer | A likelihood can be useful before choosing an estimator or a prior. A bound may already settle the action. |

## MMP.7:4 - Solution {#solution}

Construct the possible recorded outcomes from the observation procedure. Combine the subject and recording laws, remove the unobserved alternatives by the appropriate probability operation, and inspect what the resulting law permits you to infer. Return to the procedure or assumptions when its output does not answer the working question.

### MMP.7:4.1 - Choose the target and the recorded outcome separately {#choose-the-target-and-the-recorded-outcome-separately}

State what the answer concerns: a rate in a population, a property before measurement, a future response, or another quantity selected by the work. Specify the population, conditions and time range when they change its meaning. Use C.16 for the characteristic being measured and C.16.MR for the relation from the property to an indication.

Describe one complete outcome of the observing procedure. It may contain a value and an inclusion flag, a duration and a timeout flag, or several related readings. The mathematical outcome space must distinguish every report the procedure can produce that affects the inference.

State what the observation plan fixes. Following a known cohort produces information about excluded cases that a sample drawn only from submitted reports may lack. Stopping after a specified time, after a specified number of records, or after an event can produce different data laws. Recover the actual plan before treating any count as fixed.

### MMP.7:4.2 - Construct the joint law from the modeled dependencies {#construct-the-joint-law-from-the-modeled-dependencies}

Introduce variables for the quantities used by that procedure. Explain their domains and meanings before assigning distributions. Let Z denote an underlying event or value and O its recorded outcome. Parameters theta describe quantities held fixed in the proposed probability model. When these laws are represented by probability masses or by densities under an appropriate reference measure, write the subject law as p_theta(z) and the conditional recording law as k_theta(o given z). Their joint expression is:

`p_theta(z,o) = p_theta(z) k_theta(o given z).`

Each factor needs an interpretation. The first describes variation in the subject under the stated conditions; the second describes how the procedure records it. A deterministic recorder assigns probability one to its specified output and zero to the other outputs. This accommodates rounding and threshold reports as well as random response or selection.

Use a sequence of conditional laws when more stages matter. Multiplication follows the chain rule. Omitting a variable from a conditional law asserts that, given the retained variables, it does not change that law. Make that assumption from the modeled relation; separate rows in a file provide no independence argument.

Keep an unknown fixed parameter as unknown. Give it a probability distribution only when that additional modeling choice is justified for the intended inference. A shared but unknown calibration offset can remain a parameter in a joint likelihood. A distribution over possible offsets supports a different, explicitly extended model.

### MMP.7:4.3 - Obtain the law for what was actually recorded {#obtain-the-law-for-what-was-actually-recorded}

The general operation averages the chance of an observed event over the underlying cases. Let K_theta(B given z) be the chance that the report falls in a set B, given underlying value z. Then:

`P_theta(O in B) = integral K_theta(B given z) P_theta(dz).`

Here P_theta(dz) means averaging with the probability law of Z: a weighted sum for discrete cases or an integral for continuous ones. A deterministic recorder O=g(Z) has K equal to one when g(z) lies in B and zero otherwise. This constructs its output law even when the joint pair (Z,O) has no ordinary joint density, as with O=Z for a continuously varying Z.

When the masses or densities used in :4.2 are available, the same averaging operation gives the law of a particular report. For discrete unobserved alternatives, sum:

`p_theta(o) = sum_z p_theta(z) k_theta(o given z).`

For continuous alternatives, integrate the product of the subject density and the recording factor. A report produced exactly when Z lies in a fixed set A has recording factor one inside A and zero outside; its probability reduces to the integral of the density over A. If the procedure chooses which set to report, retain that choice in k_theta(A given z).

For example, let Z be equally likely to be 0 or 1. A truthful recorder reports {0,1} always when Z=0 and with probability 1/2 when Z=1; otherwise it reports {1}. The probability of receiving {0,1} is `1/2 + (1/2)(1/2) = 3/4`, although the probability that Z lies in {0,1} is one. The recording factor makes the difference.

For an individually observed continuous value, use a density with respect to the stated measurement convention. A point density and the probability of an interval have different meanings.

When inclusion in the dataset is itself a condition of sampling, retain its normalization. If Z has density or mass p_theta(z), and s_theta(z) is its probability of inclusion, the included-case law is:

`p_theta(z given included) = p_theta(z) s_theta(z) / P_theta(included).`

The denominator is obtained by summing or integrating the numerator over all admitted z and must be positive. If it depends on theta, dropping it changes the inference. When the counts or identities of excluded cases are also observed, include that information in the joint outcome instead of silently discarding it by conditioning. Section :5.1 shows the change.

Keep shared influences shared during elimination. For observations conditionally independent given an unknown B, integrating one joint product over B generally differs from multiplying separately integrated factors. The latter construction assigns a fresh B to each observation. Use it only when that is the observing arrangement.

### MMP.7:4.4 - Connect the law to inference and prediction {#connect-the-law-to-inference-and-prediction}

When the observation laws have a common probability-mass or density representation, insert the recorded outcome o into p_theta(o). As a function of theta, this gives a likelihood, up to a factor independent of theta. It need not sum or integrate to one over theta. Estimation or a posterior distribution requires the chosen inferential method and its assumptions; the observation law is the input to that work.

Before drawing an inference, check whether the recording rule admits the received report for any parameter value. A continuous reading can be admitted even though its single-point probability is zero; determine admissibility from the modeled observation mechanism and the cases it permits. If no admitted case produces the report, return the conflict and locate which assumptions or recording steps need reconsideration, using C.16.IR:4.4. For example, a fixed signal with one fixed additive offset and one unchanged threshold must produce identical bits on repetition. A mixed sequence contradicts that joint account. It cannot be repaired by fitting a different signal within the same family.

Identify how the requested quantity depends on theta or on a future outcome. Two parameter settings can induce the same law for every possible record while assigning different values to the target. Constructing such a pair shows that this observation model cannot identify that distinction. C.16.IR supplies the corresponding compatible-case reasoning; numerical fitting alone cannot resolve it.

For a future record, specify whether its recording procedure is the same. For the underlying population quantity, return through the subject law rather than interpreting a selected-case rate as the population rate. A proposed intervention requires its changed relations under C.28; changing a predictor value in a fitted association is insufficient when the intervention changes how the data arise.

### MMP.7:4.5 - Test a consequence and revise the construction {#test-a-consequence-and-revise-the-construction}

Check normalization and a small case that follows the procedure. Enumerate a finite outcome space or generate subject cases and pass them through the recorder. Compare that construction with the probabilities or summaries derived from the observation law. C.29.2 supplies a computational construction when enumeration or integration needs further work.

When the inclusion rule, timeout, shared calibration or receiving question actually changes, revise the affected relation and carry its consequence through the calculation. Compare a plausible alternative condition when the comparison can change the intended use or returned claim; this can expose the observation mechanism beyond one fixed formula. An already sufficient construction under unchanged conditions needs no invented variation.

A simulation agreeing with the formula checks their agreement under the modeled assumptions. An available observation can challenge those assumptions; selected domain assurance determines which empirical comparison is worth performing. C.11.DUA helps choose between further observation, a conditional answer and acting with remaining uncertainty. Preserve a sufficient result without demanding another dataset merely because an influence remains unknown.

## MMP.7:7 - Conformance Checklist {#conformance-checklist}

- Can a reader identify the target and all possible reports that affect the inference?
- Do the subject and recording factors describe the stated procedure, including what it fixes and what it reveals?
- Are unobserved alternatives removed by a justified sum, integral or conditioning operation?
- Does the joint law preserve common influences and any information about excluded cases?
- Is the first result interpreted as a likelihood, estimate, prediction, bound or unresolved distinction with its respective conditions?
- Can the formulation be changed when the observing procedure or receiving question changes?

## MMP.7:9 - Consequences {#consequences}

The constructed law allows computation to answer the intended observation question and can expose an ambiguity before expensive fitting. A changed reporting procedure becomes a model change that can be analyzed. The work may also show that the target needs assumptions or information absent from the records; a narrower conditional answer can remain useful.

## MMP.7:12 - Relations {#relations}

C.16.MR constructs the relation from a sought property to its indication; this pattern makes its probability law usable for inference. C.16.IR identifies what the resulting observations can resolve. C.29.2 constructs a computation for marginalization, estimation or prediction when needed, and C.29.3 addresses its realization. C.28 governs a causal use of the result. MMP.8 uses the observation model to determine the information available to a decision. B.5.MPC.R coordinates a repair spanning subject interpretation, mathematical formulation and computation. ME uses the result when the observing procedure itself is being changed.


## Dependencies {#dependencies}

- @fact:DEPENDS-ON Dependencies (as published): spec://ai.lev/fpf-spec/contract/C-16-IR#root for interpretation and inference; spec://ai.lev/fpf-think-mmp/contract/MMP-11#root for unknown relations; spec://ai.lev/fpf-think-mmp/contract/MMP-8#root when the record informs a choice. @status:spec/done
- @fact:REFERENCED-BY Referenced by (computed from the Tables of Contents): spec://ai.lev/fpf-think-cmp/contract/CMP-7#root, spec://ai.lev/fpf-think-cmp/contract/CMP-9#root, spec://ai.lev/fpf-eng-dtm/contract/DTM-2#root, spec://ai.lev/fpf-think-mmp/contract/MMP-13#root, spec://ai.lev/fpf-think-mmp/contract/MMP-14#root, spec://ai.lev/fpf-think-mmp/contract/MMP-15#root, spec://ai.lev/fpf-think-mmp/contract/MMP-16#root, spec://ai.lev/fpf-think-mmp/contract/MMP-19#root, spec://ai.lev/fpf-think-mmp/contract/MMP-8#root, spec://ai.lev/fpf-think-mmp/contract/MMP-8-SD#root, spec://ai.lev/fpf-eng-ops/contract/OPS-10-1#root, spec://ai.lev/fpf-eng-ops/contract/OPS-15-1#root, spec://ai.lev/fpf-think-phy/contract/PHY-8#root @status:spec/done

#source spec://ai.lev/fpf-think-mmp/source/MMP-7
