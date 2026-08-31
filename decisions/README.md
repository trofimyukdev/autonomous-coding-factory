# Decisions (ADRs) - the published subset

The private repository carries 22 ADRs, measured on 2026-08-31 with
`git -C <repo> ls-tree --name-only main docs/decisions/ | wc -l` -> `22`. Eight of
them are reproduced here: the ones that decide something a reader of `DESIGN.md`
cannot infer from the design itself. The numbering is the private repository's and
is left unrenumbered, so the gaps below are real gaps and not lost files.

Cross-references of the form `docs/decisions/NNNN-...` inside these files and
inside `DESIGN.md` name files in the private repository. Only the eight listed
here are published.

Where an ADR quotes the operator in Russian, the Russian is kept verbatim - it is
the authority a decision stands on, and a translation is a paraphrase - with the
English translation beside it.

| ADR | Filed | What it decides |
|---|---|---|
| [0002](0002-fix-cycle-verification.md) | 2026-08-17 | A fix cycle answering a verifier earns a second independent verification pass; when that is mandatory rather than optional. |
| [0004](0004-m0-exit-and-queue-composition.md) | 2026-08-18 | The M0 exit review: five measured defects, what holds the milestone open and what does not, and the third fix lane. |
| [0005](0005-model-layout-and-the-foreman-seat.md) | 2026-08-19 | Which model and effort each seat runs on, and the acceptance seat (the foreman) that ADR 0001 had no row for. |
| [0017](0017-m0-62-fourth-stop-and-the-split.md) | 2026-08-24 | One task stopped four times: the operator splits it rather than re-issuing it a fifth time. |
| [0018](0018-the-roadmap-drift-and-the-three-gates.md) | 2026-08-25 | The queue filed findings and planned nothing; three gates end that drift, and a finding may not outrank the roadmap silently. |
| [0020](0020-the-controller-may-give-up-on-one-task.md) | 2026-08-29 | The controller is allowed to give up on one task, and the three questions the M2 chain could not answer. |
| [0021](0021-m3-the-chain-the-band-the-marker-and-the-contracts.md) | 2026-08-30 | M3 as an ordered chain: the planning band, the provenance marker, and the contracts the design left open. |
| [0022](0022-the-comparison-reconciled.md) | 2026-08-30 | The factory's own output compared against a separate research pass, reconciled to what has practical value. |

The `Filed` column is the date of the commit that added the file, measured on
2026-08-31 with, for each file:

```sh
git -C <repo> log --diff-filter=A --format='%ad' --date=short main -- docs/decisions/<file> | tail -1
```
