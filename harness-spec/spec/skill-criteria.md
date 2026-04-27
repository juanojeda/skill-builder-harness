## Parameterized workspace
1. Does the harness complete without error when invoked with SKILL_DIR=./harness-spec?
2. Does AGENTS.md contain no hardcoded references to spec/ or output/?
3. Does the main agent resolve all file paths from SKILL_DIR before passing them to sub-agents?
4. Do sub-agent instructions contain no reference to SKILL_DIR?
5. When invoked with SKILL_DIR pointing to an external skill dir, does harness-output/ remain unmodified?

## Main agent — setup
6. Does the skill spawn an auditor sub-agent as its first step?
7. Does the skill pass only the resolved path to the criteria file to the auditor, not the file content?
8. Does the skill halt progression and report failure if the auditor reports failure?
9. Does the skill proceed to the evaluation loop only after the auditor reports success?

## Main agent — evaluation gate
10. Does the skill run the evaluation loop against the resolved path to best before spawning a build agent?
11. Does the skill stop immediately and report success when evaluation returns 100%?
12. Does the skill update the Current best section of the log when the score exceeds the prior best?

## Main agent — build loop
13. Does the skill construct the spec as all passing criteria plus only the first failing criterion?
14. Does the skill pass the spec subset and the resolved path to best to the build agent?
15. Does the skill re-evaluate the resolved path to candidate (not best) after a build step?
16. Does the skill return to step 5 if the build agent reports failure?

## Main agent — logging and branching
17. Does the skill log each iteration to the resolved path to log with the change made, previous score, new score, and a KEEP or REVERT decision?
18. Does the skill record KEEP only when the new score exceeds the current best in the research log?
19. Does the skill replace the contents of best with candidate on a KEEP decision?
20. Does the skill return to the auditor step after a KEEP decision?
21. Does the skill discard candidate on a REVERT decision?
22. Does the skill return to step 5 (not step 2) after a REVERT decision?
23. Does the skill stop after 15 iterations without reaching 100% and report the current best score?

## Auditor sub-agent
24. Does the auditor assess whether each criterion in the file at the provided path can be answered with only true or false?
25. Does the auditor report the specific failing criterion and a rewording suggestion on failure?

## Build sub-agent
26. Does the build agent copy best to candidate before mutating?
27. Does the build agent make exactly one mutation per run?
28. Does the build agent diff candidate against best before reporting completion?
29. Does the build agent revert to best and report failure if more than one structural change is detected?
30. Does the build agent report the specific change made back to the calling agent?

## Evaluation loop
31. Does the evaluation loop spawn one runner sub-agent per scenario file?
32. Does the evaluation loop pass only file paths (not content) to each runner sub-agent?
33. Does the evaluation loop collect all runner outputs before asserting criteria?
34. Does the evaluation loop report the score in the format: X true assertions / Y criteria × N scenarios?
35. Does the evaluation loop report a per-criteria table with a column for each scenario?
