# MMP.14 - Find and Repair a Mathematical Model's Failed Predictions: depth {#depth}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Depth sections of the pattern; the working sections are in the contract document of the same id. See LICENSE.md for the list of changes.

## MMP.14:5 - Archetypal Grounding {#archetypal-grounding}

The following are constructed cases. Their arithmetic demonstrates the method; the stated observations are example inputs, not reports of empirical studies.

### MMP.14:5.1 - A correct overall mean conceals failed conditional predictions {#a-correct-overall-mean-conceals-failed-conditional-predictions}

Two message routes, A and B, are used under ordinary load. The target is the chance of timely delivery for each known route. In this small example every message has a complete binary record, the deadline is unchanged, and outcomes are assumed independent with a stable probability within each route and load regime.

The supplied records are partitioned before fitting. Only the fitting and diagnostic portions are opened during model construction; the assessment portion remains withheld until the revised forecasts are fixed.

| Portion | A: timely / total | B: timely / total |
| --- | --- | --- |
| Fitting | 8 / 10 | 2 / 10 |
| Diagnostic | 9 / 10 | 1 / 10 |
| Withheld assessment | 8 / 10 | 2 / 10 |

The original model \(M_0\) ignores route: \(Y_i\sim\mathrm{Bernoulli}(p)\). Its maximum-likelihood estimate from the fitting portion is \(\hat p=1/2\). Its expected diagnostic total equals the observed total: 10 timely deliveries out of 20. That agreement does not answer the route-specific question.

Choose \(D=|K_A/10-K_B/10|\), where \(K_A,K_B\) are the timely counts in the diagnostic portion. Observed \(D=0.8\). Under the common-probability model, condition on the observed total \(K_A+K_B=10\). Then
\[
 P(K_A=k\mid K_A+K_B=10,M_0)
   =\frac{\binom{10}{k}\binom{10}{10-k}}{\binom{20}{10}}.
\]
This reference retains the two sample sizes and removes the unknown common \(p\). The exact two-sided tail for \(D\ge0.8\) is
\[
 \frac{2(1+100)}{184756}
 =\frac{101}{92378}\approx0.001093.
\]
It exposes a discrepancy in the common-probability account under its independence and stability assumptions. It does not identify a causal route effect. A shared disturbance confounded with route could demand a different repair.

Suppose the subject account permits route-specific response probabilities. Construct \(M_1\): \(Y_i\mid g_i\sim\mathrm{Bernoulli}(p_{g_i})\). Using the same fitting records gives \(\hat p_A=0.8,\hat p_B=0.2\). The changed component is the relation between the known route and the response probability, not the binary recording rule.

Recalculate the original discrepancy under the fitted \(M_1\), retaining the same total of 10. Conditional replicate counts have weights
\[
 w_k=\binom{10}{k}^{2}16^k,\qquad
 P(K_A=k\mid K_A+K_B=10,\hat M_1)=w_k/\sum_{j=0}^{10}w_j,
\]
where \(16=(0.8/0.2)/(0.2/0.8)\) is the fitted odds ratio. Summing \(k=0,1,9,10\) gives \(P(D\ge0.8)=0.37348\). The revised point model accommodates the diagnostic contrast. This calculation is conditional on its fitted probabilities; it neither calibrates a test of the estimated family nor independently confirms the repair.

Fix these point-probability forecasts and open the assessment portion. The sum of log probabilities of its 20 individual outcomes, using natural logarithms, is
\[
 L_0=20\log(0.5)=-13.86294,\qquad
 L_1=16\log(0.8)+4\log(0.2)=-10.00805.
\]
Thus \(M_1\)'s fixed forecasts gain \(3.85490\) on this portion. This is an observed paired comparison, not a guaranteed future gain or a parameter-uncertainty interval. The diagnostic portion was used to propose the repair; it was not counted as untouched assessment.

For three future independent A messages under the same regime, the point forecast of at least one late delivery changes from \(1-0.5^3=0.875\) to \(1-0.8^3=0.488\). That receiving calculation must change. If uncertainty about the probabilities matters, MMP.13 must propagate it; the point calculation does not already do so.

**Changed condition.** The supplied operating condition now specifies high load. Before any refitting, a supplied high-load batch has 5/10 timely outcomes on each route. The ordinary-load forecasts give
\[
 L_1^{H}=10\log(0.8)+10\log(0.2)=-18.32581,
\]
whereas the common \(0.5\) forecast still gives \(-13.86294\). Carrying over the repaired forecast loses \(4.46287\) on this batch. The earlier assessment concerned ordinary load and does not establish transfer. Keep that use boundary and examine invariance if a high-load forecast is needed. A high-load common-rate fit of \(0.5\) is a possible new model; its fit here is not an untouched assessment. Its three-message late-delivery forecast would again be \(0.875\), conditional on that rate and independence.

For the narrower question of expected timely deliveries with equal numbers of A and B under ordinary load, both fitted models give one half of the total. If only that expectation is needed and its basis suffices, this case does not require adopting the richer model or obtaining new observations. It does not make the two models' conditional or joint predictions equivalent.

### MMP.14:5.2 - Repair the law of the exported records {#repair-the-law-of-the-exported-records}

A candidate latency model assigns \(X\) uniformly to the integer values 1 through 6. An export contains only values 1, 2 and 3. Comparing these records with unconditional replications of \(X\) suggests too few large values.

The documented export rule, supplied independently of that discrepancy, retains a record only when \(X\le3\). The failed comparison omitted selection. Compose the candidate event law with the actual rule:
\[
 P(R=j\mid\mathrm{retained})
 =\frac{P(X=j)}{P(X\le3)}=\frac13,\quad j=1,2,3.
\]
The predicted mean of exported values is 2, not 3.5. Their probability of exceeding 2 is \(1/3\), not \(2/3\). Construct comparable replications by applying the same filter, or draw directly from this conditional law. Do not reduce the latent model's tail merely to make the unfiltered comparison agree.

If the documented export cutoff changes to 4, the corresponding mean becomes 2.5 and the probability of an exported value exceeding 2 becomes \(1/2\), with no alteration to the candidate uniform latent law. These are recalculated consequences of the changed recording rule, not new empirical confirmation of that law.

Agreement within the retained range does not establish the distribution among unrecorded values. If the target is only the distribution of exported records, that unresolved tail may be irrelevant. If the target needs latent large-latency probabilities, return the missing information or assumption through MMP.12/C.16.IR; the selection correction has not recovered it.

### MMP.14:5.3 - A failed numerical prediction need not require a new subject model {#a-failed-numerical-prediction-need-not-require-a-new-subject}

A normalized quantity is modeled by \(u'(t)=-u(t)\), \(u(0)=1\). A record at \(t=1\) is \(0.370\), with an established absolute recording error at most \(0.005\). A forward-Euler computation with step \(h=1\) predicts 0.

Before replacing the decay law, compare the numerical result with the model's exact consequence \(u(1)=e^{-1}\approx0.367879\). Euler steps \(h=1/2\) and \(h=1/4\) give \(0.25\) and \(0.316406\); the sequence of approximations exposes a material computational error. The exact value lies in the observed admissible interval \([0.365,0.375]\). Here the repair belongs to CMP.8, while this observation supplies no reason to change the decay relation.

That interval overlap establishes compatibility for this record under the error bound, not the correctness of the decay model at every time. If a relevant observation instead excludes the accurately computed consequence, the subject relation or observation account becomes live again. Numerically precise evaluation and adequate subject prediction remain separate achievements.

## MMP.14:6 - Bias-Annotation {#bias-annotation}

Familiar diagnostics favor failures that are easy to display. Aggregate scores can hide sparse but consequential regimes; selecting the most striking plot can exaggerate ordinary variation. A preferred causal story can make one repair appear uniquely compelled when several produce the same records.

Preserve the intended use, the role of each data portion and the compatible alternatives. Do not transfer support to unrepresented conditions.

## MMP.14:8 - Common Anti-Patterns and How to Avoid Them {#common-anti-patterns-and-how-to-avoid-them}

| Anti-pattern | Repair |
| --- | --- |
| Fit the overall mean and infer adequacy for every conditional forecast | Compare the feature on which the receiving use depends. |
| Call every residual an error in the model | Compare with the model's permitted variation and relevant numerical or recording error. |
| Simulate latent states and compare them with selected records | Pass replications through the actual recording law. |
| Treat a predictive tail fraction as the probability that the model is wrong | Retain the reference distribution and its actual probability statement. |
| Tune repeatedly on a “test” set and report an untouched test result | Treat that set as development data; qualify or separately assess the adaptive procedure. |
| Replace an inconvenient observation or inflate noise until a check passes | Examine the observation basis and competing model components; preserve legitimate unusual outcomes. |
| Improve prediction and claim the causal explanation is established | Retain the predictive claim; obtain identification and subject grounds for the causal claim. |
| Require a new experiment after every mismatch | Use C.11.DUA to choose among available repair, narrower use, conditional continuation and worthwhile inquiry. |

## MMP.14:10 - Architectural Rationale {#architectural-rationale}

B.5.TC aligns competing accounts; B.5.RR carries a changed premise into its consequences. Neither alone constructs a conditional discrepancy distribution, a predictive replication or a withholding scheme. Those mathematical operations provide the contribution here.

MMP.13 determines inference under a model. This method examines where that model fails a needed prediction and changes a component before inference is repeated. MMP.7 prevents a change in recording from being mistaken for a change in the subject. MMP.11 supplies admissible replacement relations, while the subject method determines what those relations purport to represent.

The cases separate a missing conditional relation, a missing selection rule and an inaccurate computation.

## MMP.14:11 - SoTA-Echoing {#sota-echoing}

**Working question.** How can a practitioner find the model component that spoils a needed prediction and repair it without confusing better fit, statistical surprise and external confirmation?

**Selected line.** Combine discrepancy-directed predictive criticism with evaluation appropriate to the intended prediction. Use an exact conditional comparison, fitted simulation, posterior replication or held-out prediction according to the claim. No inferential framework wins independently of the question.

- Gelman, Vehtari and McElreath, [*Statistical Workflow*](https://sites.stat.columbia.edu/gelman/research/published/Statistical_Workflow_article.pdf), §§1.7–1.8 and 1.10–1.11. The text used is the author manuscript dated 5 December 2025 for the 2026 article, not the publisher's typeset version. Its operative contributions here are localizing misfit through predictive comparisons, understanding changes through related models, and separating computational calibration from subject adequacy. Adopt those in :4.3–:4.5. Adapt the wider workflow to a consequential local question; fitting increasingly flexible models until no anomaly remains can absorb legitimate rare patterns.
- [Stan User's Guide 2.39, “Posterior and Prior Predictive Checks”](https://mc-stan.org/docs/stan-users-guide/posterior-predictive-checks.html), posterior checks, discrepancy statistics and mixed hierarchical replication. Adopt the explicit replicated-data construction and the choice of what is regenerated in :4.2. Retain the limitation that a posterior predictive tail fraction is not generally a classically calibrated p-value. A statistic largely determined by fitting can miss the omitted structure. The Bayesian construction is one available comparison, not a requirement to replace an exact conditional or sufficient deterministic argument.
- Aki Vehtari, [*Cross-validation FAQ*](https://avehtari.github.io/modelselection/CV-FAQ.html), online version consulted 16 September 2026, §§3, 5 and 7–11. Adopt its separation of the prediction task, partition and loss in :4.2/:4.5, and its treatment of selection-induced bias. The closest task-matching split is a useful starting point, not an unconditional optimum: alternative partitions can trade bias for variance. Held-out performance can compare predictions without identifying the component that needs revision.

**Serious alternatives on the same question.** In :5.1, optimizing and checking the pooled fit costs less and answers the expected-total question. It fails to expose the conditional discrepancy relevant to forecasting an A message. A held-out log-score comparison of the two fixed forecasts supplies useful performance evidence on the supplied assessment portion, but the score alone does not explain what relation to change. The chosen construction adds the route contrast and a conditional reference, then compares the explicit repair on that same predictive question. It costs an additional fitted probability and leaves uncertainty and regime transfer unresolved; it is not superior for a target already supplied by the pooled expectation.

Reopen the choice when the target becomes a new group, a different horizon, a tail or an intervention; when dependence or selection changes; or when the error requirement makes an approximate comparison insufficient. A more elaborate model or checking scheme earns its place through the new question, not through its recency.


## MMP.14:End {#end}
