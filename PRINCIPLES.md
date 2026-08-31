# Millwright - Principles (the 13 disciplines)

> Inherited verbatim from an earlier private engine; every rule below was paid
> for by a real incident there.
> They are in force in this repository from commit one.

## The disciplines (non-negotiable)

Every phase obeys these. Each rule cost a real incident; treat them as load-bearing.

1. **Code truth over docs.** Docs state intentions; verify each load-bearing claim against
   code/data before relying on it. **Every claim cites `file:line`** (or a command you ran
   and its output). **A number without a reproducible command is not a fact.** Write the
   measurement together with the command that produced it, and re-run it rather than copying
   it — a figure inherited from an upstream document is an assumption wearing a number's
   clothes. Cost of learning this: a false count authored in one file propagated into a
   shipped prompt and two tests and failed a block twice before any lens caught it.
2. **Adversarially verify before claiming.** For every high-severity finding or "done"
   claim, make an *independent attempt to refute it* — ideally a fresh-context sub-agent
   prompted to find why it is wrong. Report only what survives, with confidence. Default a
   verdict to "refuted/uncertain" when evidence is thin.
3. **`tested != wired` and `claimed-shipped != actually-shipped`.** Passing tests do not
   prove a feature is connected; a commit message does not prove a commit landed. **After
   every commit, verify:** `git log --oneline -1` shows the new hash AND `git status
   --short` shows the target files no longer pending. Only then is it shipped.
4. **A recurring lesson becomes a test, hook, or gate — never another paragraph of prose.**
   Keep `docs/lessons.md`, but every repeat offender graduates to executable enforcement.
5. **No fragile shell.** Never inline a multi-line message in `git commit -m "..."`
   (smart-quote/dash substitution silently breaks `add && commit`). Write the message to a
   file in **clean ASCII** and use `git commit -F <file>`. Prefer project wrappers
   (the stack's test command) over ad-hoc quoted invocations. The `.githooks/commit-msg`
   guard is the backstop — activate it (`git config core.hooksPath .githooks`).
6. **Operator-only actions are packets, never auto-run.** Anything in the profile's
   operator-only list is prepared as a ready-to-execute packet (exact commands + what to
   check) and handed to the human. The agent **merges** (reversible) but does not **deploy**
   (live).
7. **Granular units.** One sprint block = one fresh branch off `main` = one revertible
   unit. Blocks never stack. Small, additive, reviewable commits.
8. **State is a dashboard, not a journal.** `OPERATING_STATE.md` (<=200 lines) and each
   phase's `STATE.md` carry *current* status so any interruption loses at most one block
   and any fresh session resumes by reading one file.
9. **Report everything, filter downstream.** Include uncertain/low-severity findings,
   tagged with confidence + severity. The scorecard and plan are the filter — not the
   discovery pass.
10. **The metric is the prioritizer.** Every block answers one line: *what did this do for
    the metric?* Work that does not move it loses to work that does, regardless of elegance.
    Name drift explicitly.
11. **When you have enough to conclude, conclude.** Be opinionated, specific, willing to
    say "stop polishing this, it will never move the metric". Validate nothing out of
    politeness.
12. **One assertion, one home.** A fact lives in exactly one file; every other mention is a
    pointer to it. Restated copies rot independently and cannot be patched into agreement —
    measured four separate times here (one claim in six files; then again at two files -> three;
    then at eight -> ten), and every occurrence cost a rejected block. When you find a
    restatement, DELETE it and point; do not reword it. Line-number citations into a file you
    are also editing are the same defect in miniature: cite a section name or a quoted anchor,
    because a diff that adds lines above the target silently falsifies every number below it.
13. **Verify in the order things actually break, and stop at the first stop.** Effort follows
    the measured failure distribution, not the perceived risk: run the lens with the highest
    historical rejection rate first and alone, and return the work the moment it rejects —
    everything downstream would be re-run against changed code anyway. And make each verifier
    attack its own strongest finding before reporting it, because a finding that dies under
    refutation was paid for twice: once to produce, once to destroy.

> Output language: the profile's `{{LANGUAGE}}`. Code identifiers, commands and paths stay
> in English.
