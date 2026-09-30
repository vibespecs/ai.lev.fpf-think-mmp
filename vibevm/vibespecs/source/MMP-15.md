# MMP.15 - Identify an Intervention Effect from Available Data: depth {#depth}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Depth sections of the pattern; the working sections are in the contract document of the same id. See LICENSE.md for the list of changes.

## MMP.15:5 - Archetypal Grounding {#archetypal-grounding}

These constructed population probabilities make the calculations inspectable; they are not empirical results. Each case assumes fixed intervention meanings and no interference between its units. Finite records add estimation uncertainty to the assumption dependence shown here.

### MMP.15:5.1 - Separate a production action from the batches receiving it {#separate-a-production-action-from-the-batches-receiving-it}

A production team asks whether enabling a stabilization mode \(A=1\), rather than \(A=0\), increases the probability of a conforming item \(Y=1\). Incoming batch condition \(L\) is recorded before mode selection. Half the target batches have \(L=0\), half \(L=1\). Mode 1 is used on 80% of \(L=0\) batches and 20% of \(L=1\) batches.

| Batch condition | \(P(Y=1\mid A=0,L)\) | \(P(Y=1\mid A=1,L)\) |
| --- | --- | --- |
| \(L=0\) | 0.10 | 0.20 |
| \(L=1\) | 0.70 | 0.80 |

The subject account asserts consistency and mean exchangeability given \(L\); both modes occur in both strata. Adjustment therefore gives \(\mu_0=0.5(0.10)+0.5(0.70)=0.40\), \(\mu_1=0.5(0.20)+0.5(0.80)=0.50\), and \(\Delta=0.10\).

The selected groups instead give \(E[Y\mid A=1]=0.8(0.20)+0.2(0.80)=0.32\) and \(E[Y\mid A=0]=0.2(0.10)+0.8(0.70)=0.58\): an association of \(-0.26\). Its sign differs because the two modes receive different batch mixtures.

This positive average effect is conditional on the causal account; the table does not prove exchangeability. An already supported account and sufficient estimate need no new experiment.

### MMP.15:5.2 - Use a mediator, then withdraw a pathway exclusion {#use-a-mediator-then-withdraw-a-pathway-exclusion}

A service's command \(A\) can activate a retry mechanism \(M\), which affects successful completion \(Y\). Unrecorded load can affect both command selection and completion. The initial causal account permits \(A\to M\to Y\) and an unobserved common cause of \(A,Y\), but no other arrows: in particular, no direct effect of \(A\) on \(Y\) and no hidden common cause of \(A,M\) or \(M,Y\).

All three variables are binary. The available joint law has \(P(A=1)=0.5\), \(P(M=1\mid A=0)=0.25\), \(P(M=1\mid A=1)=0.75\), and:

| Mediator and command | \(P(Y=1\mid M,A)\) |
| --- | --- |
| \(M=0,A=0\) | 0.10 |
| \(M=1,A=0\) | 0.70 |
| \(M=0,A=1\) | 0.30 |
| \(M=1,A=1\) | 0.90 |

There is no observed pretreatment adjustment variable for the shared load. The front-door conditions nevertheless hold. First adjust the mediator's effect over \(A\): the inner means are \(h(0)=0.5(0.10)+0.5(0.30)=0.20\) and \(h(1)=0.5(0.70)+0.5(0.90)=0.80\). Then average over the mediator law induced by each command:

\[
\mu_0=0.75(0.20)+0.25(0.80)=0.35,\qquad
\mu_1=0.25(0.20)+0.75(0.80)=0.65.
\]

Thus \(\Delta=0.30\). Directly comparing observed commands instead gives \(0.75-0.25=0.50\).

**Changed condition.** Inspection of the service reveals that the command can also change completion through a path bypassing retry. The revised account permits a direct \(A\to Y\) arrow. Retaining the previous formula is no longer justified.

The same full observational law now admits at least two answers. To demonstrate this, let unobserved \(U\) be a fair binary variable, let observational command selection be \(A=U\), and generate \(M\) with probability \(0.25+0.50A\) using independent random variation. In two alternative models, generate completion with respective probabilities

\[
\text{Model I: }0.10+0.60M+0.20U,\qquad
\text{Model II: }0.10+0.60M+0.20A,
\]

using a further independent random draw. Every probability lies between zero and one. Because \(A=U\) observationally, both models give every cell of the supplied joint law.

Under \(do(A=a)\), \(U\) remains fair. Model I gives \(\mu_0=0.35,\mu_1=0.65\); Model II gives \(\mu_0=0.25,\mu_1=0.75\). Their effects are 0.30 and 0.50. Both satisfy the revised account, which permits the listed influences without requiring every permitted influence to be nonzero. Model II was excluded by the original no-direct-effect premise.

This is a proof that the revised assumptions and available law do not identify the average effect. These are ambiguity witnesses, not discovered service mechanisms. More precise estimation of the same law cannot distinguish them. A substantive restriction might; further evidence is chosen by its value for the use.

### MMP.15:5.3 - Transfer an experiment to another mixture of sites {#transfer-an-experiment-to-another-mixture-of-sites}

An ecological model asks for the effect of a specified irrigation change \(A\) on establishment of a seedling \(Y\), averaged across a target collection of sites. Soil stratum \(L\) is known from an existing inventory. A selected experiment randomized both irrigation levels within each stratum, recorded every outcome, and used the same irrigation implementations as the target question.

Suppose the subject account supports equality of conditional potential-outcome means between experimental and target sites. Experimental sites are 80% \(L=0\) and 20% \(L=1\); the target inventory is 25% \(L=0\) and 75% \(L=1\).

| Soil stratum | Experimental mean under \(A=0\) | Experimental mean under \(A=1\) | Difference |
| --- | --- | --- | --- |
| \(L=0\) | 0.20 | 0.50 | 0.30 |
| \(L=1\) | 0.60 | 0.70 | 0.10 |

The experimental average effect is \(0.8(0.30)+0.2(0.10)=0.26\). The target means are \(\mu_0=0.25(0.20)+0.75(0.60)=0.50\) and \(\mu_1=0.25(0.50)+0.75(0.70)=0.65\). The requested effect is 0.15. Randomization identifies the comparisons inside the experiment; the transport assumption and target inventory justify the different outer average.

Now suppose the source is found to contain experimental outcomes only for \(L=0\); the supplied \(L=1\) values were extrapolations, with no justified response relation supporting them. Retain the target inventory and transport within the covered stratum. With no outcome restriction for \(L=1\) beyond binary outcomes, its mean effect \(\delta_1\) lies in \([-1,1]\). Therefore

\[
\Delta=0.25(0.30)+0.75\delta_1\in[-0.675,0.825].
\]

The endpoints are attainable by making every uncovered site respectively harmed or helped: \((Y(0),Y(1))=(1,0)\) or \((0,1)\). Those choices do not alter any available experimental outcome. The bound is sharp under these assumptions, and the sign of the target effect is not identified. The effect 0.30 remains available for the covered stratum if that is the agreed receiving question; it must not silently replace the original population target.

## MMP.15:6 - Bias-Annotation {#bias-annotation}

Predictive success invites reading inputs as controls. Readily measured variables invite unjustified adjustment, while unmeasured common causes disappear for lack of a data column. Construct the causal account from the subject process.

Failure of a familiar criterion can instead encourage unnecessary data collection. Search more broadly when the answer matters, preserving unresolved search as unresolved. Check that calculation has not substituted a convenient population or intervention version for the requested one.

## MMP.15:8 - Common Anti-Patterns and How to Avoid Them {#common-anti-patterns-and-how-to-avoid-them}

| Anti-pattern | Consequence | Repair |
| --- | --- | --- |
| Change a predictor value and call the prediction an effect | Conditions on naturally selected cases rather than specifying an intervention | Define the intervention target and derive its relation to the available law |
| Adjust for every recorded variable | Can block part of the requested effect or open a collider path | Justify the selected variables for that target |
| Treat no adjustment set as nonidentifiability | Misses mediated or other identifying constructions | Seek a justified broader derivation or a real obstruction |
| Pool experimental, selected and target records as one population | Changes the probability law behind the expression | Retain source conditions and derive the transport or selection correction |
| Fill unsupported cells by regression and claim data-only identification | Hides extrapolation assumptions | State the additional response restriction or return a bound |
| Treat a prior, fitted mechanism or simulation as fresh causal evidence | Conceals disagreement among compatible causal models | Show which assumption selected the answer and what the records distinguish |

## MMP.15:10 - Architectural Rationale {#architectural-rationale}

Mechanism replacement gives intervention semantics within a model. Identification adds a different construction: showing that the needed intervention consequence is common to the causal models compatible with available laws and assumptions, or exposing where it is not.

The target-first construction avoids demanding a complete causal model when a mean, contrast or bound suffices. Separating derivation from estimation lets one identifying expression support different appropriate inferential methods. Separating source laws prevents mathematical convenience from turning selected records into information about an unobserved population.

## MMP.15:11 - SoTA-Echoing {#sota-echoing}

The governing question is whether the available laws and defensible causal assumptions determine the requested intervention quantity. A serious default is justified covariate adjustment; another is to fit a response model and predict after changing its action input. Adjustment is retained when it supplies a valid, economical derivation. Prediction under a fitted response model is accepted as an intervention answer only when its structural assumptions identify that meaning.

**Historical completeness anchor.** Shpitser and Pearl, *Identification of Joint Interventional Distributions in Recursive Semi-Markovian Causal Models* (AAAI 2006, UCLA report R-327), Figure 3 and the soundness/completeness argument, supply an algorithm that can return an expression or a graphical obstruction in its specified model class. This supports :4.3 and :4.5: failure of adjustment is not the general stopping rule, and a negative algorithmic result requires the matching completeness conditions. The result is not a universal certificate for cyclic, selected or otherwise differently specified models. [Source](https://ftp.cs.ucla.edu/pub/stat_ser/r327.pdf).

**Several available laws rather than an invented joint law.** Tikka, Hyttinen and Karvanen, *Causal Effect Identification from Multiple Incomplete Data Sources: A General Search-based Approach* (2021; arXiv v5, 27 August 2021), §§2–3.4, develops do-search by retaining known distributions and deriving new ones with justified rules. This is adopted in :4.2–:4.3 when one adjustment formula or one complete observational law does not fit the information actually available. Its broader search costs more than a sufficient specialized derivation; its negative output has only the completeness scope established for the problem being solved. [Read version](https://arxiv.org/html/1902.01073v5).

**Current extension of a familiar sufficient criterion.** Wu and Robeva, *Generalization of Pearl's Front-Door Criterion* (arXiv v1, 16 April 2026), §3, gives weaker sufficient graphical conditions for the same front-door functional and worked derivations outside the classical criterion. This reinforces the broader derivation route in :4.3 instead of rejecting an effect merely because a familiar criterion fails. The simple case in :5.2 needs only the classical sufficient conditions. The newer result concerns a particular functional in its stated graphical setting; it neither removes the need for subject justification nor supplies a complete test for every causal target. [Read version](https://arxiv.org/html/2604.15288v1).

**Population scope is part of identification.** Dahabreh and colleagues, *Generalizing causal inferences from individuals in randomized trials to all trial-eligible individuals* (2019; arXiv v2, 29 October 2019), §§2–4, separates within-trial exchangeability from the conditional-mean and participation assumptions required for generalization. That distinction is adapted in :4.4 and :5.3: the target mixture can differ even when the experimental comparisons are valid. Its particular nested-trial setup is not presumed for arbitrary selected records. [Read version](https://arxiv.org/html/1709.04589v2).

Reopen the chosen derivation when the target, available laws, causal exclusions, population bridge or support changes. Consider a different identification method when it answers the same question under more defensible assumptions or with materially less effort; source recency alone does not require replacing an already sufficient argument.


## MMP.15:End {#end}
