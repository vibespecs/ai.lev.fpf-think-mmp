# MMP.8 - Formulate Information-Dependent Choices Mathematically {#root}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Working sections of the pattern; its depth sections live in the source document named by the last line. See LICENSE.md for the list of changes.

> **Type:** Method pattern
> **Status:** Usable, evolving
> **Normativity:** Normative within the stated use

## MMP.8:1 - Problem frame {#problem-frame}

Use this pattern when a mathematical problem mixes quantities you may choose with quantities you do not control, or when a proposed solution depends on information that arrives too late. A solver can find a configuration for each possible circumstance while leaving you unable to select one in advance. A simulation can show a successful continuation because it chose an environmental value that the acting system cannot choose.

Begin with one proposed action. Ask what will be known when it must be chosen, which quantities remain outside that choice, and what result the action must achieve. Construct two possible circumstances that look the same at that moment. If the proposal assigns different actions to them, it needs another observation, a different decision time or a different policy.

The result is a mathematical formulation of the available choices and the requirement they must satisfy, including their dependence on information. It can establish a feasible fixed choice, a policy, a counterexample to the proposal or the missing contribution. This is a general modeling method for design, prediction and control questions. It develops the formulation before a solver or a control algorithm is selected.

The finite examples need elementary sets, inequalities and the meanings of 'there exists' and 'for every'. More demanding cases can require optimization, stochastic processes or control theory. If the answer condition and available information are already correctly formulated, use C.29.2 or the applicable computational method to obtain the result.

## MMP.8:2 - Problem {#problem}

A mathematical unknown can represent a decision, an unobserved state, an external input or a quantity constrained by other relations. Treating every unknown as a free decision lets the solution change the problem's circumstances to make the requested result possible.

Timing introduces another error. A family of solutions indexed by the true circumstance can be mathematically valid while requiring an observation that the acting system never receives. Separately optimizing every future case then grants foresight that the described method lacks.

The difficulty is to translate the work's choices, information and requirements into a mathematical question with the corresponding dependencies and quantifiers.

## MMP.8:3 - Forces {#forces}

| Choice | Consequence |
| --- | --- |
| One decision or an adaptive rule | An adaptive rule can use later observations but needs a realizable way to receive and act on them. |
| Possible success or required success | A successful case can support possibility while leaving a guarantee unresolved. |
| Unknown state and random state | An uncertainty set permits several values; probabilities require an additional model. |
| Strong requirement and useful feasibility | A guarantee across an oversized circumstance set can reject useful choices; changing the set changes the claim. |
| Mathematical existence and an obtainable rule | A policy's existence can matter before an affordable construction is known. |

## MMP.8:4 - Solution {#solution}

Separate choices from circumstances, express the relations that must hold, and state which information each choice may use. Formulate the requested result over those objects, then test the formulation against a small contrasting pair of circumstances. Preserve any useful conditional answer when a stronger requirement is unavailable.

### MMP.8:4.1 - Name choices, circumstances and consequences {#name-choices-circumstances-and-consequences}

Start from the question in the work. Identify what a participant can change and what is supplied by the subject or environment. Let a denote the choice and w the circumstance. Give both their domains and meanings. A choice can be an arrangement, an input, a rule for later actions or another object the work can construct.

Use the subject relations to connect them to a result. For a deterministic model, a consequence may be written y=f(a,w). An implicit relation R(a,w,y) can retain several possible consequences. Additional unknowns can describe forces, flows, internal states or other quantities jointly constrained by the model. Acausal equations can constrain these quantities without making them free controls.

State what the question requires of the result. If it asks whether every permitted behavior meets a condition, a solver's ability to find one favorable y does not settle it. If the work can select among the permitted consequences, represent the mechanism that gives it that choice. A.3.3.TR supplies the relevant state-change or interaction rule.

### MMP.8:4.2 - Recover the order and availability of information {#recover-the-order-and-availability-of-information}

Describe what is observed before each decision and what arrives afterward. Express the available observation as h(w) when it is a deterministic description of the circumstance. It may reveal only part of w. For a random or noisy observation, specify its probability law for each admitted w. An unknown fixed w can index a family P_w of observation laws without having a probability distribution itself. A joint law is needed when the question also treats w as random and averages over it. MMP.7 constructs the recording law.

A policy pi selects an action from the information available: `a=pi(h(w))`. Two circumstances with the same h(w) must therefore receive the same action. This uses MATH.2's condition that an answer remains constant on cases identified by a description. Here the observation determines those groups. The information restriction is often called nonanticipativity: the policy does not use distinctions the decision-maker has yet to observe.

For repeated interaction, use the observation history available at each decision. A policy may remember earlier observations or actions. Omitting that memory is a substantive model choice. Global termination is unnecessary when the question concerns a continuing response; specify the response or progress condition that matters under the admitted inputs.

If an earlier action changes what can be observed, make h depend on that action and describe the cost and timing of observation. If action also changes the circumstance distribution or evolution, include that relation. C.28 supplies the causal-use question and the policy's permitted pre-action information; C.28.MR constructs the mechanism replacement. A changed distribution cannot be inferred from a favorable selection of historical cases alone.

### MMP.8:4.3 - State the required quantifiers and performance criterion {#state-the-required-quantifiers-and-performance-criterion}

For a deterministic success condition G(a,w), these are different questions:

| Working question | Mathematical statement |
| --- | --- |
| Is there some successful combination? | There exist a and w with G(a,w). |
| Does every circumstance have a successful action, if it were known? | For every w, there exists a with G(a,w). |
| Can one action be selected now that succeeds throughout the admitted circumstances? | There exists a such that, for every w, G(a,w). |
| Can an observation-dependent rule succeed throughout those circumstances? | There exists an allowed policy pi such that, for every w, G(pi(h(w)),w). |

Choose the statement from the work's requirement. The first two can expose possibilities or limits even when the latter two fail. A stronger claim can require a different action or information source.

When the receiving use permits failures with a stated probability, name the event and the randomness over which that probability is calculated. For unknown fixed w and random observation O, the question may require `P_w(failure of pi(O)) <= epsilon` for every admitted w. If w itself is modeled as random and the question concerns performance averaged over circumstances, use the joint law of w and O. An expected cost needs the same choice of what is averaged. Neither a probability nor an objective follows just from listing possible circumstances. Feasibility, expected performance, tail risk and worst-case performance are alternative questions with different consequences. Use the common choice and characterization methods to decide which matters to the work.

Preserve dependence within the circumstance set. Independently combining several ranges can create impossible circumstances and overstate a requirement. Conversely, excluding an inconvenient circumstance changes the range of the conclusion and needs a subject reason or an agreed narrower use.

### MMP.8:4.4 - Construct or refute a usable choice {#construct-or-refute-a-usable-choice}

For each circumstance w, let A(w) be the actions satisfying the requirement under the modeled relations. For a fixed robust choice, seek an action in the intersection of A(w) over the admitted circumstances. An empty intersection refutes that fixed-choice requirement.

For an observation-dependent choice, group circumstances by the observation they produce. For each obtainable observation o, intersect A(w) over the circumstances with h(w)=o. An action in this intersection works throughout that observationally indistinguishable group. In a finite problem, choosing one such action for each observation constructs a policy. One empty intersection proves that this observation cannot support the required policy.

For a noisy observation and an all-cases guarantee, construct the allowed pairs (w,o) from the observation mechanism's admitted realizations. This relation, rather than a positive probability for each individual report, determines compatibility. For example, if O=w+E with E uniform on [-1,1] and all errors in that closed interval are admitted, the boundary error E=1 remains in an all-cases guarantee despite having probability zero. An almost-sure or specified-probability requirement is a different claim; state that choice.

For a received report o, first check that at least one circumstance is compatible with it. If none is compatible, return the conflict between the report and the observation model under C.16.IR:4.4. A universal statement over an empty set supplies no guarantee for the situation that produced the report. With a nonempty compatible set, intersect A(w) over its members. For a probability-of-success requirement, instead calculate the event under the conditional family or joint law chosen in :4.3; the set of allowed pairs alone supplies no probability weights.

For infinite spaces or long-running interaction, these relations still specify the question, but a usable policy requires the corresponding mathematical and computational construction. A pointwise existence argument does not automatically provide an effective rule. C.29.2 addresses that obtaining work; the present method retains the information restrictions in what it asks the computation to produce.

When several outcomes remain possible for one action and circumstance, apply the required quantifier to those outcomes as well. Derive or inspect a violating outcome when refuting a guarantee. If the missing factor is an unmodeled selection mechanism, obtain it or retain the conditional answer rather than allowing the solver to invent a favorable mechanism.

### MMP.8:4.5 - Interpret the result and change the working method {#interpret-the-result-and-change-the-working-method}

Follow the resulting action or policy through one modeled case and a consequential change. Return the consequence to the original requirement. If a planned response depends on a distinction absent from the available observation, revise the observation, defer the decision, choose a more tolerant action or change the stated goal with the responsible party.

Compare these options by what they change and cost. A more informative observation can enlarge the feasible policy set, but it may arrive too late or cost more than a sufficient fixed choice. C.11.DUA supplies that comparison. An infeasible guarantee can still leave a useful bounded, conditional or risk-qualified proposal.

For a working-method change, explain who or what supplies the observation, what result it provides, when it becomes available and what the receiving action does with it. ME supplies the composition and change of those methods. The mathematical policy then describes an obtainable contribution, rather than relying on an unstated observer or decision-maker.

## MMP.8:7 - Conformance Checklist {#conformance-checklist}

- Are choices, circumstances and consequences distinguished by what the acting system can actually change?
- Does each choice depend only on information available at its decision time?
- Do the quantifiers express the intended possibility, guarantee, policy or probabilistic question?
- Are dependent circumstances and remaining possible outcomes preserved in the formulation?
- Does a witness, empty intersection, policy or bound have the claimed meaning?
- Does the interpreted result support an action, a changed method or a specific unresolved contribution?

## MMP.8:9 - Consequences {#consequences}

The formulation prevents computation from supplying unavailable control or foresight. It can expose a useful change to observation, timing or the requirement before optimization begins. It can also be harder to solve than its scenario-wise surrogate; that extra difficulty reflects the question the work actually asked.

## MMP.8:12 - Relations {#relations}

B.5.FM and C.29 connect the work's question to its mathematical formulation. A.22.CGUS exposes allowed continuations; A.3.3.TR constructs the behavior relation. MMP.7 supplies a missing observation law for probabilistic uses. MATH.2 explains the identification of cases that preserve a requested answer; here grouping by available information determines which actions a policy can distinguish. C.29.2 obtains a computation for the formulated question and C.29.3 examines realization. C.28 governs causal claims when acting changes the represented world. ME uses the result to compose observation, decision and action methods with their needed contributions and timing.

MMP.8.SD refines this formulation for continuing decisions. It constructs a decision-sufficient state or belief, transitions and observations, and the relation between a present choice and its later consequences. Use that refinement when the one-step formulation leaves a consequential continuation unresolved.


## Dependencies {#dependencies}

- @fact:DEPENDS-ON Dependencies (as published): spec://ai.lev/fpf-think-mmp/contract/MMP-7#root for reports; spec://ai.lev/fpf-spec/contract/A-3-3-TR#root for change; spec://ai.lev/fpf-think-mmp/contract/MMP-10#root for constraints; ME for changing the corresponding way of working. @status:spec/done
- @fact:REFERENCED-BY Referenced by (computed from the Tables of Contents): spec://ai.lev/fpf-think-mmp/contract/MMP-16#root, spec://ai.lev/fpf-think-mmp/contract/MMP-7#root, spec://ai.lev/fpf-think-mmp/contract/MMP-8-SD#root, spec://ai.lev/fpf-eng-ops/contract/OPS-8-1#root @status:spec/done

#source spec://ai.lev/fpf-think-mmp/source/MMP-8
