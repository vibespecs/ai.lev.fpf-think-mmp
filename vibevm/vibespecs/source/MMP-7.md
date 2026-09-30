# MMP.7 - Construct a Probability Model of the Recorded Data: depth {#depth}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Depth sections of the pattern; the working sections are in the contract document of the same id. See LICENSE.md for the list of changes.

## MMP.7:5 - Archetypal Grounding {#archetypal-grounding}

### MMP.7:5.1 - Infer a success rate from a selectively submitted log {#infer-a-success-rate-from-a-selectively-submitted-log}

A team asks what fraction of attempts succeed. In a proposed model, each attempt succeeds with probability p. Every success is logged; each failure is logged independently with probability 1/4. Initially the team has a fixed-size sample of independently drawn log entries, with no information about how many attempts produced the source log.

The event variable Y is success or failure. The recording flag R says whether the attempt enters the log. Their joint probabilities are:

| Outcome | Probability |
| --- | --- |
| Success, logged | p |
| Failure, logged | (1-p)/4 |
| Failure, unlogged | 3(1-p)/4 |

The included-case success probability is `q = p / [p + (1-p)/4] = 4p/(1+3p)`. If the observed fraction of successes is 1/2, the likelihood estimate of q is 1/2, and transforming it gives `p_hat = q_hat/(4-3q_hat) = 1/5`. Sampling uncertainty remains; this calculation corrects which rate is being estimated.

The first useful result is the distinction between a 50% rate among reports and the estimated 20% rate among attempts under the supplied reporting assumptions. If the failure-reporting probability is unknown, several combinations of that probability and p can produce the same q. The log alone then leaves the population rate unresolved.

Now the procedure changes: a register names a fixed cohort of N attempts and links each submitted report to its attempt. Model those attempts as independent, each with the same success probability p, retaining the stated reporting rule. Since every success is reported, an unreported attempt is a failure. If there are k success reports, the likelihood for p is proportional to `p^k (1-p)^(N-k)`; the failure-reporting factors do not depend on p. The estimate becomes k/N. Conditioning only on reported entries would throw away information the revised procedure provides.

This is a change in the team's observing method. ME can describe the linked-attempt register and responsibility for recording it. Whether to introduce it depends on what resolving the population rate would change in the team's work.

### MMP.7:5.2 - Preserve a common influence across readings {#preserve-a-common-influence-across-readings}

Two sensors measure quantities x1 and x2 with one shared calibration offset b. Their readings are `Y1=x1+b+E1` and `Y2=x2+b+E2`, with independent zero-mean errors of variance sigma squared. Begin by retaining b as a common parameter. The joint conditional density factors given b; each factor uses that same value.

For the difference, `Y1-Y2=x1-x2+E1-E2`: the offset cancels. Its error variance is `2 sigma^2`. A measurement of the difference can therefore be useful while either absolute value remains uncertain.

For repeated measurements of one x, suppose an additional justified model describes the common offset as a zero-mean random variable B with variance tau squared, independent of the errors. The average of n readings has variance `tau^2 + sigma^2/n`. Integrating a separate offset for every reading would incorrectly produce `(tau^2+sigma^2)/n`. Repetition reduces independent noise but leaves this common calibration contribution.

If the instrument is independently recalibrated before every reading, the arrangement changes. A separate-offset model can then be appropriate. The governing operation is to trace which influences are shared and preserve that sharing in the probability construction.

### MMP.7:5.3 - Use a timed-out trial as an interval report {#use-a-timed-out-trial-as-an-interval-report}

A test asks how long an event takes. Each independent trial is observed until its event or a fixed timeout c. Record both `V=min(T,c)` and a flag D indicating whether the event occurred before timeout. As an illustrative subject assumption, let T have exponential density `lambda exp(-lambda t)` for t at least zero, with lambda positive.

An event at time t before c contributes the density `lambda exp(-lambda t)`. A timeout contributes `P(T>=c)=exp(-lambda c)`, obtained by integrating the density over the unobserved tail. For m completed trials and total observed time S, including the timeout durations, the likelihood is proportional to `lambda^m exp(-lambda S)`.

With completions at times 1 and 2 and one timeout at 4, `S=7` and `m=2`. Maximizing this illustrative likelihood gives `lambda_hat=2/7`. Treating the timeout as a third event instead gives 3/7; dropping it gives 2/3. The flag determines which operation is correct.

If only completed trials enter a database and neither the number nor identities of timed-out trials are available, the observed-time density instead conditions on completion: divide the event density by `1-exp(-lambda c)` on the interval before c. A changed recording rule changes the model even when the stored times look the same. The exponential assumption is dispensable: a different duration law supplies its own event density and tail probability.

## MMP.7:6 - Bias-Annotation {#bias-annotation}

The visible dataset invites treating its rows as the whole observation procedure. Begin from how a row, absence or interval report is produced. A second temptation is to add one independent error to every row; trace shared influences before factorizing. More detailed modeling can also conceal missing knowledge, so retain uncertainty in the recording mechanism when the available information does not determine it.

## MMP.7:8 - Common Anti-Patterns and How to Avoid Them {#common-anti-patterns-and-how-to-avoid-them}

| Failure in this work | Repair |
| --- | --- |
| Reported-case frequency is substituted for population frequency despite selective reporting. | Derive the included-case law and the relation to the target rate. |
| An interval report is replaced by an event at its endpoint. | Sum or integrate the joint subject-and-recording law over the underlying values that can produce the report. |
| A common influence is independently removed from every observation. | Keep it in the joint law before elimination. |
| A likelihood is read as a probability distribution over the unknown parameter. | Supply the inferential method that turns it into the requested result. |
| A fitted model is trusted because its simulator reproduces its own assumptions. | Separate computational agreement from the subject comparison needed for the use. |

## MMP.7:10 - Architectural Rationale {#architectural-rationale}

The observation procedure connects the subject to the data used in inference. Keeping that connection explicit makes deterministic coarsening, random selection and shared uncertainty instances of one construction. It also separates modeling choices from the later choice of an inference algorithm.

The factors are chosen for the procedure and question. Their order as a probability factorization does not establish a causal direction in the represented world. Several factorizations can describe one joint law; the subject account and intervention question determine any causal interpretation.

This method uses C.16's measurement and resolvability work while supplying the probability operations those patterns leave to statistical modeling. Its examples require different transformations: conditioning after selection, joint elimination and tail integration. The transferable operation survives replacing the logged activity, sensor or timed event.

## MMP.7:11 - SoTA-Echoing {#sota-echoing}

[Gelman, Vehtari and McElreath, Statistical Workflow (2025), sections 1.1-1.7](https://sites.stat.columbia.edu/gelman/research/published/Statistical_Workflow_article.pdf), emphasize measurement, assumptions, shared information and the distinction between model parameters and inferential targets. Adopt the connection of those decisions to model construction and revision. Their comparison of Bayesian and other workflows supports leaving the inference method explicit; it does not select one estimator for every observation law.

[Rubin, Inference and missing data (1976)](https://doi.org/10.1093/biomet/63.3.581), is a historical foundation for specifying when a missing-data mechanism can be ignored. Adopt the requirement to establish the applicable conditions rather than assuming that absence is harmless. Its qualifications depend on the inferential method. The examples here derive their recording laws directly and require no blanket ignorability claim.

The [Stan User's Guide 2.39 treatment of truncation and censoring](https://mc-stan.org/docs/stan-users-guide/truncation-censoring.html) provides executable constructions for restricted observations and tail reports. Adapt those probability operations to :4.3 and :5.3. The guide's programming and inference conventions are useful implementations, not prerequisites of the method. A direct finite calculation or another suitable implementation can supply the same law.

The three demonstrations are elementary constructions for this pattern. They explain the modeling operations under stated assumptions; they are not empirical reports about the activities or devices used as examples.


## MMP.7:End {#end}
