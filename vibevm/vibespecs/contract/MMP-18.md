# MMP.18 - Couple Models with Compatible Exchanges and Scales {#root}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Working sections of the pattern; its depth sections live in the source document named by the last line. See LICENSE.md for the list of changes.

> **Type:** Method pattern
> **Status:** Usable, evolving
> **Normativity:** Normative within the stated use

## MMP.18:1 - Problem frame {#problem-frame}

Use this pattern when the required answer combines models whose shared quantities, representations or scales differ. One model may return an average while another needs a distribution. Two simulations may exchange a flow at different times. Two statistical analyses may reuse the same prior or observations.

Begin at one exchange that affects the answer. Identify what the supplying model returns, what the receiving model uses it to mean, and the relation needed to connect them. A matching variable name or software interface leaves that relation to be constructed.

The result is a joint formulation: component models with their shared quantities, interface relations and the assumptions needed to use their combined answer. It may expose a missing closure, incompatible conditions or a dependency that an available simulator cannot realize. The first useful result can be that obstruction, or a restricted coupled answer sufficient for the work.

This is mathematical coupling across models. A.3.3.TR supplies joint relations and change rules; MMP.10 supplies their constraint formulation. The additional work here constructs exchanges between representations, preserves the quantities the use depends on, and accounts for shared information. Subject methods supply the meaning and applicability of those exchanges.

The reader needs the mathematics used by the components and their connection. Algebra suffices for the first coupling steps; time-dependent, spatial or probabilistic branches require the corresponding integration, mapping or probability knowledge. A collaborator can construct the mathematics from supplied models and a recoverable subject question.

Use an already adequate joint model directly. Merely keeping several alternative models in a portfolio does not require coupling them into one model. Use portfolio and improvement methods when the alternatives serve complementary questions without exchanging modeled quantities or information.

## MMP.18:2 - Problem {#problem}

Locally useful models can give an unusable combination. An exchange may be counted twice or disappear between different time steps. Components may share an unknown while their combined calculation treats its values as independent. An average may conceal a variation needed by a nonlinear response. A sequential software call may insert a delay into relations intended to hold together.

The difficulty is to construct the joint model without silently changing what the components mean or the answer they are meant to support. Compatibility at the interface and adequacy in the subject remain separate questions.

## MMP.18:3 - Forces {#forces}

| Force | Tension |
| --- | --- |
| Reuse and joint meaning | Existing components save work but may describe their common quantity differently. |
| Local accuracy and combined behavior | Accurate component calculations can lose a balance or destabilize feedback through their exchange. |
| Different scales and required detail | A coarse result can omit the variation, timing or dependence another component needs. |
| Separate uncertainty and common information | Independent treatment can count shared evidence twice or remove correlation. |
| One joint solve and separate execution | Separate solvers retain existing tools but introduce exchange approximations and synchronization work. |
| More coupling and sufficient use | Recovering every interaction can cost more than the question warrants. |

## MMP.18:4 - Solution {#solution}

Choose the combined answer. Recover the meaning and conditions of each consequential exchange. Construct interface relations that preserve what the receiving use needs, then impose them with the component models. Obtain and interpret a joint result, distinguishing a formulation defect from an approximation in its computation. Reopen only the exchange or component whose changed assumption affects that result.

### MMP.18:4.1 - Identify what the models share and what they exchange {#identify-what-the-models-share-and-what-they-exchange}

Start from the required result and trace which component supplies each quantity it uses. Recover the quantity's referent, unit and reference point, as well as any time interval, spatial region or probability conditioning that changes its meaning.

Distinguish a shared quantity from a transferred result. If both models describe the same unknown offset, retain one common offset or a justified relation between their coordinates. If one supplies an estimated offset to the other, specify whether the receiving calculation uses its uncertainty or only an approximation by a point value.

Locate overlapping subject effects. If both component laws already include the same interaction, composing them may count it twice. Decide from the subject model which contribution is being retained and which is a second description of it. A.3.3.TR and C.29.BB supply the resulting joint change and balance relations.

Also recover the operating conditions. A component calibrated for one boundary condition may cease to apply when connected to a responsive neighbor. Replacing a supplied input by another model's output can therefore require a changed component law, even when the variable types match.

### MMP.18:4.2 - Construct the interface relation {#construct-the-interface-relation}

Express the exchange as a relation between the component descriptions. A deterministic map is appropriate when the supplied result determines the needed input. Use a broader relation or conditional law when several inputs remain possible.

For a conversion, translate the quantity and its reference point. For an aggregate, state the operation over the specified region or interval. For example, an amount over [t0,t1] is the integral of a rate over that interval; a rate at t0 alone determines that amount only under an additional evolution assumption.

Let x range over values expressed by the supplying model and y over those used by the receiving model. A relation H(x,y) states the compatible pairs. A.3.3.TR supplies composition with other relations, and MMP.10 expresses the joint possibilities. MATH.18 helps determine which operations and consequences the interpretation preserves. Equality of numerical values is one possible relation, not the default.

Derive the property the map must preserve. For amounts at locations, a linear map b=W*a preserves their total for every a when every column of W sums to one. For values of an intensive field, a map preserving a constant field instead has every row sum to one. If amounts must remain nonnegative, nonnegative weights are an additional sufficient condition. The needed property chooses the map; a convenient interpolation routine does not choose the property.

The two conditions solve different problems. A common field value should remain that value on another discretization. The total amount distributed among cells should remain the same total. When both requirements matter, construct a map with the appropriate geometry or integration weights rather than substituting one condition for the other.

### MMP.18:4.3 - Restore what the receiving scale needs {#restore-what-the-receiving-scale-needs}

Apply the receiving operation to the proposed supplied description. If the result still depends on discarded detail, identify that dependency before choosing a closure.

For example, a component supplies only the mean of x over a region, while a neighboring response requires the mean of x^2. The missing contribution is the variance:

~~~
mean(x^2) = mean(x)^2 + variance(x).
~~~

Two fields with the same mean can therefore yield different received responses. Supplying the squared mean silently sets the variance to zero. Retain the needed statistic, obtain it from the finer model, supply a justified closure or return bounds sufficient for the question. MMP.9 derives reduced evolution and closures; MMP.17 constructs a surrogate when that is the chosen supplier.

A time-scale change can create memory. An interval average need not determine a response at an intermediate instant. A rapidly changing component can also leave an accumulated effect after its local state has relaxed. Recover the information needed by the receiving answer instead of assuming that a small or fast component has no relevant contribution.

Use a coupled approximation only within the conditions supporting it. If feedback drives a surrogate or closure into a different regime, revise that contribution or return to a suitable supplier. Good behavior on isolated component inputs does not establish behavior on inputs generated by the coupled system.

### MMP.18:4.4 - Impose the joint conditions before choosing execution order {#impose-the-joint-conditions-before-choosing-execution-order}

Combine the component relations and interface conditions for the same modeled situation. Shared boundary values and initial conditions must satisfy that joint formulation. Redundant equations can express a useful invariant; contradictory equations expose incompatible assumptions or a failed identification of the shared quantities.

Feedback can require a joint solve. Suppose the selected same-instant relations are x=1+y and y=x/2. Substitution gives x=2 and y=1. Starting from y=0 and calling the first model once, then the second, returns x=1 and y=0.5; those values fail x=1+y. That call order is only one unfinished computation of the joint relation.

Choose between a common solve and separate interacting computations from the available capabilities and error needed by the answer. For time-dependent components, specify which inputs are held, interpolated or extrapolated between communication times, how events are synchronized, and whether a proposed step can be repeated. These are computation assumptions unless the actual subject has that delay or sampling behavior.

Compare the obtained exchange against the joint conditions and the required result. A residual can reveal a mismatch. Turning a small residual into an error bound needs the relevant conditioning or stability argument; CMP.8 supplies that approximate-computation work. CMP.14 supplies interaction between computations. More iterations cannot repair an incompatible physical or statistical premise.

### MMP.18:4.5 - Combine uncertainty without duplicating information {#combine-uncertainty-without-duplicating-information}

When components are probabilistic, construct a joint law for the common quantities and the component-specific quantities. Marginal distributions alone generally leave dependence unspecified. Obtain the needed dependence from the modeled mechanism, a conditional law or an explicit additional assumption.

For components sharing z, one possible factorization is:

~~~
p(z,u1,u2) = p(z) * p(u1 | z) * p(u2 | z).
~~~

It assumes conditional independence of u1 and u2 given z. If that assumption is unavailable, construct their joint conditional law or retain the unresolved dependence. A common random quantity is sampled or integrated once as that same quantity; two independent draws would describe a different model.

For two analyses using the same positive prior pi(z) and conditionally independent data D1,D2, their posteriors satisfy q1(z) proportional to pi(z)*L1(z) and q2(z) proportional to pi(z)*L2(z). The combined posterior is proportional to q1(z)*q2(z)/pi(z) on the common prior support. Multiplication without the division counts the prior twice.

If the analyses use overlapping records, first recover which observations and likelihood factors are shared. Dividing out a prior does not remove a duplicated observation. If component priors disagree, selecting a common prior or a pooling rule changes the model and needs a stated basis. MMP.7 supplies the record law and MMP.13 the resulting inference; a computational sampler obtains values from that law.

Point estimates can still be sufficient for a particular receiving use. To replace a distribution by a point, establish that the omitted uncertainty does not alter the required result at its chosen tolerance. Keep a consequential dependence when a nonlinear operation or tail probability needs it.

### MMP.18:4.6 - Return the coupled result and localize a failure {#return-the-coupled-result-and-localize-a-failure}

Return the combined formulation with the exchanged quantities and assumptions needed to reproduce the required result. The subject recipient must be able to interpret that result, including any approximation or unresolved interface contribution that changes its use.

Check the consequence at the scope actually claimed. An interval balance establishes the amount transferred over that interval, not the time of a threshold crossing within it. A joint posterior accounts for the supplied data under its dependence assumptions; it does not establish that those assumptions describe the subject.

If a result fails, locate whether the problem lies in the quantity identification, map, closure, component law, dependence or computation. Repair that contribution and its affected consumers. For a physical question, B.5.MPC.R coordinates a change crossing the physical, mathematical and computational accounts.

Stop with the sufficient coupled answer or the missing contribution that prevents it. C.11.DUA governs whether obtaining that contribution is preferable to a restricted answer or a different method. More detailed coupling is useful when its difference matters to the work.

## MMP.18:7 - Conformance Checklist {#conformance-checklist}

The coupled construction supports its stated use when:

- the requested combined result and the component contributions needed for it are recoverable;
- shared quantities retain their subject meanings and relevant units, reference points and conditions;
- each consequential exchange has a relation that connects what is supplied to what is used;
- aggregation or scale change retains, obtains or bounds the information the receiving operation needs;
- jointly applicable component and interface conditions hold for the claimed solution;
- computational exchange approximations are distinguished from actual subject delays or events;
- shared uncertainty and evidence have the dependence and multiplicity asserted by the joint model;
- the result retains a consequential limit and a usable return to the contribution that failed.

These conditions recognize the coupled model. Establishing its subject applicability or a numerical error guarantee needs the corresponding subject or computational argument when the use requires it.

## MMP.18:9 - Consequences {#consequences}

A component can be replaced without rebuilding the entire model when its replacement supplies the same required exchange under the same conditions. MATH.18 gives the mathematical comparison; the present method identifies what the neighboring models actually require.

Coupling may reveal that a previously useful component is insufficient or incompatible. The resulting repair can add a shared state, a closure or a joint solve. It can also remove unnecessary detail when the receiving answer depends only on an aggregate already preserved.

For working methods, this helps model the interaction of distinct procedures: a scheduling account may consume a resource or duration distribution supplied elsewhere. The coupling explains that mathematical dependence. ME retains the interpretation and change of the working procedures.

## MMP.18:12 - Relations {#relations}

- **A.3.3.TR** constructs joint change rules and **A.3.3.PI** tests whether retained information suffices for the needed continuation.
- **C.29.1** transfers a result between mathematical accounts. **C.29.BB** constructs a balance whose exchange this pattern may need to preserve.
- **MATH.18** compares mathematical accounts and the consequences their interpretations carry.
- **MMP.10** formulates constraints on the combined possibilities; **MMP.9** derives reduced evolution and closures.
- **MMP.7** supplies the observation law and **MMP.13** the inference under the combined probabilistic assumptions. **MMP.14** investigates a failed model prediction.
- **MMP.17** constructs a surrogate for a needed contribution. Its approximation conditions remain relevant inside the coupling.
- **CMP.8** controls numerical approximation, while **CMP.14** constructs interactions between computations. These obtain a result from the formulation rather than supplying its subject meaning.
- **PHY.5** selects effective physical descriptions by scales and couplings; **PHY.6** supplies physical evolution from balances and response laws.
- **B.5.MPC.R** coordinates repairs across physical, mathematical and computational accounts when the receiving question is physical; **C.11.DUA** compares further coupling work with an adequate restricted answer.
- **ME** consumes the construction when mathematical models of working procedures are combined or changed.


## Dependencies {#dependencies}

- @fact:DEPENDS-ON Dependencies (as published): spec://ai.lev/fpf-spec/contract/A-3-3-TR#root and spec://ai.lev/fpf-think-mmp/contract/MMP-10#root for joint conditions; spec://ai.lev/fpf-think-math/contract/MATH-18#root for retained consequences; spec://ai.lev/fpf-think-mmp/contract/MMP-9#root/.17 for missing contributions; spec://ai.lev/fpf-think-cmp/contract/CMP-8#root/.14 for interacting computation. @status:spec/done
- @fact:REFERENCED-BY Referenced by (computed from the Tables of Contents): spec://ai.lev/fpf-eng-dtm/contract/DTM-3#root, spec://ai.lev/fpf-eng-dtm/contract/DTM-9#root, spec://ai.lev/fpf-think-mmp/contract/MMP-17#root @status:spec/done

#source spec://ai.lev/fpf-think-mmp/source/MMP-18
