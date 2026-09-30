# MMP.15 - Identify an Intervention Effect from Available Data {#root}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Working sections of the pattern; its depth sections live in the source document named by the last line. See LICENSE.md for the list of changes.

> **Type:** Method pattern
> **Status:** Usable, evolving
> **Normativity:** Normative within the stated use

## MMP.15:1 - Problem frame {#problem-frame}

**Use this when** the work asks what changing an action, operating condition or working method would do, and available observations or experiments might already determine the answer. A fitted association, even a precise one, does not by itself say what would happen under that change. Start by writing the intervention and the quantity needed, then ask which available probability laws and causal assumptions can determine it.

The practical gain is an expression that can be estimated from the available records, a useful bound, or an explanation of the remaining ambiguity. Identification can spare an unnecessary experiment or prevent an unsupported intervention claim.

This is a method of mathematical modeling within causal reasoning. It constructs the connection from available laws to an intervention target. C.28.MR supplies the meaning and consequences of replacing a mechanism in a given causal model; here the model's relevant mechanisms may remain unknown. Subject methods must justify what the intervention changes, which influences may be shared, and which relations remain applicable. The method applies to physical, biological and computational systems and to human or AI working methods.

Preparation requires conditional probability, expectation and the ability to follow a mathematical argument about assumed causal relations. For graphical derivations, the practitioner or an available specialist must be able to check which paths remain open under conditioning and intervention. A specialist contribution must return the target, assumptions, required observable quantities and derivation or obstruction; a software answer alone is insufficient.

Do not reconstruct identification when an applicable result already answers the unchanged question. Use MMP.13 for estimation under an already identified expression, and C.28.MR for a consequence inside a fully supplied causal model. Design another experiment only when the existing result is insufficient and further evidence is worth obtaining. For a question about the same observed case under another action, or a joint or nested comparison of its responses, MMP.19 constructs the common-case relation and determines what the available information fixes.

## MMP.15:2 - Problem {#problem}

Several causal models can produce the same observable distribution and different intervention consequences. Selection adds another limitation: an experiment can identify an effect among its participants without identifying the effect in the receiving population.

The task is to determine whether the requested causal quantity follows from the available laws and stated assumptions. Failure to find an adjustment set is not failure of identification. Fitting, choosing a prior or simulating one compatible mechanism does not prove that all compatible models give the same answer.

## MMP.15:3 - Forces {#forces}

- **The requested effect versus an unnecessarily complete model.** An average contrast may be determined while individual responses or the full intervention distribution remain unknown.
- **Usable assumptions versus attractive fit.** Temporal ordering, excluded pathways and invariance across populations carry causal meaning that goodness of fit cannot supply.
- **Available information versus convenient information.** Separate experimental, selected and population laws cannot be treated as one complete joint distribution without a derivation.
- **Simple sufficient construction versus broader search.** Adjustment is often enough. Mediated identification or a general identification algorithm can succeed where adjustment does not, at the cost of additional structural reasoning.
- **A conditional answer versus another investigation.** An explicit bound or assumption-dependent result may already suffice. New observations must answer an unresolved consequential question.

## MMP.15:4 - Solution {#solution}

Define the target, recover the available laws and describe the admitted causal models. Derive a common expression for their intervention consequence, or demonstrate how they disagree. Limit the returned conclusion to what that argument establishes.

### MMP.15:4.1 - Specify the causal quantity and what counts as the same intervention {#specify-the-causal-quantity-and-what-counts-as-the-same}

For an action level \(a\), let \(Y(a)\) denote the outcome under the specified intervention setting the action to \(a\). For a target population \(T\), a common request is

\[
\mu_a=E_T[Y(a)], \qquad \Delta=\mu_1-\mu_0.
\]

Define the action, comparator, outcome, population and time horizon far enough to distinguish the actual question. A contrast of average outcomes differs from the chance that a particular unit would benefit. Identifying both marginal laws of \(Y(1)\) and \(Y(0)\) does not ordinarily identify their joint law or the distribution of individual differences.

Establish consistency: for a unit actually receiving the specified version of action \(a\), its observed outcome agrees with \(Y(a)\). Different doses, implementations or accompanying actions may give the same label different meanings. If one unit's outcome depends on other units' actions, represent the relevant joint assignment or policy; the notation \(Y(a)\) must not silently discard that dependence.

For static interventions, \(P(Y\mid do(A=a))\) denotes the corresponding intervention law. C.28.MR defines the change of mechanism that gives this notation its meaning. Identification below seeks that law or its required function without assuming all the changed model's numerical mechanisms are already known.

### MMP.15:4.2 - Recover the available laws and the admissible causal models {#recover-the-available-laws-and-the-admissible-causal-models}

Use MMP.7 to recover how records arise. With inclusion indicator \(S\), selected records supply a law such as \(P(A,Y,L\mid S=1)\), not automatically \(P(A,Y,L)\). Keep assignment, actual action, measurement and inclusion distinct when those distinctions affect the target. State which variables were jointly observed, which interventions were performed, and which population each source concerns.

For identification, provisionally treat these population laws as known. This asks what unlimited data of those kinds could determine. MMP.13 handles finite-sample estimation.

Describe the admitted causal relations. An acyclic causal graph is a useful representation: directed arrows allow direct causal influence, and a shared unobserved cause can be represented explicitly or by a bidirected edge. The absence of an arrow excludes a possible influence relative to the represented variables. A good observational fit does not justify that exclusion. Time-indexed variables can express feedback across time; a theorem for acyclic graphs must not be applied unchanged to an equilibrium model with unresolved cycles.

The operative identification test is this: whenever two admitted causal models induce the same available laws, must they give the same requested quantity? If the assumptions themselves conflict with the available laws, return that conflict rather than declaring a result identified through an empty model class.

### MMP.15:4.3 - Derive an expression, using the simplest sufficient route {#derive-an-expression-using-the-simplest-sufficient-route}

Begin with a relation that replaces an unobserved intervention quantity by available quantities under an explicit assumption. Then combine it with ordinary conditioning, multiplication and averaging. Every final factor must come from an available law or an earlier justified step. Displayed sums concern discrete variables; for continuous or mixed variables, average against their actual probability laws.

For example, let \(L\) be measured before action. For a mean effect in the same population as the data, suppose that within each relevant \(L=l\), action assignment does not select a different mean potential outcome:

\[
E[Y(a)\mid L=l]=E[Y(a)\mid A=a,L=l].
\]

This mean exchangeability assumption, consistency and positive probability of each required action in the relevant strata give

\[
\mu_a
=\sum_l E[Y(a)\mid L=l]P(L=l)
=\sum_l E[Y\mid A=a,L=l]P(L=l).
\]

The first equality averages over the target strata. The second uses exchangeability to compare the same potential outcome, then consistency to replace it by an observed outcome. Average both actions with the same target weights. The different distributions \(P(L\mid A=a)\) generally answer an association question instead.

A common graphical justification is the back-door criterion: choose pretreatment variables that block every path into \(A\) capable of linking it to \(Y\) through other causes. In checking a path, conditioning on an intermediate non-collider blocks it; a collider, where two arrowheads meet, blocks it unless that collider or a descendant is conditioned on. Thus adding every available covariate can open a path rather than remove bias. This criterion is sufficient, not the only way to justify adjustment or identify an effect.

When adjustment of \(A\)'s effect is unavailable, derive other observable intermediate quantities. In a simple front-door construction, a measured mediator \(M\) carries every directed path from \(A\) to \(Y\); \(A\) to \(M\) has no open back-door path; and conditioning on \(A\) blocks all back-door paths from \(M\) to \(Y\). Under these conditions and the required support,

\[
P(Y=y\mid do(A=a))
=\sum_m P(M=m\mid A=a)
   \sum_{a'} P(Y=y\mid M=m,A=a')P(A=a').
\]

The outer factor identifies the effect of action on the mediator. The inner adjustment identifies the outcome law under intervention on the mediator. The pathway restrictions license combining them for the action's total effect. Merely including a post-action measurement in a regression does not perform this construction. These classical conditions are sufficient; their failure does not establish that this functional or another identifying expression is impossible. [Front-door criteria and their extension](https://arxiv.org/html/2604.15288v1), §§2.1.5–3.

For a more involved graph or several input laws, derive a sequence of intermediate distributions using the rules of do-calculus and probability. Each exchange between observation and intervention needs the corresponding separation condition in the modified graph. A suitable identification implementation can carry out that search: provide the graph, the target and the actual input laws, then recover the returned derivation and check its required factors. The historical ID algorithm covers a specified acyclic model class with latent common causes and an observed joint law; generalized search can use several incomplete or experimental laws. Do not replace those inputs by a joint law that the records never supplied. [ID algorithm](https://ftp.cs.ucla.edu/pub/stat_ser/r327.pdf), Figure 3; [generalized search](https://arxiv.org/html/1902.01073v5), §§2–3.

### MMP.15:4.4 - Carry selection, transport and support through the expression {#carry-selection-transport-and-support-through-the-expression}

Identify which population supplies every average. For example, an experiment in \(S=1\) may supply action-specific outcome means by pretreatment \(L\), while an existing inventory supplies the target distribution \(P_T(L)\). If the intervention has the same meaning, assignment in the experiment is exchangeable, and the conditional potential-outcome means agree between the experimental and target populations, then

\[
\mu_a=\sum_l E[Y\mid A=a,L=l,S=1]P_T(L=l).
\]

This is a transport assumption followed by trial identification and target averaging. It requires trial coverage and both action levels wherever the target gives relevant weight. Equal variable names, similar marginal distributions, or randomization within the experiment do not establish the transport assumption. Selection after action or outcome requires its own recording and causal argument; it cannot automatically use this pretreatment bridge. [Generalizing trial results](https://arxiv.org/html/1709.04589v2), §§3–4.

Inspect the support needed by the chosen expression. Positivity means that a required conditional law is defined on the relevant target support; in the discrete adjustment example, \(P(A=a\mid L=l)>0\) whenever the target weights that stratum. For continuous variables, use the corresponding support condition. A fixed intervention value in a continuous action space may also need a continuity or other structural restriction: the observed law determines conditional responses only almost everywhere. An empty cell in a small sample does not prove a population probability is zero. A known structural exclusion is different: the missing conditional response cannot be learned there from that source.

Failure of support invalidates that expression at the excluded values. Another source, another identifying argument or an explicit structural restriction may still answer the question. Extrapolation through a response model can produce an assumption-dependent answer, but fitting or regularizing that model does not create observations at the missing support.

### MMP.15:4.5 - Distinguish a proof of ambiguity from an unfinished search {#distinguish-a-proof-of-ambiguity-from-an-unfinished-search}

To demonstrate nonidentifiability, construct two causal models satisfying the stated assumptions, reproducing all the available laws, and giving different values of the requested target. C.28.MR can calculate each model's intervention consequence. Show both the observational agreement and the difference after intervention, as in :5.2.

A complete identification algorithm can also return an obstruction; check its class and query. A time limit or exhausted search without an applicable completeness result leaves the derivation unresolved. Failure to identify a full intervention distribution also does not by itself prove failure to identify a particular mean or contrast. [ID completeness](https://ftp.cs.ucla.edu/pub/stat_ser/r327.pdf); [scope of search completeness](https://arxiv.org/html/1902.01073v5), §3.4.

When a point is not identified, use the assumptions to bound the requested quantity. Optimize it over compatible models, or derive an inequality valid for all of them. One compatible example establishes possibility; it does not establish a bound. If a bound is claimed sharp, show that compatible models attain or approach its endpoints. A bound that already settles the receiving question needs no complete reconstruction of unknown mechanisms.

A prior or added restriction may select among compatible answers; retain that dependence. It is not new evidence.

### MMP.15:4.6 - Return the sufficient result and propagate consequential changes {#return-the-sufficient-result-and-propagate-consequential-changes}

Return the target and the assumptions under which its identifying expression, bound or ambiguity result holds. Make the data factors recoverable for estimation and uncertainty under MMP.13. Numerical evaluation belongs to an appropriate computational method; a completed optimization or simulation is not an identification proof.

Check the derivation as needed: verify a finite case, inspect a disputed graph condition, or calculate a countermodel's observational and intervention laws. These checks establish the mathematical consequence of assumptions. Assurance that the assumptions describe the subject requires relevant subject evidence; successful fitting or self-consistent simulation does not provide it by itself.

When an actual change admits a direct pathway, changes an intervention's version, alters selection, or changes the target population, propagate it through the affected derivation and calculation. Compare an alternative assumption when that comparison can change the intended use. Do not invent a sensitivity exercise for an already sufficient result under unchanged conditions.

C.11.DUA selects whether remaining uncertainty warrants more evidence, an explicitly conditional answer, a narrower agreed question or no further work. MMP.16 can design an observation if that further work is chosen. A mathematical identification result does not authorize or physically carry out the intervention.

## MMP.15:7 - Conformance Checklist {#conformance-checklist}

- The intervention, comparator and receiving quantity are defined, with consistency and interference handled where relevant.
- The derivation uses the laws actually supplied by the recording and selection procedures.
- Every causal substitution has an assumption or applicable graphical argument; every final data factor is available on its required support.
- A nonidentifiability claim has a target-matched witness or applicable complete-method obstruction. An unfinished search is reported separately.
- A returned bound is justified for all compatible cases; sharpness is claimed only with an attainability argument.
- Estimation uncertainty, causal assumption dependence and computational approximation retain their different meanings.
- Actual consequential changes are propagated. A sufficient existing result does not trigger an obligatory new study.

These conditions recognize a constructed identification result. They do not establish the subject truth of its causal assumptions or authorize an intervention.

## MMP.15:9 - Consequences {#consequences}

Estimation concentrates on the required observable quantities. Nonidentifiability becomes an explicit limitation of assumptions and information, not an unexplained numerical failure.

The causal argument may demand subject knowledge unavailable in the dataset. More elaborate identification does not strengthen an unjustified premise. A conditional answer or bound can be useful without recovering every mechanism.

In methodology, this changes how a proposed improvement to a working method is assessed. Define the method change and relevant outcome, recover how cases and results were recorded, and distinguish its effect from differences in which cases received it. The same reasoning can govern a human procedure, an automated procedure or their combination, without making a population experiment mandatory for every use of the method.

## MMP.15:12 - Relations {#relations}

- **C.28** supplies the causal-use question and the distinction between identification, estimation and realizability. **C.28.MR** supplies intervention semantics and calculations within a specified causal model.
- **C.16.IR** supplies compatible-case and sufficient-target reasoning; this pattern constructs the causal identification expressions and ambiguity witnesses.
- **MMP.7** supplies the observation law, including selection and missingness. **MMP.11** supplies an explicit model family when its restrictions are needed.
- **MMP.12** handles inverse ambiguity and justified regularization. A restriction used here remains an added causal or response assumption, not new evidence.
- **MMP.13** constructs inference for the identified expression or explicitly assumption-dependent target. **MMP.14** investigates failed model predictions; observational checks alone need not distinguish observationally equivalent causal models.
- **MMP.19** constructs and bounds history-conditioned, joint and nested counterfactual comparisons; an intervention mean can remain sufficient for a choice based on expected outcome.
- **MMP.16** addresses a chosen need for additional observation design. **C.11.DUA** governs whether that work is worthwhile.
- **Computational Thinking**, including **CMP.8/CMP.9** where their numerical methods apply, obtains numerical values without supplying the missing causal argument. Subject methods justify and realize the intervention and the asserted invariances.


## Dependencies {#dependencies}

- @fact:DEPENDS-ON Dependencies (as published): spec://ai.lev/fpf-spec/contract/C-28-MR#root for intervention meaning; spec://ai.lev/fpf-think-mmp/contract/MMP-7#root/.13 for recording and estimation; spec://ai.lev/fpf-spec/contract/C-16-IR#root for compatible possibilities; spec://ai.lev/fpf-think-mmp/contract/MMP-16#root for worthwhile distinguishing observations. @status:spec/done
- @fact:REFERENCED-BY Referenced by (computed from the Tables of Contents): spec://ai.lev/fpf-eng-mkt/contract/MKT-10#root, spec://ai.lev/fpf-think-mmp/contract/MMP-19#root @status:spec/done

#source spec://ai.lev/fpf-think-mmp/source/MMP-15
