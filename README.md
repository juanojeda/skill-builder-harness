# Skill Builder Harness

Test-driven harness for iteratively optimizing AI agent skill files.

## What it does

Takes a target skill (a markdown instruction file for an agent), a set of boolean criteria, and a set of test scenarios. Runs a mutation loop — one change at a time — keeping changes that improve the score, reverting ones that don't. Stops at 100% or after 15 iterations.

## How it works

Four agents coordinate:

**Main agent** (progression loop)
1. Auditor checks all criteria are boolean-evaluable
2. Evaluation loop scores `output/best-skill.md` against all scenarios
3. Build agent makes exactly one mutation → `output/candidate-skill.md`
4. Candidate is scored; KEEP if higher, REVERT if not
5. Repeat until 100% or 15 iterations

**Auditor** — validates that every criterion in `spec/skill-criteria.md` can be answered true/false. Blocks progression if any are ambiguous.

**Build agent** — copies best → candidate, makes one discrete mutation, diffs to confirm exactly one structural change, reports back.

**Evaluation loop** — spawns one runner sub-agent per scenario file, collects outputs, asserts each criterion, reports `X / Y criteria × N scenarios` plus a per-criterion table.

## Repo structure

```
spec/
  skill-criteria.md       # Boolean criteria the skill must satisfy
  scenarios/              # One file per test scenario
    scenario-1.md
output/
  best-skill.md           # Current best skill (gitignored)
  research-log.md         # Iteration history, scores, KEEP/REVERT decisions
AGENTS.md                 # Full agent instructions (the harness itself)
```

## Usage

Point an AI agent at this repo and tell it to run the harness. The agent reads `AGENTS.md` and orchestrates the full loop autonomously.

To adapt for a different skill:
1. Replace `spec/skill-criteria.md` with your criteria (boolean questions only)
2. Add scenario files to `spec/scenarios/`
3. Seed `output/best-skill.md` with a starting draft
4. Run the harness

## Output

`output/research-log.md` tracks every iteration: the change made, score before/after, and the KEEP/REVERT decision. `output/best-skill.md` always holds the highest-scoring version seen so far.

## Inspiration

- **Andrej Karpathy** — [μ-search / AutoResearch](https://github.com/karpathy/μ-search): iterative self-improvement loops as a general research pattern
- **Antony Marcano** — [Test-Driven Agent Behaviour (TDAB)](https://www.youtube.com/watch?v=i3g9ZXiaqh0): boolean acceptance criteria as the contract for agent outputs
