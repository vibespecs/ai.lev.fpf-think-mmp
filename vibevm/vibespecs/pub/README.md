# Mathematical Modeling - Readme {#root}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Readme section of the publication. See LICENSE.md for the list of changes.

## Practical entries {#practical-entries}

Bring the question you need a model to answer. It may concern an unexplained observation, a proposed intervention, a design, a prediction or the way work is performed. A useful result can be a relation that makes calculation possible, a conditional answer, a reason to reject a proposal or a more precise question.

The methods in this language work together through the results they produce. A formulation says which possibilities the model admits. An observation model says which records those possibilities can produce. Recovery and inference determine what can be learned from those records. An information-dependent choice uses the resulting distinctions only when they are available in time. A failed prediction can send the work back to the observing procedure, a model relation or the calculation.

Enter where the difficulty occurs and reuse results you already have. If the question is not yet mathematical, FPF B.5.FM helps choose participants and propose relations; B.5.TU helps interpret an unfamiliar theory. C.29 connects the construction with what it represents. For example, a cart's total distance does not determine its final position. Signed displacements and a starting position answer that question on a straight path; a question about visits along the way needs further information. Once the needed objects are recognizable, MMP.10 expresses their constraints; MMP.11 constructs a family when a relation remains unknown.

The worked connections below show how an intermediate result changes the next operation. They are selected examples, not a catalogue or a prescribed modeling process. Use the Table of Contents for other questions and the pattern bodies for the methods, prerequisites and further examples. FPF supplies shared reasoning methods; Mathematical Thinking supplies reusable mathematical constructions.

You can ask an assisting agent: “Explain the result and give feedback in the language of my work, without framework jargon.”

A contribution already available can supply its result without being reconstructed.

### MMP-OBSERVATION-TO-ACTION - Turn an observing model into a workable instruction {#mmp-observation-to-action-turn-an-observing-model-into-a}

- **Situation:** A proposed way of working includes an observation followed by a decision, but their combined benefit is unclear.
- **Question:** What instruction can use that report, and which change to the work is worth making?
- **First useful result or blocker:** An instruction with its required information, timing and supported performance, or a contribution still needed before it can be used.
- **Start with:** [MMP.8](spec://ai.lev/fpf-think-mmp/contract/MMP-8#root) to formulate the choice; [MMP.7](spec://ai.lev/fpf-think-mmp/contract/MMP-7#root) when its reporting law is missing; ME.7 when the observing and acting methods must be combined or changed.
- **Stop or return:** Use a sufficient instruction. A changed recording procedure reopens the observation model; changed timing, allowed choices or success requirements reopen the decision. Use C.11.DUA when the benefit of further inquiry is uncertain.

#### Worked connection for MMP-OBSERVATION-TO-ACTION {#worked-connection-for-mmp-observation-to-action}

**A noisy report and a changed success requirement.** The observing and acting methods are examined together through ME.7 in [Method Engineering](spec://ai.lev/fpf-eng-me/pub/TOC#root).

Start with what successful work means. In MMP.8:5.2, one of two requests needs a scarce resource, and allocation must follow a report. With perfect timely information, an instruction can follow the report. Without a distinguishing report, each fixed allocation fails in one admitted circumstance.

For the noisy procedure, MMP.7 supplies a necessary intermediate result. Two channels may produce the report, but the record does not identify the channel. Sum over that unrecorded choice to obtain the reporting law for each actual circumstance. MMP.8:5.2 performs this calculation: following the report succeeds with probabilities 0.8 and 0.7 in the two circumstances. No prior probability for which circumstance is actual is needed for those conditional results.

Now construct what can be done with that report. MMP.8 compares the four deterministic instructions on a two-valued report. A requirement of at least 0.65 success in each circumstance admits following it. A zero-failure requirement does not. Changing the requirement to average success, with one circumstance occurring with probability 0.95, makes always allocating to that request preferable among the four instructions. The preferred instruction changed because the question changed; the observing procedure stayed the same.

Return this answer to the proposed work. The report must be produced before allocation, and the receiving participant must be able to follow the instruction. If obtaining a better report costs more than the improvement is worth, C.11.DUA can support a sufficient existing choice or acceptance of the remaining risk. If the observation itself changes the situation, first represent that intervention through C.28.MR and derive the reporting and outcome laws for the changed situation.

ME.7:4.1 helps examine the proposed composition: what each method contributes, how the report reaches the acting participant, and which timing and support conditions the whole needs. Its result can be a supported composition or a proposal with unresolved conditions. Retain the resource demands and timing when revising the mathematical question. The useful result is a change the work can perform, a supported explanation of why the present method suffices, or the specific contribution still needed to choose.

### MMP-RECORDS-TO-ANSWER - Reach a usable conclusion from incomplete and noisy records {#mmp-records-to-answer-reach-a-usable-conclusion-from-incomplete}

- **Situation:** A fitted model produces an answer, but ambiguity in the unknowns or in the observing procedure may change what that answer supports.
- **Question:** Which conclusion do the records warrant, and what must be revised when a consequential assumption fails?
- **First useful result or blocker:** An identifiable target and an inferential result with a stated meaning, or the unresolved difference that still changes its use.
- **Start with:** [MMP.7](spec://ai.lev/fpf-think-mmp/contract/MMP-7#root) for the record law, [MMP.12](spec://ai.lev/fpf-think-mmp/contract/MMP-12#root) for recovery and ambiguity, [MMP.13](spec://ai.lev/fpf-think-mmp/contract/MMP-13#root) for inference, and [MMP.14](spec://ai.lev/fpf-think-mmp/contract/MMP-14#root) when a prediction needs repair.
- **Stop or return:** Use a sufficient result under its stated assumptions. Additional diagnostics or observations are needed only when they can change the warranted use. A changed target, recording rule or dependence returns to the contribution it affects.

#### Worked connection for MMP-RECORDS-TO-ANSWER {#worked-connection-for-mmp-records-to-answer}

**1. Construct what can be observed.** Suppose two nonnegative contributions, u and v, produce only a total T=u+v in a measuring procedure. The task is to determine whether T is below 10.5 in the stated units. Initially the measuring practice supplies the model y_i=T+e_i for nine complete readings, with independent normally distributed errors of mean zero and known standard deviation 3. Their observed mean is 8.

MMP.7 turns that account into the joint law of the records. If a procedure instead discards readings outside a reporting range, its probability law must condition on that selection before the same inference can be attempted. MMP.11 is needed earlier if the relation between the unknowns and the observations has yet to be constructed.

**2. Ask what the law can distinguish.** MMP.12 examines changes that leave the records unchanged. Replacing (u,v) by (u+h,v-h), while both remain nonnegative, leaves T and the record law unchanged. No increase in the number of these total readings identifies the two contributions separately. The present target T remains identifiable, so its estimation need not wait for that unresolved decomposition. A question about u alone would require a restriction, another observation relation or a sufficient bound.

**3. Construct the claim needed for the decision.** Under the supplied law, MMP.13 gives the sample mean standard deviation 3/sqrt(9)=1. The rule “mean plus or minus 2” has about 95.45% repeated-sampling coverage for T. Applied here it gives [6,10]. Its upper end is below 10.5. Whether this is sufficient for the intended action depends on the consequence of a wrong answer and the accepted uncertainty; the interval itself supplies no permission to act. The confidence level describes the rule across repetitions, not a posterior probability for this realized interval.

This inference uses the total that MMP.12 found recoverable and the dependence assumptions that MMP.7 made explicit. A different requested claim, such as a posterior probability or the distribution of the next reading, needs the corresponding MMP.13 construction. A regularized split of u and v supplies neither of those claims.

**4. Recalculate after the observation premise changes.** An existing calibration investigation now establishes that all nine readings can share an unknown offset b, with |b|≤2. The measuring practice supplies this bound; a residual plot alone would not establish it. This changes the relation used by MMP.7 to y_i=T+b+e_i.

MMP.12 now exposes ambiguity between T and b. MMP.13 retains the interval for T+b and expands it over the admitted b values, giving [4,12] for T with at least the earlier coverage for each fixed admissible offset. The former threshold conclusion no longer follows. More repeated readings reduce the independent noise but do not determine b. A useful next move is a sufficient existing calibration bound, a qualified narrower answer or a different observation when its benefit warrants the work.

**5. Return to the question that will consume the result.** If an action must be selected despite the remaining uncertainty, MMP.8 formulates that choice using the information and timing actually available. If the question concerns changing the mechanism, FPF C.28 and C.28.MR identify the causal question and replacement: observing a variable at a value differs from forcing it to that value. MMP.15 then determines whether the available laws and causal assumptions identify the requested intervention consequence. An observational fit alone cannot supply that inference. If the original inferential answer is sufficient, the connection ends there.

If instead a consequential difference between predicted and observed records is the unresolved difficulty, MMP.14 compares them under the modeled conditions and helps locate the contribution to repair. A supplied change of premise, as in step 4, can return to the affected construction without that additional diagnosis.

The same joins support other observing procedures. Their general contribution is carrying a model's remaining ambiguity into the inference and its receiving use, then revising only the affected construction when an assumption changes.

### MMP-SUFFICIENT-ANSWER - Answer the working question before reconstructing every detail {#mmp-sufficient-answer-answer-the-working-question-before}

- **Situation:** A model omits internal distinctions, and reconstructing them may cost more than the requested answer needs.
- **Question:** Which consequences are shared by the remaining possibilities, and do they already decide the question?
- **First useful result or blocker:** A bound that settles the stated threshold, or the distinction whose unresolved value still changes the answer.
- **Start with:** [MMP.9](spec://ai.lev/fpf-think-mmp/contract/MMP-9#root) for lost evolution information; [MATH.20](spec://ai.lev/fpf-think-math/contract/MATH-20#root) for bounds; FPF C.29 for subject interpretation and C.11.DUA when further inquiry is a live choice.
- **Stop or return:** Use a settled answer under the supplied premises. A changed threshold, observation, law or time horizon returns to the affected comparison.

#### Worked connection for MMP-SUFFICIENT-ANSWER {#worked-connection-for-mmp-sufficient-answer}

**1. Make the receiving question specific.** A supplied account has two nonnegative populations with laws x'=-x and y'=-2y, where time uses the unit in which these rates are stated. The initial total is 1, but its split is unknown. Is the total remaining at time 3 below 0.1? This case starts with those laws; establishing a physical or other subject law is a different contribution.

**2. Recover the omitted contribution.** With z=x+y, MMP.9 gives z'=-x-2y. The same z=1 can have derivative -1 or -2, so the current total alone does not determine its rate of change. This result identifies the missing distinction and supplies alternatives for a bounding calculation.

**3. Derive an answer shared by those alternatives.** Put x(0)=a and y(0)=1-a, with 0≤a≤1. The equations give `z(t)=a*exp(-t)+(1-a)*exp(-2t)`. MATH.20 uses this convex combination to derive exp(-2t)≤z(t)≤exp(-t) for t≥0. At time 3, exp(-3)<0.05<0.1. The upper bound settles the question for every initial split. No estimate of a is needed for this answer.

**4. Return the consequence to the work.** C.29 asks what the populations, rates, total and threshold represent and which assumptions permit the interpretation. Under the supplied account, the condition is satisfied at time 3. Using that consequence in a real decision also uses the subject premises that made these equations applicable.

**5. Reopen what changes the answer.** Suppose the next question is whether z(1)<0.2. The bounds straddle 0.2. The same formula reduces the decision to a<(0.2-exp(-2))/(exp(-1)-exp(-2)), approximately 0.278. An available bound on a may settle this. Obtaining more about a is useful when it can change the decision enough to justify its cost; C.11.DUA helps make that choice. Changed evolution laws instead return to step 2, since the old enclosure may fail.

A different population or physical decay process can use this example when it supplies the stated laws and interpretation. The reusable connection is broader: reduction exposes a lost distinction, a mathematical comparison bounds its effects, and the receiving question decides whether those effects need further work.

### MMP-INTERVENTION-AND-INFORMATION - Decide whether an observation will improve the next action {#mmp-intervention-and-information-decide-whether-an-observation}

- **Situation:** Several actions have different consequences in circumstances that the current record does not fully distinguish.
- **Question:** What can the available data establish about those actions, and is another observation worth obtaining before acting?
- **First useful result or blocker:** A justified action comparison and a contingent instruction, or an assumption, distinction or timing condition still needed.
- **Start with:** [MMP.15](spec://ai.lev/fpf-think-mmp/contract/MMP-15#root) to identify the intervention consequences; [MMP.16](spec://ai.lev/fpf-think-mmp/contract/MMP-16#root) to compare obtainable information; [MMP.8.SD](spec://ai.lev/fpf-think-mmp/contract/MMP-8-SD#root) when observing and acting form successive choices.
- **Stop or return:** Use the sufficient existing instruction when further information cannot repay its burden. A changed recording law, effect of observing or available action reopens the affected construction.

#### Worked connection for MMP-INTERVENTION-AND-INFORMATION {#worked-connection-for-mmp-intervention-and-information}

**1. Establish what the actions would do.** A service must choose response A or B. Its current circumstance is H0 or H1, each with supplied probability 0.5. Earlier randomized work recorded the circumstance and supplies the following population mean losses:

| Circumstance | Response A | Response B |
| --- | ---: | ---: |
| H0 | 0 | 4 |
| H1 | 10 | 0 |

MMP.15 makes the use of these records explicit. The case assumes consistent response versions, no interference, positive assignment probability for each response in each recorded circumstance, and transfer of the conditional intervention means to the current service. Under those assumptions, randomization identifies the means in the table. They are stipulated population quantities here; estimates from finite records would also need MMP.13's uncertainty.

Without another indication, A has expected loss 5 and B has expected loss 2. This supplies the comparison that any proposed observation must improve.

**2. Construct the record the proposed observation would supply.** A diagnostic report is positive with probability 0.8 in H1 and 0.2 in H0. It does not change the circumstance or the subsequent action losses. Within each circumstance, the report supplies no further information about response loss. Its cost is 0.2 in the same loss units, and the report arrives before the response is chosen. MMP.7 retains this reporting law, rather than treating a positive report as certain knowledge of H1.

**3. Compare information through its consequence.** MMP.16 obtains a posterior probability of H1 equal to 0.8 after a positive report and 0.2 after a negative one. Choose B after positive: its conditional expected loss is 0.8. Choose A after negative: its conditional expected loss is 2. Each report has probability 0.5, so expected action loss is 1.4. The information reduces that loss by 0.6; including its 0.2 cost gives 1.6 rather than 2.

**4. Construct the continuing instruction.** MMP.8.SD represents the first choice, whether to obtain the report, and the later response choice. For the response choice after the report, the posterior belief is sufficient: the conditional mean losses depend only on H and there are no later choices. The resulting instruction is to obtain the report, then use the branch above. Subject and Method Engineering work supply the actual observing and acting capabilities. If the report cannot arrive in time, formulate the response choice from the information that will actually be available.

**5. Revise only what changed.** Suppose the available diagnostic now has the same positive probability, 0.5, in both circumstances. MMP.7's new law leaves the belief at 0.5 after either report. MMP.16 returns zero information benefit for the response decision; MMP.8.SD chooses B without the diagnostic and avoids its cost. If observing instead changes the circumstance, include that transition and the changed intervention consequences before reusing the former calculation.

**6. Recover the comparison if the question changes.** A later inquiry may ask which cases would have benefited from the other response, rather than which response minimizes future expected loss. [MMP.19](spec://ai.lev/fpf-think-mmp/contract/MMP-19#root) constructs the relation between a case's alternative responses. For an observed case, MMP.7/.13 first recover what its factual record implies about the underlying conditions; C.28.MR then changes the mechanism while retaining that case information.

Check what the available laws actually determine. In MMP.19:5.2, two models have identical action-specific success probabilities and identical randomized records, but give different answers about the same observed case under the other action. MMP.19 returns that ambiguity; a feasible observation is considered through MMP.16 only if it could resolve a useful distinction. Returning to the future expected-outcome criterion can make the unresolved same-case relation irrelevant. The earlier choice is then usable without that extra inquiry.

The connection can stop at a sufficient existing choice. The needed comparison determines whether to construct a report, a continuing instruction or a same-case counterfactual.

### MMP-REPLACE-AND-COUPLE - Use cheaper models without losing the combined answer {#mmp-replace-and-couple-use-cheaper-models-without-losing-the}

- **Situation:** A required answer combines expensive model contributions, and cheaper replacements are available.
- **Question:** What must each replacement supply, and which errors or shared dependencies can change the combined result?
- **First useful result or blocker:** A sufficient coupled answer with propagated approximation limits, or the component contribution that still needs refinement.
- **Start with:** [MMP.17](spec://ai.lev/fpf-think-mmp/contract/MMP-17#root) for the replacement's target and use region; [MMP.18](spec://ai.lev/fpf-think-mmp/contract/MMP-18#root) for the exchanged quantities and dependencies; MATH.20 for the needed bound.
- **Stop or return:** Keep a sufficient approximation. Return to the affected source model or interface when the bound no longer settles the question, or to MMP.14 when an observed discrepancy needs diagnosis.

#### Worked connection for MMP-REPLACE-AND-COUPLE {#worked-connection-for-mmp-replace-and-couple}

Two components contribute distinct amounts u and v to a total, in the same units and over the same interval. MMP.18 establishes that the required combination is u+v and that neither contribution already contains the other. MMP.17 selects surrogates for these two amounts on the input region being used.

For the present input, suppose their estimates are 0.42 and 0.48, with supported absolute error bounds 0.03 and 0.04. The resulting total is in [0.83,0.97]. It is below a threshold of 1 throughout that interval. No independence assumption is needed for this worst-case sum bound. Errors measured only on a few training cases would not, by themselves, supply the stipulated bounds.

Now lower the threshold to 0.94. The interval no longer settles whether the total is below it. If obtaining the second component from its source model is worthwhile, and that calculation returns 0.46 with absolute error at most 0.001, retaining the first surrogate gives [0.849,0.911]. That narrower combination settles the new question without replacing both surrogates.

A different question can instead change what the interface must carry. A time of threshold crossing needs information about evolution within the interval; two final amounts do not supply it. MMP.18 then returns the missing temporal contribution, and MMP.17 changes the response that a replacement must preserve. More accurate final amounts alone would answer the wrong question.

### MMP-REPRESENT - Why does counting the records overcount the assignments? {#mmp-represent-why-does-counting-the-records-overcount-the}

- **Situation:** A request can be left unassigned or assigned option 0 or 1. The data format uses a presence bit and an option bit.
- **Question:** Does counting the records count the intended assignments?
- **First useful result or blocker:** A representation with three possibilities per request, or weights that correct duplicate representations. When the presence bit is zero, either option bit denotes the same absent assignment.
- **Start with:** [MMP.10 - Construct and Revise a Mathematical Constraint Formulation](spec://ai.lev/fpf-think-mmp/contract/MMP-10#root), especially :5.2. Construct a valid representation, then determine whether its multiplicities preserve the requested count or sampling law.
- **Stop or return:** Use a sufficient count or representation. Reopen the translation when requirements or the requested operation change; a representation adequate for finding an assignment can still distort counting.
