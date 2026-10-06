---
name: gauntlet-loop
description: Turns any goal into a high-standard iterative gauntlet loop prompt or directly orchestrates multi-agent iterations in Google Antigravity. Sets a concrete quality bar, splits work into verifiable pieces, runs builder and harsh critic/judge subagents with fresh context, compares blind or benchmarks against the bar, and loops until victory. Supports 4 specialized workflows: Classic A/B, Tournament Arena, Adversarial Red-Team, and Benchmark Driven. Triggers on "/gauntlet-loop", "gauntlet loop", "gauntlet this", "make a gauntlet prompt", "loop until it beats X".
---

# Gauntlet Loop for Google Antigravity

Generates copy-paste ready gauntlet loop prompts or directly orchestrates autonomous multi-agent execution until your work beats a real-world reference standard (**The Bar**).

---

## 4 Specialized Workflows

Select the workflow tailored to your task:

### 1. Classic Gauntlet (1-on-1 Blind A/B)
* **Best for**: UI/UX design, landing pages, persuasive copywriting, technical articles, and visual diagrams.
* **Subagent Architecture**:
  * `Builder` (Model: `inherit` / `flash`, file edit tools enabled).
  * `Harsh Critic` (Model: `pro`, completely fresh context, unswayed by builder effort).
* **Mechanism**: The critic inspects the output side-by-side with the real reference with identifying labels stripped (blind A/B test). It picks the winner and names the single biggest remaining gap. The feedback feeds directly back to the builder.

### 2. Tournament Arena (Multi-Builder vs 1 Judge)
* **Best for**: Creative explorations, diverse algorithmic implementations, and frontend component architectures.
* **Subagent Architecture**:
  * 2–3 independent `Builder` agents, each given distinct philosophies or constraints (use `Workspace: 'branch'` to prevent file collisions).
  * 1 `Judge / Referee` (Model: `pro`).
* **Mechanism**: All candidate implementations compete against each other and against The Bar. The judge eliminates weaker variants and advances the top contender into subsequent refinement rounds.

### 3. Adversarial Red-Team (Builder vs Breaker)
* **Best for**: Backend APIs, authentication systems, data parsers, smart contracts, and mission-critical business logic.
* **Subagent Architecture**:
  * `Builder`: Implements functional features and standard test suites.
  * `Breaker / Red Team`: Actively attacks the implementation using malformed payloads, edge cases, race conditions, and boundary fuzzing.
* **Mechanism**: The loop exits only when the breaker runs out of reproducible bugs or exploit scenarios (zero unhandled exceptions & 100% boundary test passing).

### 4. Benchmark Driven (Measurable Performance)
* **Best for**: Latency/throughput optimization, frontend bundle reduction, memory footprint minimization, and SQL/query tuning.
* **Subagent Architecture**:
  * `Optimizer`: Iteratively profiles and refactors codebase.
  * `Benchmark Runner`: Executes reproducible benchmarks in the Antigravity sandbox and captures objective metrics (ms, KB, FPS, ops/sec).
* **Mechanism**: Fully deterministic exit criteria. The loop stops only when recorded telemetry objectively outperforms the competitor or threshold.

---

## Execution Flow

1. **Clarify Goal & Select Workflow**: Determine the target objective and choose the best fit among the 4 workflows.
2. **Establish The Bar (The Ground Truth)**:
   * **Named**: A specific entity, not an abstract category (e.g., "Stripe Checkout", "Ripgrep CLI benchmark", "Julia Evans technical post").
   * **Fetchable**: The critic must be able to inspect the real artifact directly (live URL, local repo, screenshot, benchmark dataset).
   * **Comparable**: Both must be capable of sitting side-by-side for blind evaluation or quantitative comparison.
   *(If the user has not supplied a reference, propose 2–3 concrete candidates before proceeding)*.
3. **Execution Choice**:
   * **Option A (Generate Prompt)**: Return a concise, paste-ready prompt (120–180 words).
   * **Option B (Direct Orchestration)**: The lead agent immediately configures and launches `define_subagent` and `invoke_subagent` to orchestrate the loop.
4. **Transparent Progress Tracking**: Log intermediate scores, gaps, and iteration diffs into an Antigravity **Artifact** so the user can observe progress live in the canvas panel.

---

## Ready-to-Use Prompt Template (Antigravity Native)

```text
Build [GOAL].

The bar is [BAR]. Fetch and inspect the real reference directly, never rely solely on a summary.
Workflow: [Classic A/B / Tournament Arena / Adversarial Red-Team / Benchmark Driven].

Decompose this task into the smallest individually verifiable components.
For each component, fan out a Builder (model: inherit/flash) and a separate Harsh Critic (model: pro) with fresh context using invoke_subagent.
The critic must evaluate blind with labels stripped, deliver blunt feedback without empty praise, and isolate the single biggest remaining gap.

Run under /goal mode and iterate relentlessly until the critic blindly selects ours over the reference.
Persist iteration logs, telemetry, and side-by-side notes into Antigravity Artifacts.
```

---

## Core Rules

* **Never allow a builder to judge its own output**: The critic must be an isolated subagent with clean context.
* **No artificial iteration caps**: Loops conclude when the reference standard is beaten, not at an arbitrary `N` rounds.
* **Binary evaluation over vague scoring**: A/B comparisons and binary win/loss criteria prevent score inflation over multiple rounds.
