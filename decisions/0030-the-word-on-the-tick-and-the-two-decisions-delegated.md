# ADR 0030 - The operator's word on the tick of 2026-09-22, and the two decisions delegated to the seat

Date: 2026-09-22. Context: a carrier session (carrier #69) by foreman decision
under the standing delegation of 2026-08-25, not a block. `main` stood at
`d20571a` when the package began - `git rev-parse HEAD origin/main | cut -c1-7 | paste -sd' '`
printed `d20571a d20571a` on 2026-09-22 at 07:08 - and `git status --short | wc -l`
printed 2 the same minute, the two operator handoffs in a private archive
that is not published.
Nothing under `src/`, `test/`, `scripts/`, `.githooks/`, `factory/checks.yaml`,
`factory/millwright.toml`, `CLAUDE.md`, `PRINCIPLES.md` or `DESIGN.md` was
touched by this package.

**This document records operator words and what they decide. It carries no
mechanism: each decision below has its home in a row and in the code that row
landed, and the rows this package minted or raised are named in its commit
messages.**

## 0. The operator's words, and the questions they answer

On 2026-09-22 between about 06:30 and 06:36, typed in the foreman's session,
and relayed operator -> the foreman seat, the same session that carried each
word out -> the seat's journal -> this carrier. Quoted verbatim on ADR 0005's precedent,
Russian as typed and with the typing kept as it is, because they are the
authority this document stands on.

The first came after the seat answered the operator's morning question
whether the tick was already running: it was not, and it needed one sentence
typed in that session.

```text
запусти тик
```

"Start the tick."

The second is one message of two numbered lines, answering items (b) and (c)
of a three-item list the seat had put; item (a) was the tick, already
answered above.

```text
2. Подумай еще раз, и прими оптимальное решение, основная цель отработаю щая фабрика
3. Проверь ещё раз, и сделай Push если ты уверен что всё в порядке
```

"2. Think again, and take the optimal decision; the main goal is a working
factory." "3. Check again, and do the Push if you are sure everything is in
order." Item (b) asked the operator to confirm two decisions the seat's list
carried as [operator-confirmable]: M0-231's shape and M0-232's reading of a
breach. Item (c) was the push of the prepared refresh of the public showcase.

## 1. The decision

### (1) One tick, by the seat's hand, and what it measured

The first sentence authorises ONE tick on `repo-truth`, started by the seat in
the session that heard it. ADR 0029 section 1a covered one tick, and its
section 2 left "A second pass of the tick, or a campaign" undecided; this word
covers exactly one more. It is bounded, as that one was, by the phrase of
ADR 0027 section 7, "ONE tick, not a campaign", with the spend bounded by the
ceiling the caller passes and by the standing weekly pacing rule, neither of which this
word enlarges.

The tick ran as `M5-03-20260922T033306Z` and its result is a fact of that
repository's journal, which is its one home. From `repo-truth`'s working
directory on 2026-09-22, `sed -n '290p' factory/state/events.jsonl` printed
the `GATE_FAILED` of candidate `e8991d7b` whose condition 2 carries "2 of 45
measured", and `sed -n '294p' factory/state/events.jsonl` printed
`RUN_FINISHED` with `"verdict":"dispatch_tempfail"` and `"exit_code":75`. The
refusal confirmed no finding. Where the task stands since is live state and is
not recorded here. A further tick is a further word.

### (2) Two decisions delegated, and what the seat decided under them

The second sentence does not choose between the options of item (b). It hands
the choice to the seat and names the criterion: a working factory. The two
decisions below are therefore the SEAT's, taken under that criterion on
2026-09-22 and recorded in the seat's journal entry "OPERATOR WORDS 2026-09-22
06:3x", which holds its arguments in full; the operator's word is their
criterion and not their content. The precedent is ADR 0021 section 4 (ii),
where the operator was asked a question and answered "хорошенько подумай и
прими правильное стратегическое решение сам" ("think it through properly and
take the right strategic decision yourself"), and the foreman took the
decision and recorded it as its own. Each decision stays
[operator-confirmable]: the operator may reopen either with a word.

**M0-231's shape (a) is confirmed: a home of its own for every seat a pass
opens.** It closes the shared-home defect before the first live merge, and
neither alternative was safer: one would wipe a reviewer's scratch under a
seat its wall cancelled, the other would close only the tools it names.

**M0-232's reading of a breach is confirmed as it landed.** Four questions
were open, and the seat answered each.

- *By name, not by the fence's prefixes.* A breach is a refused
  `factory_admin` or `gates_enabled` condition of stage 1. Stage 1 is where
  `DESIGN.md` states the rules about the change itself - section 8, stage 1:
  "diff within `allowed_paths`; forbidden paths untouched", "factory gates and
  config not disabled; only a `factory_admin` task may change the factory's
  own core". The fence is a different layer - section 13, "A `PreToolUse`
  policy hook checking capability invariants, not just command names" - and a
  reading keyed on its prefixes would measure the fence instead of the policy.
  A consumer task that has to edit its own gate paths names them in
  `allowed_paths`, so declared work is not counted. (The journal entry puts
  this argument under section 13; the stage-1 rules are section 8's row, and
  section 13 is quoted here only for the fence layer.)
- *Secrets stay out of the count.* A secret is content, not a path; the
  reading is reopened only if the operator wants it counted.
- *`error` counts as well as `fail`.* It is the conservative direction - the
  rung's threshold is reached later, never sooner - the same reading the
  ladder already gives an unreadable refusal record, and the count is printed
  by `ladder status` as `fact.policy_breaches`, so a transient hold is a fact
  the operator sees.
- *The `FACTORY_ADMIN` exception by class, as landed.* The acceptance of
  M0-232 found it wider than the sentence that justifies it; that finding is
  kept in the seat's dashboard and is unreachable until something supplies a
  promotion.

The sentence all four readings serve is `DESIGN.md` section 18: "promoted on
an agreed number of tasks with zero policy violations". The definition itself
lives where M0-213 and M0-232 put it, in src/controller/ladder.ts, whose
docstrings and cases are its home and are not restated here.

### (3) The showcase push

The third sentence was carried out in another repository: after its own
re-check, the seat fast-forwarded the public showcase's `main` to `7f0e7bd` at
06:36 on 2026-09-22. It is mentioned only because it arrived in the same
exchange, as ADR 0029 section 1a mentions the refresh of its own evening.

## 2. What this ADR does NOT decide

- **A campaign of ticks.** Section (1) covers one tick. The ladder's rung 2
  wants ten judged tasks (`tasks_per_rung` in src/controller/config.ts,
  default 10; `repo-truth` sets no other), and whether ticks run as a
  campaign once the mutant
  ceiling is fixed is an open question for the operator.
- **How the mutant ceiling is fixed.** The tick's refusal named it; the row
  that owns it names the shapes known on the day and prescribes none.
- **Whether candidate `e8991d7b` is accepted.** The gate refused it and it is
  kept; no word touched it.
- **The wall's numbers.** Unchanged, and M0-195's.
- **The mechanism of any row this package minted or raised.**

## 3. What is filed elsewhere

The rows this package minted or raised are named in its commit messages and are
not listed here, for ADR 0020 section 3's reason: a decision document that
carries a backlog acquires two homes for every row in it.
