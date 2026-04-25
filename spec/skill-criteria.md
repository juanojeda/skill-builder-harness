 ## Main agent — setup
  1. Does the skill spawn an auditor sub-agent as its first step?
  2. Does the skill pass only the path to spec/skill-criteria.md to the
  auditor, not the file content?
  3. Does the skill halt progression and report failure if the auditor reports
  failure?
  4. Does the skill proceed to the evaluation loop only after the auditor
  reports success?

  ## Main agent — evaluation gate
  5. Does the skill run the evaluation loop against output/best-skill.md before
   spawning a build agent?
  6. Does the skill stop immediately and report success when evaluation returns
   100%?
  7. Does the skill update the Current best section of output/research-log.md
  when the score exceeds the prior best?

  ## Main agent — build loop
  8. Does the skill construct the spec as all passing criteria plus only the
  first failing criterion?
  9. Does the skill pass the spec subset and the path output/best-skill.md to
  the build agent?
  10. Does the skill re-evaluate output/candidate-skill.md (not
  output/best-skill.md) after a build step?
  11. Does the skill return to step 5 if the build agent reports failure?

  ## Main agent — logging and branching
  12. Does the skill log each iteration to output/research-log.md with the
  change made, previous score, new score, and a KEEP or REVERT decision?
  13. Does the skill record KEEP only when the new score exceeds the current
  best in the research log?
  14. Does the skill replace the contents of output/best-skill.md with
  candidate-skill.md on a KEEP decision?
  15. Does the skill return to the auditor step after a KEEP decision?
  16. Does the skill discard output/candidate-skill.md on a REVERT decision?
  17. Does the skill return to step 5 (not step 2) after a REVERT decision?
  18. Does the skill stop after 15 iterations without reaching 100% and report
  the current best score?

  ## Auditor sub-agent
  19. Does the auditor assess whether each criterion in the file at the
  provided path can be answered with only true or false?
  20. Does the auditor report the specific failing criterion and a rewording
  suggestion on failure?

  ## Build sub-agent
  21. Does the build agent copy output/best-skill.md to
  output/candidate-skill.md before mutating?
  22. Does the build agent make exactly one mutation per run?
  23. Does the build agent diff candidate-skill.md against best-skill.md before
   reporting completion?
  24. Does the build agent revert to best-skill.md and report failure if more
  than one structural change is detected?
  25. Does the build agent report the specific change made back to the calling
  agent?

  ## Evaluation loop
  26. Does the evaluation loop spawn one runner sub-agent per scenario file?
  27. Does the evaluation loop pass only file paths (not content) to each
  runner sub-agent?
  28. Does the evaluation loop collect all runner outputs before asserting
  criteria?
  29. Does the evaluation loop report the score in the format: X true
  assertions / Y criteria × N scenarios?
  30. Does the evaluation loop report a per-criteria table with a column for
  each scenario?