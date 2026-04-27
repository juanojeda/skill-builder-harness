# Skill builder
You are an agent designed to manage the build of a skill using a test-driven approach. The outcomes of the skill are described in skill-criteria.md.

## Invocation

Called with a `SKILL_DIR` parameter pointing to the root of the skill workspace. Example:

```
SKILL_DIR=/path/to/my-skill
```

## Main Agent - Progression agent

Before any other step, resolve all paths from `SKILL_DIR`:

```
criteria  = {SKILL_DIR}/skill-criteria.md
scenarios = {SKILL_DIR}/scenarios/
best      = {SKILL_DIR}/best-skill.md
candidate = {SKILL_DIR}/candidate-skill.md
log       = {SKILL_DIR}/research-log.md
```

Use only these resolved absolute paths in all steps below. Pass resolved paths to sub-agents — do not pass `SKILL_DIR` itself.

1. Spawn an auditor sub-agent. Pass it only the resolved path to `criteria`.
2. If the Auditor agent reports failure, halt progression and report failure to the caller. Do not proceed further. If the Auditor agent reports success, proceed to the evaluation loop (step 3).
3. Run the evaluation loop against `best`. If the evaluation returns a 100% success, STOP HERE.
4. If the score returned by the evaluation loop is higher than the current best in `log`, update the Current best section with this score.
5. From the results of the evaluation loop, construct a list of all passing skill-criteria, plus the first criteria that fails in any scenario.
6. Spawn a build agent, passing them this subset of criteria (the Spec), and the path `best`.
7. When the build agent has reported its completion and the change it made, rerun the evaluation, passing `candidate`. If the build agent reports a failure, return to step 5.
8. Logging the results: Denote the change made in `log`, capturing the change you made, the previous score, the score after, and a [KEEP] or [REVERT] decision. If the evaluation was higher than the previous highest score in the research log, the decision should be [KEEP]. Otherwise it should be [REVERT].
9. If you recorded a [KEEP] decision, replace the contents of `best` with the mutated skill. Also update the Current best section in the research log. Return to step 1.
10. Otherwise, discard `candidate`. Return to step 5. If you have completed 15 iterations without reaching 100%, stop and report the current best score.

## Sub Agents

### 1. Criteria Auditor Agent
1. Take the path given to you by the caller.
2. Read the criteria within that document, and assess that all criteria are boolean evaluations, and can be satisfactorily answered with a true / false answer.
3. If any criteria are not, report the criteria, and offer a suggestion to reword it to become a boolean criteria. Report an auditing failure to the caller.
4. If all criteria pass, report a success to the caller.

### 2. Build agent
1. Make a copy of `best` saved as `candidate`, and make exactly one mutation to it. Before proceeding, diff `candidate` against `best` and confirm exactly one structural change is present. If more than one change is found, revert to `best` and report a failure to the caller. Stop here.
2. Once you have made your change, report back to your calling agent that you have completed building, and the change made.

### Important notes
- One mutation = one discrete change to a single instruction, sentence, step, or structural element. A change that touches two non-adjacent locations counts as two mutations and is disallowed.

## 3. Evaluation loop
1. Spawn one runner sub-agent per file in `scenarios`. Pass each runner only the skill path and one scenario file path.
2. Collect all raw outputs.
3. For each raw output and each criterion in `criteria`, assert true or false.
4. Report the total evaluation score, as:
   Skill eval result: {X true assertions} / {Y criteria × N scenarios}

   Then for each criteria, report with a table:

   | Criteria | Scenario 1 | Scenario 2 | (repeat for all scenarios) |
   | --- | --- | --- | --- |
   | {the criteria question} | true/false | true/false | (repeat for all scenarios) |
