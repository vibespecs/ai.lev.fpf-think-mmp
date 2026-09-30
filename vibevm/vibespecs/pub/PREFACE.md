# Mathematical Modeling - Preface {#root}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Preface of the publication. See LICENSE.md for the list of changes.

## MMP.Preface:1 - Problem frame - Make a mathematical question useful {#preface-1}

You may know the relevant formulas and still be unable to build a model for the question in front of you. The candidate objects may be unclear. A recorded value may hide part of the observing procedure. A proposed decision may use information that arrives too late. A detailed model may become affordable only after removing something its answer depends on.

Mathematical Modeling develops methods for constructing and revising such mathematical questions. Its subject can be a physical situation, a working method, a computational process or another mathematical construction. The useful result may be a prediction, an explanation, an admissible arrangement, an instruction, a bound or a question that directs further inquiry. Start with what that result would let you understand or do.

This language belongs to the Foundational Thinking DPF Suite alongside Mathematical Thinking, Physical Thinking, Computational Thinking and Notational Engineering. Its three parts address formulation, inference and model revision, and changes that preserve a needed use. The Table of Contents identifies the methods available here; obtaining a contribution outside them still needs another source or collaborator.

The mathematical account and the subject supply different parts of the reasoning. A relation describing a material, an observing procedure or a permitted action needs its corresponding subject knowledge. A mathematical construction then helps express the relation and derive consequences. The answer returns to the original question with the conditions under which that interpretation holds. The [First Principles Framework (FPF)](spec://ai.lev/fpf-spec/pub/TOC#root) develops this connection in B.5.FM and the C.29 family; the bodies here develop particular model-forming operations within it. Find a named FPF pattern by its full code in FPF-Spec.md and open its Problem frame and Solution. If GitHub cannot display the large file, use its View raw or Download raw file action, then search that copy.

The needed preparation depends on the operation. Finite arrangements can use sets, functions and elementary counting. Probabilistic recording needs conditional probability and sums or integrals. Evolution and reduction can require differential equations. Each body states its prerequisites and works small cases. When a collaborator or assisting agent supplies the mathematics, ask for the meaning of its inputs, its conditions and the result the next part of your work can use. You can ask for that explanation in the language of your work.

Begin with the [Readme](spec://ai.lev/fpf-think-mmp/pub/README#root) when the useful entry is unclear. Enter a body directly when its Problem frame matches the difficulty.

## MMP.Preface:2 - Problem and forces - Choose what the model must retain {#preface-2}

A model can answer a mathematically well-formed question that differs from the one the work needs. This often happens before calculation: a convenient variable excludes an allowed arrangement, a mean hides a distinction needed for action, or a fitted relation describes observation while the question concerns an intervention.

Several choices therefore shape the construction:

| Working tension | Consequential choice |
| --- | --- |
| A familiar representation and the intended objects | Which distinctions must variables, domains and conditions preserve? |
| Supported structure and an unknown relation | What may vary, and what must remain true throughout that variation? |
| An event and its recorded description | Which unobserved, selected or combined alternatives can produce this record? |
| Knowing a circumstance and choosing before it is known | Which information may the instruction actually use? |
| A detailed account and an affordable answer | Which eliminated contribution needs reconstruction, approximation or a bound? |
| Resolving every unknown and settling the present question | Which remaining differences can change the required consequence? |
| Stable recovery and added assumptions | What variation does a restriction suppress, and could the requested target depend on it? |
| An uncertainty label and the claim it supports | Is the needed result a coverage guarantee, a posterior probability or a prediction for a new outcome? |
| Agreement in one use and a changed use | Which premise, mechanism or interpretation must be reconsidered? |

The requested answer determines how far to develop the model. A bound can settle a threshold question while leaving parameters unresolved. A proposal for a new working method can instead require distinctions that an earlier prediction ignored. C.11.DUA helps decide whether another calculation, observation or refinement is worth its possible contribution.

## MMP.Preface:3 - Solution - Connect the contributions the question needs {#preface-3}

### MMP.Preface:3.1 - Form the first account and recover its interpretation {#mmp-preface-3-1-form-the-first-account-and-recover-its}

If there is no mathematical question yet, use B.5.FM: identify the participants, propose the relations relevant to the difficulty, work a small consequence and return it to the question. B.5.TU helps when an available theory supplies those relations. Mathematical Thinking provides constructions of objects, operations, representations and arguments when the needed mathematics itself must be developed.

Recover what a request to use a model means in this situation. A structure satisfying stated axioms answers a different question from a representation used to predict an observed process. Both can be useful mathematical work. E.10 clarifies the intended use when the word *model* conceals it; keep the subject's established vocabulary when it is already clear.

A drawing, formula, program or learned representation also needs an operation that obtains the requested answer. A person may reason from a diagram; software may solve equations; an experimental arrangement may exhibit a behavior. Make the required interpretation available when another participant must continue the work. A.6.3.RT.OE helps make an expression usable for that operation, and C.29.2 develops a computational formulation when computation is needed. The obtaining procedure can itself become a subject of mathematical investigation.

### MMP.Preface:3.2 - Represent admissible objects and construct missing relations {#mmp-preface-3-2-represent-admissible-objects-and-construct}

[MMP.10](spec://ai.lev/fpf-think-mmp/contract/MMP-10#root) starts from intended candidate objects and their requirements. It chooses a representation, derives the conditions that make the representation valid and expresses the required answer. These steps matter for sets, sequences, functions and quantitative objects alike. If several records describe one object, a count or probability over records can require correction before it answers the subject question.

[MMP.11](spec://ai.lev/fpf-think-mmp/contract/MMP-11#root) starts with supported relations and an unknown contribution among them. It constructs adjustable families that retain the needed properties and inserts that contribution into the connected model. A known total, a monotone response and a normalized probability law require different mathematical constructions. Their common modeling question is how to permit the unknown variation while retaining what is supported.

Choose the form from the next operation. Direct constraints may already describe all useful candidates. A parameterization can make changes preserve the constraints automatically, but may introduce duplicate descriptions or omit parts of the allowed family. Retain that difference when interpreting a fitted value, an impossibility result or an observed agreement.

### MMP.Preface:3.3 - Construct change and observation together when they interact {#mmp-preface-3-3-construct-change-and-observation-together-when}

For an evolving situation, A.3.3.TR constructs a state-change rule from the contributing relations, including simultaneous constraints, alternatives and events. If situations assigned the same state need different continuations under the same modeled inputs, revise the state or retain the alternatives. The computation's chosen solution order need not be the represented order of physical change.

[MMP.7](spec://ai.lev/fpf-think-mmp/contract/MMP-7#root) derives a probability law for the record produced by an observing procedure. Compose the source and recording laws, retain shared unknowns, sum or integrate unrecorded alternatives, and account for selection. The resulting law can supply a statistical inference or prediction method. C.16.IR addresses what a supplied observation relation resolves, including bounds and consequential ambiguity.

[MMP.12](spec://ai.lev/fpf-think-mmp/contract/MMP-12#root) constructs recovery from a forward relation. Find which changes to the unknown leave the records unchanged or change them too little for stable recovery. A restriction or penalty can make a useful reconstruction possible; derive both the error it suppresses and the target detail it may remove. A bound that already settles the question can end the work before regularization.

[MMP.13](spec://ai.lev/fpf-think-mmp/contract/MMP-13#root) constructs the inferential claim. Choose whether the use needs a repeated-sampling guarantee, a posterior probability or a prediction for a new outcome; derive that result under the record law and the additional assumptions it requires. Propagate joint uncertainty to the quantity the receiver actually needs. A regularized optimum alone supplies neither a posterior distribution nor a coverage guarantee.

Observation can also change the situation. C.28 and C.28.MR help formulate that intervention and replace the affected mechanism. [MMP.15](spec://ai.lev/fpf-think-mmp/contract/MMP-15#root) asks whether its requested consequence is determined by the available laws and causal assumptions. It derives an identifying expression, a sufficient bound or an unresolved difference between compatible causal accounts. MMP.13 can then estimate an identified quantity from finite records; an observational fit alone does not identify it.

A question about the same case under another action needs a further connection. [MMP.19](spec://ai.lev/fpf-think-mmp/contract/MMP-19#root) constructs the underlying conditions shared by its alternatives, uses MMP.7/.13 to recover what the factual record says about them, then applies the changed mechanisms. Separately known intervention distributions can leave their same-case relation ambiguous. The result can be a conditional response or a bound; a choice based only on expected outcomes can remain settled without resolving that ambiguity.

### MMP.Preface:3.4 - Turn uncertainty into a question about available action {#mmp-preface-3-4-turn-uncertainty-into-a-question-about}

[MMP.8](spec://ai.lev/fpf-think-mmp/contract/MMP-8#root) separates circumstances from choices and specifies when information arrives. It then formulates whether the work needs a fixed decision or an instruction depending on an available report, and whether performance is required for each admitted circumstance or on average under a stated probability law.

This formulation can expose a change needed in the work itself: observe earlier, distinguish another circumstance, permit another action or revise the requirement. [Method Engineering (ME)](spec://ai.lev/fpf-eng-me/pub/TOC#root) develops the observing and acting methods and their composition. Their timing and resource demands return as premises of the mathematical question.

An information-dependent instruction needs both an obtainable report and a participant able to act on it at the stated time. Check this condition for the combined method. A correct reporting law and a correct decision calculation can still describe an instruction that the proposed work cannot perform.

[MMP.16](spec://ai.lev/fpf-think-mmp/contract/MMP-16#root) constructs the records that alternatives would produce under feasible designs. Compare the distinction an observation could resolve with its contribution to the receiving question and its burden. An informative report can still leave the preferred action unchanged.

[MMP.8.SD](spec://ai.lev/fpf-think-mmp/contract/MMP-8-SD#root) develops continuing choice: retain a state or belief sufficient for the proposed decisions, construct transitions and observations, and derive how a present choice and its continuation determine the accumulated consequence. This joins observation design to action when timing, information or changes caused by observing matter.

### MMP.Preface:3.5 - Simplify, diagnose and revise for the required consequence {#mmp-preface-3-5-simplify-diagnose-and-revise-for-the-required}

[MMP.9](spec://ai.lev/fpf-think-mmp/contract/MMP-9#root) starts with a source evolution law and quantities to retain. It derives their change, identifies the contribution that depends on removed detail and constructs a replacement through elimination, memory, added state, approximation or a sufficient bound. Initial conditions, inputs and the requested horizon determine whether the replacement serves the question. MMP.11 can supply a family for a still-unknown replacement relation.

[MMP.17](spec://ai.lev/fpf-think-mmp/contract/MMP-17#root) constructs a cheaper supplier for selected source-model responses. Choose the responses and input region from their intended use, build the replacement, and refine or return to the source where approximation changes the answer. Retaining a value can be insufficient when the receiver needs a derivative, tail event or explanation.

[MMP.18](spec://ai.lev/fpf-think-mmp/contract/MMP-18#root) connects models through the quantities and conditions they exchange. Translate between their quantities and scales, supply any omitted influence needed by the connection, and retain shared information. Preserving a total amount, a constant field or a joint probability law requires different conditions on that connection. Matching software inputs and outputs does not establish those conditions.

[MMP.14](spec://ai.lev/fpf-think-mmp/contract/MMP-14#root) helps when available observations reveal a consequential prediction failure, or a proposed use makes a comparison worth performing. Choose a discrepancy relevant to that use, derive predictions for comparable records, locate the mismatch and change the implicated relation or assumption. Recalculate the receiving consequence. Several repairs may explain one discrepancy; predictive improvement alone does not identify its cause. Existing records, an algebraic comparison or a restricted use can be sufficient.

When a premise or question changes, B.5.RR identifies the reasoning that depends on it and derives the revised consequence. If the argument must first be recovered, use B.5.RA. B.5.MPC.R develops the comparison when the difficulty concerns a connection among physical, mathematical and computational accounts. The repair may belong to subject assumptions, observation, mathematical formulation or computation.

These contributions admit several entry points and returns. A changed reporting procedure can require a new probability law while leaving the choice criterion intact. A changed criterion can require another instruction while leaving the reporting law intact. A changed intervention can require revising the model's mechanisms. Preserve each still-useful result and reconsider the part whose conditions changed.

### MMP.Preface:3.6 - Use the model-forming result across the Suite {#mmp-preface-3-6-use-the-model-forming-result-across-the-suite}

The [Foundational Thinking Suite Reference](spec://ai.lev/fpf-think/pub/REFERENCE#root) explains the shared architecture and worked combinations. Mathematical Thinking constructs the objects and arguments a formulation needs. Physical or other subject methods supply the supported relations. Computational methods obtain the consequence, and the subject interpretation determines what that consequence lets the work do. Notational methods make these operations recoverable by their participants.

A particularly useful boundary concerns an unknown relation. MMP.11 can construct a family respecting supported conditions without selecting one fitted member. MMP.7 supplies a probabilistic recording law when that is the question, while C.16.IR can expose what a supplied indication or bound resolves. The appropriate next step can therefore be inference, a discriminating observation, an already sufficient bound, or action under the remaining uncertainty.

The Readme illustrates two further connections: carrying intervention consequences through a diagnostic report into a continuing instruction, and using cheaper components while retaining a sufficient combined answer. The needed intermediate result chooses the next method. General portfolio comparison and improvement remain with the existing FPF methods.

### MMP.Preface:3.7 - Constituent actions in ongoing work {#mmp-preface-3-7-constituent-actions-in-ongoing-work}

While constructing a model of recorded observations, summing over unrecorded alternatives can be part of forming the observation law, within the modeling inquiry already under way. If the observing procedure changes from recording a below-threshold result to omitting the case entirely, that local operation must follow the changed selection rule. Mathematical calculation and knowledge of the subject may both be available while the intermediate description of observation is missing. MMP.7 helps construct the recorded-data law; obtaining the procedure's actual conditions still requires the appropriate source or contributor.

FPF B.1.5.EW helps recover these constituent–whole connections; B.1.5.RS examines a proposed replacement. Use the parts of the vertical that can change the present result. A Method described here can require additional capability, available support and compatible resources at other grains.

## MMP.Preface:4 - Archetypal Grounding - A report, an instruction and a changed question {#preface-4}

The Readme's [observation-to-action entry](spec://ai.lev/fpf-think-mmp/pub/README#mmp-observation-to-action-turn-an-observing-model-into-a) works the connection between MMP.7, MMP.8 and Method Engineering. One of two requests needs a scarce resource. Allocation follows a report produced through an unrecorded choice of channel.

MMP.7's operation first sums over the channel to obtain the reporting law. In the worked case, following the report succeeds with conditional probabilities 0.8 and 0.7 in the two circumstances. MMP.8 then asks what performance the instruction must supply. At least 0.65 success in each circumstance permits following the report. Zero failure does not. An average-success criterion with one circumstance occurring with probability 0.95 instead favours a fixed allocation among the four deterministic instructions considered.

The calculation changes the proposed way of working: whether to obtain and follow the report depends on the requirement, the circumstances it distinguishes and its cost. The receiving participant must get it before allocation. The complete elementary comparison is in [MMP.8:5.2 - Decide which participant gets a scarce resource](spec://ai.lev/fpf-think-mmp/source/MMP-8#decide-which-participant-gets-a-scarce-resource). The Readme explains the return to the work when observation itself changes the situation. Each changed condition selects the contribution to revise.

### MMP.Preface:4.1 - A total is sufficient until the question changes {#mmp-preface-4-1-a-total-is-sufficient-until-the-question-changes}

Suppose material passes through two cycles in two intermediate buffers. Each incoming portion retains 80% of its amount. Its fractions going to each buffer are unknown but constant across the cycles and independent of the portion's amount. Initially the amounts are `(10, 0)`. Both buffers have sufficient capacity; the material remains there until a receiver is selected and the later transfer begins. Transfer losses are neglected. How much capacity does that receiver need for all the material?

MMP.10 represents one cycle by `x_next = A*x`, where the two components of x are the amounts in the buffers. Nonnegative entries of A express the fractions received; each column sums to 0.8. MMP.11 retains the family defined by those conditions. Direct constraints suffice: choosing one fitted matrix would add information the situation has not supplied.

MMP.9 derives a simpler relation for the total `S = x_1 + x_2`: `S_next = 0.8*S`. After two cycles the total is 6.4, so capacity 7 suffices. The unknown distribution does not need to be resolved for this answer.

Now transfer only from the first buffer. One admissible model, `A = 0.8*I`, leaves 6.4 there. Another, `A = 0.8*[[0,0],[1,1]]`, leaves none there. Both give the same total. Capacity 7 still suffices, but the total alone cannot justify using a cheaper receiver of capacity 4. Return to the retained model family to ask which differences can affect the local amount. A further observation is useful if resolving those differences can change the receiver choice enough to justify its cost; C.16.IR and C.11.DUA support that question. The revised use changes what the model must preserve while leaving the total calculation valid for its original question.

Other bodies show different mathematical work: representing partial functions without distorting the requested count, deriving a bound after removing population detail, and constructing an unknown response while preserving its shape. Use their worked cases to learn the corresponding operations and their limits. The choice among those operations follows the difficulty, not the example's subject.

## MMP.Preface:5 - Conformance Checklist - Can the result do its intended work? {#preface-5}

For the combination being used, ask:

- What question does the result answer, and how will that answer be interpreted or used?
- What do the chosen mathematical objects represent? Which cases, operations and distinctions are retained or excluded?
- Which relations come from the subject, which follow mathematically, and which remain hypotheses or adjustable contributions?
- What operation obtains the answer, and what information or capability does its performer need?
- Do the connected contributions agree on the situation, timing, admissible variation and required consequence?
- Does a restriction, ambiguity or approximation still permit the proposed use? If the question changes, which part must be reconsidered?

A small use may already have these answers in one body and its worked argument. Carry that answer forward. Seek an additional check or observation when its result can change the decision enough to justify the cost, using C.11.DUA.

## MMP.Preface:6 - Common Anti-Patterns and How to Avoid Them {#preface-6}

The methods address consequential failures visible in their constructions. An encoding with ignored fields can give several records for one object; MMP.10 shows how that affects counting and interpretation. A probability law for the source event can omit the procedure that selected the available records; MMP.7 reconstructs that procedure's contribution. A decision rule can accidentally depend on information unavailable at the time of action; MMP.8 constructs the allowed dependence.

Recovering one best-fitting unknown can also hide a distinction the observations never resolved; MMP.12 separates recovery from the restriction that selects it. MMP.13 distinguishes the meaning of a confidence interval, a posterior probability and a prediction. MMP.14 shows why fitting an overall mean can leave the conditional prediction wrong, and why matching the data used to design a repair is not an untouched test of that repair.

Two further failures concern changing a model. Removing variables can leave a missing contribution in the retained evolution; MMP.9 derives that contribution before choosing its replacement. A flexible fitted function can violate a property known about the modeled relation; MMP.11 constructs the variation within that property and exposes any additional restriction.

Their repairs are specific. More numerical accuracy will not recover an excluded candidate object or an omitted relation. A different equation solver can help when the obtaining operation is the actual difficulty. Locate the consequential discrepancy before deciding what to change.

## MMP.Preface:7 - Consequences, biases and limits {#preface-7}

The language makes intermediate modeling results available for subsequent work: an admissible representation, a reporting law, a recoverable target, an inferential conclusion, a repaired prediction, a feasible instruction, a reduced evolution law or a family retaining known relations. Their explicit conditions help collaborators divide the work and change one contribution while retaining others.

Construction costs time and mathematical effort. A familiar adequate model or direct calculation can be sufficient. A reusable model family or derivation becomes valuable when the work needs several cases, revisions or explanations. A remaining ambiguity can also be useful if it tells the team which proposed consequence is unresolved.

The worked cases favour small constructions whose reasoning is inspectable. Larger instances can require specialist mathematics, computational resources and subject knowledge. A proof of existence, a practical obtaining procedure and a reliable implementation have different requirements. Questions involving additional causal structures or specialist statistical constructions can require further methods and subject knowledge.

Prediction, explanation and intervention can also favour different accounts. Use C.2.8 and Explanation Design (EXD) when the recipient's recoverable understanding is at issue. A predictive success supplies the performance it demonstrates; explaining a phenomenon or changing a mechanism requires the corresponding content. Several models can contribute to the same project, with comparison and improvement supplied by the existing FPF methods.

## MMP.Preface:8 - Architectural Rationale - Organize by model-forming operations {#preface-8}

The organization follows difficulties that arise before and during the construction of a mathematical question. An arrangement, a recorded observation and a changing quantity can require different operations. A solver catalogue begins after many of these choices; a universal modeling cycle usually leaves their detailed construction to the reader. Addressable methods preserve that detail while allowing different combinations.

The formulation part constructs admissible cases (MMP.10), a varying relation inside supported structure (MMP.11), and choices under available information (MMP.8 and its sequential refinement MMP.8.SD). The inference and revision part derives the recording law (MMP.7), formulates inverse recovery and regularization (MMP.12), constructs an inferential conclusion (MMP.13), repairs failed predictions (MMP.14), identifies intervention consequences (MMP.15), and designs discriminating observations (MMP.16). The model-change part derives reduced evolution (MMP.9), constructs a surrogate (MMP.17), and couples models through their exchanges (MMP.18). These parts help find a needed operation; they prescribe no fixed sequence.

Common reasoning remains in FPF: constructing a first account, applying a theory, connecting a mathematical result to its subject, describing change, replacing a mechanism and revising an argument. Mathematical Thinking develops the mathematical constructions. MMP develops the model-forming operation that uses those contributions; it keeps the actual subject premises visible. This division allows mathematical, physical and computational thinking to support one another while retaining their different questions.

The same division applies to modeling a working method. A function, path or state rule can describe an aspect of that method. Its mathematical properties become useful only through the correspondence with the work: what counts as input, which operations are available, what state can change and what result is returned. Method Engineering uses the consequence to retain, compose or change the working methods. A mathematical transformation may preserve returned values while changing time, information or execution demands; include the demands relevant to the proposed use.

A more detailed construction can need its own pattern and further refinements. A profile can combine several methods with additional conditions for a narrower practice, and one method can participate in several profiles. Specialization, composition and reuse describe different relations.

Reconsider a boundary when a recurring difficulty requires an unavailable operation, when two bodies develop the same operation, or when their combination leaves a needed contribution implicit. Preserve still-useful arguments, examples and source qualifications while changing the organization.

## MMP.Preface:9 - Source use and currentness {#preface-9}

[Nguyen and Frigg's Scientific Representation](https://www.cambridge.org/core/elements/scientific-representation/A5C2A74998C15C36D4B204E4B3E70B1C), especially its comparison of inference and representation, helps separate deriving a consequence within a model from using it about a subject. This is a useful philosophical account of representation; the language's practical operations do not require adopting it as the only account of models.

The historical [SIMULA account by Nygaard and Dahl](https://www.cs.tufts.edu/comp/150FP/archive/kristen-nygaard/hopl-simula.pdf), printed pages 457-458, connects system description with simulation programming and reasoning from a description. [Modelica's equations and initialization](https://specification.modelica.org/maint/3.7/equations.html) provide a maintained example in which simultaneous relations and their computational treatment are distinct. These contributions support recovering the interpretation and obtaining operation rather than imposing one representation medium or execution order.

The individual bodies keep the operative sources for their mathematical construction. MMP.10 compares direct constraints with representation and refinement work in MiniZinc and Conjure. MMP.7 uses statistical workflow and observation/selection constructions. MMP.8 compares fixed and information-dependent choices. MMP.9 uses closure and reduction research. MMP.11 compares constrained construction with data-driven discovery and hybrid known/unknown relations. MMP.12 compares regularization constructions with unregularized recovery and learned restrictions. MMP.13 and MMP.14 use statistical workflow to connect inference, consequential prediction checks and localized revision; they distinguish mathematical calibration from agreement with the modeled subject. MMP.15 distinguishes identification from estimation using causal identification and population-transfer constructions. MMP.16 combines discrimination and decision-valued observation design. MMP.8.SD develops decision-sufficient state and continuation; MMP.17 compares surrogate and correction constructions; MMP.18 connects interface-preserving maps with coherent shared information. Their bodies give the operative sources and limits. Each source contributes at its stated scope; the resulting organization and elementary cross-practice examples are conceptual synthesis.

Source changes matter when they alter an operation, its assumptions, its practical cost or the conclusion it supports. Return to the affected body's comparison in that case. A new implementation can change how cheaply a result is obtained while leaving the mathematical relation intact; a newly recognized observation or intervention effect can instead require a different model.

## MMP.Preface:10 - Relations to continued inquiry and work {#preface-10}

B.5.QD helps turn a result, obstruction or unresolved difference into a further question. A model can therefore contribute before it supplies a final numerical answer: it may expose a new distinction, make a comparison possible or suggest a different way of working. Choose further inquiry in relation to the work it could enable.

When the difficulty is acquiring or transferring the ability to use such constructions, Human Capability Development (HCD), Explanation Design (EXD) and the relevant development methods address that learning and use. Their question differs from whether one displayed calculation is correct. Retain the preparation and support a participant needs when dividing work among people and AI agents.

For evaluating alternatives and improving them, reuse FPF's characteristic, comparison and development methods. Define the consequences that matter for the question, including approximation, explanatory use, effort and ability to revise the model when relevant. Different models may supply different contributions. The next modeling operation follows the deficiency or opportunity that comparison identifies.

## MMP.Preface:End {#preface-end}
