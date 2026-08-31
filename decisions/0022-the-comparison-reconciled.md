# ADR 0022 - the comparison reconciled: what of the foreman's research has practical value

Date: 2026-08-30. Context: a carrier session (carrier #31) by foreman decision
under an operator order, not a block. `main` stood at `96c398a` when the package
began and the tree was clean apart from two untracked operator handoff files
published. Nothing under `src/`, `scripts/` or `.githooks/` was
touched by this package; `DESIGN.md` was touched at one line, which the addendum
to ADR 0021 owns.

This document is the reconciliation the operator ordered, and it is a LEDGER: it
ranks, it discards, and it points. It does not restate the research it reconciles
(discipline 12). The research itself is two foreman memory files - the designs of
2026-08-26 and the system-versus-research comparison of 2026-08-27 - which live
outside this repository, in the foreman seat's own memory directory, and are read
only. Where an item's content matters it is named in one sentence and the reader
is sent there.

## 0. The order

The comparison was set up on 2026-08-26 at about 20:45, in Russian, and the
foreman's research file quotes the operator verbatim:

```text
сам продумал то как решить все эти моменты которые тебе не нравятся, сложил в
сторону, и потом сравним результат как справилась сама система и твои изыскания,
и потом приведём к общему знаменателю
```

"Think through yourself how to solve all these things you do not like, put it
aside, and then we will compare how the system itself coped against your
research, and then bring it to a common denominator."

The comparison ran on 2026-08-27. The order to reconcile came on 2026-08-30 at
about 10:2x and is quoted verbatim for the same reason:

```text
по поводу сравнения фабрики и твоих изысканий- нужно привести к «общему
знаменателю». Ну хорошенько все обдумать теперь рассчитать, вытянуть только то
что действительно имеет практическое значение
```

"About the comparison of the factory and your research - it needs to be brought
to a common denominator. Think everything through properly now, work it out, pull
out only what really has practical value."

Both lines reached this session as a relay from the foreman rather than from the
operator's own terminal, which is stated rather than smoothed over - the same
disclosure ADR 0018 section 0, ADR 0020 section 0 and ADR 0021 section 0 make
about their own sanctions. The Russian is quoted rather than translated away
because it is the authority this document stands on; ADR 0006 sets that
precedent.

**[operator-confirmable]** applies to the rankings and the discards below, and to
nothing else: two items in section 2 carry an operator decision of their own and
say so where they stand.

## 1. What has already landed on its own

Four of the twelve measures the research designed have since been built by the
system without the research being consulted, and this section records it because
a reconciliation that re-proposes delivered work is worse than no reconciliation.
Every sha below was re-read on 2026-08-30 with `git log -1 --format='%h %s'`.

- **P1, `millwright queue --next`.** Landed as M2-26, merge `b5d1090` - "what the
  tick would take next, and the six guards nothing pinned". It prints the pick
  and every refusal with its clause, which is the whole of what the design asked
  for, and this carrier used it as its own closing check rather than the awk
  reconstruction the foreman used before it existed.
- **L0, the doctor's live readiness.** Landed as M2-25, merge `6bc0230` - "what a
  live tick would refuse at, and the two things the first attempt got wrong".
- **L2/L3, M0-129 above M2-12.** The raise and the dependency edge were filed by
  carrier #21 and are delivered: M0-129 stands DONE at priority 87 and M2-12
  names it in its `dependencies`, both read on 2026-08-30.
- **A1's FORM, though not its content.** M0-134 is filed and open at 79. It owns
  the question "what number does `quality_attempts` take", and the research's
  answer is an input to its block rather than a competing spec - see section 2
  item (7).

The remaining eight are what section 2 and section 3 dispose of.

## 2. What has practical value, ranked by dollars per verified merged task

Seven items. The ranking is the operator's question answered directly: what
returns the most per verified merged task. Nothing here is minted that this
package did not mint, and nothing here is a restatement of the research.

### (1) A deterministic mutation probe over the changed files, BEFORE the LLM verifier

**Sanctioned by the operator on 2026-08-30 at about 10:55, verbatim:**

```text
Санкционирую мутационный прогон «как план-строку M3»
```

"I sanction the mutation run as an M3 plan row." That is an operator decision and
is therefore not marked [operator-confirmable]. This section is its one home, and
the two rows it authorises - **M3-12** at 99 and **M3-13** at 98 - carry their own
outcomes and are not restated here.

The design already has the slot: DESIGN.md section 8's stage 5 trigger row ends
"weak suite -> test strength (mutation probe or reproduction test)". Nothing
implements it. On 2026-08-30 `grep -n -i mutation DESIGN.md` printed two lines,
that row and an unrelated sentence about not mutating the base branch, and
`grep -n '"scripts"' -A 8 package.json` printed seven scripts and no mutation
tool.

The fact of the day is what moved this to the top of the ranking. On 2026-08-30
the SECOND adversarial pass of two separate blocks found a weakness in the TESTS
rather than in the logic - `git log -1 --format='%h %s' 41ef43a` printed "fix:
M2-16 - the open half of the band is pinned, and the excused case says so", and
the same command on `e32e49d` printed "test: M0-07 - the boundary of the allowed
set was the one thing nothing measured". Both are exactly what a probe finds for
free, and both cost a full LLM pass to discover. The verifier passes took the
larger part of both blocks' walls; that proportion is the foreman's stopwatch
over the two blocks and not a command's output, so it is stated as an order of
magnitude rather than as a measurement, the way ADR 0018 decision (g) states its
own.

**One carrier or operator item is left open by the split and is recorded here so
it is not lost.** M3-13 is forbidden to edit `.claude/commands/block.md`, because
two open rows already claim that file - M0-134 and M0-30 - and a third writer is
the defect discipline 12 measures. The sentence the ritual owes is "before the
adversarial verifier, run the probe and put its survivors in the prompt", and it
belongs to whichever of those two rows lands first, or to a carrier once M3-13
has landed.

### (2) A live rung 1, with money, on a consumer repository rather than on the factory's own

The factory has run two attempts in its life and the soak ladder's first rung has
not run since 2026-08-23; every one of this repository's landings is hand-run.
That is the single largest blind spot the comparison found, and it is the one
that neither more fixtures nor more prose can close.

What is new since the research is that the obstacle is now measured rather than
suspected, and it is structural: `node dist/cli.js doctor` on 2026-08-30 printed,
inside `live.readiness`, that a live tick on THIS repository would refuse at
`pick.factory_admin`, because every task in the band writes inside the paths the
factory's own core holds and no promotion producer exists (open spec M0-101). So
a live rung 1 on millwright's own queue cannot succeed by construction, and a
live run has to happen on a consumer repository.

**Which repository is the operator's decision and this document does not take
it.** The first (private) consumer is the one named by the private CLAUDE.md and by DESIGN.md
section 4. Recorded as the next point of proof, and as the item whose absence
makes every claim about the factory's economics an estimate.

### (3) `millwright evidence <id>` - the report's machine section

Minted by this package as a spec, so the argument lives there and only the
ranking is here. It is third because it converts a class of defect this
repository produced TWICE on the morning of 2026-08-30 - an evidence line that
cannot be pasted into a shell - into a command's output. Both instances were
empty documentation commits that fixed nothing but their own evidence:
`git log -1 --format=%s 947e3dd` printed "docs: the evidence line 7a6dbf1 wrote
names a file that did not exist when it ran" and the same command on `d36f6c9`
printed "docs: M0-111 - the saving's evidence line in 57287fc cannot be pasted
into a shell", both on 2026-08-30. The measurement gate checks that a number has
a command and a date near it; it does not check that the command runs.

### (4) Carrier cadence, and a filing threshold

**A seat rule, decided here, [operator-confirmable].** At most one carrier
session per four merge blocks; and a finding with no consumer in the current or
the next milestone becomes a line in a ledger rather than a spec.

The exception is named rather than hidden, because this package violates the
cadence: carriers #29, #30 and #31 ran one-to-one with blocks. The reason is a
milestone exit - the M2 chain was consumed on 2026-08-30 and gate G1 stood red
until `947e3dd`, so there was planning work and not merely tidying work to do.
A milestone exit is the case the cadence rule is suspended for, and it is the
only one.

### (5) `findings_net_7d` in `millwright status`

Minted by this package as a spec; the argument is there. It is fifth because it
is cheap and diagnostic rather than corrective: gate G1 catches the FLOOR of the
queue - whether plan work outranks findings - and nothing at all watches the RATE
at which findings arrive. The rate is what produced the drift ADR 0018 measured,
and the factory currently cannot print it.

### (6) The auto-mode prompt, globally

Two sessions stalled on 2026-08-30 waiting on a Claude Code menu rather than on
work - carrier #29 and block67, both reported by the foreman from its own
observation of the panels rather than by a command, which is why no timestamps
are asserted here. The fix is a Claude Code setting and therefore the operator's
act; a session cannot change the setting that is blocking it. Recorded as the
operator item it is.

### (7) The research's counting rule for `quality_attempts`, as an input to M0-134

The research states a rule: `quality_attempts` is the number of fix cycles, one
per verifier pass that returned a finding the block then fixed, of ANY class
(logic, test-only, own-diff comment), with a clean first pass counting zero; the
cycle boundary made derivable by a per-commit marker rather than by reading
subjects; and the derived count recorded BESIDE the declared one rather than
replacing it.

M0-134 is the spec that owns the question, and its own text forbids anyone but
its block to answer it. So this is filed as an INPUT: a pointer added to M0-134's
comment block by this package, naming this section as the pointer's home, and
adding no acceptance item and no anti-criterion. The block argues with it against
ADR 0002 and against the controller's own charge, and may refuse it.

## 3. What is discarded, and why

Four of the twelve. Each is dropped with its reason, because an unrecorded
discard comes back as a proposal.

- **F1, a risk-first tie-break inside a priority slot, with the ADR 0003
  amendment it needs.** Discarded. The measurement that motivated it was an
  eleven-row tie at 79 with a security row running fifth. With a plan at the top
  of the band, the pick is decided by priority long before the tie-break is
  reached: on 2026-08-30 `node dist/cli.js queue --next` selected the top of the
  chain at rank 1 and refused everything below it on a clause, not on a tie. The
  tie-break by id stays, and amending a ratified decision to reorder rows nothing
  is about to pick is cost with no return. **[operator-confirmable]**, and it is
  the operator's own open question 1 from the comparison, answered here rather
  than left standing.
- **F3, "sliding homes" written up as a sixth rule of ADR 0004 section 2.**
  Discarded as a paragraph. The practice is real and this repository does it
  constantly - a repeating finding is raised on the class's existing row rather
  than filed as a sibling - but a paragraph executes nothing, and discipline 4
  says a recurring lesson becomes a test, hook or gate and never more prose. The
  executable form the research itself proposed needs a declared `finding_class`
  field that does not exist. Left as practice until the field does.
- **L4, the list of classes fixture-only proofs are blind to** - packed refs, the
  StopFailure channel, a full disk, an offline install in a fresh clone.
  Discarded as a filing target. Every one of them is closed by item (2), a real
  run, and none of them is closed by another fixture. Filing four rows to
  describe what a live tick would find in an afternoon is answering a blind spot
  with paperwork.
- **F2, re-striping the findings band.** Discarded, and it was already agreed on
  2026-08-27: a raise re-issues the row and `specHash` covers the whole spec, so
  a re-stripe of the band would supersede scores of rows and falsify every
  cross-spec sentence about priorities in the queue. Recorded here only so the
  discard has one home.

## 4. What this ADR does not decide

- The content of M3-12 or M3-13 beyond their slots and their seam. Each spec is
  the home of its own outcome.
- What `quality_attempts` counts. That is M0-134's, by its own text.
- Which consumer repository the first live rung runs against, and when. That is
  the operator's, and item (2) is where the question stands.
- Anything about the foreman's research beyond the twelve measures the
  comparison enumerated. This document ranks what was compared; it does not
  reopen the comparison.
