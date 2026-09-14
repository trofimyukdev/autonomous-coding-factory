# ADR 0005 - Model layout, and the seat that accepts a block

Date: 2026-08-19. Context: the foreman role moves into this repository from the
session of an earlier private engine that has been carrying it, and is filed as
`.claude/commands/foreman.md`. ADR 0001 decision 6 fixed the model layout for
block sessions, builder subagents and adversarial verification; it has no row for
an acceptance seat, because at the time there was none - the block session
reported to the operator directly. Decision by the blueprint author, relayed
through the foreman; **[operator-confirmable]** - it stands unless the operator
vetoes it.

## 1. The layout - this ADR is its one home

| Seat | Model | Why |
| --- | --- | --- |
| Foreman (acceptance) | Fable - the strongest tier available | judgement and independent re-measurement |
| Block session | Opus 5, effort high | builds one block end to end, holds the spec |
| Builder subagents | Sonnet | bounded production work under a spec |
| Adversarial verification | Opus | refutation is the block's own highest-value pass |
| ~~Scout (pre-flight)~~ RETIRED | ~~strongest tier available; today the foreman seat, by hand~~ | retired by M0-66, which landed as merge `95e5092`: the role is the controller's, and its model is `[models.scout]` |

The scout row was added on 2026-08-21 by operator decision relayed through the
foreman; **[operator-confirmable]** like the rest of this ADR. It is the only row
that is temporary: the seat named in it is a stand-in until `M0-66` makes
scouting an attempt role the controller dispatches, and the block that lands
M0-66 is the one that strikes the row. The account of what the missing role cost
is ADR 0009 section 6, and the hand-applied procedure is the pre-flight
paragraph of `.claude/commands/block.md`; neither is restated here.

**Retired by M0-66, which landed as merge `95e5092`: the hand-applied seat
described above no longer exists.** Scouting is an attempt role the controller
dispatches (`src/controller/dispatch.ts`, `src/controller/scout.ts`), and its
model is the `scout` entry of `MODEL_ROLES` (`src/controller/config.ts`) - a
`[models.*]` line of the consumer's configuration like every other role's, so it
is DESIGN.md section 11's to list and no longer this table's to name. The row is
struck rather than deleted because the dates are the record: between 2026-08-21
and 2026-08-25 the factory scouted by hand. Operator sanction 2026-08-25;
**[operator-confirmable]** like the row it retires.

**This table supersedes the model sentence of ADR 0001 decision 6.** The rest of
that decision - one block equals one fresh session in this repository, and
the earlier private engine's mechanics are not used - stands unchanged. One
assertion, one home (discipline 12): a session asking which model a seat runs on
reads this table and nothing else.

## 2. Why the acceptance seat gets the strongest tier

Acceptance is not production. The foreman writes no code; it re-runs the block's
own commands in the named tree, plants its own mutants, and reads the report's
prose for the failure classes this factory has actually recorded. Every one of
those recorded failures was a claim in prose rather than a defect in code:
M0-14's spec shipped a suite count that the next commit falsified (ADR 0004
section 3 names it with the command), and an external check on 2026-08-18 read a
false first-pass rate out of the gap an amend left (same section). None of them
would have been caught by more building; all of them were catchable by reading
harder.

The cost argument runs the same way. The strongest tier is the expensive one, and
the foreman is the seat where it buys the most per token: one verdict per block,
bounded by the number of blocks rather than by the size of a diff, against a
builder seat whose spend scales with the code it writes. Under the north star -
dollars per verified merged task - a wrong acceptance is the most expensive
outcome the factory can produce, because it merges and then propagates.

Adversarial verification stays on Opus rather than moving up with the foreman: it
runs many times per block, inside the block session, and its job is bounded by
the block's own diff. The foreman's is not - it is the only seat that reads the
report as a whole against a tree it did not build.

## 3. How it is applied

The layout is not enforced by code and this ADR does not pretend otherwise; it is
an operator convention until the controller launches its own workers (M1-M2), at
which point the model per seat becomes configuration and this table is what that
configuration is derived from. Today: the operator starts the foreman session on
Fable and types `/effort high` in a block session at its start, and the block
session's own subagent routing follows the table above.

## Amendment 2026-08-25 - the foreman seat gets an effort, not only a model

The table of section 1 names a model for every seat and an effort for exactly
one of them: `| Block session | Opus 5, effort high |`. The foreman row named
the tier and stopped there, so the effort of the acceptance seat was whatever
the session happened to open with, and it had to be re-agreed out loud each time
a foreman was reincarnated. It cost one round-trip on 2026-08-25 and that is the
whole reason this amendment exists.

**The foreman (acceptance) row reads `Fable 5, effort max`.** The row above is
not rewritten: the table is dated and what it said between 2026-08-19 and today
is the record, exactly as the struck scout row is kept rather than deleted.

The operator's decision, quoted in Russian for the same reason ADR 0018 section
0 quotes its sanction and ADR 0006 set the precedent - the sanction is the
authority and a translation is a paraphrase. Asked on 2026-08-25:

> Есть смысл перейти на max там у него, как и у тебя?

("Does it make sense to move him to max there too, as with you?" - `him` is
the foreman seat just reincarnated as Forman-5, opened by Forman-4 at `xhigh`;
`you` is Forman-4, which the operator had opened at max. Both sides of the
question are this table's foreman row; the block seat is not in it.) The foreman
answered yes and the operator took the answer, then closed it:

> Добавь это в инструкции, чтобы в следующий раз не пришлось повторяться про max

("Put this in the instructions so that next time there is no need to repeat
myself about max.") **[operator-confirmable]** like every other row of this
table.

Two consequences worth stating once:

- **A live session does not need to be recreated.** Effort is raised in place by
  typing `/effort max` in the session itself; only the model is fixed at open
  time. Section 3's account of how the layout is applied is unchanged otherwise.
- **The operator has already written the rule into the global
  `~/.claude/CLAUDE.md`**, which is outside this repository and is not quoted
  here. That file is where a session opening a seat reads the procedure; this
  table stays the one home of which model and which effort a seat runs on
  (discipline 12), and the two agree by pointing at each other rather than by
  restating.

## Point release 2026-09-06 - the foreman row names a point version

**The foreman (acceptance) row reads `claude-fable-5-1`, effort max.** The
amendment above is unchanged in everything but the model string: the effort was
already `max` and stays `max`, and the rows for the block session, the builder
subagents and adversarial verification are untouched. The rows above are not
rewritten, for the reason the amendment above gives about its own predecessor -
the table is dated, and what it said between 2026-08-25 and today is the record.

The operator's decision, quoted for the reason ADR 0006 set and this ADR's own
amendment repeats - the sanction is the authority and a translation is a
paraphrase. On 2026-09-06, relayed through the foreman:

> форман = claude-fable-5-1 + max

("the foreman = claude-fable-5-1 + max".) **[operator-confirmable]** like every
other row of this table.

**An incident is what made the version worth naming, and it is recorded here
rather than in a session's memory.** The machine was rebooted between 2026-09-05
and 2026-09-06, the bot restored the surviving sessions, and the foreman seat
came back SILENTLY on Opus 4.8 - a tier below the one this table names, with no
error and no notice. Nothing in the restore path asserts the model of a seat. It
was caught by the MODEL TAG in the session's own statusline and fixed by the
operator by hand, and the whole reason it was caught at all is that the tag is
read as a matter of routine.

Two consequences, both of which this ADR states and neither of which it fixes:
a fallback that is silent is a fallback nobody notices at 3am, and a table that
names a family rather than a version cannot tell a fallback from a release. The
first is a real gap with no owner in `factory/tasks/` and it is not filed by this
edit - the seat layout is an operator convention until the controller launches
its own workers, which section 3 says already, and there is nothing in this
repository's source to assert it against. The second is what this point release
closes.
