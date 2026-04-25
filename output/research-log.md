# Research log

## Current best

| Timestamp  | Best score |
| ---------- | ---------- |
| 2026-04-25 | 30 / 30    |

## Changelog

| Timestamp  | Change                                                     | Score before | Score after | Decision |
| ---------- | ---------------------------------------------------------- | ------------ | ----------- | -------- |
| 2026-04-24 | Init with the AGENTS.md that describes the builder harness | ???          | ???         | N/A      |
| 2026-04-25 | Completed truncated step 2 in Main Agent: added "failure, halt progression and report failure to the caller. Do not proceed further." | 28 / 30 | 29 / 30 | [KEEP] |
| 2026-04-25 | Added "Only proceed to the evaluation loop if the Auditor agent reports success." to step 2 | 29 / 30 | 29 / 30 | [REVERT] |
| 2026-04-25 | Added explicit success branch to step 2: "If the Auditor agent reports success, proceed to the evaluation loop (step 3)." | 29 / 30 | 30 / 30 | [KEEP] |