# MMP.8.SD - Construct a Sequential Decision Model from Information and Consequences: depth {#depth}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Depth sections of the pattern; the working sections are in the contract document of the same id. See LICENSE.md for the list of changes.

## MMP.8.SD:5 - Archetypal Grounding {#archetypal-grounding}

The following are constructed finite models. Their numbers show what follows from the stated assumptions; they are not measured effects or recommendations for a particular organization.

### MMP.8.SD:5.1 - Reserve a resource for an observed later request {#reserve-a-resource-for-an-observed-later-request}

A portable power unit has enough energy to serve one task in either of two slots, with no recharge. Serving the current task in slot 1 yields 4 units on an already selected gain scale. In slot 2 a different task arrives with probability 0.6 and yields 10 if served. Arrival is observed before the slot-2 decision. Unused energy has terminal value zero; the current task cannot be deferred. Serving consumes the whole unit.

Let b be remaining energy, either 0 or 1, and d indicate the later arrival. At slot 2,

    V_2(b,d) = 10*b*d.

Use the retained state `(time, remaining energy, current request)`. The slot-1 comparison is

    serve now: 4 + 0 = 4
    reserve:   0 + 0.6*10 + 0.4*0 = 6.

The resulting policy reserves energy, then serves if the request arrives. It has larger expected gain than immediate service, although it yields zero when no request arrives. If the requirement is a gain of at least 4 in every admitted case, serving now meets it and reservation does not.

Two histories can show the same later request but differ in whether the energy was already used. Merging them would make the slot-2 service appear available after both histories. Retaining b prevents that error.

Suppose the arrival probability changes to 0.3, with the other premises unchanged. Reservation now gives 3 and immediate service gives 4, so the first action changes. If instead the only available probability statement is `0.55≤p≤0.65`, reservation gives expected gain between 5.5 and 6.5 and exceeds 4 throughout. Refining p is unnecessary for that comparison.

### MMP.8.SD:5.2 - Pay for information only when a later choice can use it {#pay-for-information-only-when-a-later-choice-can-use-it}

An unfamiliar encoded document uses format A or B, initially with equal probabilities. Two supplied decoders are available: the matching decoder gives a usable output worth 10, and the other gives 0. The model permits one final decoder application. An optional diagnostic costs 1 on the same gain scale and leaves the format unchanged.

The diagnostic returns + with probability 0.8 in format A and 0.2 in format B; the complementary probabilities give −. Its result arrives before decoder selection. The supplied observation model and A.3.3.PI's conditioning give:

| Information before decoder choice | Probability of format A | Best decoder | Expected final gain |
| --- | --- | --- | --- |
| No diagnostic | 0.5 | A or B | 5 |
| Diagnostic + | 0.8 | A | 8 |
| Diagnostic − | 0.2 | B | 8 |

The decision state can be `(stage, p)`, where p is the current probability of A. At the final stage,

    V_2(p) = max(10*p, 10*(1-p)).

Each diagnostic result has probability 0.5 under the initial model. Thus

    skip diagnostic:  V_2(0.5) = 5
    use diagnostic:  -1 + 0.5*V_2(0.8) + 0.5*V_2(0.2) = 7.

The continuation's choice changes with the observation. Fixing one decoder in advance gives 5 before the diagnostic cost, or 4 after it. This is why the extra information has value here.

Now the diagnostic result is delayed until after the final decoder choice. The decoder choice can no longer depend on that result. Using the diagnostic then has net expected gain 4, so skipping it gives the better value 5. This repair changes the information timing rather than the arithmetic of conditioning.

A different changed condition also reverses the comparison: with a timely but weaker symmetric diagnostic that is correct with probability 0.55, using its result gives `-1+10*0.55=4.5`. Skipping still gives 5 and is preferable.

The decoder and diagnostic behavior are premises of this example. A real use requires the applicable processing and observation methods to supply those consequences.

### MMP.8.SD:5.3 - Retain accumulated progress when the terminal goal changes {#retain-accumulated-progress-when-the-terminal-goal-changes}

In a two-round game, all awarded points are observed immediately. The first move is either A, giving 2 points with probability 0.5 and 0 otherwise, or B, giving 1 point certainly. In the last round, the player chooses Safe, adding 1 point certainly, or Gamble, adding 3 with probability 0.4 and 0 otherwise. The gamble's outcome is independent of the first round.

The objective is initially to maximize the probability of finishing with at least 3 points. Let c be points already earned. The terminal contribution is `g(c)=1` when `c≥3` and 0 otherwise. With zero intermediate contribution, the continuation compares terminal attainment:

| Points before last round | Safe: attainment probability | Gamble: attainment probability | Best continuation |
| --- | --- | --- | --- |
| 0 | 0 | 0.4 | Gamble |
| 1 | 0 | 0.4 | Gamble |
| 2 | 1 | 0.4 | Safe |

Therefore first move A gives `0.5*1+0.5*0.4=0.7`, while B gives 0.4. Choose A and condition the last move on earned points. Retain the state `(round, c)`. The round number alone is insufficient: histories with c=0 and c=2 require different continuations.

If the objective were expected final points, Gamble's expected increment 1.2 exceeds Safe's 1 at every c. Both first moves have expected increment 1, so both then give 2.2 expected final points. That calculation answers a different question from attainment probability.

Now change the requested terminal target from 3 to 4 points. From c=2, Gamble attains it with probability 0.4 and Safe fails. From c=0, neither last move can attain it. Thus A gives `0.5*0.4+0.5*0=0.2`. B followed by Gamble gives 0.4 and becomes preferable. The transition probabilities remain unchanged; the changed terminal criterion alters both the continuation and the first choice.

### MMP.8.SD:5.4 - Preserve one unknown condition across stages {#preserve-one-unknown-condition-across-stages}

A two-stage processing route incurs costs w and `1-w`, where an unknown w is fixed for the whole run and belongs to `{0,1}`. Choosing that route commits to both stages. A supplied alternative has total cost 1.5. The question is to minimize worst total cost, with no probability model.

The two possible cost sequences for the route are `(0,1)` and `(1,0)`; both total 1. The route therefore beats the alternative. Adding the worst first-stage cost 1 to the worst second-stage cost 1 gives 2, but combines different possible runs.

For the first choice, the common total 1 already suffices. If the remaining cost is later needed and the first-stage cost is observed, that observation identifies w and determines the remaining cost.

Now the operating condition is allowed to change between stages: costs are `w_1` and `1-w_2`, with all four pairs `(w_1,w_2)` allowed. The pair `(1,0)` gives total cost 2. The route's worst total is now 2, so the fixed-cost alternative 1.5 is preferable. The old conclusion fails because the admitted dependence changed.

## MMP.8.SD:6 - Bias-Annotation {#bias-annotation}

Finite stochastic examples make expectations and recursion easy to inspect, but may encourage a probability model or scalar gain where neither is supplied. Keep non-probabilistic possibilities and multiple criteria when that is what the work supports.

A model with one decision maker can also conceal separate information held by different people or systems. Represent communication and its timing when the proposed continuation depends on shared knowledge. Learned memory is attractive in large problems; its convenience does not establish sufficiency for a changed action set or criterion.

## MMP.8.SD:8 - Common Anti-Patterns and How to Avoid Them {#common-anti-patterns-and-how-to-avoid-them}

| Anti-pattern | What goes wrong | Repair |
| --- | --- | --- |
| Latest reading called the state | Histories with different resources or beliefs become indistinguishable. | Compare the histories' allowed actions and continuation, then retain the missing distinction. |
| Future knowledge used now | A policy selects a branch before its observation arrives. | Place observations and commitments on the same decision timeline. |
| Immediate score treated as total value | Resource use or information acquisition changes the future comparison. | Include the continuation under each current action. |
| Every objective written as a sum of immediate rewards | A terminal target or policy constraint changes meaning. | Preserve the criterion and augment the state or formulation where it needs history. |
| Independent worst values substituted for one fixed unknown | The calculation creates a trajectory excluded by the model. | Preserve coupling across stages or explicitly adopt the enlarged uncertainty set. |
| Convergence treated as decision sufficiency | A solver can converge for a representation that loses relevant history. | Identify the solved problem and evaluate the returned policy under the intended model. |

## MMP.8.SD:10 - Architectural Rationale {#architectural-rationale}

The construction begins with available histories because they expose the actual information constraint. A state is then a justified reduction of the decision problem. Starting from a convenient list of current features reverses that order and can hide lost memory.

Prediction contributes the distribution or set needed to describe a continuation. Decision modeling additionally specifies allowable actions and how consequences are accumulated and compared. In :5.3, identical transition knowledge supports different policies after a change of goal. In :5.2, identical diagnostic accuracy has different value after a change of timing.

A full history tree is a serious alternative to state compression. For a small problem it is often the clearest and cheapest model. A fixed plan is adequate when future information cannot improve the selected comparison; the delayed diagnostic shows such a boundary. For larger problems, a justified compact state makes repeated questions reusable by computational methods.

The continuation relation describes the mathematical problem consumed by those methods. It does not prescribe a solver or the worth criterion. This keeps model construction usable in physical operations, investigation, computational work and method design without replacing their subject methods.

## MMP.8.SD:11 - SoTA-Echoing {#sota-echoing}

The practice question is how to retain enough information for a useful sequential choice without demanding an unnecessarily complete reconstruction.

| Question and comparison | Adopted or adapted contribution and limit |
| --- | --- |
| Can a compact summary replace the full history tree? | **Adopt** the information-state line of Subramanian, Sinha, Seraj and Mahajan, [*Approximate Information State for Approximate Planning and Reinforcement Learning in Partially Observed Systems*](https://jmlr.org/papers/volume23/20-1165/20-1165.pdf), JMLR 23 (2022), §§2.2–2.3 and 3.2, especially Theorems 5 and 9. Preservation of expected gain and the next summary's law supports the reduction in :4.3–:4.4; approximate preservation needs a consequence bound. A full history tree remains preferable when small. This line saves representation and computation only when its conditions are obtainable; prediction fit alone supplies less. Reopen when a newly relevant action, history or criterion changes the equivalence between merged histories. |
| What if compact memory is useful but not sufficient? | **Adapt** Sinha and Mahajan, [*Agent-state based policies in POMDPs: Beyond belief-state MDPs*](https://arxiv.org/html/2409.15703v1), arXiv v1, 24 September 2024, §§II-C–II-D and III. Its comparison of policy classes supports :4.5: evaluate a restricted controller as such, rather than assuming an arbitrary recurrent memory admits the continuation equation in :4.4. Direct policy search is a serious alternative when sufficient-state construction is too costly. Preserve whether its result is locally optimal or best within a restricted policy class. Reopen when memory, available computation or required policy class changes. |
| Does convergence of a modern learning algorithm close the state question? | **Reject that inference**, using Sinha, Geist and Mahajan, [*Convergence of regularized agent-state-based Q-learning in POMDPs*](https://arxiv.org/html/2508.21314v2), arXiv v2, 2 September 2025, §§II-B–IV and Theorem 1. Under its learning-rate and visitation assumptions, the limit is for a regularized model that depends on the behavior policy's limiting distribution. The result sharpens :4.5's separation of numerical convergence from the intended policy comparison. Regularized learning remains a computational option; it brings its objective and representation conditions. Reopen when a proposed solver claims a stronger use than its result supports. |
| What if probabilities are unavailable and the criterion is worst consequence? | **Adapt** Dave, Venkatesh and Malikopoulos, [*Approximate Information States for Worst-Case Control and Learning in Uncertain Systems*](https://arxiv.org/html/2301.05089v2), arXiv v2, 6 April 2024, §§II–III. Conditional ranges and a criterion-specific continuation are a serious alternative to expected gain. The paper derives continuations for maximum instantaneous and terminal cost. For accumulated costs, :4.5 and :5.4 preserve the allowed complete trajectories. The trade-off is a worst-case comparison in place of a probabilistic average; reopen when the uncertainty set or its cross-stage dependence changes. |


## MMP.8.SD:End {#end}
