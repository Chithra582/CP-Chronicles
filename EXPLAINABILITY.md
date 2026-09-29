# EXPLAINABILITY — CP Chronicles Agent

> **Admissibility & Transparency Report for OpenGAP / Agent Passport**  
> *Agent Name:* CP Chronicles Agent (`cp-chronicles-agent`)  
> *Specification:* OpenGAP v0.1.0  
> *Domain:* Education / Competitive Programming & Algorithmic Mentorship  

---

## 1. Overview & Pedagogical Purpose

CP Chronicles Agent is an autonomous competitive programming mentor, algorithmic complexity auditor, and daily practice intelligence designed for the **CP-Chronicles** daily challenge archive. The underlying system operates across structured problem directories (`day-XXX`), tracking problem statements, algorithmic tags, optimal solutions (C++, Python), and empirical complexity notes.

The agent's primary pedagogical purpose is to bridge the gap between theoretical data structures and high-performance contest problem solving. By analyzing problem constraints, calculating exact asymptotic time/space complexities, identifying subtle boundary edge cases, and sustaining daily practice streaks, the agent cultivates long-term discipline and technical interview readiness.

---

## 2. How the Agent Decides (Decision-Making Logic)

CP Chronicles Agent operates across a deterministic, multi-stage decision pipeline that grounds every recommendation in rigorous computational complexity:

```
[Problem Statement & Constraints] ──> [Constraint & Budget Analysis] ──> [Paradigm & Data Structure Selection]
                                                                                               │
                                                                                               ▼
[Optimized Solution & Habit Feedback] <── [Edge-Case & Safety Gate] <── [Asymptotic Complexity Verification]
```

### 2.1 Constraint & Operational Budget Analysis
- **Decision:** Determines feasible algorithmic time complexity classes based on input bounds ($N$).
- **Rules:**
  - $N \le 12$: Permutations / Bitmask exponential search ($O(N!)$ or $O(2^N \cdot N)$).
  - $N \le 500$: All-pairs graph algorithms / Floyd-Warshall ($O(N^3)$).
  - $N \le 5000$: Quadratic algorithms / nested dynamic programming ($O(N^2)$).
  - $N \le 2 \times 10^5$: Linearithmic divide-and-conquer / sorting / Segment Trees ($O(N \log N)$).
  - $N \le 10^8$: Pure linear scan ($O(N)$) or logarithmic search ($O(\log N)$).

### 2.2 Algorithmic Paradigm & Data Structure Selection
- **Decision:** Classifies the optimal problem-solving pattern and underlying data structure.
- **Rules:**
  - Optimal substructure with overlapping subproblems -> Dynamic Programming (memoization / tabulation).
  - Monotonic search space or range queries -> Binary Search or Two Pointers.
  - Connected components, reachability, or shortest paths -> BFS, DFS, Dijkstra, or Disjoint Set Union (DSU).
  - Dynamic range aggregations with point updates -> Fenwick Tree (Binary Indexed Tree) or Segment Tree.

### 2.3 Asymptotic Complexity & Edge-Case Verification
- **Decision:** Calculates worst-case time and space bounds and checks against boundary failures.
- **Rules:**
  - Evaluates recursion depth against stack limits (typically 256MB on online judges).
  - Verifies integer arithmetic bounds; mandates 64-bit integers (`long long` in C++) if accumulated sums exceed $2^{31}-1 \approx 2 \times 10^9$.
  - Tests boundary conditions: $N=0$, $N=1$, identical array elements, self-loops in graphs, and negative weights.

### 2.4 Code Optimization & Habit Scheduling
- **Decision:** Suggests constant-factor improvements and records practice streak continuity.
- **Rules:**
  - In C++, verifies fast I/O setup (`cin.tie(NULL)`, `\n` over `endl`).
  - Recommends space-saving optimizations (e.g. state compression in DP from $O(N)$ to $O(1)$).
  - Updates daily challenge progression and flags topics due for spaced-repetition review.

---

## 3. Data Sources & Inputs Used

| Data Input | Source | Purpose | Data Handling & Privacy |
|---|---|---|---|
| **Problem Statement & Constraints** | Challenge Markdown (`problem.md`) / User prompt | Establishing input limits ($N, M, K$), target time limits, and test cases | Processed in-memory; strictly grounded in problem text |
| **Solution Source Code** | User code submissions (`solution.cpp`, `solution.py`) | Inspecting algorithmic strategy, time/space complexity, and code quality | Evaluated ephemerally; never transmitted to third-party databases |
| **Practice Notes & Error Logs** | Learner reflection logs (`notes.md`) | Tracking recurrent mistakes (e.g. off-by-one, integer overflow, TLE) | Local file parsing; used to tailor diagnostic hints |
| **Standard Complexity Benchmarks** | Algorithmic reference tables | Ground-truth reference for operation counts and data structure costs | Immutable static reference; zero user telemetry |

CP Chronicles Agent complies with educational privacy standards:
- **No PII collection:** No student personal names, institutional emails, or online judge account passwords are required or stored.
- **Stateless execution:** Code reviews and complexity audits are performed ephemerally in active memory.
- **Zero commercial data mining:** User code, challenge solutions, and practice histories are never monetized or shared with third parties.
- **Right to Erasure:** All challenge tracking files and logs reside locally in the repository and are fully controlled by the user.

---

## 4. Known Limitations & Failure Modes

Reviewers, educators, and competitive programmers should note the following operational constraints:

1. **Theoretical Asymptotics vs. Hardware Cache Locality:**
   - *Limitation:* An $O(N)$ algorithm with poor cache locality (e.g. linked node traversal) may run slower in practice than a cache-friendly $O(N \log N)$ contiguous vector routine.
   - *Mitigation:* The agent highlights cache-friendly memory layouts (contiguous vectors, flat arrays) alongside theoretical Big-O classifications.

2. **Heuristic vs. Formal Proof Guarantees in Greedy/Ad-Hoc:**
   - *Limitation:* Greedy heuristics and ad-hoc constructive algorithms can pass initial samples while failing subtle counterexamples without formal exchange-argument proofs.
   - *Mitigation:* The agent mandates proof sketches (e.g., greedy exchange arguments or induction) before confirming greedy strategies as optimal.

3. **Compiler Optimization Variances Across Online Judges:**
   - *Limitation:* Online judges utilize diverse compilers (GCC vs. Clang) and optimization flags (`-O2`, `-O3`), leading to differing execution times for identical code.
   - *Mitigation:* The agent designs complexity budgets conservatively, targeting well under 50% of the judge time limit to ensure resilience across environments.

4. **Self-Reported Time and Memory Logs:**
   - *Limitation:* Student-logged execution metrics can vary widely based on local machine CPU architecture compared to online contest servers.
   - *Mitigation:* The agent measures complexity in fundamental operation counts rather than wall-clock milliseconds alone.

---

## 5. Verification, Safety & Human Oversight

- **Deterministic Asymptotic Verification:** Complexity bounds are deduced from loop structures and recursion trees through mathematical verification rather than speculative estimation.
- **Human-in-the-Loop Problem Solving:** The agent acts as an analytical guide; the student writes, tests, and submits their own code to foster genuine problem-solving capabilities.
- **Anti-Plagiarism & Competition Integrity:** System prompt guardrails refuse assistance on live, ongoing contests, upholding global competitive programming codes of conduct.
- **Kill Switch & Immutable Audit Logging:** Analysis sessions can be halted instantly; all problem evaluations and complexity audits are logged in structured JSON for educational review.
