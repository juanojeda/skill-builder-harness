# Research log

## Current best

| Timestamp  | Best score |
| ---------- | ---------- |
| 2026-04-27 | 35 / 35    |

## Changelog

| Timestamp  | Change                                                     | Score before | Score after | Decision |
| ---------- | ---------------------------------------------------------- | ------------ | ----------- | -------- |
| 2026-04-24 | Init with the AGENTS.md that describes the builder harness | ???          | ???         | N/A      |
| 2026-04-25 | Completed truncated step 2 in Main Agent: added "failure, halt progression and report failure to the caller. Do not proceed further." | 28 / 30 | 29 / 30 | [KEEP] |
| 2026-04-25 | Added "Only proceed to the evaluation loop if the Auditor agent report success." to step 2 | 29 / 30 | 29 / 30 | [REVERT] |
| 2026-04-25 | Added explicit success branch to step 2: "If the Auditor agent reports success, proceed to the evaluation loop (step 3)." | 29 / 30 | 30 / 30 | [KEEP] |
| 2026-04-27 | Added SKILL_DIR path resolution preamble to Main Agent and updated step 1 to use resolved `criteria` path. | 27 / 35 | 28 / 35 | [KEEP] |
| 2026-04-27 | Updated step 3 to use resolved path variable `best` instead of hardcoded `output/best-skill.md`. | 28 / 35 | 29 / 35 | [KEEP] |
| 2026-04-27 | Updated step 6 to use resolved path `best` instead of hardcoded `output/best-skill.md`. | 29 / 35 | 30 / 35 | [KEEP] |
| 2026-04-27 | Updated step 7 to use resolved path `candidate` instead of hardcoded `output/candidate-skill.md`. | 30 / 35 | 31 / 35 | [KEEP] |
| 2026-04-27 | Updated step 8 to use resolved path `log` instead of hardcoded `output/research-log.md`. | 31 / 35 | 32 / 35 | [KEEP] |
| 2026-04-27 | Updated step 9 to use resolved `best` and `log` instead of hardcoded paths. | 32 / 35 | 32 / 35 | [REVERT] |
| 2026-04-27 | Updated Build agent step 1 to use resolved `best` and `candidate` instead of hardcoded filenames (attempt 1). | 32 / 35 | 32 / 35 | [REVERT] |
| 2026-04-27 | Attempted multi-step fix (steps 4+9+10); build agent reported failure (two non-adjacent mutations). | 32 / 35 | N/A | [REVERT] |
| 2026-04-27 | Updated step 4 to use resolved `log` instead of hardcoded `output/research-log.md`. | 32 / 35 | 32 / 35 | [REVERT] |
| 2026-04-27 | Updated step 9 to use resolved `best` and `log` instead of hardcoded `output/best-skill.md` / `research log`. | 32 / 35 | 32 / 35 | [REVERT] |
| 2026-04-27 | Updated step 10 to use resolved `candidate` instead of hardcoded `output/candidate-skill.md`. | 32 / 35 | 32 / 35 | [REVERT] |
| 2026-04-27 | Updated Build agent step 1 to use resolved `best` and `candidate` instead of hardcoded filenames (attempt 2). | 32 / 35 | 32 / 35 | [REVERT] |
| 2026-04-27 | Updated Evaluation loop step 1 to use resolved `scenarios` instead of hardcoded `spec/scenarios/`. | 32 / 35 | 32 / 35 | [REVERT] |
| 2026-04-27 | Attempted two-change eval loop rewrite; build agent rejected (two non-adjacent mutations). | 32 / 35 | N/A | [REVERT] |
| 2026-04-27 | Updated Evaluation loop step 3 to use resolved `criteria` instead of hardcoded `spec/skill-criteria.md`. | 32 / 35 | 32 / 35 | [REVERT] |
| 2026-04-27 | Updated steps 9+10 to use resolved `best`, `log`, `candidate` instead of hardcoded paths (adjacent steps = one mutation). | 32 / 35 | 32 / 35 | [REVERT] |
| 2026-04-27 | Replaced path resolution code block to remove hardcoded `spec/` and `output/` subdirectory names (all 5 paths now resolve directly under SKILL_DIR). | 33 / 35 | 34 / 35 | [KEEP] |
| 2026-04-27 | Updated Evaluation loop step 4 table format to use proper markdown table with `Criteria` column and `Scenario N` column headers with true/false cell values. | 34 / 35 | 35 / 35 | [KEEP] |