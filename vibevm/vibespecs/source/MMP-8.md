# MMP.8 - Formulate Information-Dependent Choices Mathematically: depth {#depth}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Depth sections of the pattern; the working sections are in the contract document of the same id. See LICENSE.md for the list of changes.

## MMP.8:5 - Archetypal Grounding {#archetypal-grounding}

### MMP.8:5.1 - Choose a preload before or after learning an external load {#choose-a-preload-before-or-after-learning-an-external-load}

An ideal static arrangement has a downward load w, an adjustable upward preload a and a residual y=w-a. A later use requires `abs(y)<=1/4`. The load is either 1 or 2, and a can be any value from 0 to 2. The relation is a supplied illustrative mechanical model; the pattern's work is to formulate the choice and its information.

If w=1, acceptable choices form `[3/4,5/4]`; if w=2, they form `[7/4,2]` after the actuator limit is applied. Both sets are nonempty, so each known load has a feasible choice. Their intersection is empty. No one preload chosen before distinguishing the loads can meet the requirement for both.

Suppose a reading available before adjustment reports which of the two loads is present. The policy `a=w` then meets the requirement. A reading received only after the preload is locked cannot support that policy at the relevant decision.

Now the tolerance is relaxed to 3/5. The acceptable intervals overlap from 7/5 to 8/5, so `a=3/2` works before any reading. Additional measurement is unnecessary for this revised requirement. The change is in the required result, not the sophistication of the computation.

### MMP.8:5.2 - Decide which participant gets a scarce resource {#decide-which-participant-gets-a-scarce-resource}

Two work requests, L and R, may need the only available resource. Exactly one needs it. Allocation succeeds when the resource goes to that request. The instruction must choose L or R deterministically from one report received before allocation.

With no distinguishing report, there are two constant instructions: always allocate to L or always allocate to R. Each fails in one circumstance. A truthful timely report permits an instruction that follows it and succeeds in both. A report arriving after allocation cannot supply that choice.

Now the timely report is noisy. The observing procedure independently chooses one of two channels with equal probability, then sends its L/R report without naming the channel. The model supplies these conditional reporting probabilities; the remaining probability in each row produces the opposite report:

| Channel | Actual request needing the resource | Probability of a correct report |
| --- | --- | ---: |
| 1 | L | 0.9 |
| 1 | R | 0.5 |
| 2 | L | 0.7 |
| 2 | R | 0.9 |

Use MMP.7 to remove the unrecorded channel by summing over it. For fixed circumstance L, `P(report L)=0.5*0.9+0.5*0.7=0.8`. For fixed R, `P(report R)=0.5*0.5+0.5*0.9=0.7`. No probability for which request actually needs the resource was needed for this construction.

There are four deterministic instructions from one two-valued report:

| Instruction | Success probability in fixed L | Success probability in fixed R |
| --- | ---: | ---: |
| Always allocate to L | 1 | 0 |
| Always allocate to R | 0 | 1 |
| Follow the report | 0.8 | 0.7 |
| Choose opposite to the report | 0.2 | 0.3 |

If the requirement is success probability at least 0.65 in each admitted circumstance, following the report satisfies it. None of these instructions gives a zero-failure guarantee. The conditional laws are sufficient to make both statements while the circumstance remains unknown and fixed.

Change the question to average success in a stream of requests modeled as L with probability 0.95 and R with probability 0.05, retaining the channel procedure. Following the report gives `0.95*0.8+0.05*0.7=0.795`. Always allocating to L gives 0.95; always allocating to R gives 0.05, and choosing opposite to the report gives 0.205. The instruction with greatest average success among the four is now always L. It still fails in fixed R.

Choose the performance requirement from the work's purpose before adopting an instruction. The observing model supplies conditional probabilities; the decision about the work determines whether performance in each circumstance or an average matters.

To retain the zero-failure requirement, the work could obtain a truthful report in time or provide enough resource to serve both requests. Compare the cost of those changes with the consequences of accepting a mistaken allocation, using C.11.DUA. A changed channel, recorded channel identity or permission to randomize the instruction changes the information or choice set; formulate the revised question accordingly.

### MMP.8:5.3 - Find a strategy, rather than an answer chosen with future knowledge {#find-a-strategy-rather-than-an-answer-chosen-with-future}

A program repeatedly receives a bit b and emits a bit a. A requirement asks it to emit the same bit. If receipt precedes emission, the rule `a=b` works on every round. If emission must precede receipt, each possible future bit has a matching answer, but no deterministic rule using only the earlier history can guarantee a match against every admitted next bit.

To see the failure, hold the earlier history fixed. The rule chooses either 0 or 1. Both next input bits are still admitted, including the opposite one. That continuation refutes the guarantee for this history. Inspecting more successful traces cannot remove it.

A changed requirement may ask for success probability under independent fair input bits. Any earlier choice then matches with probability 1/2 in one round, including a randomized earlier choice independent of the next bit. Success in every one of N such rounds has probability 2^(-N). These probabilistic claims use the new input assumption. They do not establish success against every input stream.

This is a continuing computational interaction. The construction determines how each response may depend on incoming information. The same observation-order construction identifies what a distributed team or controller would need to know before acting.

## MMP.8:6 - Bias-Annotation {#bias-annotation}

Optimization tools encourage viewing every variable they can assign as an available choice. Recover the subject meaning of each unknown before interpreting a solution. A second bias is to make robustness the default goal. State the receiving requirement first; a conditional answer or an explicitly accepted risk may be more useful than an infeasible all-circumstances guarantee.

## MMP.8:8 - Common Anti-Patterns and How to Avoid Them {#common-anti-patterns-and-how-to-avoid-them}

| Failure in this work | Repair |
| --- | --- |
| A solver changes an external load or unknown state to satisfy the goal. | Treat it as a circumstance and apply the required quantifier. |
| A separately optimal action for every future is presented as one available strategy. | Group cases by the information available at the decision; require a common action within each group. |
| An existentially chosen consequence stands in for all allowed behavior. | Retain the behavior relation and test the quantifier required by the goal. |
| A larger uncertainty set is called safer without examining its subject meaning or cost. | Check the joint possible circumstances and choose the requirement for the actual use. |
| Better observation is required after a sufficient common action is already available. | Compare what the additional information can change before commissioning it. |

## MMP.8:10 - Architectural Rationale {#architectural-rationale}

Quantifier order and permitted dependence express different aspects of the working problem. 'For each circumstance there is an action' concerns a family of possible solutions. An executable policy also needs a way to select its action from obtainable information. Grouping indistinguishable circumstances makes that additional condition visible and gives a constructive test for finite cases.

This mathematical formulation can describe physical adjustment, resource allocation or computational interaction. Its source premises and available actions differ across those practices. The method keeps those differences explicit while reusing the same reasoning about choices and information. It complements FPF's continuation and computation methods by constructing the mathematical answer condition they consume.

## MMP.8:11 - SoTA-Echoing {#sota-echoing}

[Boyd and Vandenberghe, Convex Optimization, section 4.1](https://www.stanford.edu/~boyd/cvxbook/bv_cvxbook.pdf), distinguish the feasible set from the objective and transformations of a problem. Adopt that separation in :4.1 and :4.3. The present finite constructions do not require convexity; the book's convex solution guarantees apply only under their conditions.

[Ben-Tal, Goryashko, Guslitzer and Nemirovski, Adjustable robust solutions of uncertain linear programs (2004)](https://doi.org/10.1007/s10107-003-0454-y), develop adjustable decisions alongside choices fixed before uncertainty is revealed. Adapt this distinction into the information-dependent formulation; do not transfer linear-program tractability to unrestricted policies.

[Duchi, Optimization with uncertain data (2018), sections 1 and 6](https://web.stanford.edu/class/ee364b/lectures/robust_notes.pdf), compares uncertainty-set requirements with probabilistic ones and makes choosing the uncertainty set a modeling question. Adopt that choice explicitly; no worst-case objective is imposed by this pattern.

[Vayanos, Georghiou and Yu, Robust Optimization with Decision-Dependent Information Discovery, version 3 (2022)](https://arxiv.org/abs/2004.08490v3), treats actions that affect when uncertainty can be observed. Carry that extension into :4.2 and the return to method design. Its specialized algorithms are further methods, not assumed capabilities of every reader.

The interval, allocation and bit-response examples are constructed demonstrations of the method under their stated assumptions.


## MMP.8:End {#end}
