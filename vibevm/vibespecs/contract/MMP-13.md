# MMP.13 - Infer Unknowns Statistically under a Stated Observation Model {#root}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Working sections of the pattern; its depth sections live in the source document named by the last line. See LICENSE.md for the list of changes.

> **Type:** Method pattern
> **Status:** Usable, evolving
> **Normativity:** Normative within the stated use

## MMP.13:1 - Problem frame {#problem-frame}

Use this pattern when a probability model describes how records arise, and the work needs an estimate, an interval or a probability about something not directly known. The wanted quantity may be a failure probability, a mean before measurement error, a response for a different mix of cases, or a future outcome.

Start by writing the sentence the result must support. “This procedure covers the fixed unknown in at least 95% of its modeled repetitions” differs from “the unknown lies here with 95% posterior probability under these assumptions.” A probability about the next observation is another question. Choose the inferential construction that supports the required sentence.

The result is an estimator or posterior and its consequence for the requested target, with an interpretable account of uncertainty. It exposes which assumptions make the conclusion possible and which change would require recalculation. Reporting a fitted coefficient and a number labeled “error” can otherwise leave the actual question unanswered.

This is statistical inference within mathematical modeling. MMP.7 supplies the law of the records; MMP.12 supplies unresolved recovery ambiguities and any regularization choices. The present method constructs what may be concluded under that law and additional inferential assumptions. Selecting an action also needs its consequences and preferences, supplied by a decision method such as MMP.8.

The reader needs conditional probability, expectations and quantiles; continuous models also use integration. A mathematically qualified collaborator can supply those operations when the practitioner can specify the observation process and interpret the target.

Use an existing sufficient inference directly. If a compatible range already settles the question, C.16.IR can end the work without a probability model. A missing observation law returns to MMP.7; constructing a numerical sampler for an already specified posterior belongs to CMP.9.

## MMP.13:2 - Problem {#problem}

The distribution of the observed records does not itself choose an estimator, an uncertainty statement or a prior. Those additions can produce different useful conclusions from the same data.

The inferential target may also differ from the fitted parameters. A nonlinear function of parameter estimates can give a different answer from averaging that function over a posterior. Shared uncertainty can remain after many repeated readings. A narrow interval for an expected response can coexist with a wide distribution for the next response.

The problem is to construct the inference needed by the receiving use while preserving its sampling, conditioning and approximation assumptions. Changing one of those assumptions must change the relevant calculation, rather than only the qualification attached to an unchanged number.

## MMP.13:3 - Forces {#forces}

| Force | Tension |
| --- | --- |
| Target and parameterization | The model can contain many unknowns while the use needs only one function of them. |
| Conditional probability and repeated-use performance | A posterior probability and confidence coverage answer different questions. |
| Convenient defaults and supported assumptions | Independence, a prior or a normal approximation can simplify the calculation while changing its meaning. |
| Joint uncertainty and simple summaries | Separate standard errors can lose covariance needed by the target. |
| Inferential precision and computational precision | More accurate integration can leave the subject uncertainty unchanged. |

## MMP.13:4 - Solution {#solution}

Specify the target and the intended uncertainty claim. Combine the record law with the inferential assumptions needed for that claim, derive the estimator or posterior, and propagate it to the target. Carry any actual consequential revision through the affected calculation. Compare a plausible alternative assumption only when doing so can change the use or returned claim. Return the sufficient result at the scope the calculation supports.

### MMP.13:4.1 - Fix the target before choosing a fitting routine {#fix-the-target-before-choosing-a-fitting-routine}

Write q=g(theta), where theta denotes the unknowns in the observation model. It can index a distribution or unknown function, not just a finite vector. State the population, conditions and time range that make q meaningful. Distinguish unknowns needed only to explain the records from the target being returned.

For prediction, instead name the new outcome Y_new and its observing conditions. A conditional mean of Y_new is a function of theta; the realized Y_new also varies under the model. A proposed intervention requires a supplied causal identification argument before a fitted association can be interpreted as its effect.

Select the smallest result that changes the next use. It may be a point estimate with a stated error property, an upper confidence bound, a posterior probability of a threshold, or a predictive distribution. A threshold action still needs its loss or decision rule; a probability or confidence level does not choose that action by itself.

### MMP.13:4.2 - Recover the law and the assumptions being added {#recover-the-law-and-the-assumptions-being-added}

Take the joint law P_theta of the records Y from MMP.7. Retain its inclusion, censoring, dependence and stopping conditions. Where a common probability-mass or density representation exists, inserting the observed y gives the likelihood L(theta;y)=p_theta(y).

The likelihood compares how parameter values account for the same records. It is not a probability distribution over theta merely because it can be plotted or maximized. Likewise, records in separate rows are not necessarily independent observations.

Use the existing ambiguity result from MMP.12 or C.16.IR. If two parameter values give the same observation law and different q, the records cannot distinguish that target. A prior or restriction may support a conditional answer, whose dependence on that addition remains visible.

Choose the inferential branch by the claim required. Frequentist construction assesses a data-to-answer rule across the specified observation law at fixed unknown values. Bayesian construction adds a prior law and conditions their joint model on the observed records. Neither branch removes the need for a justified observation model.

If the same data choose a model, tuning value or prior hyperparameter, include that adaptation in the inference being claimed. Treating an estimated quantity as externally known can understate uncertainty. A sensitivity comparison can instead hold the data fixed and show the consequence of several explicitly conditional assumptions.

### MMP.13:4.3 - Construct an estimator and its frequentist uncertainty when needed {#construct-an-estimator-and-its-frequentist-uncertainty-when}

An estimator is a rule q_hat=T(Y), chosen before its repeated-use properties are assessed. Derive it from the target and observation law: for example, invert an observable expectation, solve an estimating equation, or maximize a likelihood and obtain the required function of the fitted values. State the selected property, such as a controlled error probability or mean squared error. Likelihood maximization alone supplies no interval.

One general confidence construction chooses, for each admitted theta, an acceptance region A_theta of possible records such that

`P_theta(Y in A_theta) >= 1-alpha.`

After observing y, retain those theta for which y lies in A_theta, and map them through g. The resulting set C(y) has coverage

`P_theta(g(theta) in C(Y)) >= 1-alpha`

under the stated law. A target-specific statistic can make this much cheaper than constructing a set for every nuisance parameter. The binomial inversion in :5.1 is a small example.

Coverage describes the procedure across repetitions allowed by the model, at fixed theta. It does not assign posterior probability to the parameter in the one observed interval. Nor is a confidence set the set of all logically possible values: a value outside it may still assign a small positive probability to these records.

Use an exact distribution or justified pivot when available. An asymptotic approximation needs its sample-size, regularity and boundary conditions. A bootstrap needs a resampling unit and mechanism that represent the dependence and the fitted procedure; resampling individual readings cannot reproduce an omitted common calibration error. Retain approximate coverage as approximate unless a stronger result is available.

The observation plan belongs to the guarantee. An interval justified at a fixed sample size need not preserve its coverage when repeatedly inspected until it looks favorable. Use a method valid for the actual stopping plan. For countably many looks, one conservative construction allocates error probabilities alpha_j with sum at most alpha to valid per-look intervals; the union bound gives simultaneous coverage. An applicable confidence-sequence method can provide a less conservative construction. This is a choice of inferential guarantee, not a requirement to collect more data.

### MMP.13:4.4 - Construct a posterior when conditional probability is needed {#construct-a-posterior-when-conditional-probability-is-needed}

Supply a prior probability law Pi with its subject meaning. Reweight that law by the observed likelihood and normalize, preserving any point masses and continuous parts. For a set A to which the prior assigns a probability,

`Pi_y(A) = integral_A L(theta;y) Pi(dtheta) / integral L(u;y) Pi(du).`

Pi_y denotes the posterior law. Integration against Pi means combining values under the actual prior: a sum for discrete unknowns, integration against a density where one exists, and both contributions for a mixture. A function-valued unknown requires a specified prior law and likelihood on that space, not an assumed ordinary density.

The denominator must be finite and positive; an unnormalized expression alone does not establish a posterior probability law. For a real vector theta whose prior has a density pi(theta) with respect to ordinary volume dtheta, the posterior density is

`pi(theta | y) = L(theta;y)*pi(theta) / integral L(u;y)*pi(u) du.`

This density formula is a representation of the preceding law construction under that condition. A uniform prior depends on the parameterization, and an improper prior requires a separate argument that the posterior exists.

For example, give a failure probability p prior mass 1/2 at p=0 and a uniform distribution on [0,1] for the remaining 1/2. One failure-free Bernoulli observation has likelihood 1-p. The unnormalized atom has mass 1/2; the weighted continuous part has mass 1/4. Normalizing by 3/4 leaves posterior mass 2/3 at zero. The remaining 1/3 has conditional density 2*(1-p) on [0,1]. Using only the ordinary density would lose the atom.

Retain joint dependence when removing nuisance unknowns. Sum or integrate the joint posterior over them, or calculate g(theta) from joint posterior draws. Independently combining draws from marginal distributions changes the joint law unless independence is established.

Derive the posterior of q through that transformation. For a set B,

`P(q in B | y) = integral 1{g(theta) in B} Pi_y(dtheta).`

A credible set has its stated posterior probability under this model and prior. A posterior mean, median or quantile is a chosen summary of that law. In general, `E[g(theta)|y]` differs from `g(E[theta|y])`; :5.1 computes the difference.

A penalized optimum from MMP.12 can coincide with a posterior mode when its objective represents the chosen likelihood and prior. That optimum still does not supply the posterior spread. If a prior resolves an otherwise unidentified difference, preserve that source of the resolution in the returned result.


### MMP.13:4.5 - Propagate uncertainty to the actual receiving quantity {#propagate-uncertainty-to-the-actual-receiving-quantity}

For a posterior predictive result, construct the law of the new observation under its specified conditions and average it over the posterior law:

`P(Y_new in B | y) = integral P(Y_new in B | theta,y) Pi_y(dtheta).`

In the density case of :4.4, Pi_y(dtheta) is pi(theta | y) dtheta. For a mixed posterior, include its atoms as well as its continuous contribution.

This includes both uncertainty in unknowns and the modeled variation of a new outcome. Where variances exist, the decomposition is

`Var(Y_new|y) = E[Var(Y_new|theta,y)|y] + Var(E[Y_new|theta,y]|y).`

The second term alone concerns uncertainty in the conditional mean. It is not the full predictive variance.

A frequentist prediction interval also needs the joint law of the original and future records. Derive a prediction error or another statistic with the needed coverage. Sharing a calibration influence with the old readings and using a fresh calibration produce different prediction problems, as in :5.2.

For a posterior of a real parameter vector theta with covariance V, the linear target q=a^T*theta has posterior variance a^T*V*a. A frequentist covariance calculation instead uses the sampling covariance of the joint estimator, retaining its repeated-use interpretation. For a nonlinear target, propagate the joint posterior or derive uncertainty from the estimator's sampling law; an approximation needs its own conditions. A confidence set for theta can be mapped through g to obtain a confidence set for q; projecting a large joint set can be conservative. A marginal interval for each coordinate does not automatically give simultaneous coverage for a function of them.

Then obtain the numerical answer with the needed accuracy. CMP.8 supplies controlled approximate computation; CMP.9 supplies a sampler or randomized computational estimator. The posterior distribution, a confidence procedure and the algorithm approximating their consequences are different results. More posterior draws can reduce Monte Carlo error in a computed mean while leaving the posterior uncertainty about q unchanged.

### MMP.13:4.6 - Test the claimed consequence and revise the assumption that matters {#test-the-claimed-consequence-and-revise-the-assumption-that}

Check the derivation at the level needed for its use. In a finite model, normalization, enumeration or an exact calculation may suffice. For an approximate frequentist procedure, simulation at fixed parameter values can expose bias or coverage failures under the assumed law. For a posterior computation, a suitable simulation-based calibration check draws parameters and data from their joint model and tests the inference computation. These are different checks. Agreement under a model does not establish that the model describes the subject.

Select such work for an unresolved claim. A routine use of an applicable exact result need not become a new simulation study, and simulated datasets are not additional subject observations.

When a premise or target actually changes, recalculate the affected target and uncertainty; reuse unaffected results. Compare a plausible alternative dependence, prior scale, inclusion probability or target-population weight only when that comparison can change the intended use or returned claim. State whether an altered result comes from changed records, changed assumptions or a changed target, and keep a material disagreement visible. A sufficient inference under unchanged grounds needs no invented alternative.

If observed failures call for a richer model, return the model-criticism and revision question to the relevant subject method and MMP.11. If the desired effect is not causally identified, return that identification question. Designing a new observation is a further choice when the existing result is insufficient; it is not part of every inference.

### MMP.13:4.7 - Return the conclusion at its established meaning {#return-the-conclusion-at-its-established-meaning}

Return the target, the estimate or distribution, the meaning of its uncertainty, and the assumptions whose variation changes its use. Identify a numerical approximation limit separately. Give the receiver enough to distinguish a frequentist coverage claim, a posterior probability and a predictive claim without consulting the fitting software.

Use the sufficient result. C.11.DUA helps compare another observation, a changed formulation, more computation or action with remaining uncertainty when that choice is live. B.5.RR carries a changed premise through the reasoning; MMP.8 receives inference when an actual choice needs its consequences and preferences.

A methodological use can revise how a working method treats uncertainty: retain a shared influence, compute the requested derived quantity, or stop demanding an unidentified parameter when a sufficient consequence is available.

## MMP.13:7 - Conformance Checklist {#conformance-checklist}

- The inferential target and its subject conditions are stated separately from nuisance unknowns and the subsequent decision.
- The observation law retains consequential recording, dependence and stopping assumptions.
- The estimator's repeated-use claim or the posterior's conditioning assumptions are recoverable; normalization or coverage has an applicable basis.
- Joint uncertainty is propagated to the actual target. Parameter uncertainty, future-observation variation and numerical error are distinguished.
- Any actual consequential revision is propagated through the affected target and uncertainty calculation. A sensitivity comparison addresses a live alternative that can change the use or returned claim; an unchanged sufficient inference needs none.
- The returned conclusion is sufficient for its use or names the missing contribution without requiring an automatic new experiment.

## MMP.13:9 - Consequences {#consequences}

The receiver gets an estimate or distribution with a usable meaning for its uncertainty. A needed probability, bound or prediction can be obtained without recovering every parameter, and a changed target can sometimes reuse the existing joint inference.

The method also makes the cost of assumptions visible. Another record, another prior and another numerical approximation change different parts of the answer. A sufficient inference can be used while a stronger claim remains unresolved.

## MMP.13:12 - Relations {#relations}

- **Uses MMP.7** for the law of recorded outcomes and **MMP.11** for the model family when that family needs construction.
- **Uses MMP.12 and C.16.IR** for unresolved recovery distinctions and sufficient target bounds. Adds estimator or posterior construction and the meaning of inferential uncertainty.
- **Uses CMP.8 and CMP.9** to obtain numerical consequences of the selected inference, with computational error separate from inferential uncertainty.
- **Supplies prediction and model criticism** with conditional consequences that can be compared with relevant observations. A causal interpretation additionally needs its identification argument under C.28.
- **Supplies MMP.8** with estimates or distributions used in a decision; **C.11.DUA** compares the value of further information or computation when needed.
- **Uses B.5.RR** to propagate a changed premise. Method Engineering can use the resulting inference when revising how a working method obtains or interprets records.


## Dependencies {#dependencies}

- @fact:DEPENDS-ON Dependencies (as published): spec://ai.lev/fpf-think-mmp/contract/MMP-7#root for the record law; spec://ai.lev/fpf-think-mmp/contract/MMP-12#root/spec://ai.lev/fpf-spec/contract/C-16-IR#root for ambiguity; spec://ai.lev/fpf-think-cmp/contract/CMP-8#root/.9 for numerical computation; spec://ai.lev/fpf-think-mmp/contract/MMP-14#root/.8 for prediction checks and decisions. @status:spec/done
- @fact:REFERENCED-BY Referenced by (computed from the Tables of Contents): spec://ai.lev/fpf-think-mmp/contract/MMP-12#root @status:spec/done

#source spec://ai.lev/fpf-think-mmp/source/MMP-13
