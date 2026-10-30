# ADR 0051 - The operator's words of 2026-10-11 and 2026-10-12 on the rows his freeze keeps: a candidate set aside with no confirmed finding is resumed and not rebuilt, the loser at its own pass's lock waits inside the pass, and the uncharged carry is bounded before rung 4

Date: 2026-10-12. Context: a carrier session (carrier #98, package item K1)
by foreman decision under the standing delegation of 2026-08-25, opened off
cadence by exception - not a block - to carry into its record four words of
the operator on the millwright rows his freeze of 2026-10-11 keeps, and the
evidence of the tick series on `repo-truth` that those words answer. Merge
blocks since carrier #97's last commit (e62f65b):
`git log --oneline --first-parent e62f65b..origin/main | grep -c ' merge: '`
printed 3 on 2026-10-12 at 17:01 - M0-292, M0-293 and M0-289. `main`
stood at `378c366 378c366` when this record was committed -
`git rev-parse HEAD origin/main | cut -c1-7 | paste -sd' '` printed
`378c366 378c366` on 2026-10-12 at 17:01.
Nothing under `src/`, `test/`, `scripts/`, `.githooks/`, `.claude/`,
`factory/policy/`, `factory/checks.yaml`, `factory/compat.json`,
`factory/millwright.toml`, `CLAUDE.md`, `PRINCIPLES.md`, `DESIGN.md` or
the private archive was touched by this package, nothing under `docs/decisions/`
but this record's own file, and nothing was written in `repo-truth`; the
package's other files are named in its commit messages.

This is a new record and not an amendment. ADR 0039's paragraph that opens
"THE CORRECTION the record carries:" already carries the fact this record's
words change - a candidate refused with nothing measured false is kept as
evidence and is not judged again, and the next pass opens a builder; ADR
0029 section 1 (3) carries the condition-2 rule, which these words keep; ADR
0046 decision (c), M0-286 and M0-289 carry the charge of a refusal at the
integration lock and its exemption for a dispatch of the same pass. None of
them is edited.

**This document records operator words and what they decide. It carries no
mechanism and moves no priority: the rows that carry the decisions out are
the homes of their own content and are named in the commit messages.**

## 0. The words, and the messages they answer

Quoted verbatim on ADR 0005's precedent, Russian as typed. One transcript
holds them, the session of the foreman seat that heard them (its live
session then): `<transcript>`.
His rows were listed by the seat's read-only lister of the rows whose
`origin.kind` is exactly `human`, at the row's top or inside a
`queued_command` attachment (`<lister>` below,
run as `node <lister> <transcript> 900`), and every row below - his and the
seat's - was printed by its uuid with `jq` over the transcript on 2026-10-12. Every
quoted line below equals a whole line of the row it is quoted from, character
for character: `grep -c -x -F -e '<the line>'` over that row's printed text
printed 1 for each, and `grep -c -F -e '<the line>' <transcript>` printed at
least 1 for each, on 2026-10-12 at 17:01. Timestamps are UTC; the times
below are those timestamps plus three hours, local time. A quoted
block holds whole lines; what a message says beyond them is not part of this
record.

**WHOSE PROPOSALS THEY ARE.** Each proposal this record decides on is THE
SEAT'S, and only his rows are his. The freeze is first put in the seat's
question row of (a); the protection against an endless uncharged loop at the
integration lock is first put in the seat's row of (c), as its question 2's
risk and its question 3's bullet; the wait inside the pass is first put in
the seat's question row of (e); and the widening is first put in the seat's
question row of (g). Over the lister's output for the transcript, his rows of
2026-10-11 and 2026-10-12 are 29, and a case-insensitive count of seven
Russian stems - freeze, lock (two forms), loop, rebuild, ceiling and refusal
- over them printed 0, on 2026-10-12 at 17:01: no row of his names any
of the four before the seat put it to him. The command is not quoted here,
because this record carries non-ASCII text in its quotations only; it is the
form ADR 0050 section 0 used, with these stems.

### (a) The freeze - the question of 2026-10-11 08:09:17

The seat's row at 2026-10-11T05:09:17.359Z (assistant), a list of numbered questions. Its line 8, whole:

```text
8. **Заморозить самостройку фабрики (задачи на её собственный код), кроме задач, открывающих M5.** Рекомендую да. Путь к M5 теперь проходит через repo-truth и несколько конкретных задач фабрики: блокировку при вливании для двух строителей и статистику проверок. Остальная полировка на цель не работает. Список задач, которые остаются, подготовлю.
```

"8. Freeze the factory's self-building (tasks on its own code), except the
tasks that open M5. I recommend yes. The road to M5 now goes through
repo-truth and a few specific tasks of the factory: the lock at merging for
two builders and the statistics of the checks. The rest of the polishing does
not work for the goal. I will prepare the list of the tasks that stay."

The last seat row carrying text before his word of (b) is a later one,
at 05:34:38.407Z, the seat's report of
its verifier on M0-293's landing; it holds no question on the freeze and is
pointed at, not quoted.

### (b) His word - 2026-10-11 08:35:37

His user row at 2026-10-11T05:35:37.546Z, `origin` kind `human`, ten numbered answers. Its
line 8, whole:

```text
8. Да
```

"8. Yes." The list the seat keeps under it is
`<control-root>/briefs/<freeze-list>`, an operator-local file of
the seat's, named here and not copied.

### (c) The morning packet - 2026-10-12 05:11:21

The seat's row at 2026-10-12T02:11:21.920Z (assistant), five numbered questions. It is the last seat row
carrying text before his answers of (d). Question 2 asks for rung 3, two
builders a pass; its last paragraph, whole:

```text
Риск: если у победителя прохода проверку слияния раз за разом обрывает таймаут, второй строитель будет крутиться без списаний. Я принимаю каждый тик и замечу это за два прохода. Защиту от этого нужно построить до ступени 4.
```

"Risk: if the pass winner's merge check is cut by a timeout time after time,
the second builder will spin with no charges. I accept every tick and will
notice it within two passes. The protection against this must be built
before rung 4."

Question 3's head line and the bullet of its list that names that
protection, each whole:

```text
**3. Список заморозки v2**, то есть что из millwright строим.
- **Защита от бесконечного круга из п. 2:** новая задача до ступени 4.
```

"3. The freeze list v2, that is, what of millwright we build." - "The
protection against the endless loop of item 2: a new task before rung 4."

Question 4, whole - one line:

```text
**4. Отказы из-за непроверенного измерения ревьюера (ADR 0029).** Ревьюер называет измерение, которое сам не проверил, и шлюз отказывает, хотя проба и оценщик цели зелёные. Так было с RT-17, RT-21, RT-26 и RT-27. Каждый раз пересборка за $0.7–0.85, попытка качества при этом не списывается. Рекомендую правило не менять: оно из DESIGN, «каждый пункт проверен». Вернуться к нему, когда будет статистика линз.
```

"4. Refusals because of a reviewer's unverified measurement (ADR 0029). The
reviewer names a measurement it did not check itself, and the gate refuses,
although the probe and the goal evaluator are green. So it was with RT-17,
RT-21, RT-26 and RT-27. Each time a rebuild for $0.7-0.85, and no quality
attempt is charged for it. I recommend not changing the rule: it is from
DESIGN, 'every item verified'. Return to it when there are lens
statistics."

### (d) His answers - 2026-10-12 09:51:45

His attachment row at 2026-10-12T06:51:45.103Z, of type `queued_command` with `origin` kind
`human`: a message he typed while the seat's turn ran. The transcript holds no user row
for it; it holds a `queue-operation` row "enqueue" at the same timestamp and
a `queue-operation` row "remove" whose `reason` is "absorbed_mid_turn" at
06:51:55.825Z, the shape ADR 0043 section 0 (c) describes. Its answers 2, 3
and 4, each whole:

```text
2. Да, в сесси тиков отправил фразу
3. По твоим рекомендациям
4. По твоим рекомендациям
```

"2. Yes, I sent the phrase in the ticks' session." - "3. By your
recommendations." - "4. By your recommendations." Answer 2 took rung 3 and
is not this record's decision; it is quoted because the paragraph of (c)'s
question 2 it answers is where the loop is first named. Answer 3 takes
question 3's list, the bullet of (c) among it. Answer 4 keeps the rule of
question 4.

### (e) Item 4 - the question of 2026-10-12 10:38:35

The seat's row at 2026-10-12T07:38:35.625Z (assistant), the seat's acceptance of tick 70. It is the last
seat row carrying text before his word of (f). Its question line, whole:

```text
**Вопрос, не срочный, серия идёт дальше.** Добавить в список заморозки новую задачу до ступени 4? Её суть: кандидат, которому отказал замок собственного прохода, ждёт, пока сосед вольётся, и вливается поверх него в том же проходе. Встанет рядом с защитой от бесконечного круга: обе про замок интеграции. Рекомендую «да» и строить после партии 2.
```

"A question, not urgent, the series goes on. Add to the freeze list a new
task before rung 4? Its substance: a candidate refused by the lock of its own
pass waits until the neighbour is merged, and is merged on top of it in the
same pass. It will stand beside the protection against the endless loop: both
are about the integration lock. I recommend 'yes' and building after batch
2."

### (f) His word - 2026-10-12 10:43:05

His user row at 2026-10-12T07:43:05.887Z, `origin` kind `human`:

```text
Да
```

"Yes."

### (g) The widening - the question of 2026-10-12 14:35:31

The seat's row at 2026-10-12T11:35:31.340Z (assistant), the seat's report of tick 84 and the close of batch
2. Its question line, whole:

```text
**Вопрос к вам.** В 10:43 вы сказали «Да» исправлению: задача, проигравшая замок, продолжает с уже проверенной сборки, а не собирается заново. Распространить его и на отказы, в которых ошибки не найдено? Само правило отказа из вашего ответа 4 не меняется. Меняется одно: после такого отказа фабрика заново проверяет ту же сборку, а не строит новую. Рекомендую «Да», это убирает основную часть потерь партии.
```

"A question to you. At 10:43 you said 'Yes' to a fix: a task that lost the
lock continues from the already verified build and is not built anew. Extend
it to the refusals in which no error was found as well? The refusal rule
itself, from your answer 4, does not change. One thing changes: after such a
refusal the factory checks the same build again and does not build a new
one. I recommend 'Yes'; it removes the main part of the batch's losses."

**THE QUESTION'S OPENING IS THE SEAT'S PARAPHRASE.** Its first sentence
restates his word of (f) as a fix by which the task that lost the lock
"continues from the already verified build". The question he answered at
10:43, (e), asked something narrower: waiting for the sibling's integration
and integrating on top of it inside the same pass. This record reads (f) as
covering what (e) asked, and reads the rest as the seat's (section 2,
reading 3).

The same restatement was first put to him earlier, in the seat's row
at 2026-10-12T08:50:18.256Z (11:50:18),
a report on tick 73 whose paragraph above it describes the lock's loser
being rebuilt. Its line 7, whole:

```text
Тик 73 возьмёт RT-31 и RT-33. Обе почти готовы, так что, скорее всего, столкнутся снова. Исправление в коде — это задача, на которую вы сказали «Да» в 10:43, но строить её будем после партии.
```

"Tick 73 will take RT-31 and RT-33. Both are almost ready, so most likely
they will collide again. The fix in code is the task you said 'Yes' to at
10:43, but we will build it after the batch." It names his word of (f) as
the fix of that rebuild; it is the seat's line, and it may be what his
reply of (h) means by "I already said yes".

The last seat row carrying text before his word of (h) is a later one,
at 11:45:15.992Z, which repeats the same
question in its last clause. Its one line, whole:

```text
Сработал резервный таймер, поставленный на тик 83. Сейчас он не нужен: тиков нет, серия на паузе. Новый не ставлю и жду вашего ответа: распространять ли исправление на отказы, в которых ошибки не найдено.
```

"The fallback timer set for tick 83 fired. It is not needed now: there are
no ticks, the series is paused. I set no new one and wait for your answer:
whether to extend the fix to the refusals in which no error was found."

### (h) His reply - 2026-10-12 16:02:31

His user row at 2026-10-12T13:02:31.899Z, `origin` kind `human`, his whole text:

```text
По поводу твоего вопроса, я же уже говорил да, этого недостаточно? Это же тоже самое что-то рекомендуешь сейчас, да?
```

"About your question - I already said yes, is that not enough? It is the
same thing you are recommending now, isn't it?"

The seat answered him in two seat rows of the transcript: one at
13:04:12.303Z, one line saying the two are almost the same but not quite,
and one at 13:27:13.548Z, which says that
his word of (f) named the lock's road only, that his answer 4 of (d) kept the
condition-2 class, so the seat had not widened his word alone, and that it
took his reply as a yes to both. That answer is the seat's, never his; it is
pointed at, not quoted. Its paragraph at line 19 left one thing to his veto:
the wider road (i) of reading 4 - resuming wherever the factory already says
a row resumes, a wall-cut integration among them - put to him as the seat's
own reading, wider than his two cases, with the narrow shape his for one
word. The transcript held no row of his after that reply when the lister was run on
2026-10-12 at 18:09. If he takes the veto, M0-294 is re-issued in the
narrow shape.

## 1. The evidence

Read from `repo-truth`'s journal as a file, from
`<repo-truth>`, since rung 3 was taken (journal seq
5728). THE TALLY, one command, re-run by this carrier on 2026-10-12 at
17:01:

```text
node -e 'const fs=require("fs");const E=fs.readFileSync("factory/state/events.jsonl","utf8").trim().split("\n").map(l=>JSON.parse(l)).filter(e=>e.seq>=5729);const s=[];for(const e of E){const p=e.payload||{};if(e.type==="INTEGRATION_REFUSED"&&p.pass_sibling===true)s.push([e.seq,String(e.task_id).slice(0,5),p.candidate_sha.slice(0,8),"sibling_lock"]);if(e.type==="INFRA_RETRY"&&/^nothing was measured false: the gate refused ([0-9a-f]{40})/.test(p.reason||""))s.push([e.seq,String(e.task_id).slice(0,5),RegExp.$1.slice(0,8),"no_finding"]);}const ok=new Set(E.filter(e=>e.type==="GATE_PASSED").map(e=>String(e.payload.candidate_sha).slice(0,8)));for(const r of s)console.log(r.join(" "),ok.has(r[2])?"later_passed_same_sha":"never_passed_again");'
```

printed six lines:

```text
5806 RT-30 6e68c83a sibling_lock never_passed_again
5905 RT-32 61d220e4 no_finding never_passed_again
5983 RT-31 54e35876 sibling_lock never_passed_again
6080 RT-32 4173d064 no_finding never_passed_again
6282 RT-33 997e080a no_finding never_passed_again
6581 RT-34 6d94763f no_finding never_passed_again
```

Six candidates set aside with no confirmed finding against them - two at the
lock their own pass held, four refused by the gate with nothing measured
false - and no GATE_PASSED event after seq 5728 names any of their SHAs.
The seat's sums of what they cost are
in its run journal's archive entry that opens "- TICK 84 ACCEPTED"; they are
pointed at and not re-run here.

**THE TWO ROADS, by journal seq.** The lock's loser rebuilt: RT-31's 5983
INTEGRATION_REFUSED (`where` lock, `pass_sibling` true), 5999 INFRA_RETRY
READY_TO_INTEGRATE -> RETRY_WAIT, whose reason names the recovery
`resume_at_verifying`, 6085 RETRY_WAIT -> READY, 6088 DISPATCH_DECIDED and
6098 AGENT_STARTED for a builder at `attempt_no` 4, and 6114 BUILDING ->
VERIFYING on a new candidate ddfeb2be. The refusal with no finding rebuilt:
RT-34's 6580 GATE_FAILED on 6d94763f, 6581 INFRA_RETRY INTEGRATING ->
RETRY_WAIT "nothing was measured false: the gate refused 6d94763f... with 0
confirmed finding", and a later pass's builder made 9b2e7180, whose
src/checks/strictness.ts holds the defect the discarded candidate had removed
- `git -C <run tree> grep -n -F` printed its line 184 in 9b2e7180's tree
(`if (oldPath === null || !isTsconfig(oldPath)) continue;`) and line 188 of
the fix in 6d94763f's (`const after = newHere ? await readConfig(cwd, newMode, newSha) : NO_CONFIG;`),
the run trees being RT-34-M5-03-20261012T111413Z and
RT-34-M5-03-20261012T105352Z under `repo-truth`'s factory/runs/, on
2026-10-12 at 17:01; the holdout refused 9b2e7180, and 6665
FIX_CYCLE_BLOCKED and 6666 TASK_BLOCKED "quality attempts exhausted (2 of
2)" followed. `git -C <the second tree> cat-file -t 6d94763f` printed
`commit`: the discarded fix is still on disk.

**WHAT THE CODE SAYS OF IT.** `landUnmeasuredRefusal`'s docstring
(src/controller/fix-cycle.ts) says of the kept candidate "and it is kept as
EVIDENCE: the next pass does not re-verify this candidate."; the record that
already carries that fact is ADR 0039's CORRECTION paragraph, pointed at and
not copied. The reaper's outcome for an evidence-intact stranding is named
`resume_at_verifying`, and its own report reads "...and the attempt that
built it: it resumes with no attempt spent" (src/controller/reaper.ts); for
a READY_TO_INTEGRATE stranding `declared` replaces that report with one that
says the row comes back through RETRY_WAIT (journal seq 5999's reason), and
the next pass of the lock road above opened a builder.

**THE METRIC.** The ladder counts a refusal overturned when the refused
row's spec stem has merged and a row of that stem still names the refused
SHA as its candidate -
`if (refusal.rows.some((row) => row.candidate_sha === refusal.candidateSha)) overturned += 1;`
(src/controller/ladder.ts). A rebuild on the same row writes its new
candidate over the refused one, so neither road above enters the
false-block count unless a later version of the spec leaves the old row
holding the refused SHA. The seat's observation of this is its freeze
list's line that opens "OBSERVED 2026-10-12 13:12". What the count itself
should read is M0-238's subject, kept by his answer 3 of (d) in the shape
the seat recommended - the reading by the spec's stem - and is not this
record's.

**THE LOOP.** The protection of (c) answers a road found by reading only:
the seat's verifier over M0-289's landing,
`<control-root>/briefs/<verifier-reply>` (`wc -l -c` printed
113 lines and 15391 bytes, `sha256sum | cut -c1-16` printed
1a4388b2e732a68e, on 2026-10-12 at 17:01), its finding F3 and its line
under NOT CHECKED that opens "- I did not trace the wall-cut road end to
end". A winner whose gate phase the wall's alarm cuts is swept uncharged, and
since M0-289 its sibling's refusal at the lock is uncharged too, so the two
can loop with nothing spent from either budget. It was never sighted live:
over `repo-truth`'s journal after seq 5728, a count of the events whose type
holds "WALL" printed 0 on 2026-10-12 at 17:01.

## 2. The decision

His words of section 0, to the questions they answer:

1. **THE ROWS ARE KEPT UNDER HIS FREEZE.** The rows this package mints are
   kept under his item 8 of (b): the loop's protection by his answer 3 of
   (d), the wait and the resume by his word of (f) and his reply of (h). The
   list itself is the seat's and operator-local (section 0 (b)).
2. **THE LOOP'S PROTECTION IS OWED BEFORE RUNG 4** - his answer 3 of (d) to
   the bullet of (c)'s question 3.
3. **ITEM 4 AS (e) ASKED IT.** A candidate refused at the integration lock
   its own pass holds waits for the sibling's integration and integrates on
   top of it inside the same pass - his word of (f).
4. **THE WIDENING AS (g) ASKED IT.** After a refusal in which no error was
   found, the factory checks the same build again instead of building a new
   one - his reply of (h), read as reading 1 below. His answer 4 of (d) is its
   boundary: the rule of ADR 0029 section 1 (3) stays as it is, and only the
   road after the refusal changes.

Six readings follow. Each is **THE SEAT'S**, and each is
**[operator-confirmable]**:

1. **His reply of (h) is a yes to decision 4.** Its text asks whether his
   earlier yes was not enough and says the two are the same thing; the seat
   reads it as taking the question of (g), which it answers, and the seat
   told him so in its answer of section 0 (h).
2. **Decision 4 covers every gate refusal decided `unmeasured`** by
   `decideFixCycle` (src/controller/fix-cycle.ts) and landed by
   `landUnmeasuredRefusal`, by the question's own words, "refusals in which
   no error was found"; a refusal on condition 2 alone is the measured case,
   all four of section 1's. It does not cover the carry of an unfinished
   measurement past `MEASUREMENT_CARRIES` (`landUnmeasured`'s second caller)
   nor a walk that answered `error` (`landRefusedCandidate`): neither is a
   gate refusal.
3. **The resume of the lock's loser in a later pass is part of item 4.** His
   word of (f) took what (e) asked, a wait inside the pass. That a loser the
   pass could not hold resumes its kept, verified candidate in a later pass
   instead of being rebuilt is the seat's reading - its freeze list's line
   that opens "OBSERVED 2026-10-12 11:05", the seat's row of 11:50:18 quoted under
   (g), and the opening of (g) - which his
   reply of (h) took together with the widening; so the cross-pass resume
   rests on (h) read through reading 1, not on (f) alone.
4. **The shapes of the rows.** One carried record - the kept candidate -
   written on two roads, the reaper's `resume_at_verifying` for every
   evidence-intact stranding it declares of a candidate with no confirmed
   finding against it (the lock's loser among them, and not the
   `pass_sibling` refusal alone) and the gate's `unmeasured` refusal - the
   reaper also declares that outcome for a row still carrying an earlier
   pass's candidate, a refused one included, and the bound to a candidate
   with no finding is taken from decision 4's own words;
   read by the dispatch beside the deferred seat and the deferred fix cycle,
   and resumed over that candidate with no builder; its tree kept from the
   reclaimer until the resume; and a candidate that can no longer be pinned
   falling back to today's builder with the reason in the journal, never
   waiting for an operator. The wait of decision 3 bounded by the pass's
   working wall, a wait the wall cannot hold landing as today and resumed by
   that record. The protection of decision 2 as a charge: the first carry of
   a candidate stays free, and each next carry of the same candidate SHA with
   nothing landed between costs one infrastructure retry, so the existing
   ceiling ends the loop. Each shape is named in its row as the shape known
   on the day, and each row is the home of its mechanism.
5. **The false-block count sees the class.** Once the kept candidate is
   judged again and merged, its row still names the refused SHA, and the
   ladder's rule of section 1 reads its earlier refusal overturned. That is
   a consequence of decision 4, named here; no rung threshold is touched,
   and the count's own definition stays M0-238's.
6. **No `DESIGN.md` amendment.** Section 10 already runs integration from
   step 1 on the moved base under `integrations = 1` and names no landing for
   a lock refusal; section 6's key edge `INTEGRATING -> READY_TO_INTEGRATE`
   says re-integration on a moved base is not an attempt, and its recovery
   line "candidate commit present and evidence intact -> resume at
   `VERIFYING`;" is what the resume carries out; section 9's "A first failure
   buys one fix cycle" is about a failure with a finding, and decision 4 is
   about none. For the lock's loser, section 6's
   `READY_TO_INTEGRATE -> RETRY_WAIT` bullet charges one infrastructure
   retry after a refusal at the lock, and the charge of reading 4 stays
   within it; for the winner whose gate phase the wall cut, which lands
   from INTEGRATING, section 6's recovery line names no counter, so the
   charge of reading 4 has no `DESIGN.md` sentence for or against it and
   makes none false.

## 3. What this ADR does NOT decide

- **Any priority or row.** Those are the rows' footers, each
  **[operator-confirmable]**.
- **The mechanism of any row** - the record's name and home, where it is
  read, the wait's bound and the ceiling's counter. Each row names the shapes
  known on the day, ADR 0029 section 2's precedent.
- **RT-34's road.** It stands BLOCKED at quality attempts 2 of 2, and
  `qualityBar` (src/controller/fix-cycle.ts) refuses a build at that ceiling;
  its road is his.
- **The condition-2 rule's revisit**, which his answer 4 of (d) puts in M5
  with lens statistics.
- **The walk's `error` road and the carry past `MEASUREMENT_CARRIES`**, which
  are not gate refusals (reading 2).
- **The subjects of M0-247, M0-256 and M0-259** - the reclaimer's other gaps,
  a seat resumed and then stopped, and the stage-0 walk and probe paid again
  on a resume.
- **The rung-4 questions** - how many two-builder passes the soak needs, and
  whether the thresholds from rung 3 to rung 4 are his.
- **His other words of those two days** - rung 3 taken, the two batches and
  the lines of the session that ran the ticks - which are not this record's.
- **`DESIGN.md`**, untouched (reading 6).
- **That any tick, task, condition or the gate passes after any row lands.**

## 4. What is filed elsewhere

The rows this package minted are named in its commit messages and are not
listed here, for ADR 0020 section 3's reason: a decision document that
carries a backlog acquires two homes for every row in it.
