# MMP.11 - Construct a Mathematical Model Family from Known Relations {#root}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Working sections of the pattern; its depth sections live in the source document named by the last line. See LICENSE.md for the list of changes.

> **Type:** Method pattern
> **Status:** Usable, evolving
> **Normativity:** Normative within the stated use

## MMP.11:1 - Problem frame {#problem-frame}

Use this pattern when part of a model is supported, but a function or other relation is still unknown. You may know which quantities interact, what must be conserved, or how a response begins and ends, while lacking its form between those conditions. You need candidate models that retain this knowledge while allowing the missing contribution to vary.

Begin by locating the unknown contribution in the relations needed for the question. Say what it takes as input, what it supplies and which properties its variation must preserve. Construct a family for that contribution, then put it back into the model. For a response that rises from zero to one, a family of curves constrained by those properties gives a different starting point from an unrestricted fitted curve.

The first useful result is a family of models, its remaining adjustable parts and the restrictions introduced by its construction. It may already give a sufficient bound. When observations are available, the same construction lets you ask which functions, parameters or consequences those observations can distinguish.

You need the subject grounds for the retained relations and enough mathematics to construct and use the family, or access to that mathematical contribution. A known adequate relation can be used directly. An unknown numerical parameter inside a suitable family normally needs its estimation method. Use this pattern when the family itself needs construction or revision. B.5.FM and B.5.TU help when the missing contribution is the subject account or theory from which a relation should come.

## MMP.11:2 - Problem {#problem}

A familiar formula can exclude the response being sought. Giving a learner unrestricted freedom can create the opposite problem: the fitted response may violate a known relation. Fitting two interacting contributions independently can also destroy a property that depends on their connection.

Agreement with recorded outputs leaves another difficulty. Several parameter settings may define the same function, and several functions may produce the same observations. Some receiving questions distinguish those alternatives; others need only a consequence on which they agree. Choosing one fitted instance can conceal this difference.

The modeling work is to construct the adjustable contribution in a form that retains the supported relations, then determine what that family can establish for the present question. The construction itself may impose additional restrictions, so its expressive limits belong to the answer.

## MMP.11:3 - Forces {#forces}

| Force | Tension |
| --- | --- |
| Retained knowledge and flexibility | A structural relation can rule out impossible candidates; an unsupported restriction can remove the needed one. |
| Local fitting and coupled behavior | A contribution can fit its own samples while disrupting the model in which it is used. |
| Simple representation and family coverage | A small parameterization is easier to fit but can omit admissible functions. |
| Parameter recovery and useful inference | Parameters may remain ambiguous while a required consequence is determined. |
| Prediction and intervention | Two accounts can agree during observation and differ after one mechanism is changed. |

## MMP.11:4 - Solution {#solution}

Locate the missing relation, separate what is retained from what may vary, construct the adjustable family, and derive its contribution to the receiving question. Observation or computation is then selected for what remains unresolved.

### MMP.11:4.1 - Locate the contribution that may change {#locate-the-contribution-that-may-change}

State the result wanted from the model. Identify the unknown relation and the quantities it connects. Keep its inputs, output, domain, units and permitted dependence explicit enough to substitute a candidate into the surrounding relations. A function of present state, a function of its history and a random response law admit different constructions. If equal proposed inputs require different deterministic outputs in the admitted circumstances, revise the inputs or retain those alternatives. Greater flexibility of a single-valued function cannot supply both outputs. For a dynamic model, A.3.3.TR supplies the corresponding reconsideration of state.

Recover the grounds and application range of the relations you retain. A balance may be required by the chosen boundary; monotonicity may hold only over one operating range; a shape assumption may be provisional. Keep an allowed discrepancy when the subject account supplies one. A convenient property is not automatically a property of the subject.

Use the smallest part that can be varied without silently changing another retained claim. If an adjustable term can absorb a known contribution, include that possibility in the inference question. Section :5.2 shows an ambiguity between two gross transfers even when their net effect is known.

### MMP.11:4.2 - Construct the permitted variation {#construct-the-permitted-variation}

Translate each retained property into a mathematical condition, then choose a construction that satisfies it. MMP.10 supplies the general work of representing candidate objects and their conditions. Here the object being constructed is a family of relations to insert into the model. Direct conditions may already give a workable representation of that family. Constructing through free elements is useful when their variation should preserve the conditions; compare its obtaining and revision operations with those of the direct representation.

A useful construction separates a fixed part from free variation. If a linear operator L must satisfy `L(g)=b`, find one particular solution g0 and choose a correction h with `L(h)=0`. Then `g=g0+h` retains the condition. This describes every solution only if the admitted corrections cover the whole null space in the chosen function domain. Restricting h to a few basis functions supplies a smaller family. Establish the linearity and domain before using this construction.

For a sign, bound or shape condition, construct through a map whose output has that property. Nonnegative weights can be normalized to probabilities. Integrating a nonnegative function can produce a nondecreasing response. Work out the domain and boundary of the resulting family: strict positivity excludes zeros, and an integral of an ordinary integrable function produces an absolutely continuous curve. Section :5.1 develops one such construction and its restriction.

When a property depends on coupling, construct the coupled contribution. Using the same transfer with opposite signs in two balance equations preserves their total. Two separately fitted right-hand sides have no such identity unless their joint conditions supply it. Use A.3.3.TR to assemble a change rule from the interacting relations.

A penalty during fitting offers a different construction: it discourages violations while allowing them. Use it when that allowance fits the question. If the account requires an identity, either build it into the representation or use an obtaining method that enforces it. The size of a training penalty does not by itself establish the identity.

### MMP.11:4.3 - Choose the representation and its range {#choose-the-representation-and-its-range}

Choose a representation whose operations fit the required use and available resources. A table can represent a finite function. A basis expansion or program can retain a useful structure. A neural representation can supply a flexible adjustable function. The meaning of its inputs and outputs, and the retained relations, remain part of the model.

Check two different questions. Does every admitted parameter setting produce a relation allowed by the construction? Does the construction cover all relations needed for the present conclusion? A witness may need only one candidate; an impossibility claim over all admissible models needs coverage of that whole family or another sufficient argument.

State restrictions introduced by knots, basis functions, regularity, network architecture or domain truncation when they can change the answer. A numerical fit inside the restricted family answers for that family. If its consequence is sufficient, a more flexible family may add only cost. If the missing case matters, change the representation.

Different parameters can denote the same function. Recover the function or consequence needed by the receiving use rather than demanding unique parameters by default. Section :5.3 gives a normalization redundancy. Use MATH.7 when a change of representation has constructed inverse maps; use C.29.1 when correspondence is more general.

### MMP.11:4.4 - Put the family into the model before using its fit {#put-the-family-into-the-model-before-using-its-fit}

Substitute the adjustable contribution into the relations that consume it. Derive the resulting observable or answer condition with shared quantities kept shared. An error measured on an isolated contribution and an error in the coupled output are different fitting questions.

Choose the insertion point from what must remain meaningful. In a component model, inserting an unknown relation before algebraic elimination can retain a named component's inputs, outputs and connections. Adding a correction after elimination can be simpler, but the correction then acts on the transformed relations. Recover how it affects the properties needed by the original question. A reduced model may use MMP.9 to derive the contribution its simplification leaves open.

Represent how observations are produced. MMP.7 derives a probability law for records when probability is needed; C.16.IR uses the supplied indication relation to obtain compatible cases or bounds. Fitting an unobserved internal term as if it were measured supplies an extra premise. If that premise is unavailable, fit or constrain through the observable relation instead.

For a dynamic or implicitly defined model, obtain the consequence through its coupled equations and conditions. A good component fit does not settle whether the resulting evolution, initialization or constraints are usable. Apply the mathematical and computational method appropriate to the stated consequence; C.29.2 helps formulate its obtaining operation.

### MMP.11:4.5 - Determine which remaining differences matter {#determine-which-remaining-differences-matter}

Ask what the available observations constrain: the adjustable parameters, the unknown function over a stated domain, or a particular consequence. Use C.16.IR on the resulting observation relation. The function can remain undetermined away from the observed inputs even when its recorded values are fixed.

When ambiguity could change the answer, construct two admitted candidates with the same relevant observations and different receiving consequences. Such candidates show what further information must distinguish. If all compatible candidates or a sufficient bound give the same answer to the present question, use that answer without resolving unrelated differences.

Repeated numerical fits can discover alternatives. Agreement of finitely many fitted instances leaves unsearched alternatives possible. A claim of uniqueness needs its mathematical or statistical grounds; a sufficient decision can require much less. Numerical search failure also differs from a proof that the family is inconsistent with the observations.

Change the question explicitly when a new use requires it. An intervention may distinguish models with the same observational behavior. C.28.MR supplies the replacement of the affected mechanism under its causal premises. Explanation or modification of a working method can require structure beyond that needed for prediction; characterize the required explanatory use through C.2.8 and Explanation Design (EXD).

### MMP.11:4.6 - Use the consequence or revise the family {#use-the-consequence-or-revise-the-family}

Return the result with the family, input range and conditions that affect its use. It may be a candidate relation, a bound, a conditional prediction, a supported instruction or a located missing contribution. When the model is used to change a working method, Method Engineering receives the consequence and the relations the proposed change must preserve.

Revise the part whose restriction prevents the needed result: the subject premise, permitted dependence, representation, observation relation or obtaining method. Use B.5.RR to carry a changed premise or question through the reasoning. General comparison, portfolios and improvement use the existing C.16, C.11 and E.22/E.23 methods when those questions arise.

Stop when the receiving use has a sufficient answer or the missing contribution is clear enough to obtain. Use C.11.DUA when deciding whether another observation, a richer family or further computation can improve that use enough to warrant its cost. A more detailed family is valuable only through what it enables.

## MMP.11:7 - Conformance Checklist {#conformance-checklist}

- The unknown contribution has interpretable arguments, result, domain and permitted dependence.
- The retained relations have subject grounds and an application range.
- The construction shows why admitted adjustable values preserve the required properties.
- Restrictions introduced by representation are carried into conclusions that depend on family coverage.
- Coupled effects and the actual observation relation determine the fitting or inference question.
- Remaining parameter, function and consequence ambiguities are distinguished when they change use.
- A changed intervention or receiving question reopens the relevant contribution.
- The result can be used, qualified or passed to a named next method without requiring unrelated identification work.

## MMP.11:9 - Consequences {#consequences}

The family carries usable knowledge through variation and fitting. It can supply a bound before a particular model is selected, or reveal why more observations of the same kind will leave the important ambiguity intact.

The cost is constructing and checking the representation. Strong restrictions reduce the search but can exclude useful candidates. A flexible family can retain more possibilities while increasing inference cost and leaving more uncertainty. Compare these costs against the result the work actually needs.

## MMP.11:12 - Relations {#relations}

- **MMP.10** constructs representations and the conditions making them admissible. **MMP.9** derives an unknown contribution caused by reduction and can use a constructed family to replace it.
- **A.3.3.TR** composes a rule of change; **C.29.1** relates model consequences to their receiving use; **C.29.2** constructs the needed computation.
- **MMP.7** supplies the recording probability law. **C.16.IR** determines what the resulting indication relation resolves. **MMP.8** uses the available information in a choice question.
- **C.28.MR** constructs the changed mechanism for an intervention. **B.5.RR** revises reasoning after a changed premise or question.
- **C.2.8 and Explanation Design (EXD)** characterize the explanatory contribution needed by a reader. **Method Engineering (ME)** uses a model consequence to develop or revise the corresponding way of working.
- **C.11.DUA** compares a further modeling contribution with its cost; general model comparison and improvement use the existing framework methods.


## Dependencies {#dependencies}

- @fact:DEPENDS-ON Dependencies (as published): spec://ai.lev/fpf-think-mmp/contract/MMP-10#root for admissible representation; spec://ai.lev/fpf-spec/contract/A-3-3-TR#root for state; spec://ai.lev/fpf-spec/contract/C-16-IR#root for observation-based inference; spec://ai.lev/fpf-spec/contract/C-28-MR#root for intervention; spec://ai.lev/fpf-think-mmp/contract/MMP-9#root for reduction. @status:spec/done
- @fact:REFERENCED-BY Referenced by (computed from the Tables of Contents): spec://ai.lev/fpf-eng-dtm/contract/DTM-6#root, spec://ai.lev/fpf-think-mmp/contract/MMP-10#root, spec://ai.lev/fpf-think-mmp/contract/MMP-12#root, spec://ai.lev/fpf-think-mmp/contract/MMP-17#root, spec://ai.lev/fpf-think-mmp/contract/MMP-7#root, spec://ai.lev/fpf-think-mmp/contract/MMP-9#root, spec://ai.lev/fpf-think-phy/contract/PHY-4#root @status:spec/done

#source spec://ai.lev/fpf-think-mmp/source/MMP-11
