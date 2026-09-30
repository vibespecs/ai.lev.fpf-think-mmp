# MMP.18 - Couple Models with Compatible Exchanges and Scales: depth {#depth}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Depth sections of the pattern; the working sections are in the contract document of the same id. See LICENSE.md for the list of changes.

## MMP.18:5 - Archetypal Grounding {#archetypal-grounding}

These constructed cases keep the model assumptions visible so that the reader can change the exchange and recompute its consequence.

### MMP.18:5.1 - Preserve a transfer across different time resolutions {#preserve-a-transfer-across-different-time-resolutions}

Two components model stores A and B. Material flows from A to B with the supplied rate q(t)=k*t, where t is time since the interval's start and k=1 unit per minute squared. The stores have enough material and capacity for the stipulated transfer over T=1 minute. Initially A=10 units and B=0.

The donor computes the interval amount:

~~~
Q = integral from 0 to T of k*t dt = k*T^2/2 = 0.5 units.
A(T) = 10 - 0.5 = 9.5 units.
~~~

The receiving simulator takes the initial rate q(0)=0 and holds it throughout the minute. It obtains B(T)=0. The combined stores now total 9.5 units, although the model contains no external removal.

The error is in the exchange. Both components must use the same transferred amount over the same interval. Sending Q=0.5 units and applying A(T)=10-Q, B(T)=Q gives a total of 10 units. C.29.BB supplies the balance; this construction makes the exchange between the two component representations satisfy it.

Now change the requested result: when does B first reach 0.125 units? Under the supplied continuous rate, B(t)=k*t^2/2, so it reaches the threshold at t=0.5 minutes. A receiver that inserts the entire amount only at T=1 minute reports a different crossing time despite preserving the final balance.

For that question, send or reconstruct the cumulative transfer Q(t)=k*t^2/2 over the interval, or use a computation with adequate intermediate and event resolution. Exchanging only the interval amount is sufficient for the final stores but insufficient for the crossing. The changed question reopens the temporal representation, not the already correct conservation argument.

A nonlinear receiver can likewise need more than an averaged input. Suppose two equally weighted fine cells supply x values (0,2), and the receiver requires the average of x^2. The mean input is 1, but the required response is (0+4)/2=2. Sending only the mean and squaring it gives 1. Supplying variance 1 restores 1^2+1=2; a justified closure could supply the same missing contribution in a larger model.

### MMP.18:5.2 - Join two analyses without counting their prior twice {#join-two-analyses-without-counting-their-prior-twice}

Two analyses concern the same binary condition z. Both start from P(z=1)=0.2 and P(z=0)=0.8. Each has one positive observation with the supplied law:

~~~
P(positive | z=1) = 0.75
P(positive | z=0) = 0.25.
~~~

The two observations are distinct and conditionally independent given z. Each separate posterior gives:

~~~
P(z=1 | one positive) = (0.2*0.75)/(0.2*0.75 + 0.8*0.25) = 3/7.
~~~

Multiplying the two posterior mass functions and normalizing gives 9/(9+16)=9/25=0.36. This has counted the shared prior twice.

Construct the joint model from one prior and the two likelihood factors:

~~~
P(z=1 | two positives)
 = (0.2*0.75^2)/(0.2*0.75^2 + 0.8*0.25^2)
 = 9/13, approximately 0.692.
~~~

The same result is recoverable from the separate posteriors by dividing their product by the common prior before normalizing. That operation preserves their intended contributions under the supplied conditional independence.

Now discover that the two reports contain the same observation, copied into two analyses. There is only one likelihood factor. The correct result under the original observation model is again 3/7; the 9/13 calculation is no longer supported. If there are two dependent observations instead, their joint conditional law is needed.

The exchange therefore includes the identity and dependence of the contributing information, not just two numbers labeled “probability.” In a method assessment, the same problem appears when two models of performance use overlapping case records.

## MMP.18:6 - Bias-Annotation {#bias-annotation}

Coupling is often presented through physical simulations, which can suggest that every interface carries a conserved flow. Statistical components instead require coherent shared distributions and dependence. Both cases need an explicit relation between components; the relation's governing property comes from the modeled quantity.

The examples use small equations with known solutions. A large coupled formulation may be well defined but expensive to compute, or locally accurate but poor for the receiving use. Preserve that distinction when choosing a simpler interface or component.

## MMP.18:8 - Common Anti-Patterns and How to Avoid Them {#common-anti-patterns-and-how-to-avoid-them}

| Anti-pattern | Failure | Repair |
| --- | --- | --- |
| Connect equal names as equal quantities | Different intervals, references or populations become silently identified | Construct the quantity correspondence before exchanging values |
| Use an interpolation because the tool offers it | A total or constant field may be altered | Derive the preservation condition from the receiving use |
| Pass an average into an arbitrary nonlinear operation | Lost variation changes the result | Derive and supply the missing statistic or closure |
| Treat software call order as the subject law | Inserts a delay or leaves same-instant relations unsatisfied | Formulate the joint conditions, then choose their computation |
| Preserve the final balance and claim the trajectory | Intermediate timing remains unresolved | Retain the temporal information required by the question |
| Multiply fitted component distributions | Can duplicate a prior or shared records | Recover and combine the actual likelihood and dependence contributions |
| Reuse an isolated closure under changed feedback | The coupled system can leave the closure's supported regime | Revise its supply conditions or use a suitable richer component |

## MMP.18:10 - Architectural Rationale {#architectural-rationale}

The general relation-composition method supplies the way to impose conditions together. Model coupling adds the construction needed when those conditions use different representations, scales or overlapping information. It makes the supplier's result usable by the receiver.

A separate interface relation keeps three possible repairs distinguishable: change a component, change how its contribution is represented, or change the computation of their joint conditions. Without that distinction, solver adjustments can conceal a subject-model error, while a harmless numerical approximation can provoke an unnecessary redesign of the subject account.

Conservation and probabilistic coherence are different preservation questions. Their coexistence here reflects a common modeling task, not an assertion that a probability distribution is a physical flow. The appropriate mathematics remains with its governing pattern or specialist method.

## MMP.18:11 - SoTA-Echoing {#sota-echoing}

**Interoperable components still need a coupling construction.** The Modelica Association's *Functional Mock-up Interface* 3.0.2, §§3–4, distinguishes exchanging model equations from co-simulation and leaves the coordinating solver to the importer. This supports :4.4: an interface format does not select the numerical interaction or establish its error. Reusing existing simulators remains valuable when their exchange capabilities support the required result; a joint solve is the alternative when independently advanced components do not. [Specification](https://fmi-standard.org/docs/3.0.2/).

**Choose a map by what it preserves.** The current preCICE documentation, “Mapping configuration,” distinguishes sum-preserving maps, constant-field interpolation and weighted integral preservation. The adopted move in :4.2 is to derive the required map property from the exchanged quantity. The documentation's mesh algorithms are useful specialized realizations, not universal choices for every representation. A cheap nearest-neighbor map can suffice when its error and preserved quantities fit the use. [Source](https://precice.org/configuration-mapping).

**A common unknown needs a coherent joint distribution.** Goudie and colleagues, *Joining and splitting models with Markov melding* (2019; arXiv v3), §3, constructs combinations through shared variables and addresses inconsistent marginal priors. This supplies a serious alternative to informal transfer of fitted summaries. The simple common-prior case in :4.5 and :5.2 is adopted here; more general pooling requires its additional assumptions. [Read version](https://arxiv.org/html/1607.06779v3). Manderson and Goudie, *Combining chains of Bayesian models with Markov melding* (2023), extends the construction to distinct shared quantities along a chain while retaining their dependence. That extension matters when one shared variable cannot represent all interfaces; an arbitrary network or dependent evidence still requires its own joint construction. [Source](https://arxiv.org/html/2111.11566v2).

**Scale interfaces can need learned or derived closures.** Sanderse and colleagues, *Scientific machine learning for closure models in multiscale problems: a review* (2024), §2, locates the missing contribution when reduction and evolution do not commute. That result supports :4.3's return to MMP.9 or a suitable surrogate. A learned closure is one candidate alongside derived memory, retained state and sufficient bounds; its isolated fit does not settle its coupled use. [Source](https://arxiv.org/html/2403.02913v2).

Revisit the coupling when a component, exchange representation, shared data, scale or receiving result changes. A new numerical or learned method is useful when it improves that same coupling under its applicability conditions and available resources.


## MMP.18:End {#end}
