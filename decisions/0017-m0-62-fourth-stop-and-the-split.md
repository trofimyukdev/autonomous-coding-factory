# ADR 0017 - M0-62 stopped a fourth time, and the operator split it

Date: 2026-08-24. Context: M0-62, re-issued a fourth time after ADR 0016, built
five commits on `m0-62-fence-v4`, closed both findings that stopped the third
attempt, spent both quality attempts its own spec authorises, and was stopped at
`BLOCKED`. Nothing was merged. The branch is published as
`origin/fence-attempt-4-2447da0`. This ADR is the record, written by a carrier
session for the reason ADR 0010, ADR 0012, ADR 0013, ADR 0014, ADR 0015 and ADR
0016 were: a stop that exists only in a session dialogue is invisible to the
next session that opens this repository.

It is also the answer to ADR 0016 section 7, which handed the operator one
question and nobody else. The foreman escalated it after the fourth stop and the
operator answered on 2026-08-24: **SPLIT**. Section 4 is the shape, section 5 is
which half keeps the id.

## 1. What was decided

**(a) The stop was taken at the limit, not past it.** `factory/tasks/M0-62.yaml`
sets `budget.quality_attempts: 2`, the block spent both, and the second
independent pass returned a finding against the branch as the last fix left it.
A third cycle would have been a spend the spec does not authorise. The foreman
re-measured the stop in full and accepted it.

**(b) It is the FOURTH stop of this one task**, after ADR 0010, ADR 0013 and ADR
0016. What is new is not the count but the SHAPE of the last two: neither was a
fix-cycle regression. Both were one more unlisted name of the same class - an
executable whose own flags run a program, absent from the table that judges
them. `find -rm` stopped nothing (the block closed it inside its own cycle) but
`sed`, `tar` and `rg` did. Section 3 is the finding.

**(c) The operator split the task, and the split is not a re-issue.** A fifth
attempt under one id was refused by the foreman before the question was asked -
the standing line of this run is that a fourth stop escalates rather than
re-issues. The split is the operator's answer and this ADR carries it.
**[operator-confirmable]** - it stands unless the operator vetoes it, in the form
ADR 0012 through ADR 0016 use.

**(d) The acceptance of the half that lands now is re-scoped**, and that is the
load-bearing decision of this ADR. Preventing a write that an executable
performs through shell grammar becomes best-effort **DETECTION**, and stops
being a fail-closed guarantee. Section 4 is the argument; it is the same
argument ADR 0010 made about the layer, applied to what remains of the layer
after M0-73 landed.

## 2. What the fourth branch built, and what it measured

The branch is not a description of a problem. Both findings that stopped the
third attempt are closed on it, a third class was found and closed inside its
own fix cycle, and the live vector was proved a third time - this time on a
sandbox with no relaxation in it. The figures below are the block's own, quoted
from the bodies of its commits together with the commands those bodies carry;
what this carrier session re-took itself is structural, by `git show <ref>:<path>`
and `git grep <ref>`, and it says which is which.

**F1 of ADR 0016 is closed, and closed in ONE body.** The writing flag's target
now goes through `judgeWord` - the same function every other word goes through -
so `pathCandidates` and `checkExpansion` both run on it, and a caller cannot opt
out of either. The raw `checkPath` stayed BEFORE that shared body rather than
instead of it, because the first fix for F1 deleted it and reopened a narrower
case: this carrier session read the branch's own commit body for `2447da0`,
which records that `find <abs> -fprint -fprint` at a cwd outside the workspace
went from a `workspace_containment` refusal to ALLOW when the line was gone.

**F9 of ADR 0016 is closed, and the block states which of the two answers it
took.** The suite is green without a build; nothing was skipped. Every
`runShadow` call site in `shadow.test.ts` states its hook script through the
seam `controller/workspace.ts` documents, and `compiledHook()` in
`policy.test.ts` now rebuilds when the newest mtime under `src/` is newer than
the compiled hook - so a `dist/` from another commit is a stale gate rather than
an accepted answer. From the body of `48b2497`: in a worktree with no dist
directory, at that commit, on 2026-08-24, `npm test` printed Test Files 22
passed (22) and Tests 1344 passed | 4 skipped (1348).

**A third class was found and closed inside the block's own fix cycle, and it is
the class that later stopped the branch.** `CODE_BEARING_FLAGS.find` was built
from GNU find's actions, and the `find` a worker gets is not GNU find. From the
body of `2447da0`: `find --version` printed bfs 4.1.1 on 2026-08-24 in this
repository's own shell, while `/usr/bin/find` is GNU findutils 4.10.0; in a
temporary tree on 2026-08-24, `find factory -rm` exited 0 and `factory/` was
gone, while the same tree's `find factory -delete` is refused by the fence. The
lesson became a gate rather than a name: section 24 of `test/unit/policy.test.ts`
reads the bfs binary's own `Actions:` section back and fails BY NAME on any
action flag neither table classifies and the file does not list as harmless.

**The live vector was proved on an honest sandbox.** From the body of `4fe687c`:
against claude 2.1.241 - `claude --version` printed 2.1.241 (Claude Code) on
2026-08-24 - with the operator's AppArmor profile applied the same day and NO
`security.sandbox_allow_all_unix_sockets` relaxation anywhere,
`MILLWRIGHT_LIVE_BACKEND=1 npx vitest run test/unit/policy.test.ts` printed 107
passed on 2026-08-24. The operator's tree gained nothing: the same body records
`ls -1 ~/.claude/projects/ | grep -c tmp-millwright` printing 12 before the live
lane and 12 after it on 2026-08-24.

**And the suite is green on the branch.** From the body of `2447da0`: `npm test`
printed Test Files 22 passed (22) and Tests 1350 passed | 3 skipped (1353) on
2026-08-24 in the control checkout, and `npx vitest run
test/unit/policy.test.ts` - the spec's own `measure` command - printed 110
passed and 2 skipped on 2026-08-24.

## 3. Why the stop

One finding is the stop, and it is one sentence long.

### The finding, high

`sed`, `tar` and `rg` are on `TRANSPARENT_EXECUTABLES` and their
program-bearing flags are on no list at all, so each of them runs an arbitrary
program named in its own argv and the fence returns ALLOW. The block's own
report gives the shape: `sed '1e rm -rf factory' a.txt` is ALLOW and really
removes the protected tree, while `rm -rf factory` is refused. `sed` also
carries the `s///e` modifier; `tar` carries `--to-command`,
`--use-compress-program` and `-I`; `rg` carries `--pre` and `--hostname-bin`.

This carrier session re-took the structural half on 2026-08-24, without moving
the checkout:

```text
git show origin/fence-attempt-4-2447da0:src/backend/fence.ts | sed -n '/export const CODE_BEARING_FLAGS/,/^};/p' | grep -oE '^  [a-z0-9]+:' | tr -d ' :' | tr '\n' ' '
node deno bun python python3 perl ruby find
```

Those are every key the table has. `sed`, `tar` and `rg` are not among them, and
all three appear in `TRANSPARENT_EXECUTABLES` in the same file at the same ref.

**It is not a regression of this block.** The block said so and the reading
holds: the hole is equally open on `origin/fence-attempt-3-3b46a74`, and no
commit of the fourth branch touched either list except to add `-rm` to `find`.

**It is the same shape as the finding the block closed itself**, one executable
further out. That is the measurement this ADR exists to carry: the fence's
executable grammar is not a thing a block finishes, it is a thing a block
extends, and the extension has no natural end that a budget can be sized
against.

### The two LOW findings, filed rather than fixed

**The section-24 gate can switch itself off in silence.** `bfsActionFlags()`
extracts action flags with `/^ {2}(-[a-z0-9]+)/`, and when that yields nothing
it returns a skip reason; the `it.skipIf` above the assertion then turns the
whole gate off, and the only remaining test asserts that the skip reason is a
non-empty string. So a change to the regular expression - or a bfs release that
indents its help differently - leaves the suite green with the gate dead. This
carrier session read that on the branch on 2026-08-24 by `git show
origin/fence-attempt-4-2447da0:test/unit/policy.test.ts` around its section 24.

**The comment on the restored raw `checkPath` overstates order.** It says "The
order matters and so does having both". Having both is real - the block paid a
finding for deleting the first one. The ORDER is not: both branches return on
the first deny, so swapping them changes no rule, only which reason text the
worker is shown. A comment that claims a load-bearing property the code does not
have is discipline 1 pointed inward, which is exactly what the same branch was
caught by once already.

Both are filed as a spec of their own, named in section 6.

## 4. The split, and the acceptance that changes with it

The operator's answer to ADR 0016 section 7 is a split into two tasks, along the
seam the last two stops drew themselves.

**Task A - the journal, the detection, and the flag families that have readers.**
This is everything the four attempts actually BUILT and that works: refusals
that name their class, a policy read from the consumer's `factory/policy/` that
fails closed when it is missing, the refusal journal in the worker's own `HOME`
read back into `POLICY_REFUSED` events by `src/controller/shadow.ts`, the four
declared flags each with a reader, the hook's own timeout, the glued-value
grammar, and the `find` family - which is complete, gated against its own
binary's help, and proved live. It lands NOW, from
`origin/fence-attempt-4-2447da0`, as defence in depth.

**Task B - the executable grammar, extended.** `sed`, `tar` and `rg` today, and
whatever the next reader of a `--help` finds tomorrow. Low band, and explicitly
never a reason to stop a block.

**What changes in Task A's acceptance, and why.** Under the old edition, a
worker writing a protected file through an executable's own grammar was a
`protect_factory_files` failure - a fail-closed guarantee broken. That framing
is what made a single unlisted executable name a stop-shaped finding, and it has
now produced two stops in a row.

It is also, after M0-73, false where it matters. The real prevention boundary is
the operating system, and it landed: the sandbox denies the write whoever asked
for it and whatever spelled the request, and it does not need to have heard of
`sed`. What this layer does that no sandbox does is SEE the attempt and name the
task and the rule that refused it - which is the input to the soak ladder's
"zero policy violations" condition (DESIGN.md section 18). ADR 0010 moved the
boundary; this ADR moves the CLAIM to match, four attempts later.

So under the re-scoped acceptance:

- prevention of a write via shell grammar is **best-effort detection**, not a
  guarantee, and the spec says so in its own words rather than leaving a reader
  to infer it;
- a named executable whose program-bearing flags are absent from the tables is a
  **logged coverage gap**, filed as Task B - not an anti-criterion that stops
  the block;
- what remains fail-closed is what genuinely is: a missing or unreadable policy
  file, an executable that is not on the allowlist at all, and a refusal that
  leaves no record. Those three are unchanged.

**And the branch passes as it stands.** That is the test of whether the
re-scoping is honest rather than convenient, and it is stated as a claim this
package can be refuted on: under Task A's re-scoped acceptance, nothing on
`origin/fence-attempt-4-2447da0` needs to change for it to be accepted. The
block that lands it re-measures that itself; this ADR does not assert the
verdict.

## 5. Which half keeps the id, and why

**Task A keeps `M0-62`.** M0-69 declares `M0-62` among its dependencies, and it
names precisely what it is waiting for: `GATE_PATHS` is a list in millwright's
source, DESIGN.md section 4 gives that list to the consumer's `factory/policy/`,
and M0-69's own `not_done_if` forbids building a second reader - "a policy
reader is built here rather than used from M0-62". The reader is Task A's. Task
B has no reader in it at all. Giving the id to Task B would leave M0-69 pointing
at the flag tables and waiting for a thing that is not its dependency.

Task B is filed under a new id, `M0-94`. Nothing depends on it, which is the
whole point of where it sits.

## 6. What else is in this package

Six items, each `[operator-confirmable]` with its date and reason in a comment
beside the field it changes:

- **M0-66 raised to 81.** Scouting as an attempt role is the mechanism that
  decomposes a task before a branch is cut, and four stops of one task is the
  measurement that argues for it. Its three dependencies are DONE, so the raise
  is schedulable and not symbolic. It sits directly below M0-62 and above
  M0-75, which amends the post-M1.5 run order on the same operator sanction
  that ordered the raise.
- **M0-95, priority 67** - an EVIDENCE line that is green only in a built tree.
  F9 of ADR 0016 is the incident: a commit body carried a suite count that was
  true of a built checkout and false of a fresh one, and the correction had to
  live in an ADR because a commit body cannot be edited.
- **M0-96, priority 51** - a claim of impossibility with no reproducible
  attempt behind it. Two incidents: the `tree` finding the third attempt refused
  correctly, and the `find` tables copied from GNU documentation, which cost a
  fix cycle on the fourth branch.
- **M0-97, priority 9** - the two LOW findings of section 3, in one spec because
  one source file and one test file hold both.
- **M0-94, priority 8** - Task B.

M0-97 outranks M0-94 deliberately: the section-24 gate is what keeps Task B's
class from silently reopening after Task B closes it, so a gate that can turn
itself off is worth more than the next three names on the list.

## 7. What exists after the stop, and what does not

The branch is kept, as DESIGN.md section 9 requires, and is published as
`origin/fence-attempt-4-2447da0`. Nothing of it is on `main` and nothing about
it is in the factory's record. Measured on 2026-08-24 by this carrier session:

```text
git merge-base --is-ancestor 2447da0 main; echo $?
1

grep -c 2447da0 factory/state/events.jsonl
0
```

The branches of the first three attempts are still kept as well:
`origin/fence-attempt-1-881d76a`, `origin/fence-attempt-2-ec4551f` and
`origin/fence-attempt-3-3b46a74` (ADR 0010 section 4, ADR 0013 section 5, ADR
0016 section 5).

Editing `factory/tasks/M0-62.yaml` retires the live version of its queue row and
mints a new one, which is the ordinary mechanism of DESIGN.md section 6 -
`QUEUED -> SUPERSEDED`, with the successor named in the event payload. The
carrier runs `enqueue` in this package and reports the row count it produced.

## 8. Where the work goes

Task A goes to a block session under `M0-62`, and its first act is to carry
`origin/fence-attempt-4-2447da0` onto a fresh branch - by cherry-picking
`d7fc0b6` through `2447da0`, or by hand if the pick does not apply. Rebuilding
from nothing would pay a fifth time for what four budgets bought.

Task B waits at the floor of the queue until somebody has a reason to run it,
and it has no deadline because the boundary it thickens is not the boundary that
holds.

What this ADR does NOT decide, and hands to nobody: whether the hook layer is
worth extending indefinitely at all. That question is answerable only with the
`POLICY_REFUSED` rows Task A produces - how often a real worker actually reaches
for a refused thing, and through what. Until those rows exist the argument is
taste. After they exist it is arithmetic, and this is the note that says to come
back and do it.
