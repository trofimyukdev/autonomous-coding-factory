# ADR 0033 - The budget exit DESIGN.md section 7 names appears not to be the one the CLI produces

Date: 2026-09-26. Context: a carrier session (carrier #73) by foreman decision
under the standing delegation of 2026-08-25, not a block. `main` stood at
`71618eb` when the package began - `git rev-parse HEAD origin/main | cut -c1-7 | paste -sd' '`
printed `71618eb 71618eb` on 2026-09-26 at 22:16 - and `git status --short | wc -l`
printed 2 the same minute, the two operator handoffs in a private archive
that is not published.
Nothing under `src/`, `test/`, `scripts/`, `.githooks/`, `factory/checks.yaml`,
`factory/millwright.toml`, `CLAUDE.md`, `PRINCIPLES.md`, `DESIGN.md` or
the private archive was touched by this package, and nothing was written in
`repo-truth`. Every command below ran from this repository's working directory
on 2026-09-26 between 22:17 and 22:19, the reading of the exit expression's
second operand at 23:28, and code is quoted at `71618eb`.

**This document records an apparent divergence between DESIGN.md section 7
and the CLI this factory runs - an inference from minified code (section 1), and the seat's decision about it. It carries no operator
word: the decision is taken under the standing delegation and is
[operator-confirmable], and the row that carries it into the code is named in
this package's commit message, for ADR 0020 section 3's reason.**

## 0. The sentence, and where the code repeats it

DESIGN.md section 7, in its list of what the backend must get right about one
worker call:

```text
- `--max-budget-usd` reports an overrun as exit 2, and the backend classifies that as
  a spent budget rather than a generic crash - the two feed different counters;
```

`git grep -n 'reports an overrun as exit 2' 71618eb -- DESIGN.md src/backend/run.ts`
printed DESIGN.md:396 and src/backend/run.ts:265. The code restates the
sentence twice. The file docstring of src/backend/run.ts says an overrun
"arrives as exit 2 and is a SPENT BUDGET rather", and the comment over the
constant says:

```text
/** DESIGN.md section 7: `--max-budget-usd` reports an overrun as exit 2. */
const BUDGET_EXIT_CODE = 2;
```

`classify` in the same file acts on it: `if (run.exitCode === BUDGET_EXIT_CODE) {`
is followed by `return infra("budget_spent", "the attempt reached --max-budget-usd (exit 2)", usage);`.
test/unit/backend.test.ts drives its case, "gives a --max-budget-usd overrun its
own class rather than calling it a crash", with `exitCode: 2`.

## 1. What the CLI's own code says - an INFERENCE from minified bundles

What follows is read out of the CLI's minified bundles. It is an INFERENCE,
not a measurement: no envelope of a real `--max-budget-usd` overrun has ever
been kept by this factory, because a worker call's stdout and stderr are
written nowhere, and so no exit code of such an ending has been observed.

- The expression that picks the process's exit code at the end of a headless
  session sets 1 for an error result, 1 when the transport closed
  permanently, and 0 otherwise. In 2.1.283
  `node -e 'const b=require("fs").readFileSync("<claude-install>/versions/"+process.argv[1],"latin1");const re=/\w+\(\w+\?\.type==="result"&&\w+\?\.is_error\|\|\w+\?1:0\)/g;let m;while((m=re.exec(b)))console.log(m.index,m[0])' 2.1.283`
  printed `221724237 yo(Wr?.type==="result"&&Wr?.is_error||jn?1:0)`, and the
  same command with 2.1.280 printed
  `212917281 co(lr?.type==="result"&&lr?.is_error||kn?1:0)`.
  The second operand, `jn`, is set a few statements earlier in the same
  function to `pe instanceof xK&&pe.permanentCloseCode!==void 0`, and the
  message beside it says "transport closed permanently":
  `node -e 'const b=require("fs").readFileSync("<claude-install>/versions/2.1.283","latin1");const i=221724237;console.log(b.slice(i-900,i+120))'`
  prints both; so an error envelope and a permanently closed transport both end
  on 1, and neither is a budget-specific code.
- The bundle's `process.exit(2)` call sites are not the budget ending. In 2.1.283
  `node -e 'const b=require("fs").readFileSync("<claude-install>/versions/"+process.argv[1],"latin1");let i=-1,n=0,near=0;while((i=b.indexOf("process.exit(2)",i+1))>=0){n++;if(/budget/i.test(b.slice(i-400,i+100)))near++}console.log(n,near)' 2.1.283`
  printed `16 1`, and the one site whose neighbourhood mentions a budget is
  an embedded script's usage error for its `--variant` argument, which prints
  "--variant must be 'baseline' or 'v<N>'" before it exits. The same command
  with 2.1.280 printed `17 1` on 2026-09-26, its one such site the same
  `--variant` usage error. The count covers `process.exit(2)` calls only; a
  site that sets `process.exitCode` to 2 is not counted by it.
- The CLI does name the ending, in the envelope rather than in the exit code:
  the subtype `error_max_budget_usd`, which src/backend/run.ts already lists in
  the docstring over `readEnding` ("`error_max_budget_usd` for a spent
  `--max-budget-usd`").

Nothing in either journal says otherwise:
`grep -c budget_spent <repo-truth>/factory/state/events.jsonl <repo>/factory/state/events.jsonl`
printed 0 for each file. The `budget_spent` rung has never been recorded
firing.

## 2. What that does today

If the inference holds, a real overrun exits 1 with an error envelope, passes
the exit-2 rung, and reaches the envelope rungs. Since M0-88 landed, an
envelope that carries no reply is `infra_format`, and `readEnding` puts the
CLI's own ending into its detail ("the CLI ended the session as ..."). So the
class is right in its words and wrong in its counter: `chargeFor` in
src/controller/builder.ts sends `budget_spent` to `"budget"` and everything it
does not name, `infra_format` among them, to `"infra_retry"`. An attempt that
spent its budget is retried as an infrastructure failure at the same budget,
which buys the same ending - the confusion the sentence in section 0 exists to
prevent.

## 3. The decision

**[operator-confirmable]**, the seat's, under the standing delegation.

The INTENT of DESIGN.md section 7's sentence stands: a spent budget is its own
class and feeds its own counter, never a generic crash and never an
infrastructure retry. Its MECHANISM - exit 2 - does not describe CLI 2.1.280
or 2.1.283 on the reading of section 1. The code therefore follows the intent
through what the CLI writes into the envelope, and the row that owns it
tests the inference with one live reading that prints the call's exit code
before the rung is rebuilt.

## 4. What this ADR does NOT decide

- **DESIGN.md's own text.** The sentence in section 0 is false in its
  mechanism on the reading above, and its correction waits for the operator's
  word. DESIGN.md has been edited after its ratification before, each time on
  a word or a sanction and with the ratification digest held in
  test/unit/design-ratification.test.ts moved alongside (`git log --format='%h %s' 71618eb -- DESIGN.md`
  lists them); ADR 0025 section 2 is one such edit made by a carrier on the
  operator's answer. This package has neither such a word nor that test file
  in its paths, so it makes no such edit.
- **Whether the exit code is 1.** Section 1 is an inference until the live
  reading prints it.
- **A new exit class.** `budget_spent` already exists (src/backend/exit-class.ts);
  whether its counter is the right one is not reopened here.

## 5. What is filed elsewhere

The row that carries the decision into src/backend/run.ts is named in this
package's commit message and not here, for ADR 0020 section 3's reason: a
decision document that carries a backlog acquires two homes for every row in
it.

## 6. Rework

Reworked 2026-09-26 on the seat's verifier: the title line inside this file
states the divergence as an appearance (the file name and the first commit's
subject are history and keep the older wording); section 1 names the second
operand of the exit expression; section 3 says the live reading TESTS the
inference rather than confirming it.
