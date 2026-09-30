# MMP.9 - Derive a Reduced Mathematical Model of State Evolution: depth {#depth}

<status stage="spec" state="done"/>

> Source: Anatoly Levenchuk, *Mathematical Modeling DPF* (22 September 2026), `Foundational Thinking DPF Suite/MATHEMATICAL-MODELING-PRACTICE-DPF.md` at https://github.com/ailev/FPF commit d131d30a44e7, licensed CC BY 4.0. Depth sections of the pattern; the working sections are in the contract document of the same id. See LICENSE.md for the list of changes.

## MMP.9:5 - Archetypal Grounding {#archetypal-grounding}

### MMP.9:5.1 - Replace many response components by two evolving quantities {#replace-many-response-components-by-two-evolving-quantities}

Suppose a dimensionless model has an observed x and n hidden response components:

`x_dot=-x+sum_i y_i+u(t)`, `y_i_dot=c_i*x-2*y_i`,

where the nonnegative c_i sum to one. Initial values and a prescribed input u(t) are supplied. The question asks for x over a finite horizon; each y_i separately is irrelevant to that result.

Retaining x alone leaves the unclosed contribution sum_i y_i. Solve each hidden equation and sum:

`sum_i y_i(t)=exp(-2*t)*sum_i y_i(0)+integral_0^t exp(-2*(t-s))*x(s) ds`.

All hidden contributions have the same decay kernel. Define v=sum_i y_i. Differentiating the sum gives the two-variable model:

`x_dot=-x+v+u(t)`, `v_dot=x-2*v`, `v(0)=sum_i y_i(0)`.

The derived equations and initial sum preserve x for every supplied input for which these linear equations have their solution. For n>1 this uses two evolving quantities instead of n+1. The required hidden initial information is their sum. Arbitrarily setting v(0)=0 would already change x_dot(0) when the actual sum is nonzero.

The initial sum requires n terms once. Each subsequent evaluation of the reduced right-hand side uses x, v and u(t); it no longer recomputes n component contributions. This saves repeated arithmetic when those components would otherwise be advanced separately.

Now one component has decay rate 3 instead of 2. Summing produces `v_dot=x-2*v-y_1`; the old two-variable model has lost a contribution. Retain y_1 separately and update it by `y_1_dot=c_1*x-3*y_1`, or separate the two decay groups. The change determines which added state is needed. The same grouping can combine any components that share their response kernel; different kernels remain distinct until another justified approximation combines them.

### MMP.9:5.2 - Answer about a nonlinear population without a closed mean equation {#answer-about-a-nonlinear-population-without-a-closed-mean}

A finite population has nonnegative member values X_i with `X_i_dot=-X_i^2`. The available initial information is 0<=X_i(0)<=M and mean m0. The requested output is the mean m(t).

Differentiating the mean gives:

`m_dot=-mean(X_i^2)=-m^2-Var(X_i)`.

Replacing this by m_dot=-m^2 sets the variance contribution to zero. Populations with the same mean can have different variance, so first ask whether a bound already answers the question.

Each member has `X_i(t)=X_i(0)/(1+t*X_i(0))` for t>=0. Since X_i(0)<=M, averaging gives the lower bound `m0/(1+M*t)`. The response `a/(1+t*a)` is concave for nonnegative a and t>=0; the mean of the responses is at most the response of the mean. Thus:

`m0/(1+M*t) <= m(t) <= m0/(1+m0*t)`.

With M=2, m0=1 and t=1, the mean lies between 1/3 and 1/2. A requirement m(1)<=0.55 is established without a variance model or a complete initial distribution.

Change the requirement to m(1)<=0.4. A population whose members all start at 1 has m(1)=1/2. An equally divided population starting at 0 and 2 has m(1)=1/3. Both fit the supplied initial information, so it cannot settle the changed requirement. Information about the initial population or a different acceptable requirement would change the next move. Treating the zero-variance closure as the whole population would conceal this distinction.

### MMP.9:5.3 - Decide whether a fast transient can be omitted {#decide-whether-a-fast-transient-can-be-omitted}

For a dimensionless model with epsilon>0,

`x_dot=y`, `epsilon*y_dot=-y`,

the solutions for t>=0 are `y(t)=y0*exp(-t/epsilon)` and `x(t)=x0+epsilon*y0*(1-exp(-t/epsilon))`.

Suppose the admitted initial values satisfy abs(y0)<=Y. Replacing the model by constant x0 gives an error at most epsilon*Y for every t>=0. With epsilon=0.01 and Y=1, that is 0.01. It can meet a tolerance 0.02 while failing to establish tolerance 0.001. The coefficient alone is insufficient if the initial class changes: y0=1/epsilon leaves a later change approaching one.

When y0 is known and the use concerns only later times, a different approximation is constant `x0+epsilon*y0`. Its error is at most `epsilon*Y*exp(-t/epsilon)`. For tolerance `0<eta<epsilon*Y`, it meets that tolerance at all times starting from `t_start=epsilon*log(epsilon*Y/eta)`. With eta=0.001 in the preceding case, t_start is about 0.0231. The adjusted initial value has retained the transient's later effect; it does not reproduce the initial interval.

If y0 is unknown, the adjusted value is also unknown. Its stated range can still yield a useful interval for x. The choice between an early transient calculation, a later approximation and a bound follows the requested result and available initial information.

## MMP.9:6 - Bias-Annotation {#bias-annotation}

Compact equations can conceal transferred effort. Removing variables may require a history integral, extra initial information or an expensive closure. Compare the work needed to obtain the requested result. A familiar equilibrium substitution or learned fit is a candidate construction whose lost contribution must remain visible in that comparison.

## MMP.9:8 - Common Anti-Patterns and How to Avoid Them {#common-anti-patterns-and-how-to-avoid-them}

| Observed difficulty in the construction | Repair |
| --- | --- |
| Replacing the mean of a nonlinear response by the response at the mean loses heterogeneity. | Derive the missing moment term, then retain, model or bound its effect; :5.2 may already settle the output question. |
| Hidden state is eliminated together with its initial effect. | Carry the initial-condition term in the memory formula or initialize the corresponding auxiliary value. |
| A small coefficient is used as the entire error argument. | Bound the multiplied state, accumulated contribution and admitted initial class, as in :5.3. |
| A closure is judged only on inputs from the source trajectory. | Insert it into the retained evolution and compare the requested result at its intended horizon. |
| Adding a moment is presented as completing a model although its equation needs another moment. | Continue the derivation until a usable closure or sufficient bound is obtained; otherwise retain the unresolved contribution. |

## MMP.9:10 - Architectural Rationale {#architectural-rationale}

Reduction is organized around the requested result and the source law's unclosed contribution. This makes the choice between retained state, memory, approximation and bounds depend on what each construction obtains. Beginning with one favored approximation would select what to discard before establishing its effect.

A.3.3.PI supplies the question-relative information test. This method develops the subsequent mathematical construction of a replacement contribution. C.29.1 supplies the common exact-or-bounded transfer and error propagation; those rules also apply to constructions outside model reduction.

Linear response, nonlinear aggregation and fast transients require different constructions. A new source law requires deriving its own discarded contribution; it need not resemble one of these examples. When the deriving operation itself requires a further subject method, retain that mathematical dependency rather than presenting a technique's name as an already obtained closure.

## MMP.9:11 - SoTA-Echoing {#sota-echoing}

The practice question is how to replace unresolved dynamics economically while retaining the needed result. **Adopt** construction from the source law and evaluation within the reduced evolution, including memory, initial information and question-relative outputs. A serious alternative fits an instantaneous missing term on source trajectories and judges primarily that fit. It can be cheaper and adequate for a limited use, but it can miss errors generated when the closure supplies its own future inputs.

[Sanderse, Stinis, Maulik and Ahmed, Scientific machine learning for closure models in multiscale problems, version 2 (2024), sections 2.1-2.2, 3.2 and 7.1](https://arxiv.org/html/2403.02913v2), is a comparative synthesis of closure constructions. It distinguishes an unclosed term from its replacement, and fitting the term from testing the evolving reduced model. **Adapt** these distinctions in :4.1-4.4. Its memory discussion supports preserving initial and historical effects during elimination. An exact elimination identity still needs an affordable way of obtaining its result; :4.2 makes that cost question explicit. The linear elimination, population bounds and transient estimates above are elementary derivations developed here, not empirical validation claims.

[Freitas, Um, Desbrun, Buzzicotti and Biferale, A posteriori closure of turbulence models: are symmetries preserved? (2026 preprint), sections 3-5](https://www.geometry.caltech.edu/pubs/FUDBB26.pdf), provides a current countercase. A learned shell-model closure reproduces selected statistics while missing other correlations and scale-invariance properties. **Adopt** its consequence in :4.4: select the observables that the receiving use needs instead of extending fit of one statistic to all requested behavior. Missing memory is a proposed explanation in that case; it does not establish a universal cause or require every reduced model to carry the same memory construction.

The selected method spends effort on the omitted contribution and the use it can change; it need not reproduce every property of the detailed model. A sufficient analytic bound can be cheaper than training or testing another closure. Reopen the comparison when changed inputs, initial conditions, horizon or requested observables expose a consequential error, or when another construction obtains the same needed result at lower cost.


## MMP.9:End {#end}
