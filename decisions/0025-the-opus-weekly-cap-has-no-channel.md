# ADR 0025 - the Opus weekly cap has no channel, and the row that goes looking for one

Date: 2026-09-10. Context: a carrier session (carrier #49) by foreman decision
under the operator order quoted in section 0, not a block. `main` stood at
`22380bb` when this file was written - two carrier #49 chores above the M4-02
landing `1caf753` - and the tree was clean apart from two untracked operator
handoff files in a private archive that is not published. Nothing under `src/`, `scripts/` or
`.githooks/` was touched by this package, and `DESIGN.md` was touched by exactly
one sentence, under the sanction section 2 records.

**ONE FILE UNDER `test/` WAS TOUCHED, and this paragraph says so because the
first version of it claimed otherwise and the claim went false the moment the
package finished.** That DESIGN sentence moved the ratification digest of section
11, which `test/unit/design-ratification.test.ts` holds and which its own failing
message requires to be updated with the edit - the mechanism ADR 0006 set. Only
that one digest value and the comment above it changed; no case in that file was
touched and no other file under `test/` was. The foreman seat sanctioned that one
file on 2026-09-10 under the standing delegation, **[operator-confirmable]**, on
the precedent that carrier chores have moved that table before. Verified against
the tree rather than asserted: `git diff --stat 1caf753..HEAD` names
test/unit/design-ratification.test.ts and no other path under `src/`, `test/`,
`scripts/` or `.githooks/`.

**Why a new ADR and not an addendum.** ADR 0023 is the public showcase and the
second repository, and none of its seven sections is about the subscription
windows; ADR 0021 decision (d) IS about the rate-limit channel, but it is the
decision that gave M3-06 the contract, and that decision is executed and closed.
What is recorded here is a NEW operator decision about a promise the design makes
and the channel cannot keep, which is its own subject and gets its own file.

## 0. The order

The question reached the operator from the foreman seat on 2026-09-10 at about
11:2x, in the relay this run uses: operator <-> the foreman seat <-> this carrier. The
disclosure ADR 0018 section 0, ADR 0020 section 0, ADR 0021 section 0, ADR 0022
section 0 and ADR 0023 section 0 each make about their own sanctions is made here
too - the seat that executes an order never heard it spoken.

The question put to the operator was: DESIGN.md section 11 promises that "a
router escalating to Opus is drawing on the scarcer of the two" weekly limits,
and the factory can read only the general one. Does the design's sentence get
corrected now, or does the factory go and find the missing figure?

The answer, quoted rather than translated away, which is the precedent ADR 0006
sets:

```text
(а) сейчас и (б) отдельным рядом M5
```

"(a) now and (b) as a separate M5 row." Both halves are executed by this package:
(a) is the DESIGN sentence section 2 records, (b) is the row section 3 records.

## 1. The reading, which lives in the code and is pointed at rather than restated

**The fact has one home and it is not this file.** The docstring over
`RATE_LIMIT_FIELDS` in `src/controller/rate-limit.ts` states why the Opus weekly
window is deliberately absent from the contract, carries the two greps that
separate the statusline payload from the `/usage` snapshot, and names the trap -
this repository's own first attempt at M0-176 shipped a field, a producer and a
reader for `seven_day_opus` on the strength of the wrong one of those two greps,
and an adversarial pass caught it. Discipline 12 forbids a second copy of that
argument, so it is cited and not repeated.

**What this carrier added to it is a fresh reading on a NEWER CLI, because the
one in the docstring was taken on a version this machine no longer runs.** That
docstring measures Claude Code 2.1.263; `claude --version` printed
`2.1.267 (Claude Code)` on 2026-09-10, and the docstring's own command returns
nothing there - `grep -aoc 'co.five_hour.utilization\*100'
<claude-install>/versions/2.1.267` printed 0 the same day, because
the binary's minified shape moved. **The conclusion survives the version bump
anyway**, on a reading taken by field shape rather than by call site:
`grep -ao 'five_hour:.\{0,200\}' <claude-install>/versions/2.1.267`
printed, as its first line, the schema whose members are `{utilization,
resetsAt}` - the shape the statusline payload carries - declaring `five_hour`,
`seven_day` and `seven_day_overage_included`, and NO Opus key; the schemas that
do declare `seven_day_opus` are the `/usage`-snapshot shape, with their
`seven_day_oauth_apps` and `seven_day_sonnet` neighbours beside it. So the gap
is a property of the channel and not of the version that was measured first.

**A version-sensitive measurement is a maintenance cost this decision accepts.**
Both of the docstring's commands are pinned to an absolute path carrying a
version number, and one of them is already dead. The repair is not a wider
pattern - it is the row of section 3, whose first acceptance item is precisely to
establish whether a channel exists at all, and which would have to re-take these
readings on whatever CLI it runs against.

## 2. Decision (a): DESIGN.md section 11 says what the factory can read

**[operator-confirmable]**, and it is the FIRST edit this run has made to
`DESIGN.md` outside a ratification. The design's sentence about the two weekly
limits is TRUE about the account and stays exactly as it is; what was missing is
that the factory cannot see the smaller one. One sentence is added after the
clause that lists the statusline figures, saying that the factory reads the
general weekly cap only, that Opus routing is therefore bounded by that cap
rather than by its own, and pointing at this ADR and at the row of section 3.

**Why the sentence goes in DESIGN.md rather than only here.** ADR 0021 decision
(d) settled the general form - a contract the design underdetermines is invented
in the spec and NOT by editing the design - and this is the other case: the
design does not underdetermine anything here, it states a capability the factory
does not have. A reader of section 11 who is deciding whether to escalate to
Opus needs that fact where the escalation is described, and a pointer is the
smallest form that does not restate the argument (discipline 12).

**What the sentence is not.** It does not say the Opus window is unimportant, it
does not set a threshold for it, and it does not authorise the router to treat
the general cap as a proxy. It records a limit of the instrument.

## 3. Decision (b): one M5 row, research first

**[operator-confirmable]**. The row is `M0-197`, minted by this package into the
M5 planning band below the M4 chain, and its FIRST acceptance item is a research
result rather than a field: establish where the `/usage` snapshot can be read
from outside the interactive command, **and whether such a channel exists at
all**. The row is written so that "there is no channel" is a PASSING outcome with
a recorded finding, because the alternative - a row that can only be finished by
shipping a reader - is exactly the pressure that produced the first M0-176
attempt's decoration.

**Why M5 and not the M4 chain.** M4 is the unattended factory: wrapper, unit,
timer, breakers, notification, morning report. The Opus cap changes what the
ROUTER may spend, and the router's own economics are M5's subject in DESIGN.md
section 17. Nothing in M4 reads it, and a row placed in that chain would sit
ahead of work that unblocks the factory running at all.

## 4. What this ADR does not decide

It does not decide the shape of the field, the name of the key, or which side of
the producer boundary a `/usage` reader would sit on: those are the row's, argued
against whatever the research half finds. It does not reopen ADR 0021 decision
(d), whose contract stands unchanged. And it does not touch `weekly_reserve_pct`,
which section 11 also names and which no row has yet been filed for - that gap is
older than this one and belongs to whoever files it.
