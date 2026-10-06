<p align="center">
  <img src="assets/logo.png" alt="Gauntlet Loop Logo" width="160" height="160" />
</p>

<h1 align="center">Gauntlet Loop for Google Antigravity</h1>

<p align="center">
  <b>Autonomous Multi-Agent Quality Enforcement and Iterative Loop Workflows</b>
</p>

---

## Overview

**Gauntlet Loop** is an Antigravity plugin and meta-prompting engine designed to drive AI-generated work to beat real-world quality benchmarks (**The Bar**). Instead of settling for mediocre first-drafts, it orchestrates builder and critic subagents across isolated context windows until the output wins an objective comparison.

### Why It Works
1. **Concrete Reference Standards**: No subjective hallucinations. Every loop anchors against a fetchable, real-world benchmark (e.g. Stripe's checkout UI, Ripgrep benchmarks, Julia Evans' technical blogs).
2. **Context-Isolated Subagents**: Employs Google Antigravity's native `invoke_subagent` and `define_subagent` tools to prevent builders from judging their own work.
3. **Blind A/B Comparisons**: Harsh critics evaluate outputs without author labels, stripping bias and eliminating unhelpful flattery.

---

## 4 Specialized Workflows

| Workflow | Best For | Subagent Topology | Exit Criteria |
| :--- | :--- | :--- | :--- |
| **1. Classic Gauntlet** | UI/UX, Landing Pages, Copywriting, Technical Articles | `Builder` vs `Harsh Critic` (`pro` model, blind A/B) | Critic blindly selects our output over the benchmark |
| **2. Tournament Arena** | Creative Concepts, Competing Algorithms, UI Variants | Multi-`Builder` (isolated branches) vs 1 `Judge` | Best contender wins the tournament brackets |
| **3. Adversarial Red-Team** | Secure APIs, Auth Flows, Smart Contracts, Parsers | `Builder` vs `Breaker / Attacker` | Breaker fails to find any new exploits or crashes |
| **4. Benchmark Driven** | Latency, Memory Tuning, Bundle Size, Throughput | `Optimizer` vs `Benchmark Runner` | Telemetry objectively outperforms competitor metrics |

---

## Usage

### 1. Slash Commands & Trigger Phrases
Invoke Gauntlet Loop directly within any prompt:
* `/gauntlet-loop [your goal]`
* `gauntlet this: [your goal]`
* `make a gauntlet prompt for [your goal]`

#### Example:
> `/gauntlet-loop Build a modern SaaS pricing table benchmarked against Stripe Pricing using Classic Gauntlet mode`

### 2. Autonomous Multi-Agent Orchestration
Request Antigravity to manage the entire iteration autonomously:
> *"Run a Benchmark Driven gauntlet loop directly to optimize this SQL query engine against DuckDB benchmarks until query execution times are 20% faster."*

---

## Installation & Setup

### Install in Antigravity
Clone this repository directly into your Antigravity global plugins directory:

```bash
git clone https://github.com/davigmacode/gauntlet-loop.git ~/.gemini/config/plugins/gauntlet-loop
```

Restart Google Antigravity or your IDE to discover the plugin.

---

## Directory Structure

```text
gauntlet-loop/
├── assets/
│   └── logo.png              # Plugin emblem
├── skills/
│   └── gauntlet-loop/
│       └── SKILL.md          # Multi-agent directives and instructions
├── plugin.json               # Antigravity plugin manifest
└── README.md                 # Documentation and quick reference
```

---

## License

MIT © [Irfan Vigma Taufik (davigmacode)](https://github.com/davigmacode)
