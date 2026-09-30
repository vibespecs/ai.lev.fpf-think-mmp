# MMP.13 - Infer Unknowns Statistically under a Stated Observation Model: depth {#depth}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Depth sections of the pattern; the working sections are in the contract document of the same id. See LICENSE.md for the list of changes.

## MMP.13:5 - Archetypal Grounding {#archetypal-grounding}

### MMP.13:5.1 - Zero recorded failures: two different uncertainty claims {#zero-recorded-failures-two-different-uncertainty-claims}

A device is tested for a fixed four operations. All failures are recorded, and the supplied model gives independent Bernoulli outcomes with one unchanged failure probability p. No failures occur, so K=0 and the likelihood is proportional to (1-p)^4.

Suppose the requested target is the probability of at least one failure in two further operations under the same condition:

`q=1-(1-p)^2.`

The future operations are assumed independent conditional on the same p. The question concerns q, rather than every detail of an operating model.

**Frequentist construction.** The likelihood estimate is p_hat=K/4=0. Inserting it into the familiar normal standard-error expression gives zero estimated standard error and the interval [0,0]. At p=0.2, zero failures occur with probability 0.8^4=0.4096, and [0,0] excludes the true p on every such occurrence. This alone rules out 95% coverage.

For a one-sided 95% binomial upper confidence procedure, invert the lower-tail probability: for k<4 choose U(k) satisfying

`P_(p=U(k))(K<=k)=0.05,`

and set U(4)=1. Binomial test inversion gives coverage at least 95%, allowing conservatism from discreteness. At k=0,

`(1-U)^4=0.05; U=1-0.05^(1/4)=0.5271.`

Since q increases with p, its upper confidence limit is

`1-(1-U)^2=1-sqrt(0.05)=0.7764.`

This is the result of a covering procedure, not a statement that q has a 95% probability of being below 0.7764 after these records.

**Bayesian construction.** Choose a uniform prior for p on [0,1]. Multiplying and normalizing gives posterior density

`pi(p|K=0)=5*(1-p)^4; 0<=p<=1.`

Thus E[p|K=0]=1/6, and the posterior 95% upper quantile of p is `1-0.05^(1/5)=0.4507`. Transforming that quantile gives a posterior 95% upper quantile of q of `1-0.05^(2/5)=0.6983`. Its smaller value does not make it a uniformly better confidence limit; it expresses a different conditional claim with a prior.

To obtain the probability of a failure in the next pair, average q itself:

`E[q|K=0] = 1 - integral_0^1 (1-p)^2*5*(1-p)^4 dp = 2/7.`

Using the posterior mean of p first would give `1-(5/6)^2=11/36`, a different value. The posterior predictive probability is 2/7; the event of a failure in that pair remains a binary future outcome.

**Changed assumption.** Hold the four records fixed but replace the uniform prior with density `9*(1-p)^8`, favoring lower failure probabilities. The posterior becomes `13*(1-p)^12`. The posterior probability of p<0.2 changes from `1-0.8^5=0.67232` to `1-0.8^13=0.94502`; the predictive probability for a failure in the next pair becomes 2/15.

These changes come entirely from the prior. They neither add operations to the observed test nor establish that the new prior is appropriate. If its relevance is unresolved, return the conditional results and their difference. The frequentist bound remains available without that prior under the original fixed-sample observation model.

### MMP.13:5.2 - A common calibration error survives averaging {#a-common-calibration-error-survives-averaging}

Four readings in fixed units are 9, 10, 10 and 11, giving mean 10. Initially suppose

`Y_i=mu+epsilon_i; epsilon_i independently Normal(0,1).`

The noise variance 1 is supplied, not estimated from these four values. The sample mean is an estimator of mu with variance 1/4. An exact normal 95% confidence procedure uses `mean(Y) +/- c/2`, where c is the 0.975 standard-normal quantile, approximately 1.96. The realized interval is approximately [9.020,10.980].

A prediction interval for one independent future reading uses the error `Y_new-mean(Y)`, whose variance is `1+1/4`. Its realized 95% interval is approximately [7.809,12.191]. Uncertainty about the mean and variation of the future reading require different intervals even before any model revision.

Now revise the calibration account:

`Y_i=mu+B+epsilon_i; B~Normal(0,1).`

B is independent of the individual errors, shared by all readings in one setup, and drawn afresh across the repeated setups used to define the coverage claim. Then

`Var(mean(Y))=1+1/4.`

The confidence interval for mu widens to [7.809,12.191]. Treating B as a fresh independent error on each row would instead give variance 2/4 and understate the uncertainty. More readings in this same setup reduce the individual-noise term but leave the calibration term.

Prediction also depends on what stays shared. A new reading in the same setup has the same B, which cancels in `Y_new-mean(Y)`; the prediction-error variance remains 1+1/4. A reading in a new setup with independent B_new has variance `1+1+1+1/4=3.25` for that error, giving approximately [6.467,13.533].

These are coverage statements over the stated repeated-observation law. If B is only an unknown fixed offset with no bound or probability law, these normal intervals for mu do not follow. MMP.12 then retains the unresolved separation of mu and B; assigning B a distribution is an additional modeling contribution.

### MMP.13:5.3 - Infer the rate for the receiving workload {#infer-the-rate-for-the-receiving-workload}

Two classes of requests have different probabilities of finishing by a deadline. For class A, seven of eight observed requests finish; for class B, one of eight finishes. Assume fixed sample counts, independent Bernoulli outcomes within each class, independent class data, and independent uniform priors for p_A and p_B.

The posterior densities are proportional to `p_A^7*(1-p_A)` and `p_B*(1-p_B)^7`: Beta(8,2) and Beta(2,8). Their means are 0.8 and 0.2, and each variance is 4/275. The posteriors are independent under the stated construction.

For a future workload selecting the two classes equally, the conditional completion probability is `q_old=(p_A+p_B)/2`, with posterior mean 0.5. Now change only the receiving workload: its known class proportions are one-quarter A and three-quarters B. The target becomes

`q_new=p_A/4+3*p_B/4.`

Its posterior mean is 0.35 and its posterior variance is

`(1/4)^2*(4/275)+(3/4)^2*(4/275)=1/110.`

No new fitting is needed for this changed target. Carrying forward 0.5 would answer for the old mixture. If the target were an individual future completion indicator, its posterior predictive probability would be 0.35 and its variance 0.35*0.65, rather than 1/110.

The transfer assumes that the within-class probabilities remain applicable. Changed operating conditions require their own relation. Uncertain class proportions or a shared influence on the two probabilities require joint uncertainty, rather than the independent weighted-variance calculation above.

## MMP.13:6 - Bias-Annotation {#bias-annotation}

The worked laws are simple enough for exact calculations. Real records can have selection, dependence, weak identification or model mismatch that a convenient binomial or normal family conceals. The resulting uncertainty is conditional on the assumptions represented; it does not automatically include an omitted mechanism.

Bayesian and frequentist results are compared by the conclusions they support. A narrower interval alone cannot rank different probability meanings. The choice of prior, coverage domain and receiving target is part of the inference, even when software supplies defaults.

## MMP.13:8 - Common Anti-Patterns and How to Avoid Them {#common-anti-patterns-and-how-to-avoid-them}

| Failure | Repair |
| --- | --- |
| A confidence interval is read as posterior probability for the observed interval. | State which object varies under the probability law and which claim the construction supports. |
| A likelihood curve or penalized optimum is treated as a posterior distribution. | Supply and normalize the prior-likelihood construction before using posterior probabilities. |
| A derived result is computed only from parameter means or separate standard errors. | Transform the joint inference; retain nonlinear effects and covariance. |
| More readings are assumed to remove a shared uncertainty. | Derive the variance under the actual dependence, as in :5.2. |
| Smaller Monte Carlo error is reported as less subject uncertainty. | Qualify the computed summary separately from the distribution it summarizes. |
| The prior or fitted model is changed without recalculating the receiving conclusion. | Carry the revised assumption through the target and uncertainty calculation. |

## MMP.13:10 - Architectural Rationale {#architectural-rationale}

The observation model describes how records vary. The inferential construction determines how those records support conclusions about unknowns. Target propagation determines which consequence reaches the receiving use. Their separation permits a computation to be correct while its prior, target or observation assumption is still reconsidered.

This preserves the distinction from inverse-problem regularization, numerical computation, causal identification, model criticism and decision making. Those methods supply or receive particular contributions; none is obtained merely by fitting a statistical model.

## MMP.13:11 - SoTA-Echoing {#sota-echoing}

**Carrying fitting into the required conclusion.** **Adopt** target-specific propagation of joint uncertainty rather than reporting a coefficient table or substituting parameter means. [Gelman, Vehtari and McElreath, *Statistical Workflow*, §§1.3–1.6 and 1.10, author manuscript dated 5 December 2025 for the 2026 article](https://sites.stat.columbia.edu/gelman/research/published/Statistical_Workflow_article.pdf) explains how dependencies, derived quantities and calibration affect both Bayesian and non-Bayesian workflows. This changes :4.1 and :4.5–4.6. In :5.1 and :5.3 the extra calculation is small and corrects the actual requested probability or workload target. The source does not rank one inferential philosophy above the other, nor validate a particular subject model. Reopen when another construction gives the same target meaning and uncertainty at lower effort, or when changed dependencies defeat the propagation.

**Uncertainty near a parameter boundary.** The serious default is the normal standard-error interval, which collapses in :5.1. **Adopt** binomial tail inversion when its fixed-sample coverage is the requirement; **retain** a posterior alternative when its prior-conditional probability is wanted. [NIST/SEMATECH e-Handbook, §7.2.4.1](https://www.itl.nist.gov/div898/handbook/prc/section2/prc241.htm) supplies the explicit comparator and small-sample construction. The few tail calculations cost little here and repair the degenerate result; discreteness can make coverage conservative. A posterior requires the additional prior and can change materially with it. This comparison governs :4.3–4.4 and :5.1, not a universal preference for exact intervals. Reopen for a changed sampling law or a justified approximation that meets the same coverage need more efficiently.

**Inference when observations determine stopping.** **Adapt** simultaneous coverage as a conditional alternative to fixed-time intervals in :4.3. [Howard et al., *Time-uniform, nonparametric, nonasymptotic confidence sequences*, §1 and equation (1), arXiv:1810.08240v9](https://arxiv.org/html/1810.08240v9) supplies the stronger guarantee and its cost in interval width. Its stated stochastic conditions still apply. A fixed-time method remains sufficient for its own observation plan; sequential machinery is unnecessary there. Reopen when the actual stopping rule changes or a narrower valid construction improves the needed inference at comparable effort.


## MMP.13:End {#end}
