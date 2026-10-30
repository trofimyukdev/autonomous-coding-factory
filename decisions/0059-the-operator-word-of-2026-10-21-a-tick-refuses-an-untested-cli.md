# ADR 0059 - The operator's words of 2026-10-21: a tick refuses a Claude CLI other than the tested one, and the janitor's orphan rule takes the user's service manager

Date: 2026-10-21. Context: a carrier session (carrier #113, package item
K9, the foreman seat's corrections 1 and 2 to its kickoff), by foreman
decision under the standing delegation of 2026-08-25 - not a block - to
give a home to two words the operator typed in the foreman seat's session
on 2026-10-21, and to the questions they answer. M0-318's outcome paragraph
that opens "THE OPERATOR'S WORD FIRST" asks for this record: DESIGN.md's
text is his, so its row is opened only after his word on section 12's
sentence is recorded here, and the record that holds the word edits the
sentence. Two commits write this record. The first wrote this file with
the first word, DESIGN.md section 12's sentence, and section 12's digest
with its dated paragraph in test/unit/design-ratification.test.ts. The
second, after the second word reached the carrier, adds the second word
(sections 0 (b) and 5, with the title and the headings of sections 0 and
1 that two words need), DESIGN.md section 13's sentence, and section 13's
digest with its dated paragraph in the same test file, and nothing else.

**This document records operator words and what they decide. It carries
no mechanism and moves no priority. M0-318 carries out the first and is
not edited by this record; M0-319 carries out the second and points here
(discipline 12).**

## 0. The words, and the questions they answer

### (a) The CLI version protection - 2026-10-21 21:50:10

Quoted verbatim on ADR 0005's precedent, Russian as typed. One transcript
holds all four rows of (a) and (b), the session of the foreman seat then,
`<transcript>` below. Each row was printed by its uuid from the transcript, and
each quoted line equals a whole line of the row's text, character for
character, a trailing space included; line numbers count the row's text
lines from 1, blank lines included. Timestamps are UTC; the time beside
each is that timestamp plus three hours, local time.

The question. The seat's assistant row at
2026-10-21T18:45:02.247Z (21:45:02),
its stop reason `end_turn`, is the last seat text before his word: between
the two rows the transcript holds one `system` row and two `queue-operation` rows and
no other text but the enqueue of the same message. Its line 19 opens the list of questions, and its line 20 is
the one his first line answers:

```text
**Из пакета #112 появились вопросы к тебе.** Задам по одному, утром:
- защита версии CLI (M0-318) меняет фразу в DESIGN §12 и требует твоего слова. До неё в repo-truth должен лечь `tested` 2.1.306, иначе тики repo-truth начнут отказывать. Пока держу её вне пика;
```

"**Questions for you came out of package #112.** I will ask them one at
a time, in the morning: / - the CLI version protection (M0-318) changes a
sentence in DESIGN section 12 and needs your word. Before it, `tested`
2.1.306 must land in repo-truth, or repo-truth's ticks will start to
refuse. For now I keep it out of the pick;"

The word. His row at
2026-10-21T18:50:10.862Z (21:50:10), `origin.kind` `human`, line 1 of
four (lines 2 and 3 ask the seat to explain the other questions in plain
words, and line 4 asks what is needed of him; none decides anything this
record carries):

```text
* да, защищай версию в repo-truth 
```

"* yes, protect the version in repo-truth"

### (b) The janitor's orphan rule - 2026-10-21 22:32:56

The question. The seat's assistant row at
2026-10-21T18:53:10.965Z (21:53:10),
its stop reason `end_turn`, is the last seat text before his word: between
the two rows the transcript holds one `system` row and two `queue-operation` rows,
the enqueue and dequeue of his same message, and no other text. Its
lines 5, 7 and 9 put the question:

```text
Убирать их должен уборщик фабрики, и только своих, никогда твои программы. Правило в DESIGN §13 узнаёт сироту по признаку «родитель — процесс №1». На этой машине это не так. Я проверил: осиротевший процесс переходит не к №1, а к systemd твоего пользователя. Признак не срабатывает никогда, и уборщик не остановит ни одну сироту.
```

"The factory's janitor must clean them up, and only its own, never your
programs. The rule in DESIGN section 13 recognises an orphan by the sign
'the parent is process no. 1'. On this machine that is not so. I checked:
an orphaned process passes not to no. 1 but to your user's systemd. The
sign never fires, and the janitor will not stop a single orphan."

```text
Предложение: признак «родитель — процесс №1 или systemd пользователя». Остальные проверки остаются: возраст процесса и совпадение времени старта и командной строки с записью фабрики. Поэтому чужое уборщик не тронет. Нужно это только для работы без присмотра, по таймеру.
```

"Proposal: the sign 'the parent is process no. 1 or the user's systemd'.
The other checks stay: the process's age, and its start time and command
line matching the factory's record. So the janitor will not touch what is
not its own. This is needed only for unattended work, on the timer."

```text
**Вопрос: расширяем правило так?** Рекомендую: да. Можно ответить и утром, ночью это ничего не блокирует.
```

"**Question: do we widen the rule this way?** I recommend: yes. You can
also answer in the morning; at night this blocks nothing."

The word. His row at
2026-10-21T19:32:56.094Z (22:32:56), `origin.kind` `human`, its one line:

```text
Да по сиротам, делай
```

"Yes on the orphans, do it"

## 1. What the first word decides

His word is a yes to the question of line 20: the CLI version protection
of M0-318 goes ahead, and with it the change of DESIGN.md section 12's
sentence that the question named. His words name repo-truth, the
consumer whose ticks the factory runs and the one line 20 names. M0-318
builds the refusal for every consumer, each against its own
`factory/compat.json`: that the protection is not confined to repo-truth
is THE SEAT'S READING **[operator-confirmable]**, a widening of his words.
His earlier word on the factory's own CLI pin narrowed it to the factory
and repo-truth (ADR 0058, its line 157, his answer 2), and the one other
consumer, the first (private) consumer, is paused by his word of
2026-09-10; its compat.json names `tested` 2.1.233
(`git -C <first-consumer> show HEAD:factory/compat.json`
printed it on 2026-10-21), so its ticks too would refuse after M0-318
lands until that file moves.

## 2. The sentence of DESIGN.md section 12

Before this record, section 12 said: "a version above the minimum but
outside the tested set notifies rather than passing in silence". It now
says what the code does today - a version above the tested one notifies -
and what M0-318 adds and is not done today: a version other than the
consumer's tested one is also refused by a tick before any worker call
(its part (1)), and an attended `doctor` reports that refusal as a
failing check beside the version's own, which answers as today (its part
(3)). The new wording is THE SEAT'S READING **[operator-confirmable]** of
what M0-318 builds, and not his words; he said yes to the protection, and
the seat wrote the sentence.

## 3. Section 7's steps 1b and 2b are left to M0-318's landing

Steps 1b and 2b of DESIGN.md section 7 count the doctor-lite checks ("all
six are asked at once", "the other three"). They are true of the code
today, and they turn false only when M0-318's check lands, as M0-318's
outcome says. So this record leaves them as they are, THE CARRIER'S
READING **[operator-confirmable]**: editing them now would make section 7
name a check the code does not run. M0-318's own paths forbid DESIGN.md,
so the count is the foreman seat's to bring to the code after M0-318
lands, by the next carrier package, with section 7's digest.

## 4. What lands first

repo-truth's `factory/compat.json` names `tested` 2.1.233 at its
origin/main, while its ticks run the pinned 2.1.306 (M0-318's outcome
says so). On the day M0-318 lands, every repo-truth tick refuses until
that file carries 2.1.306. The change is his `!` line in repo-truth's next
packet, and it lands before M0-318's merge. Until then the seat holds
M0-318 out of the pick, as line 20 of the question says.

## 5. What the second word decides

His second word is a yes to the question of (b): DESIGN.md section 13's
predicate for the janitor's reap, "parent is init, older than 120 s,
command line matches a worker", now reads "parent is init or the user's
service manager (systemd --user), older than 120 s, command line matches a
worker". The other clauses are unchanged, and the rule that blind
pattern-based process killing is forbidden to everyone stands beside it.
The proposal is the seat's, its line 7; only the yes is his. That "the
user's service manager" is told apart by the parent's command line and
user id, read from the process table and compared whole, and never by a
name pattern alone, is THE SEAT'S READING **[operator-confirmable]** of how
the rule is applied; M0-319 builds it. The seat's datum for the question:
on this machine an orphaned `sleep` was re-parented to a process whose
command line was "/usr/lib/systemd/systemd --user", not to pid 1, as
M0-319's paragraph that opens "A READING NAMED" recorded before this word.
