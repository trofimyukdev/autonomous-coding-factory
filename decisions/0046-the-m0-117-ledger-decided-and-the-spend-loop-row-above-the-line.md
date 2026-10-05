# ADR 0046 - READY_TO_INTEGRATE gets its RETRY_WAIT edge, and a recovery with no edge comes back through RETRY_WAIT (M0-117)

Date: 2026-10-04
Status: decided on the operator's word of 2026-10-04 15:13:22 local time, quoted in section 0 - decisions (a) and (b) below no longer stand "unless the operator vetoes" them, and decision (c) is added by the same word
Asked by: block #180 (M0-117), landed 6e7adf7 (4f4e3e2 + 32af5bf, merged 2026-10-04 06:39:26)

Context: a carrier session (carrier #91, package item K1) by foreman
decision under the standing delegation of 2026-08-25, AT CADENCE, and on the
operator's word below. Merge blocks since carrier #90's last commit:
`git log --oneline --first-parent 87e45c3..origin/main | grep -c ' merge:'`
printed 4 on 2026-10-04 at 16:32. `main` stood at
`495674a 495674a` when this record was committed -
`git rev-parse HEAD origin/main | cut -c1-7 | paste -sd' '` printed
`495674a 495674a` on 2026-10-04 at 16:32.
The package this record belongs to writes `factory/tasks/`, this record and
ADR 0047, one row of `DESIGN.md` section 8 with that section's digest in
`test/unit/design-ratification.test.ts`, and two new files in a private
directory. Nothing under `src/`, `scripts/`, `.githooks/`,
`.claude/`, `factory/policy/`, `factory/checks.yaml` or
`factory/millwright.toml` is touched by it, nor `CLAUDE.md`, `PRINCIPLES.md`
or the private archive, and nothing is written in `repo-truth` or in the
showcase repository.

The text of decisions (a) and (b), "Not added" and "Consequences named" is
the ledger packet block #180 prepared and the acceptance seat corrected
(`<control-root>/briefs/ledger-packet-m0-117.txt`, 74 lines, 4526
bytes, sha256 beginning `416bfa6d6947cf04`), kept word for word. What this
record adds to it is the Status line above, this header, section 0, decision
(c) and the two closing sections.

**This document records an operator word and what it decides. It carries no
mechanism and moves no priority: the row it puts above the finish line,
M0-286, carries its own figure and its own form, and is named under "What is
filed elsewhere".**

## 0. The word, and the message it answers

Quoted verbatim on ADR 0005's precedent, Russian as typed. One transcript
holds them, the session of the foreman seat that heard the word (its live
session then, which grew while it was read): `<transcript>`. It was read only
through the read-only tools named below, on 2026-10-04 between 15:55 and
15:58; `stat -c '%s %y'` printed
`4469269 2026-10-04 15:55:30.306998277 +0300` for it at 15:55.

The tools, each read-only and each over the transcript. The exact filter ADR 0043
section 0 quotes whole, which reads `origin.kind === "human"` at a row's top
or inside its `attachment`, lists the human rows. A window lister of the form
ADR 0040 section 0 describes prints the uuid, type, timestamp, stop reason and
first characters of each user or assistant row in a time window that carries
text. The row printer ADR 0037 section 0 quotes whole prints one row by its
uuid; its own first output line is the row's type and timestamp, so the
printer's line numbers below count that line as line 1. A user row's fields
are printed by the field grep ADR 0043 section 0 quotes for a user row. Every
quoted line below was found in the transcript by `grep -c -F -e '<the line>' <transcript>`,
which printed at least 1 for each on 2026-10-04 at 15:57. Timestamps are UTC;
the times below are those timestamps plus three hours, local time.
A quoted block holds whole lines; what a message says beyond them is not part
of this record.

The exact filter printed four human rows over the transcript at 15:55. One is the word
recorded here; two more, an attachment row and a user row typed after it, are
ADR 0047's; and his user row at 07:26:06Z is
his request to walk the six questions step by step - a request, not a
decision, so it is not part of this record, for the reason ADR 0044 section 0
gives for the rows it leaves out.

### (a) The question - 10:29:36

The seat's row at 07:29:36.820Z (assistant, stop
reason `end_turn`) lays out four of his six questions. The row printer prints
it as 79 lines; question 1 is its lines 8 to 26, quoted whole:

```text
### 1. Петля трат M0-117 и правка DESIGN §6

**О чём.** Ночью приземлился M0-117 (коммит 6e7adf7). Раньше бывала «зависшая» строка: задача проверена, но интеграция её так и не забрала. Уборщик только сообщал о ней. Теперь он сам возвращает такую строку в очередь повторов (RT, RETRY_WAIT).

**Побочный эффект.** Его нашёл верификатор. Бывает, что замок интеграции занят навсегда: держатель на другом хосте или запись замка не читается. Тогда строка ходит по кругу: раз в два тика новый проход оплачивает билдера и ревьюера, интеграция упирается в замок, строка снова уходит в повтор.
- Счётчик строки при этом не растёт.
- Остановят её только общие лимиты: $60 в день, $12 за тик, STOP и недельный лимит.
- До M0-117 такая строка просто застревала после одной траты.
- Сейчас тиков нет (на repo-truth стоит STOP), так что петля пока ничего не стоит. Важна она к возобновлению тиков.

**Что ещё ждёт вашего подтверждения.** Две вещи уже действуют, но пока вы не наложите вето:
- (а) В DESIGN §6 добавлен переход READY_TO_INTEGRATE → RETRY_WAIT.
- (б) Моё прочтение фразы DESIGN «кандидат есть, доказательства целы → продолжить с VERIFYING». Для строк в CLAIMED/PREPARING уборщик ведёт их в повтор: прямого перехода в VERIFYING нет, а строку в VERIFYING без аренды ни один тик не взял бы. Текст §6 при этом не меняется.

**Рекомендую: да.**
- Подтвердить (а) и (б).
- Завести строку-ограничитель: отказ на замке или на STOP списывает инфраструктурный повтор, и после исчерпания повторов строка выходит из круга. Поставить её выше черты, то есть до любого тика.

**Что запустит «да».** Carrier #91 запишет ADR 0046 с вашим словом и заведёт эту строку. Блок по ней пройдёт до перевыпуска RT-08.
```

"1. The M0-117 spend loop and the edit of DESIGN section 6.

What it is about. Overnight M0-117 landed (commit 6e7adf7). Before it there
could be a 'stuck' row: the task was verified, but the integration never took
it. The janitor only reported it. Now the janitor itself returns such a row to
the retry queue (RT, RETRY_WAIT).

The side effect. The verifier found it. It happens that the integration lock
is held for ever: the holder is on another host, or the lock's record cannot
be read. Then the row goes round in a circle: once every two ticks a new pass
pays a builder and a reviewer, the integration runs into the lock, and the row
goes back to retry. - The row's counter does not grow meanwhile. - Only the
general limits stop it: $60 a day, $12 a tick, STOP and the weekly limit. -
Before M0-117 such a row simply got stuck after one spend. - There are no ticks
now (STOP stands on repo-truth), so for now the loop costs nothing. It matters
for when the ticks resume.

What else awaits your confirmation. Two things are already in force, standing
until you veto them: - (a) the transition READY_TO_INTEGRATE -> RETRY_WAIT has
been added to DESIGN section 6. - (b) My reading of the DESIGN sentence
'candidate present, evidence intact -> resume at VERIFYING'. For rows in
CLAIMED / PREPARING the janitor takes them to retry: there is no direct
transition into VERIFYING, and a row in VERIFYING with no lease would be taken
by no tick. The text of section 6 does not change.

I recommend: yes. - Confirm (a) and (b). - Open a limiting row: a refusal at
the lock or at STOP charges an infrastructure retry, and once the retries are
spent the row leaves the circle. Put it above the line, that is, before any
tick.

What a 'yes' starts. Carrier #91 will write ADR 0046 with your word and open
this row. A block on it will run before RT-08's reissue."

The row's last line, printer line 79, is the answer form, and asks for
answers by number.

### (b) The last seat text before the word - 10:33:55

The window lister over the transcript from 07:29:00Z to 12:19:30Z printed,
at 15:55, eight rows that carry text: the question row above; a user row at
07:33:18Z, a message from another session and not a human row; an assistant
row at 07:33:32Z (stop reason `tool_use`), the seat's working note on that
message; the seat's row at 07:33:55Z; his word; and three rows after it that
are ADR 0047's. So the LAST seat text before the word is not the question row
but the seat's row at 07:33:55.255Z (assistant, stop reason `end_turn`),
printed as eight lines. Its lines 4 and 6, whole:

```text
В нём 13 пунктов, все ниже черты. Среди них — новая строка M0-286 против петли трат M0-117 (приоритет 79).
Ваши ответы на вопросы 1 и 4 меняют его состав: ADR 0046, подъём M0-286 выше черты, пункты 5.1, 5.6, 5.9 и 5.10. Поэтому после ответов поправлю kickoff и только тогда открою carrier.
```

"There are 13 items in it, all below the line. Among them is a new row,
M0-286, against the M0-117 spend loop (priority 79). / Your answers to
questions 1 and 4 change its make-up: ADR 0046, raising M0-286 above the
line, items 5.1, 5.6, 5.9 and 5.10. So after the answers I will amend the
kickoff, and only then open the carrier." ("It" is carrier #91's kickoff,
which its line 2 says the seat holds until his answers.) It puts no new
question: its last line, printer line 8, asks for answers by number to the
questions of the previous message, which is the question row of (a). Both
rows are named here; the question his word answers is that row's.

### (c) The word - 15:13:22

His user row in the transcript at 12:13:22.862Z. The
row printer prints it as eight lines. Its line 2, the answer to question 1,
whole:

```text
1 - Да
```

"1 - Yes." Its fields: `"origin":{"kind":"human"}`,
`"promptSource":"queued"` and `"entrypoint":"cli"`. The row's lines 3 to 5
answer questions 4, 5 and 6, and its lines 7 and 8 ask where the posts
belong; all of them are ADR 0047's and are not this record's.

## Decision (a) - the DESIGN.md section 6 edit

`READY_TO_INTEGRATE -> RETRY_WAIT` is a key edge of the task state machine.
It is declared in `FORWARD_EDGES` (src/store/state-machine.ts) and named in
DESIGN.md section 6 "Key edges" in the same commit, and section 6's ratified
digest is re-ratified (9af4153b03a494f5 -> 3002686f00feaf1b,
test/unit/design-ratification.test.ts).

Why: a verified row whose integration never claimed it is left in
READY_TO_INTEGRATE with no lease. Five roads lead there, each after the walk landed the row there and released
its lease: a hard death; an integration refused at the integration lock; an
integration refused at a STOP read at integration step 1; and the gate phase
returning before `integrate()` is called - a candidate it could not bring out
of the workspace (`if (!brought.ok) return nothing;`) or a checks
configuration it could not read (`integration did not run: ...`), both in
src/controller/gate-phase.ts. The sweep does not ask which road it was. Every other
running state already had a RETRY_WAIT landing; this one did not, so the
reaper reached the right recovery and could only report the row on every
sweep, and no tick took it. The sweep now lands the row in RETRY_WAIT with the
counters its recovery decided (none when the candidate and its attempt
survived). A run that throws while the row stands there lands on the same
edge, on the infrastructure counter (it used to land in BLOCKED).

## Decision (b) - the seat's reading of "resume at VERIFYING" (no DESIGN.md edit)

DESIGN.md section 6, "Lease and recovery": "candidate commit present and
evidence intact -> resume at `VERIFYING`;". `declared()`
(src/controller/reaper.ts) lands a recovery whose resume point the machine
gives the row no edge to - CLAIMED or PREPARING resuming "at VERIFYING", and
CLAIMED or a torn READY_TO_INTEGRATE row whose new quality attempt resumes at
BUILDING - in RETRY_WAIT, with the outcome and counters unchanged. That is the
rule M2-13 already applied to a resume point equal to the row's own state. A
`reconcile_to_merged` is excluded and stays a report. No edges into VERIFYING
or BUILDING are added: a leaseless row there is taken by no tick, and the next
sweep would send it to RETRY_WAIT anyway, at a second quality charge on the
BUILDING road. Ruled by the seat (an earlier foreman seat, 2026-10-04) as its reading;
section 6's text is unchanged for this part.

## Not added

`CLAIMED|PREPARING|BUILDING|VERIFYING|READY_TO_INTEGRATE -> MERGED`. The
tick's probe targets only rows one edge from MERGED, so no production road
reaches these pairs. Each such edge would widen `MAY_HAVE_MERGED` (fail-closed
reports under an unasked probe, a fetch on every sweep, no throw landing).
M2-11 owns reading what origin carries. These pairs stay reported.

## Consequences named

- A stranded row that the sweep lands in RETRY_WAIT leaves `CARRIED_STATES`,
  so a sibling version of its spec id becomes pickable while it waits.
- Under a lock that stays held (a holder on another host, or a lock record
  that cannot be read - src/integrate/lock.ts refuses both for ever), the row
  loops - RETRY_WAIT, READY, a whole pass, refused at the lock - at most once
  every second tick (the janitor skips the row its own sweep answered, and the
  backoff stays at retry_backoff_seconds because infra_retries stays 0). The
  sweep charges no counter on that loop and no breaker counts it, so nothing
  per row bounds it: each pass pays a builder and a reviewer (and a scout when
  one is dispatched), bounded only by the factory-wide max_usd_per_day and
  max_usd_per_tick, STOP and the weekly cap. Before this decision the same row
  stuck after one spend and needed a hand edit. A row that charges an infra
  retry on a lock or STOP refusal would bound it; that is a next row, not this
  decision.
- A second live tick's sweep inside the window between the walk's
  landing and `integrate()`'s claim (the candidate's fetch, the checks
  configuration's read, the lock and the STOP read) lands the row in RETRY_WAIT, and the claim
  refuses with `where: "row"`.
- The next pass after RETRY_WAIT carries no verified candidate: it resumes only
  an owed seat or fix cycle and otherwise opens a builder.

## Decision (c) - the spend loop is bounded by its own row, above the finish line

His "1 - Yes" answers question 1's recommendation, quoted in section 0 (a):
confirm (a) and (b), and open a limiting row "above the line, that is, before
any tick" (printer line 24). So decisions (a) and (b) above are taken as they
stand, and the loop that the second bullet of "Consequences named" calls "a
next row, not this decision" gets that row: **M0-286, minted by the same
package, stands ABOVE the finish line of ADR 0034 section 1 (3) - above M5-03
and every roadmap row - so that the loop is bounded before any tick resumes.**
The row carries the bound out and restates none of this record; its footer
and its `outranks_roadmap` point here.

Two things beside it are THE SEAT'S, each **[operator-confirmable]**:

1. **The figure 98.** His word names no figure. 98 is the slot his earlier
   word put above the line held - M0-281 and M0-283, raised on the word ADR
   0044 section 1 item 4 records, a figure that was the seat's there too - and
   no open row stands at it when M0-286 is enqueued.
2. **The form.** Printer line 24 recommends one form: a refusal at the lock or
   at STOP charges an infrastructure retry, so the spec's own ceiling ends the
   loop. M0-286 names that form and a second one - the verified candidate is
   carried, so the next pass pays no builder and no reviewer for it - and
   prescribes neither, leaving the choice to its block. That his "yes" to a
   recommendation naming the first form leaves room for the second is THE
   SEAT'S reading, **[operator-confirmable]**.

## What this ADR does NOT decide

- **M0-286's figure as a figure, and its form.** Decision (c) items 1 and 2.
- **The ticks.** None is sanctioned here. That the ticks on `repo-truth` wait
  for M0-286 to land is question 6's recommendation and is recorded, with his
  answer to it, by ADR 0047.
- **When M0-286's block runs.** Printer line 26 states what a "yes" starts in
  the seat's plan - this record, the row, and a block on it before RT-08's
  reissue; the block's turn is the seat's, as every pick is.
- **`DESIGN.md` beyond section 6's edit.** Section 6's "Key edges" bullet for
  the edge still marks itself **[operator-confirmable]** as of 2026-10-04 and
  "it stands unless the operator vetoes it"; this record is the word that
  bullet waited for, and the bullet's text is not edited by this package,
  whose `DESIGN.md` path is section 8's stage-1 row alone.
- **The external-timeout sentences** of `DESIGN.md` sections 7 and 13. His
  word, not asked in this walk.
- **block #180's F2 prose sites.** "Five roads lead there", decision (a) says;
  the `DESIGN.md` section 6 bullet, the `FORWARD_EDGES` comment
  (src/store/state-machine.ts) and the section 6 ratification comment in
  `test/unit/design-ratification.test.ts` name fewer. This word is the
  section 6 word those sites waited for; they sit outside this package's
  paths, and a later package edits them together.
- **That any tick, task, condition, the gate or the ladder passes after any
  row lands.**

## What is filed elsewhere

- **M0-286** (`factory/tasks/M0-286.yaml`) - the row decision (c) puts above
  the line: the road, the forms it names, its cases and its bounds.
- **ADR 0047** - his other answers in the same row, his word of 15:13:22: items 5.1 to
  5.10 of the decision brief, the step (2) packet, RT-08's reissue, the
  posts' home and style, and M5-03's closure.
