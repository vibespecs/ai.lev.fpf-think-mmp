# MMP.9 - Derive a Reduced Mathematical Model of State Evolution {#root}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Working sections of the pattern; its depth sections live in the source document named by the last line. See LICENSE.md for the list of changes.

> **Type:** Method pattern
> **Status:** Usable, evolving
> **Normativity:** Normative within the stated use

## MMP.9:1 - Problem frame {#problem-frame}

Use this pattern when a supplied model describes how a state changes, but predicting the quantities you need would be easier with less state, shorter memory or a simpler update. After removing detail, the proposed update still depends on something you removed. You need to derive what can replace that contribution while retaining a useful answer.

Start with the quantity you want to keep and compute its change from the supplied model. Circle the part that cannot be obtained from the proposed smaller state. For an average, this may be the variance of the underlying values. For one observed component, it may be the effect of unobserved components. That expression identifies the construction needed next.

The result can be a smaller evolution law, a history-dependent rule, an approximation with a stated error, or bounds sufficient for the question. Keep the initial information, inputs and time range on which it depends. A model that is already affordable and sufficient can be used directly. If the original change law is missing, recover or construct it in the subject practice before using this reduction method.

You need the mathematics used by the supplied law: substitution and recurrence for discrete changes; differentiation and integration for differential equations; expectations when reducing a probability distribution. A mathematical collaborator may perform those operations from your stated question and model. This is reduction within mathematical modeling. A.3.3.PI supplies the general test of which information a prediction needs; C.29.1 supplies the comparison that transfers the reduced result back to the source question.

## MMP.9:2 - Problem {#problem}

A description can retain today's quantity while losing what determines tomorrow's. Differentiating a mean can introduce higher moments. Solving for an unobserved component can make its past influence explicit. Dropping a quickly decaying component can retain a lasting change it caused before decaying.

The missing contribution is often called an **unclosed term**: the proposed retained state does not determine it. A **closure** supplies a way to obtain or approximate that contribution from the information the reduced model carries. Its choice changes the resulting evolution.

Finding the unclosed term locates the difficulty. The remaining work is to derive a usable replacement and determine what that replacement permits the model to answer.

## MMP.9:3 - Forces {#forces}

| Choice | Consequence for the construction |
| --- | --- |
| Smaller state and longer memory | Eliminating coordinates can replace present-state work with a history calculation. |
| Detailed trajectory and selected result | A bound on one output can be cheaper than a replacement for the whole trajectory. |
| Additional moments and finite closure | Deriving another moment can expose yet another missing moment. |
| Short-lived component and lasting effect | A small or fast component can make a consequential accumulated contribution. |
| Fit to supplied trajectories and use inside a new evolution | Once the replacement supplies the next state, its errors can change the states it later receives. |
| Several adequate replacements and available effort | An existing bound or larger model can cost less than developing a new closure. |

## MMP.9:4 - Solution {#solution}

**Choose the retained result → derive its change → expose the unclosed contribution → construct a replacement or bound → use it over the required horizon → revise the part that changes the answer.**

The work may end at a useful bound. It may also show that the smaller description would cost more than continuing with the source model.

### MMP.9:4.1 - Express the retained result and its change {#express-the-retained-result-and-its-change}

Name the source state z, its initial possibilities and the admitted inputs u. Specify the answer and horizon: a quantity at time T, a threshold crossing, a response to an input, or a distributional feature. Construct the retained description x=r(z) from those needs. A.3.3.PI:4.1-4.2 tests whether merged source states can still answer that question; use an already sufficient result from that test.

For a discrete source update z_next=F(z,u), substitute it into the retained description:

`x_next = r(F(z,u)).`

For a differentiable r and a differential law z_dot=F(z,u), the chain rule gives:

`x_dot = Dr(z) F(z,u).`

Dr is the derivative of r. If r also depends explicitly on time, include its time derivative. A discontinuous readout or event needs its own change relation rather than this differentiable formula. A.3.3.TR supplies composition of the relevant changes.

Rewrite the result using x, the admitted inputs and whatever other information the smaller model proposes to carry. The part still depending on discarded quantities is the unclosed contribution. One convenient decomposition is `x_dot=f0(x,u)+c(z,u)`, where f0 is the part you will compute directly and c is the remaining contribution. Another decomposition can be useful; what matters is the complete retained law and what information obtains each term.

If every term is obtainable from the retained information, construct the closed update through A.3.3.PI and compare it through C.29.1. Continue here when the replacement itself still needs construction.

### MMP.9:4.2 - Derive the discarded contribution before approximating it {#derive-the-discarded-contribution-before-approximating-it}

Try to express the discarded variables through their own evolution, initial conditions and the retained history. In a discrete law, iterate the discarded update and substitute each earlier term until the dependence has a usable form. In a differential law, solve or integrate the discarded equation under the supplied retained history, then substitute the result into the retained equation.

For constant compatible matrices and supplied initial values, consider:

`x_dot=A*x+B*y`, `y_dot=C*x+D*y`.

Solving the second equation while treating x(s) as its input gives:

`y(t)=exp(D*t)*y0 + integral_0^t exp(D*(t-s))*C*x(s) ds`.

Substitution gives the retained law:

`x_dot(t)=A*x(t)+B*exp(D*t)*y0 + integral_0^t B*exp(D*(t-s))*C*x(s) ds`.

The first added term carries the discarded initial condition. The integral carries the past influence of x through y. With a forcing term in the discarded equation, its propagated contribution also appears in the integral. These terms identify what a proposed memory approximation would replace. Unknown y0 remains an initial uncertainty; it cannot be set to zero solely because y is being removed.

Look for a less costly way to compute the derived expression. Equal decay modes can be combined; a sum of exponentials can be updated through a few auxiliary variables. For example, `v(t)=integral_0^t exp(-lambda*(t-s))*x(s) ds` satisfies `v_dot=x-lambda*v`, v(0)=0. This replaces storage of the whole history with an evolving value. Carry a nonzero initial contribution separately or incorporate its matching initial condition. Count the required auxiliary values and update work before claiming a computational saving.

For nonlinear discarded dynamics the same elimination question remains, but the response to retained history may require solving a nonlinear problem. Use the derived dependence to select an approximation, retained variable or bound; an implicit formula that still requires the original computation has not yet supplied a cheaper model.

### MMP.9:4.3 - Choose and construct a useful replacement {#choose-and-construct-a-useful-replacement}

Use the expression just derived to decide which information or calculation earns its cost.

**Retain a quantity that obtains the missing contribution.** If c depends on a small additional observable v, derive v's update from the source law and repeat the closure test for the pair (x,v). This operation can reveal a useful finite system or a growing hierarchy. For members obeying `Z_dot=-Z^2`, the mean m has `m_dot=-mean(Z^2)`. Retaining `q=mean(Z^2)` gives `q_dot=-2*mean(Z^3)`. The new equation exposes the next assumption needed; adding q alone does not finish the closure.

**Compute the effect through memory.** Use the history expression from :4.2. To truncate old history, bound its omitted contribution for the admitted histories. To replace the memory kernel by a simpler one, bound or estimate the resulting difference on those histories, then propagate that difference through the retained evolution. A slowly decaying kernel can make distant history consequential. An auxiliary-state representation can be cheaper than truncation when a few modes express that kernel.

**Bound the requested output.** If the use asks for a threshold or interval, derive bounds directly from the source law and available initial information. For a population, solve or bound the member response as a function of its initial value, then average using known ranges or moments. Monotonicity, convexity or conservation can give a bound without choosing a complete distribution. The nonlinear example in :5.2 constructs such bounds. Use C.29.1:4.5 to turn them into the corresponding decision, or to expose the still-unresolved range.

**Approximate a contribution whose accumulated effect is small.** Identify the parameter and the class over which smallness is claimed: initial values, inputs, horizon and required error. Derive or bound the contribution integrated over that horizon. A small coefficient can multiply a large hidden value, and a fast transient can shift the later state. If a transient only matters near the start, retain its effect in an adjusted initial value and state when the later approximation begins. :5.3 shows both constructions.

A learned closure is another possible approximation to the missing contribution. Specify what its inputs contain and how its output enters the retained update. Pairs of retained inputs and source contributions can support fitting, but different hidden states can give different contributions at the same retained input. A fitted conditional mean then answers a distribution-dependent question; it is not an all-cases replacement of those contributions. When probability is needed, MMP.7 helps construct the law of the sampled or recorded training cases. Use the resulting closure at its intended inputs and horizon before drawing the corresponding predictive conclusion.

Compare the candidates through the existing characterization and choice methods: the required output or bound, obtaining cost, initial information and conditions. There is no need to develop every alternative. C.11.DUA helps choose whether more derivation, data or computation can change the decision.

### MMP.9:4.4 - Evaluate the replacement inside the retained evolution {#evaluate-the-replacement-inside-the-retained-evolution}

Write the model that will actually be used, including its initial values, any auxiliary variables, input rule and observation interpretation. Construct the requested output from that model. Substituting the closure into known source trajectories tests a different computation from letting it generate successive retained states.

Compare the retained source result and the reduced result for the same admitted initial case and input. For an identity, use the derivation to establish the covered equality. For an approximation, propagate the discrepancy to the requested output and horizon through C.29.1:4.5. A numerical scheme adds its own approximation; include it when it can change the answer. A.3.3.PI:4.5 supplies the repeated-use and changed-condition questions.

For a probabilistic model, choose the distributional feature the work needs. Agreement of a mean can coexist with different variance, correlations or event probabilities. A further observable is worth checking when it can change the planned use. State which result the comparison supports rather than extending one fitted statistic to the whole model.

When inputs are chosen from observations, retain the information the choice rule uses. If reduction removes that information, formulate the revised choice under MMP.8 before claiming that the same intervention or control method remains available. A changed intervention also requires the corresponding source law or mechanism under C.28.MR.

### MMP.9:4.5 - Return the result and revise the construction when needed {#return-the-result-and-revise-the-construction-when-needed}

Return the reduced law, sufficient bound or located obstacle with the assumptions that affect its use. An existing derivation and calculation can carry this information. Explain which discarded contribution was replaced, how to initialize and run the replacement, and which question it answers.

If a bound settles the working question, use it. If the result is too weak, locate why: uncertain initial influence, unresolved higher moment, long memory, error amplification, or information unavailable to an action. Improve that contribution or retain more of the source model. A mathematical construction can also show that the proposed simplification offers no saving.

Reopen the affected construction when the source law, initial class, inputs, observation, horizon or required output changes. Keep conclusions whose conditions still hold. In a model of a working method, ME can use the comparison to design a different method or representation; the actual work must still provide the quantities and relations assumed in the model.

## MMP.9:7 - Conformance Checklist {#conformance-checklist}

- Can the retained quantity's change be derived from the supplied law, with its initial and input conditions?
- Which contribution is unavailable from the proposed retained information, and how does the replacement obtain, approximate or bound it?
- Does an added variable have its own usable update and initialization? If a hierarchy remains, where is the closing assumption?
- For a memory or small-parameter approximation, what bounds the omitted effect on the requested output over the stated horizon?
- Is the comparison made in the model's intended repeated use, with the relevant numerical and observation conditions?
- Does the resulting law or bound settle the working question? If not, which changed contribution could do so at worthwhile cost?

## MMP.9:9 - Consequences {#consequences}

A reduced model can expose which information determines the answer and make repeated calculation cheaper. Bounds can support a decision before a full reduced trajectory is available. Derivation also identifies a reusable limitation: which initial conditions, inputs or new questions require restoring discarded content.

The cost can move into initialization, memory, closure construction or verification at the required horizon. Where that cost exceeds using the source model, the larger account remains a useful option.

## MMP.9:12 - Relations {#relations}

- **A.3.3.TR and A.3.3.PI:** compose source changes, determine the information needed for the future question and update the retained account. MMP.9 constructs a remaining closure or bound after those operations expose the gap.
- **C.29.1 and MATH.2:** compare the retained construction with the source and determine which answers survive identification; use their exact or bounded transfer where applicable.
- **MMP.7 and MMP.8:** construct observation laws and information-limited choices when a learned or controlled reduced model uses them. Their conditions determine which data law or action rule is actually being compared.
- **C.28.MR and B.5.MPC.R:** reconsider the relevant mechanism or connected accounts when an intervention or model change alters the source law.
- **C.11.DUA:** decide whether further derivation, observation or comparison is worth its cost for the receiving decision.
- **E.22 and E.23:** frame the question for evaluating a candidate, then organize repeated improvement under that evaluation when needed.
- **EXD and C.2.8:** EXD develops an explanation for the recipient's question; C.2.8 compares what structure that recipient can recover from its expression under stated conditions. Prediction and explanation can require different retained results.
- **ME:** use the mathematical result to construct or change the working method it describes.


## Dependencies {#dependencies}

- @fact:DEPENDS-ON Dependencies (as published): spec://ai.lev/fpf-spec/contract/A-3-3-TR#root for evolution; spec://ai.lev/fpf-spec/contract/C-29-1#root for preserved structure; spec://ai.lev/fpf-think-mmp/contract/MMP-11#root for a replacement family; spec://ai.lev/fpf-spec/contract/B-5-RR#root for affected revision. @status:spec/done
- @fact:REFERENCED-BY Referenced by (computed from the Tables of Contents): spec://ai.lev/fpf-think-mmp/contract/MMP-11#root, spec://ai.lev/fpf-think-mmp/contract/MMP-18#root, spec://ai.lev/fpf-think-phy/contract/PHY-5#root, spec://ai.lev/fpf-think-phy/contract/PHY-8#root @status:spec/done

#source spec://ai.lev/fpf-think-mmp/source/MMP-9
