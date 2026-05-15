# Toy 05 — The Proxy Decay Simulator

> *Part of **The Architecture of Thriving** — a four-article series.*
> This toy is a companion to Article 2: The Depth Constraint *(link forthcoming)*.

---

## AI Alignment Simulation — When Does Optimization Consume What It Depends On?

Series 2, Article 1 established the behavioral foundation: directed behavior requires both navigation toward preferred states and recognition that those states have been reached. Article 2 formalizes the conditions under which that foundation generates structural constraints.

> **When a system's optimization pressure erodes the modeling capacity required to distinguish proxy from territory, the gap between what the system is pursuing and what it should be pursuing grows in the direction of the optimization. This simulator makes that failure mode interactive, observable, and falsifiable.**

The central variable is V(t) — the latent capacity whose degradation produces observable changes in recovery latency, behavioral diversity, and sensitivity to low-intensity signals. The central ratio is Ψ = S / D: scope of influence over territory divided by depth of modeling what that territory requires. When Ψ is high and D erodes, the system cannot correct the drift. This simulation shows why.

---

## What This Simulation Demonstrates

The Proxy Decay Simulator directly models the **proxy decoupling** failure direction: how optimization pressure erodes the modeling capacity D required to distinguish the proxy P(t) from the territory V(t), producing self-reinforcing degradation that becomes progressively harder to correct. The sufficiency failure direction is shown as a conceptual counterpart — its full dynamics require separate instrumentation.

What remains open: whether V(t) collapse and substrate collapse share formal absorbing-state properties in the same structural sense — the series' central open problem [OP2].

---

## Key Variables

| Variable | Meaning |
|---|---|
| **V(t)** | Territory — the latent capacity the system is supposed to serve. Degrades when the proxy decouples. Observable anchors: recovery latency ↑, behavioral diversity ↓, signal sensitivity ↓ as V falls. |
| **P(t)** | Proxy — the agent's map of the territory. Rises under optimization pressure. Diverges from V(t) when D erodes. |
| **D (D_base, D_eff)** | Modeling depth — how accurately the agent models what V(t) requires. D_base erodes under optimization pressure independently of V. D_eff = D_base × V. |
| **Ψ = S / D_eff** | The structural phase ratio. High Ψ = scope far outpacing modeling depth = failure-mode-dominant regime. |
| **α, α_eff** | Optimization pressure. α_eff = α(1 + κP²) — escalates steeply as the proxy nears saturation, modeling the lock-in effect. |
| **Correction window** | The interval in which D_base has eroded enough to trigger correction but recovery is still possible. The knife edge. |

---

## Key Concepts

**Proxy decoupling as structural failure** — The model doesn't just drift. Optimization chases the drift and makes the model harder to correct. Policy updates conditioned on a degraded state make correction progressively less likely. This is what distinguishes a structural constraint from a calibration problem.

**D_eff = D_base × V** — Multiplicative coupling that induces compounding fragility. When V falls, D_eff falls with it — and recovery requires D_eff × (1 − V), which also falls. The system loses both the territory and the capacity to recover it simultaneously.

**The absorbing state** — No hard switch. The equations run continuously below the absorption threshold. As V → 0, recovery → 0 naturally. Irrecoverability is derived from the equations, not imposed by a rule.

**The counterfactual** — With perfect modeling depth (D_eff = 1 always), erosion algebraically vanishes. Collapse requires imperfect representation, not pressure alone. This is the simulation's most important result: the failure is structural to inadequate modeling depth under optimization, not to optimization itself.

**The correction window** — The interval between "D_base has eroded enough to detect" and "V has fallen too far to recover." The τ slider controls response latency. At τ = 0, intervention fires immediately on detection. At τ = 4–5t, detection happens but correction fails anyway. The dynamics of this knife edge are explored in Part 3: The Inner Crossing.

**Connection to RLHF** — In Article 2's application: P(t) corresponds to the expressed preference signal RLHF optimizes; V(t) corresponds to the underlying capacity expressed preference is supposed to track. The RLHF preset illustrates parameter values consistent with this dynamic. Not an empirical placement of any system — illustrative of the structural gap identified in Article 2.

---

## Simulation Panels

**Main chart** — V(t) territory and P(t) proxy diverge in real time. The gap between them is the proxy decoupling made visible. Counterfactual V(t) (D_eff = 1) shows the upper bound on V preservation. Corrected trajectory shows the outcome when intervention fires.

**D_eff sub-chart** — D_base erodes under α independently of V. D_eff = D_base × V. The correction window threshold is shown as a structural indicator.

**V(t) observable anchors** — Recovery latency, behavioral diversity, and signal sensitivity update from V(t) in real time. Article 2 justifies V(t) through these three measurable behavioral signatures, which can dissociate under targeted intervention. Illustrative, not empirical measurements.

**Collapse horizon sweep** — Runs 26 mini-simulations across S = 0.5 → 3.0. Shows whether collapse is parameter-specific or emerges systematically under scaling. The structural claim made visible across parameter space.

**Phase map** — S × D₀ viability grid. Green = viable through T. Amber = crossover without absorption. Red = absorbed. Shows the full regime structure at current parameters.

**Bilateral structure** — Proxy decoupling is directly simulated. Sufficiency failure is the structural counterpart: optimization continues past the resolution point, degrading V(t) through saturation rather than misdirection. Both share the feedback pattern "degraded V(t) → worse policy sensitivity → harder correction." Formal absorbing-state equivalence remains open [OP2].

---

## Controls

| Control | Function |
|---|---|
| **δ — Erosion rate** | How strongly proxy pursuit degrades V(t) |
| **ρ — Recovery capacity** | Restoration rate × D_eff — recovery requires the capacity it's trying to restore |
| **α — Optimization pressure** | Base pressure; α_eff rises quadratically with proxy gains when κ > 0 |
| **κ — Optimization feedback** | Lock-in: α_eff = α(1 + κP²); escalates steeply at proxy saturation |
| **γ — Proxy gravity** | Natural proxy decay without active maintenance; makes correction cost visible |
| **τ — Response latency** | Time from D_base detection to intervention |
| **S — Scope** | Capability reach over experiential states; symmetric: scales both P growth and V erosion |
| **D₀ — Initial depth** | Starting accuracy of the agent's model of V |
| **ε — Depth erosion** | Rate at which α directly erodes D_base |
| **θ — Absorbing threshold** | V level below which the system is in the absorbing regime |
| **Counterfactual toggle** | D_eff = 1 always — shows what V preservation looks like with perfect modeling depth |
| **D_eff sub-chart toggle** | Shows D_base and D_eff erosion over time |
| **Correction toggle** | Fires when D_base drops to 94% of D₀; α cut 40%, D_base rebuilds |
| **Structural analog (Φ) toggle** | Overlays the Series 1 structural correspondence — one-directional causal result |

**Presets:** Default · Engagement platform · RLHF — illustrative · High depth · Near rescue · Falsification (stable baseline)

---

## The Architecture of Thriving: Series 2

```
Universal Generator  →  Structural Correspondence  →  Inner Crossing  →  Asymptote
       (1)                        (2)                      (3)               (4)
```

**Article 1 (Toy 04):** Establishes the behavioral foundation — the three-state taxonomy, the two-directional failure of relative rationality, and why directed behavior structurally requires a stopping condition.

**Article 2 (this toy):** Formalizes the conditions under which the behavioral foundation generates structural constraints — through V(t) as a latent variable and the proxy decoupling failure direction as self-reinforcing degradation under endogenous policy dynamics.

**Article 3:** Identifies Ψ = S / D as the governing ratio and the crossing window that determines whether systems reach the viable regime.

**Article 4:** Characterizes the structure of the region the constraints leave standing.

---

## Run Locally

No build step. No dependencies. Open `toy_05.html` in any modern browser.

```bash
open toy_05.html
# or drag the file into a browser tab
```

---

## Article

*The Depth Constraint — Architecture of Thriving, Series 2, Part 2 · Link forthcoming.*

---

*"The model doesn't just drift. Optimization chases the drift and makes the model harder to correct. The self-reinforcing structure under endogenous policy dynamics is the formal claim that distinguishes a structural constraint from a common pattern."*
