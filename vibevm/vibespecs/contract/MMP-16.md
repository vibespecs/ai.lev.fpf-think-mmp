# MMP.16 - Design Observations to Separate Mathematical Model Alternatives {#root}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Working sections of the pattern; its depth sections live in the source document named by the last line. See LICENSE.md for the list of changes.

> **Type:** Method pattern
> **Status:** Usable, evolving
> **Normativity:** Normative within the stated use

## MMP.16:1 - Problem frame {#problem-frame}

Use this pattern when several mathematical accounts remain possible and the next useful answer depends on a difference between them. You can choose which cases to observe, under which conditions, or how to record them. The difficulty is to find an attainable observation that exposes the relevant difference.

The desired result may be a better decision, a supported prediction, a distinction between proposed mechanisms, or a new research direction. For example, two response laws agree at all previously tried inputs but imply different behavior in the intended use. Repeating those inputs more accurately may leave the disagreement untouched.

This pattern constructs the mathematical design of an observation. It returns what to observe, what records the alternatives would produce, and how those records would change the answer. It can instead return a useful limitation: the available observation choices leave the needed distinction unresolved. The subject practice supplies feasible access and performs the observation; PHY.9 and PHY.10 do that work for a physical readout and test.

Start with the receiving question, the alternative models and the observation law from MMP.7. Set-valued reasoning needs functions and sets. Probabilistic design also needs conditional probability and the inferential meaning chosen in MMP.13. An analyst can supply that mathematics while another participant supplies the observing conditions and interprets the result.

Use the present answer directly when the remaining alternatives make no consequential difference. A new observation is only one possible response to uncertainty. C.11.DUA supplies the comparison with using what is already known, changing the claim or taking another feasible step. A routine prescribed measurement with an already sufficient design needs no new design study.

## MMP.16:2 - Problem {#problem}

A model can predict a large difference that the actual record cannot show. An instrument may saturate, a log may aggregate away timing, or an unknown offset may account for the apparent difference. Conversely, overlapping distributions can still support a useful distinction; requiring one observation to identify the model without error can reject worthwhile designs.

An observation can also be highly informative about something irrelevant to the requested result. Choosing a design by parameter uncertainty, fit or model label can therefore direct effort away from the question that made the modeling useful.

The problem is to construct a feasible observation whose possible records support a consequential comparison, with the uncertainty and cost that this use can tolerate.

## MMP.16:3 - Forces {#forces}

| Force | Tension |
| --- | --- |
| Visible contrast and recorded contrast | Models can disagree about an unobserved quantity while predicting the same available record. |
| Model identity and receiving result | Different models may support the same answer; a single model family may contain the important disagreement. |
| Discrimination and uncertainty | One certain separating observation is attractive, but useful statistical distinctions often retain error. |
| Informative design and model adequacy | A design can be excellent within an inadequate model family. |
| Learning and available work | A better distinction can cost more time, access or computation than its contribution warrants. |
| Immediate gain and continued inquiry | One observation may prepare a later useful test without answering the final question itself. |

## MMP.16:4 - Solution {#solution}

State the disagreement that matters. Derive the records each alternative can produce under feasible observation choices. Construct a comparison of those records that improves the receiving answer, and compare the attainable benefit with the work involved. Obtain the selected observation only when that comparison supports it; otherwise use the present result or change the question or access.

### MMP.16:4.1 - Locate the consequential disagreement {#locate-the-consequential-disagreement}

Write the answer that would differ. It may be a threshold response, a predicted event, an intervention consequence or which conjecture to develop next. For a numerical target, write it as q(h,theta), where h selects a model and theta contains its remaining unknowns. Different theta within one model can matter as much as different model labels.

Recover what the present observations and assumptions leave possible. MMP.11 constructs the family of models; MMP.12 exposes a recovery ambiguity; MMP.13 supplies probabilistic conclusions when used. Group equivalent parameterizations by the behavior relevant to this question.

Ask which remaining disagreements change the intended answer or a worthwhile later inquiry. If all retained alternatives already support the same sufficient answer, return it.

### MMP.16:4.2 - Construct the law of the obtainable records {#construct-the-law-of-the-obtainable-records}

Let d denote a feasible design: the selected inputs or cases, preparation, observing times and recording procedure. For each alternative derive either:

- a set R(h,theta,d) of possible records under its bounded uncertainties; or
- a probability law P(Y | h,theta,d) for the records Y.

The record includes what the procedure would actually retain. Compose the modeled response with the selection, measurement, censoring, rounding or aggregation operation. If an intervention changes the subject, derive its response under that intervention; an observational association alone supplies no such law.

Keep unknowns shared across readings shared. An unknown calibration offset cannot take one arbitrary value for the first reading and an unrelated value for the next if the same offset governs both. A repeated observation can reduce independent noise while leaving that common ambiguity intact.

A probabilistic comparison integrates unknowns only under a supplied probability law. Otherwise retain them as conditional possibilities or compare performance across their admitted range. Choosing a convenient nuisance value separately for each model can make a design look more discriminating than it is.

For an adaptive design, later observation choices are functions of records already available. Derive their joint law with that dependence. A sequence of fixed-design calculations does not by itself describe an outcome-dependent stopping or sampling rule.

### MMP.16:4.3 - Find what a design can distinguish {#find-what-a-design-can-distinguish}

First seek a simple consequential contrast. For a set-valued model, take the union of R(h,theta,d) over the remaining possible theta. Disjoint unions for two alternatives give a separating observation under those assumptions. If the unions overlap, identify records that would settle the needed distinction and records that would leave it open.

Equal sets alone do not establish equal statistical information: probability laws can weight the same possible records differently. In a probabilistic model, compare the full record laws or a statistic whose retained information suffices for the requested result. Distinct means are one possible contrast, not a universal criterion.

An impossibility conclusion needs its scope. Two alternatives that give the same record law under every currently feasible design, yet different required answers, demonstrate a distinction unavailable through those designs. More repetitions under the same uninformative access do not resolve it. Changing the observation type, access or target may do so. Failure of a numerical search to find a good design establishes only that search result.

A narrower target can remain obtainable. Suppose all feasible records leave the individual parameters unresolved, but every compatible parameter pair gives the same total response. Return the total when it answers the work question. Recovering each parameter is then unnecessary.

### MMP.16:4.4 - Construct the design criterion from the receiving use {#construct-the-design-criterion-from-the-receiving-use}

For a required distinction with controlled statistical error, construct a rule T(Y) that returns the answer or an unresolved result. For example, let two specified hypotheses have record densities p0(y;d) and p1(y;d) relative to the same measure. For a chosen threshold c, the rule selects H1 on the region A={y: p1(y;d)>c*p0(y;d)} and H0 otherwise. Calculate P0(A), the chance of selecting H1 under H0, and P1(A-complement), the opposite error. Compare designs and thresholds that meet the required error bound. For a composite hypothesis, the claimed protection across its parameter range requires controlling the error across that range, rather than only at a fitted value.

Other decision rules can retain an unresolved answer when that is useful. Their comparison likewise follows from their record laws and the error consequences the use requires.

When probability, actions and losses are appropriate, let pi be the current joint law of the unknowns, a an available action, and L(a,h,theta) its loss. For a finite set of action choices and an observation that changes information alone, compare:

~~~
R0 = min_a E_pi[L(a,h,theta)]

R(d) = E_Y[min_a E[L(a,h,theta) | Y,d]]

value of sample information = R0 - R(d).
~~~

The inner choice uses the observed record; the outer expectation averages records that are still unknown when the design is chosen. In this formulation the recipient can ignore the record and retain the old action, so R(d) cannot exceed R0 under the same model. Subtracting the full cost of obtaining and using the information can still make the proposal unattractive. :5.2 carries out the calculation.

If the experiment itself changes the state, available actions or their consequences, include those effects in the decision model. The simple information-only comparison above is then insufficient. MMP.8.SD constructs the continuing state, information and consequence model.

An information criterion is another branch. For a selected unknown Q, expected information gain is the mutual information I(Q;Y | d) under the supplied joint law. Choosing Q as the model label, all parameters or a wanted prediction defines different design problems. Use this criterion when resolving that uncertainty serves the stated inquiry. It does not measure every practical consequence of the observation.

The comparison need not be a probability calculation. A guaranteed separation, an ordinal improvement, or a change in attainable answers can suffice. Use the existing FPF choice and portfolio methods when several gains and burdens remain incomparable. This pattern supplies the modeled observation consequences, not a new general system for valuing research.

### MMP.16:4.5 - Construct and compare attainable designs {#construct-and-compare-attainable-designs}

Use the contrast to generate alternatives: observe where responses differ, resolve an omitted component, vary an input independently, measure at a different scale or time, or change how the record is made. Derive the resulting record laws before optimizing a convenient proxy.

For a small set of designs, calculate the selected criterion directly. For a large set, use the applicable search or numerical method from Computational Thinking. Count the cost of evaluating a design as part of the work. If approximate criteria cannot reliably order close candidates, return that uncertainty, retain several designs, or refine the calculation where a changed ranking matters.

Compare against using current information. C.11.DUA governs the attainable contribution, delay, displaced work and any disputed evidence demand. When an information-only design has a bound on its possible benefit below its cost, that bound can end the comparison without computing its criterion more accurately.

For a sequence of observations, decide whether the immediate comparison represents the intended horizon. An apparently uninformative first step may enable a later separating observation. Construct that continuation with MMP.8.SD when it changes the choice; do not require a full sequential optimization for a sufficient one-step design.

### MMP.16:4.6 - Use the result and reopen the implicated assumption {#use-the-result-and-reopen-the-implicated-assumption}

Return enough for the observation to be performed and interpreted: the selected conditions, records to retain, comparison rule, and the consequence of an unresolved or conflicting result. A design calculation remains a prediction about possible records; it is not an observation already obtained.

After observing, use the inference and comparison that match the actual procedure. If access, stopping or recording changed, revise the affected law before interpreting the result. For example, replacing a numerical readout by a threshold alarm changes the available distinction.

Model discrimination compares the alternatives supplied. If every alternative fails to explain an important record, MMP.14 returns to the relevant subject or observation assumption. Selecting the least poor alternative can support a limited approximation, but its winning score alone does not establish adequacy.

Where the intended use covers different conditions from the selected observations, carry that difference into the receiving prediction. Recent work on active learning under model misspecification shows why concentrating observations for parameter information can worsen prediction elsewhere. Compare alternative observation regions or model families when this vulnerability can change the design or receiving prediction.

## MMP.16:7 - Conformance Checklist {#conformance-checklist}

A constructed design supports its intended use when:

- the remaining disagreement and the answer it could change are identifiable;
- its predicted records follow from the alternatives and the actual selection and recording procedure;
- shared unknowns and adaptive choices retain their dependencies;
- the claimed separation, error property or expected improvement follows from a reconstructible comparison;
- any criterion based on information names the unknown being learned and its receiving use;
- feasibility and burden are compared at the scope needed for the decision, using present information as an available alternative;
- the result explains how the selected records change the answer and when an incompatible record returns to the model or observation assumptions.

These conditions concern the mathematical design and its stated assumptions. They do not establish that the observation was performed, that its subject assumptions hold, or that access is authorized. Stronger assurance belongs to the actual intended use.

## MMP.16:9 - Consequences {#consequences}

The next observation becomes a constructed part of modeling: a specified change in available information with a stated consequence. A no-separation result can redirect effort from repeated measurement to a different readout, access route or question.

Good designs depend on assumptions about records and their use. A computed optimum can change when the observer, cost, model family or research horizon changes. For expensive searches, a sufficient feasible design may be more useful than a more precisely optimized proposal.

In methodology, the same construction helps compare alternative accounts of a working method. Choose a case or observation that makes their consequential disagreement visible. Human and automated procedures can both be studied this way; the subject method supplies what can be changed and observed.

## MMP.16:12 - Relations {#relations}

- **MMP.7** constructs the law of what is recorded; **MMP.11** constructs the admitted model family.
- **MMP.12** exposes recovery ambiguities; **MMP.13** supplies inference and uncertainty claims that match the chosen observation procedure.
- **MMP.14** investigates failed predictions and returns to the implicated subject or observation assumption.
- **MMP.15** supplies causal identification when the target is an intervention effect. A new association does not by itself identify that effect.
- **MMP.8** formulates the receiving choice; **MMP.8.SD** constructs a longer observation-and-action sequence when continuation changes the design.
- **C.11.DUA** appraises an evidence demand and its attainable contribution; **C.11** and the applicable portfolio methods compare attainable gains with resources and other consequences.
- **C.16.IR** supports a sufficient answer despite unresolved distinctions. **B.5.TC** relates a test to the theoretical comparison it is meant to change.
- **PHY.9** constructs a physical readout and **PHY.10** a physical test. Other subject practices realize the corresponding access and observation.
- **Computational Thinking** supplies the selected search, sampling or approximation procedure. **MMP.17** consumes an informative-case design when constructing a surrogate.


## Dependencies {#dependencies}

- @fact:DEPENDS-ON Dependencies (as published): spec://ai.lev/fpf-think-mmp/contract/MMP-7#root/.11/.12/.13 for predicted record laws; spec://ai.lev/fpf-think-mmp/contract/MMP-8#root/.8.SD for decisions; spec://ai.lev/fpf-spec/contract/C-11-DUA#root for worthwhile further work; subject methods for realization. @status:spec/done
- @fact:REFERENCED-BY Referenced by (computed from the Tables of Contents): spec://ai.lev/fpf-eng-dtm/contract/DTM-5#root, spec://ai.lev/fpf-eng-dtm/contract/DTM-7#root, spec://ai.lev/fpf-think-mmp/contract/MMP-15#root @status:spec/done

#source spec://ai.lev/fpf-think-mmp/source/MMP-16
