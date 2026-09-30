# MMP.16 - Design Observations to Separate Mathematical Model Alternatives: depth {#depth}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Depth sections of the pattern; the working sections are in the contract document of the same id. See LICENSE.md for the list of changes.

## MMP.16:5 - Archetypal Grounding {#archetypal-grounding}

The cases use stipulated models and costs so that the design can be reconstructed. They demonstrate the method, not reports of performed experiments.

### MMP.16:5.1 - The largest response difference disappears in the readout {#the-largest-response-difference-disappears-in-the-readout}

A team has two candidate response laws for a calibrated device assumed valid over the input range 0 to 2:

- H1: y=x;
- H2: y=x^2.

Both agree at the previously inspected inputs 0 and 1. The team needs to know whether the modeled response at x=2 is below or above 3. The laws answer differently: 2 and 4. Their applicability across the range is an assumption supplied for this case.

With a numerical readout r=y+e and a known error bound -0.1 <= e <= 0.1, the design x=2 gives:

| Design | H1 records | H2 records | Consequence |
| --- | --- | --- | --- |
| x=2, numerical readout | [1.9,2.1] | [3.9,4.1] | Disjoint intervals separate the alternatives. |

Now recover a missed feature of the actual instrument: it saturates at 1. Its record is r=min(1,y+e). At x=2 both alternatives always record 1. The large latent response difference gives no distinction at all.

Changing the input to x=0.5 yields:

| Design | H1 records | H2 records | Consequence |
| --- | --- | --- | --- |
| x=0.5, saturating readout | [0.4,0.6] | [0.15,0.35] | Both ranges lie below saturation and are disjoint. |

This design separates the supplied alternatives without replacing the instrument. A record 0.27 retains H2; a record 0.52 retains H1. A record 0.37 fits neither under the given error bound, so it reopens the response or observing assumptions rather than forcing a label.

The result at x=0.5 supports the answer at x=2 through the supplied response families. If those families were justified only up to x=1, this design would not establish the requested extrapolation. The next work would concern that range extension or access to a suitable direct observation.

If the only available inputs were 0 and 1 and the record error law were the same under both accounts, the available designs would not separate them. That conclusion concerns the stated access; it does not say the response question is unanswerable under every possible instrument.

### MMP.16:5.2 - A useful signal is still too costly {#a-useful-signal-is-still-too-costly}

A service team must choose one of two recovery procedures. It models two possible failure modes H0 and H1 with current probabilities 0.5 each. The loss is remaining recovery time, in hours:

| Procedure | H0 | H1 |
| --- | --- | --- |
| A | 0 | 10 |
| B | 4 | 0 |

With current information, expected losses are 5 for A and 2 for B. The team chooses B.

A proposed diagnostic produces either "+" or "-". Its supplied law is P(+ | H1)=0.8 and P(+ | H0)=0.2. Each signal has marginal probability 0.5. Bayes conditioning gives P(H1 | +)=0.8 and P(H1 | -)=0.2.

After "+", A has expected loss 8 and B has 0.8, so the team chooses B. After "-", A has expected loss 2 and B has 3.2, so it chooses A. Expected loss with the signal, excluding diagnostic cost, is therefore:

~~~
R(d) = 0.5*0.8 + 0.5*2 = 1.4 hours.
R0 - R(d) = 2 - 1.4 = 0.6 hours.
~~~

If obtaining, interpreting and waiting for the diagnostic adds 0.7 hours to recovery, its total expected loss is 2.1 hours; using current information is better under these conditions. At an all-inclusive cost of 0.2 hours, the diagnostic gives 1.6 hours and improves the choice. The example assumes the diagnostic does not change the failure mode or the two procedures.

A different test might reveal a device identifier perfectly. If that identifier is independent of the failure mode and losses in this model, its information gain about the identifier does not reduce this recovery loss. Selecting all available uncertainty as the target would misdirect the design.

Now change the current probability of H1 to 0.95. The "-" posterior is 0.19/(0.19+0.04), approximately 0.826, and the "+" posterior is 0.76/(0.76+0.01), approximately 0.987. B remains the better procedure after either result. The diagnostic still changes beliefs about the mode, but its sample-information value for this particular choice is zero.

A later method-development investigation could use the same signal for another target, such as learning how failure modes arise. That research value needs its own question and horizon; the zero above applies to the specified recovery choice.

## MMP.16:6 - Bias-Annotation {#bias-annotation}

The worked cases make the candidate models and observing conditions unusually explicit. In practice, deriving the record law can be the hardest contribution. The mathematical design must retain uncertainty about that law rather than quietly treating a convenient simulator as the subject.

A small named model set also favors choosing a winner. Keep the possibility that all proposed accounts fail the receiving use. Conversely, do not turn that possibility into a demand for an unlimited search for alternatives: pursue it when a discrepancy or consequential vulnerability makes it useful.

## MMP.16:8 - Common Anti-Patterns and How to Avoid Them {#common-anti-patterns-and-how-to-avoid-them}

| Anti-pattern | What goes wrong | Repair |
| --- | --- | --- |
| Maximize a difference before deriving the record | Saturation, selection or aggregation can erase it | Compare the obtainable records, as in :5.1 |
| Demand disjoint supports for every useful test | Discards informative but uncertain observations | Construct the required error or decision comparison |
| Average away an unknown without a probability basis | Hides the assumption deciding which design looks best | Retain conditional cases or supply the probability law |
| Maximize information about every model parameter | Can favor learning that leaves the receiving question unchanged | Select the target or consequences that matter |
| Treat the best candidate as an adequate account | A closed comparison can select a poor explanation of the subject | Use a consequential mismatch to reopen the family |
| Require new data whenever models disagree | Spends effort even when the answer is already sufficient | Compare with the attainable use of current information |
| Interpret an adaptive sample as if it were fixed in advance | Can invalidate the claimed uncertainty or error property | Derive the law for the actual choices and stopping rule |

## MMP.16:10 - Architectural Rationale {#architectural-rationale}

The general contribution is the construction of discriminating observations from models and their receiving use. It is separate from performing a physical test, deriving an estimator after observations, or choosing among all possible projects.

Separating the predicted response from its recording prevents a mathematical contrast from being mistaken for an observable one. Separating information from decision consequence lets exploratory research retain its own value while avoiding an automatic demand for more evidence in ordinary work.

The deterministic and probabilistic branches share that construction. Their guarantees differ, so the pattern does not reduce every use to one statistical test or one information metric. Existing FPF choice, resource and improvement methods receive the consequences produced here.

## MMP.16:11 - SoTA-Echoing {#sota-echoing}

**Design according to its goal.** Huan, Jagalur and Marzouk, *Optimal experimental design: Formulations and computations* (Acta Numerica, 2024), §2.2 and the goal-oriented and model-discrimination formulations, distinguish information targets and decision utilities. The adopted contribution is the explicit selection of what an observation should improve in :4.4. A design maximizing information about every parameter is a serious default when that is the actual aim; it is replaced when the receiving target differs. Numerical optimization methods are delegated to the applicable computational construction. [Source](https://arxiv.org/html/2407.16212v1).

**Information that can change a decision.** Heath and colleagues, *Simulating Study Data to Support Expected Value of Sample Information Calculations: A Tutorial* (2022), “Background and Notation,” gives the pre-observation comparison of decisions after possible records. Its loss-form equivalent is used in :4.4 and the original recovery example in :5.2. The model's costs and consequences must describe the receiving work; the source's health-economic conventions are not generalized into mandatory monetary valuation. [Source](https://journals.sagepub.com/doi/10.1177/0272989X211026292).

**An informative design can misdirect learning.** Tang, Sloman and Kaski, *Representative, Informative, and De-Amplifying: Requirements for Robust Bayesian Active Learning under Model Misspecification* (arXiv v2, 2026), §§2–4, studies prediction under a fixed, potentially inadequate model family. Its analysis separates approximation error, estimation error and their interaction under the intended input distribution. This motivates the explicit receiving conditions in :4.6. Their proposed acquisition rule is not a universal remedy: its assumptions and quantities need their own justification before use. The adopted general move is to compare consequential model inadequacy and observation placement, rather than assuming that higher information gain implies better prediction. [Read version](https://arxiv.org/html/2506.07805v2).

These sources develop statistical branches. The bounded-error construction in :5.1 is an elementary set-valued derivation; it needs no prior distribution. Reopen the selected design when the target, record law, feasible access, receiving population or substantive model alternatives change. A newer optimization technique matters when it improves that same construction at worthwhile effort.


## MMP.16:End {#end}
