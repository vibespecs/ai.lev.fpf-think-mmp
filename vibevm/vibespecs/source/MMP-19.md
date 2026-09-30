# MMP.19 - Construct and Bound a Mathematical Counterfactual Comparison under a Causal Model: depth {#depth}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Depth sections of the pattern; the working sections are in the contract document of the same id. See LICENSE.md for the list of changes.

## MMP.19:5 - Archetypal Grounding {#archetypal-grounding}

These are constructed cases with supplied mechanisms or exact probability laws. They demonstrate the mathematical operations and limits, not empirical effectiveness.

### MMP.19:5.1 - Change the route for an already observed processing case {#change-the-route-for-an-already-observed-processing-case}

A routing model gives latency in ticks as Y=2A+U. Route A=1 adds two ticks; residual latency U is 0 or 1 with equal probability. The recorded case used A=1 and had Y=3.

Under the factual equation only U=1 is compatible. Keeping that input and replacing the route by A=0 gives Y_0=1. Drawing a fresh U from the population instead gives mean latency 1/2. That is a new-case mean, not the requested alternative for the observed case.

If the record is noisy, use its likelihood rather than selecting U with certainty. If an exact Y=4 is reported under the unchanged model, neither admitted U is compatible; return the conflict instead of calculating a posterior with zero denominator. Whether the same residual condition would persist under a real route change is a subject premise of this model.

### MMP.19:5.2 - Expose a coupling that experiments do not determine {#expose-a-coupling-that-experiments-do-not-determine}

Let a randomized binary action A be independent of the response type U=(Y_0,Y_1). Consider two possible type distributions:

| Type (Y_0,Y_1) | Model S | Model T |
| --- | ---: | ---: |
| (0,0) | 3/8 | 1/8 |
| (0,1) | 1/8 | 3/8 |
| (1,0) | 1/8 | 3/8 |
| (1,1) | 3/8 | 1/8 |

Each action succeeds with probability 1/2 in both models. With a fair random assignment, all four observed (A,Y) combinations have probability 1/4 in each model.

For a case observed with A=1,Y=1, only types (0,1) and (1,1) remain. In S, the probability that it would also succeed under A=0 is (3/8)/(1/2)=3/4. In T it is (1/8)/(1/2)=1/4. Both models fit the supplied observational and intervention laws, so these laws do not identify the answer.

For a future choice scored only by expected success, the actions tie at 1/2 under both models. If A=1 adds a positive cost and no other consequence, A=0 is sufficient for that criterion. Resolving the counterfactual ambiguity would not improve this choice.

### MMP.19:5.3 - Bound benefit without inventing a joint law {#bound-benefit-without-inventing-a-joint-law}

Suppose binary success probabilities under actions 1 and 0 are p1=7/10 and p0=2/5. Let b=P(Y_0=0,Y_1=1), the probability of succeeding only under action 1. The four type masses must be

```text
P(0,1)=b                 P(1,1)=p1-b
P(1,0)=p0-p1+b           P(0,0)=1-p0-b.
```

Nonnegativity gives max(0,p1-p0) <= b <= min(p1,1-p0), hence 3/10 <= b <= 3/5. At b=3/10 the masses in order (00,01,10,11) are (3/10,3/10,0,2/5); at b=3/5 they are (0,3/5,3/10,1/10). Both attain the supplied marginals, establishing the bounds for this unrestricted response-type class.

Now suppose assignment A is independent of the response pair (Y_0,Y_1), P(A=1)>0, and a case is observed with A=1,Y=1. The probability that this case would fail under action 0 is P(Y_0=0 given A=1,Y=1)=b/p1, hence between 3/7 and 6/7. Conditioning retains the types with Y_1=1; the independent assignment probability cancels from numerator and denominator. The same endpoint distributions attain these conditional bounds, since their denominator is the fixed positive p1=7/10.

The mean effect is p1-p0=3/10 in every compatible model. An expected-success criterion with an action-1 cost of 1/10 therefore has net gain 1/5 without identifying b. A criterion that explicitly requires b to exceed 2/5 remains unsettled by these bounds.

If subject knowledge warrants that action 1 never changes a success into failure, P(1,0)=0 fixes b=3/10. That is an additional monotonicity assumption; it was not learned from the two marginal probabilities.

### MMP.19:5.4 - State which mediated contrast is being calculated {#state-which-mediated-contrast-is-being-calculated}

Take the supplied mechanisms M=A+U and Y=3A+2M+AM, with U=0 or 1. Compare actions 0 and 1 for the same u. The total change is 6+u.

First retain the mediator at M_0=u while changing A: Y_(1,M_0)-Y_(0,M_0)=3+u. Then change the mediator to M_1=1+u while retaining A=1: Y_(1,M_1)-Y_(1,M_0)=3. The components sum to 6+u.

Reversing that decomposition gives mediator change 2 at A=0, followed by direct change 4+u at M_1. These components also sum to 6+u. The interaction AM makes the two decompositions different. A request for “the part caused through M” must select its intended contrast. Knowing the total effect alone supplies neither decomposition; observing data that identify it is a further question.

## MMP.19:6 - Bias-Annotation {#bias-annotation}

The explicit examples use finite inputs and simple structural functions. Their transparency helps inspect a comparison but does not show that such a causal account is obtainable for every subject. Subject ambiguity can remain after a numerical method computes a definite answer.

The same-unit relation is part of the model. Its appropriateness in a physical, organizational or human setting depends on what is held common and what each action changes. A purely numerical pairing can be useful for variance reduction while lacking the interpretation required by the causal question.

## MMP.19:8 - Common Anti-Patterns and How to Avoid Them {#common-anti-patterns-and-how-to-avoid-them}

| Recognizable failure | Repair |
| --- | --- |
| Use the population input law after receiving information about the case. | Condition under the factual account before evaluating its alternative response. |
| Independently simulate two marginals and interpret the pairs as the same units. | Construct or bound the joint response law the interpretation needs. |
| Replace a nested intermediate value by its population mean. | Compute the intermediate response for each common input before evaluating the outer mechanism. |
| Report a uniquely identified answer because one chosen model yields a number. | Examine the target across the admissible models, or report the result as conditional on that model. |
| Demand a benefit probability for a choice determined by expected outcomes. | Recover the criterion and use the sufficient marginal comparison. |

## MMP.19:10 - Architectural Rationale {#architectural-rationale}

The hard step is often the relation between calculations, rather than each calculation separately. Ordinary conditioning recovers case information; mechanism replacement constructs an alternative; the common input or response-type law connects them. Maintaining that relation permits a joint question and exposes assumptions invisible in separate marginal fits.

The same construction supports historical explanation, probabilities of benefit and nested pathways. Their targets remain distinct. In particular, a decision based on realized outcomes can use less structure than a question about how those outcomes would differ for the same unit.

## MMP.19:11 - SoTA-Echoing {#sota-echoing}

[Correa and Bareinboim (2025)](https://proceedings.mlr.press/v267/correa25a.html), Definitions 1.1–1.3 and §2.1.1, supply the shared-input and nested-response semantics used in :4.2–:4.4. The finite examples here use those definitions; the richer graphical calculus has further conditions and operations.

[Mueller and Pearl (2023)](https://ftp.cs.ucla.edu/pub/stat_ser/r513.pdf) separate average effects from probabilities of benefit or harm. [Dawid and Senn (2025, v2)](https://arxiv.org/pdf/2301.11976), §§2–4, supply a serious alternative: intervention distributions suffice for maximizing expected realized outcomes under the stated information and constraints. Adopt the target distinction in :4.1/:4.6. In :5.2 the same two models require a joint account for the historical question but no such recovery for the stated future choice. The changed question justifies the more elaborate construction.

[Raghavan and Bareinboim (2026, preprint)](https://arxiv.org/html/2602.23541v1), §§2 and 4–5, distinguish identification, partial identification and physically realizable counterfactual sampling. Adapt those distinctions in :4.4–:4.5. Their available-action, finite recursive and positivity assumptions limit the algorithmic results. Establishing a model consequence leaves its physical sampling conditions to be established separately when sampling is needed.

Reopen the selected construction when a supported additional mechanism or information source changes the compatible comparisons, or when another method obtains the required answer with less unsupported structure or burden. The worked finite constructions establish their stated mathematical consequences; practical validity still depends on the subject account.


## MMP.19:End {#end}
