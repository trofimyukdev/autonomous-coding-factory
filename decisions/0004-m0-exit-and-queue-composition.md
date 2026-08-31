# ADR 0004 - M0 exit review, queue composition, and the third fix lane

Date: 2026-08-18. Context: a carrier session by operator decision - not a block.
Five defects were put to it, each with the command that shows it: the database is
an orphan (`node dist/cli.js status` prints 13 tasks, all QUEUED, attempts q0/i0,
oldest M0-01, while `git log --oneline | grep -cE 'feat: M0-'` prints 9 and
`ls factory/tasks | wc -l` prints 25); fix cycles are not derivable from history
(ADR 0003 section 2 records five logic fix cycles for M0-03, `git log` shows one
feat commit for it - sessions amended); merge commits carry no DESIGN.md section
10 trailers (`git log --format='%(trailers)' -1 204f0ce` is empty); the queue
holds no M1 spec at all, 19 of 25 specs are `discovered_from`, and hygiene
outranks plan (M0-17 at 58 above M0-10 at 55); and the DESIGN.md ratification
block of ADR 0001 decision 1 never became a spec, with the pre-autonomy checklist
of blueprint section 20 locked behind it.

Decisions by the blueprint author. **[operator-confirmable]** items stand unless
vetoed.

## 1. M0 is closed - the criterion is met, with two conditions named

DESIGN.md section 17 states M0's done-when: "`kill -9` at any moment loses no
task; doctor is honest". Both halves are now machine-evident on `main` at
`076f82d`:

```text
npm run test:kill   -> === 5/5 kill suite runs passed   (5 tests each run)
npm test            -> Test Files 9 passed (9), Tests 398 passed (398)
node dist/cli.js doctor -> 16 check(s): 10 pass, 1 fail, 5 skipped; exit 78
```

The doctor run is the honesty evidence, not a blemish: the one `fail` is
`environment.auth` reporting truthfully that `CLAUDE_CODE_OAUTH_TOKEN` is absent
from that shell, and the five `skip(M1)` lines name the milestone that will turn
each into a real check rather than omitting them. A report that fails when it
must and says which checks it did not run is what the criterion asks for. The
operator re-verified both halves independently on 2026-08-18 (mutants in
`src/store/**` killed across 5/5 runs; doctor reproduced live).

**Closing a milestone means its done-when is met. It does not mean the family is
empty.** Sixteen M0-numbered specs stay open and are repriced by section 2 below;
they are follow-up work, not unfinished M0.

Two findings argue that closing is premature. Both are recorded here as
conditions rather than left to silence, per the operator's instruction:

**(a) M0-20 - the one live overclaim inside the honest report.** doctor's
`resources.disk` check is titled "at least 2.00 GiB free where the factory
writes" and measures a single directory, the resolved factory dir
(`src/doctor/doctor.ts`, `checkDisk`), while the factory also writes under
`~/.config/millwright/<repo>` - the control root, the holdout directory and the
authoritative STOP file (`src/controller/config.ts`, `configRoot`, `holdoutDir`,
`stopFileAuthoritative`), routinely a different filesystem. Judgement: this does
not hold M0 open, because the check's evidence line names exactly what it
measured (`131.69 GiB free on <repo>/factory`) - the title
generalises, the output does not hide its scope. It becomes load-bearing before
M4, when an operator arms a kill switch on a filesystem doctor never measured.
Condition: M0-20 lands before the first unattended tick, and its priority is set
as plan work, not as hygiene.

**(b) M0-23 - `kill -9` is process death, not machine death.** Deleting
`fsyncSync` from `EventMirror.append` leaves the kill suite 5/5 green, because
SIGKILL does not empty the page cache and the suite runs on tmpfs (measured in
M0-23, discovered from M0-05). The criterion says `kill -9` and the criterion is
met as written; durability against losing the machine is a DESIGN.md section 18
pre-autonomy item and is not an M0 item. Condition: it is not closed by silence -
M0-23 stays open, and the pre-autonomy checklist (blueprint section 20) may not
be declared satisfied while it is.

## 2. Queue composition - the milestone is what earns priority  [operator-confirmable]

The queue drifted into serving itself: no M1 spec existed, 19 of 25 specs were
discovered-from tails, three of the nine merged blocks (M0-09, M0-14, M0-15) were
one invariant about one filename, and a comment-pinning spec outranked the
supersession spec that M1 needs. Five rules, in force from this ADR:

1. **Every spec names the milestone it serves** - field `milestone`. The field
   does not exist yet: the validator refuses unknown fields
   (`src/controller/taskspec.ts`, `validateFields`, "unknown field"), so adding
   one to a YAML today fails `npm test`. Until spec **M0-28** makes it a
   validated field, each spec carries a `# milestone:` comment on its first line;
   M0-28 converts the comments into data and is the only place that fact will
   then live. The stopgap is hash-neutral, which is what makes it safe: comments
   are dropped before `spec_hash` is computed, so M0-01 still hashes to
   `sha256:987cf...` after stamping - the value the database captured on
   2026-08-17 - while every repriced spec's hash did change (M0-10 from
   `5d6a983eb7ed` to `0701c...`). Measured by reading every entry's id, hash and
   priority through `readQueueDirectory` from `dist/controller/queue.js`.
   **Amended by M0-28, which landed as merge `ffbdbfc`: the stopgap described
   here no longer exists.** `milestone` is a validated field, the
   `# milestone:` comments went with the conversion that created it, and the
   hash-neutrality that made the stopgap safe protects nothing any more - the
   fact is data now, so an edit to it re-hashes the spec like any other field.
   The rule stands; only its mechanism is superseded.
2. **The id prefix is a filing counter, not a milestone claim.** A spec filed as
   M0-26 may serve M2. `milestone` is the single home for what a spec serves; the
   number only says when it was filed.
3. **Discovered hygiene never outranks an open spec of its own milestone or of
   the next one.** Hygiene means work whose entire subject is a comment, a
   duplicated constant, a dead import, or a guard about a guard. Applied to the
   whole open family on 2026-08-18; the spec files are the home of the numbers
   and `millwright queue` is the record.
4. **Every block report answers one line: "what did this do for M2 - the factory
   runs blocks itself?"** The answer "nothing" is legal and is not a defect; it
   drops the priority of that spec's family the next time the queue is read.
   This is discipline 10 with the milestone named, so drift is visible per block
   instead of per milestone.
5. **A new guard-of-guards is filed only on a live escaped mutant, never on a
   theoretical hole.** The evidence is the mutation, the command and the
   before/after counts - the ADR 0002 test-only standard, applied to the decision
   to file rather than to the decision to merge. M0-19 qualifies (`ok: true`
   survives 54 passed); a guard proposed because a hole is imaginable does not.

## 3. The third fix lane - amends ADR 0003 section 2, and no amends  [operator-confirmable]

ADR 0003 section 2 admits a finding in-block only when `acceptance` or
`not_done_if` cannot honestly pass without the fix. That leaves one class with no
home: a false comment or a dead assertion that **this block's own diff just
wrote**. Acceptance passes without touching it, so the rule sends it to a
follow-up spec - and the block merges a sentence its author knows to be false.
That is how M0-09 shipped a comment that M0-15 then had to delete, and how M0-14
and M0-17 became specs about the wording of guards.

**The third lane: a finding whose entire subject is text this block's own diff
introduced (comments, dead assertions) MAY be fixed in-block even when acceptance
passes without it. Merging a knowingly false comment is worse than fixing it.**

**Such a fix is a SEPARATE fix: a commit on the block branch, NEVER an amend.**
An amend destroys the commit the evidence belongs to, which is the object ADR
0002 points at when it requires the mutation, the command and the counts "in the
commit message". It also destroys the record of whether a block passed on its
first pass: `git log --oneline | grep M0-03` shows one commit where ADR 0003
section 2 documents five logic fix cycles, and no command over this history can
now recover that. An external check on 2026-08-18 read a false "6 of 8
first-pass" out of exactly that gap. Amending a block commit is henceforth a
defect of the same class as a false comment.

**The contradiction ADR 0002 and ADR 0003 had is closed by this lane.** They
answer different questions and were being read as one: ADR 0002's "doc and
comment-only changes carry no gate of their own and ride with whatever else the
fix cycle contains" is the **gate** question (what re-verification a fix costs);
ADR 0003 section 2's "in-block only when acceptance cannot pass" is the
**admission** question (whether the fix belongs to this block at all). Now:
admission for comment findings about the block's own new text is granted by this
lane; admission for comment findings about pre-existing text is still refused and
they become specs; and once admitted, the gate is ADR 0002's - such a fix carries
no gate of its own and rides with whatever else the cycle contains, in its own
commit.

**The class "a spec quotes a flying counter".** M0-14 shipped "(339 passed)" when
the suite stood at 340; `grep -rn "[0-9]* passed" factory/tasks/` shows the same
shape in M0-17 ("340 passed", while `npm test` printed 398 passed on 2026-08-18)
and M0-19.
Rule: **a spec names the command, not the number it expects.** Where a count is
the evidence, the spec carries the command and the count together as a
measurement with its date, never a bare number a later commit falsifies. This is
enforced, not asserted: spec **M0-27** puts one gate behind it, over commit
messages and over `factory/tasks/**` alike, because it is one lesson with two
surfaces (discipline 4).

## 4. The /block merge tail - two pointers to rules that already have homes

Neither of these is a new rule; `.claude/commands/block.md` was silent about them
and two blocks diverged as a result.

- **Delete the block branch after the post-merge verify.** Home: DESIGN.md
  section 7, tick step 2 ("delete bot branches of merged tasks") - the janitor's
  job, done by hand until the janitor exists.
- **One merge mechanic: DESIGN.md section 10.** The candidate enters through a
  merge commit carrying the trailers `Millwright-Task-ID`,
  `Millwright-Attempt-ID` and `Millwright-Spec-Hash`. Seven of the nine merged
  blocks went in fast-forward (M0-01, M0-02, M0-03, M0-06, M0-09, M0-14, M0-15)
  and the two that did use merge commits carry no trailers. Spec **M0-26** makes
  the trailers real in M0 rather than at M2, because reconciliation by trailer is
  what makes the database's account of a merge checkable against `origin`.
