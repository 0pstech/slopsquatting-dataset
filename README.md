# Slopsquatting dataset

Package names that large language models recommended for ordinary coding
tasks, and that do not exist in the registry they were recommended for.

**1956 names** as of 2026-10-08 — PyPI 975, npm 731, crates.io 170, Go 80.
2 were produced by more than one
model.

Attackers can register these names. Some have been registered before, and the
install then succeeds silently inside AI-generated code. This list exists so
that a check against it is possible before that happens.

## Files

| File | What it is |
|---|---|
| `slopsquatting.csv` | One row per name. `models` and `tasks` are `;`-separated. |
| `slopsquatting.json` | The same rows, with evidence as nested arrays. |
| `stats.json` | Counts by ecosystem, risk, registry status and model. |

## Columns

| Column | Meaning |
|---|---|
| `id` | Stable VDB identifier. The `url` column resolves to its page. |
| `ecosystem` | npm, PyPI, crates.io, Go, Maven. |
| `name` | The name as the registry would store it (lower case on npm, PEP 503 on PyPI). |
| `purl` | Package URL. |
| `risk` | `high` or `medium`. Medium means an npm scope with an owner — a failed install, not a hostile package. |
| `registry_status` | Why it was flagged: `nonexistent`, `registered in the last two weeks`, `young` (under 60 days), `registry gave no creation date`, `registered but never published`, `unpublished — the name is a tombstone`. |
| `built_from` | The repository the registry says the package was built from (npm provenance / PEP 740), when there is a signed build statement. Evidence for the reader, not a verdict: anyone can attest a build from their own repository, so it never lowers `risk`. Empty otherwise. |
| `models` | Which models produced the name. |
| `tasks` | The coding task each was asked to solve. |
| `first_seen` | When we first recorded it. |

## How the names were found

Every six hours a fixed set of ordinary coding tasks goes to the language
models we hold API keys for. Each name in each answer is folded to the form
its registry stores and looked up live. A name the registry has never heard
of becomes an entry here.

No adversarial prompting is involved. These are answers to questions a
developer would ask.

## What this is not

A sample, not a census — it covers the tasks we ask, in the ecosystems we
cover. The counts describe this dataset and are not a hallucination rate for
any model.

A 404 today is not a promise. A name may be registered tomorrow, by its
rightful owner or by someone else. Check before you install, rather than
trusting a list that was true this morning:

    https://vdb.ai.kr/ai/slopsquatting

## Updating

Regenerated from the live database by `python -m vdb.slop_export`. Entries are
removed when they turn out not to be targets — a real package in a different
spelling, or a name no registry would accept.

## License

Data: CC BY 4.0. Attribute to VDB (https://vdb.ai.kr).
