---
layout: default
name: ContainerClaw - Multi-Agent SWE-bench Harness
date: 2026-05-04
context: Autonomous Systems & Event-Driven Architecture
toc: true
toc_sticky: true
toc_label: "Table of Contents"
toc_icon: "cog"
excerpt_separator: An autonomous multi-agent software engineering evaluation framework built around Apache Fluss event streaming, dynamic Docker sidecar sandboxing, and history window compaction leveraging DeepSeek v4 context extensions.
---

# ContainerClaw: Multi-Agent SWE-bench Harness

The SWE-bench benchmark is the gold standard for evaluating autonomous software engineering agents on real-world GitHub issues. However, evaluating and orchestrating agents on complex repositories (such as `sympy`, `django`, `scikit-learn`, and `astropy`) presents critical engineering hurdles: synchronous agent communication deadlocks, catastrophic forgetting in long reasoning trajectories, and the hazards of unsandboxed code execution.

**ContainerClaw** is an event-driven multi-agent system (MAS) harness designed for rigorous, reproducible software engineering tasks. By combining **Apache Fluss** real-time event streaming with ephemeral **Docker sidecar sandboxing** and **DeepSeek v4 context compaction**, ContainerClaw establishes a scalable platform for autonomous bug fixing and benchmark evaluation.

[GitHub Repository: ContainerClaw](https://github.com/qzyu999/ContainerClaw)

---

# Architecture Overview

```
                                  [ GitHub Issue / Task ]
                                             |
                                             v
                           +-----------------------------------+
                           |          ARCHITECT AGENT          |
                           |    (Decomposition & Strategy)     |
                           +-----------------+-----------------+
                                             |
                   ================== APACHE FLUSS EVENT LOG ==================
                   [Task Stream]  [Research Stream]  [Diff Stream]  [Test Stream]
                   ============================================================
                               |             |              |            |
                               v             v              v            v
                       +-------------+ +-------------+ +---------+ +-----------+
                       | RESEARCHER  | | CODER AGENT | | CRITIC  | | VERIFIER  |
                       | AST Search  | | Synthesize  | | Review  | | Test Exec |
                       +------+------+ +------+------+ +----+----+ +-----+-----+
                              |               |             |            |
                              +---------------+-------------+------------+
                                             |
                                             v
                           +-----------------------------------+
                           |    DOCKER SIDECAR ORCHESTRATION   |
                           |   Isolated Repo Workspace Sandbox |
                           +-----------------+-----------------+
                                             |
                                             v
                           +-----------------------------------+
                           |  HISTORY WINDOW COMPACTOR (DS v4) |
                           |  Pruning, Checkpointing & Pass@1  |
                           +-----------------------------------+
```

---

# Key Features

### 1. Event-Driven Multi-Agent Collaboration via Apache Fluss
Rather than coupling agents via brittle, synchronous remote procedure calls (RPC) or nested prompt chains, ContainerClaw coordinates autonomous roles through **Apache Fluss** streaming event logs:
* **Decoupled Roles:**
  * **Architect:** Deconstructs the problem statement, identifies affected modules, and coordinates execution phases.
  * **Researcher:** Performs AST-aware code navigation, locates reproduction tests, and extracts relevant symbol definitions.
  * **Coder:** Implements minimal, surgical patches and generates unified git diffs.
  * **Critic:** Audits proposed changes against regression risks, style guidelines, and side effects.
  * **Verifier:** Orchestrates environment configuration and executes reproduction test scripts.
* **Stream-Centric State:** Every thought, tool call, compiler output, and patch candidate is appended as an immutable event. This enables complete trajectory replay, branch backtracking, and asynchronous multi-candidate exploration.

### 2. Dynamic Docker Sidecar Isolation
Executing arbitrary agent-generated code carries severe security and state contamination risks:
* **Ephemeral Sandboxing:** Each verification attempt launches a dedicated Docker sidecar container pre-configured with the exact Python runtime and dependencies for the target benchmark instance.
* **Strict Confinement:** Sandboxes enforce memory ceilings, CPU shares, and network egress blocks to prevent unintended socket connections or package tampering during evaluation runs.
* **Volume Snapshotting:** Repository checkouts leverage copy-on-write volume mounts, allowing instant rollback across iterative patch attempts.

### 3. Context Compaction & DeepSeek v4 Integration
Long-horizon coding trajectories regularly generate voluminous terminal logs and test tracebacks that saturate token limits:
* **History Window Compaction:** ContainerClaw monitors token consumption in real time. Redundant test runs and repetitive directory listings are semantically summarized, preserving critical stack traces and diff histories while freeing context space.
* **DeepSeek v4 Context Optimization:** Tailored for extended-context LLMs, utilizing prompt caching and structured reasoning markers to maintain high needle-in-a-haystack recall across trajectories exceeding 100k tokens.

```python
from containerclaw.core import FlussEventBus, AgentCluster
from containerclaw.sandbox import DockerSidecarManager

# Initialize event stream and sandboxed harness
event_bus = FlussEventBus(bootstrap_servers="localhost:9123")
sandbox_mgr = DockerSidecarManager(base_image="swebench/eval-py310:latest")

cluster = AgentCluster(
    event_bus=event_bus,
    sandbox=sandbox_mgr,
    model="deepseek-ai/DeepSeek-V4"
)

# Launch autonomous resolution loop for SWE-bench issue
result = cluster.resolve_issue(
    repo="sympy/sympy",
    issue_id="sympy__sympy-20590",
    max_iterations=12
)
print(f"Status: {result.status}, Patch: {result.patch_file}")
```

### 4. Benchmark Scoring & Ablation Suite
* **Automated Evaluation Pipeline:** Native support for both **SWE-bench Lite** and **SWE-bench Verified** datasets with automated gold test execution and pass@1 scoring.
* **Ablation Framework:** CLI tooling to empirically quantify the impact of individual architectural components—measuring the performance delta between single-agent baselines versus multi-agent debate, and evaluating context compaction strategies against raw history buffers.

---

# Tech Stack

* **Streaming Core:** Apache Fluss, Apache Arrow.
* **Orchestration:** Python, AsyncIO, Docker SDK.
* **Reasoning Models:** DeepSeek v4, Claude 3.5 Sonnet, GPT-4o.
* **Evaluation Frameworks:** SWE-bench, Pytest, Git Python.
