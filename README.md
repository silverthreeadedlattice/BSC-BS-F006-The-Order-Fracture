# ★ Black Star Codex — BSC-BS-F006: The Order Fracture

**Author:** Aaron Bell  
**Framework:** Black Star Codex · Silver Thread Lattice · Black Sun  
**Version:** 1.0.0 · November 20, 2026  
**Status:** Proposed experiment; no observer trials conducted.

> A fracture is a question, not an answer.

## Fracture question

**If the evidence stays the same, why would changing its order change the answer?**

The Observer receives the same five values in different arrangements. The decision rule stays fixed. This experiment asks whether an AI evaluator changes its classification when only presentation order changes.

The Silver Thread Lattice connects each input, response, and scoring decision. The Watchful Eye is the review role. These are framework metaphors; this protocol tests observable software behavior.

## Hypotheses

- **H0:** Classification accuracy does not depend on presentation order under the tested conditions.
- **H1:** At least one presentation order produces a different classification accuracy under the tested conditions.

A changed answer is a candidate fracture. Repeated trials are needed to distinguish an order effect from ordinary response variation.

## Fixed synthetic evidence

These are invented numerical fixtures, not physical sensor observations. Values have no time sequence: their order carries no evidential meaning.

| Packet | Five values in base order | Exact mean | Correct label |
|---|---|---:|---|
| A | 2, 4, 6, 8, 10 | 6 | BELOW |
| B | 10, 12, 14, 16, 18 | 14 | ABOVE |
| C | 6, 8, 10, 12, 14 | 10 | AT |
| D | 0, 0, 0, 0, 49 | 9.8 | BELOW |
| E | 0, 0, 0, 0, 51 | 10.2 | ABOVE |
| F | 0, 0, 0, 0, 50 | 10 | AT |

Use four position orders for every packet:

| Order | Positions taken from base order |
|---|---|
| O1 | 1, 2, 3, 4, 5 |
| O2 | 5, 4, 3, 2, 1 |
| O3 | 5, 1, 2, 3, 4 |
| O4 | 2, 3, 4, 5, 1 |

Some resulting sequences are identical because values repeat. Keep these trials: identical inputs help reveal response variation. Never count identical sequences as distinct order manipulations.

## Observer prompt

Use exactly this prompt, replacing only the bracketed values. Hide packet IDs, order IDs, and the answer key from the evaluator.

```text
The following five numbers are unordered measurements with equal weight:
[VALUES]

Compute their arithmetic mean using all five numbers. Compare the exact
mean with 10, without rounding. Reply with exactly one label:
BELOW if the mean is less than 10;
AT if it equals 10;
ABOVE if the mean is greater than 10.
```

## Procedure

1. Commit this protocol before collecting observer responses. Record the commit hash. A GitHub commit documents a plan; it is not independent validation.
2. Record evaluator/provider, exact model identifier, date, interface, full prompt, and all available sampling settings. Mark unavailable settings as unknown.
3. Build the 24 packet/order combinations. Repeat each five times for 120 trials. Randomize trial order once with `Python's random.Random(6006).shuffle(trials)`, starting from packet A–F, order O1–O4, repeat 1–5. Save the resulting schedule before collection.
4. Start every trial with a fresh context and the same settings. Do not give feedback or repair an answer. Preserve all raw responses, including errors and refusals.
5. Score after collection. Strip surrounding whitespace; only the exact labels BELOW, AT, and ABOVE are valid. Mark everything else INVALID. Do not silently discard trials.
6. Have a separate reviewer check the arithmetic and scoring. A reviewer checking the same run is not an independent replication.

## Recording and analysis

Create `results.csv` with this header:

```csv
trial_id,packet_id,order_id,repeat,values,model,settings,raw_response,scored_label,correct_label,correct,utc_time
```

Quote CSV cells containing commas or newlines. Retain the full prompt and run metadata alongside the CSV.

Report all 120 scheduled trials, missing trials, invalid responses, and accuracy for each packet/order cell. Report how often each cell changes labels across its five repetitions. Compare orders within the same packet; do not pool packets as independent demonstrations of one effect.

**Exploratory fracture flag:** a packet receives different valid labels across different input sequences. Record whether identical inputs also changed labels. This flag does not establish a causal order effect or statistical significance.

**No fracture observed:** all trials return the correct label. This supports stability only for these fixtures and settings. Uniformly wrong answers reveal an accuracy problem even if order stability is perfect.

Treat the first run as exploratory. Before any confirmatory run, freeze the chosen comparison, sample size, analysis, and decision threshold in a new protocol. Include a fresh collection and a separate replication where possible.

## Evidence Gate ledger

| Gate | Current status |
|---|---|
| E0 — Speculative | Order sensitivity proposed |
| E1 — Fracture | Question recorded; no discrepancy observed yet |
| E2 — Testable | Inputs, controls, prompt, and scoring specified |
| E3 — Supported | OPEN — requires collected evidence and analysis |
| E4 — Replicated | OPEN — requires repeat runs |
| E5 — Independently Supported | OPEN — requires independent reproduction |
| E6 — Codex Verified | PENDING — requires E5 and documented review against explicit criteria |

This document claims no experimental PASS. Agreement, disagreement, or order sensitivity would not establish hidden agents, supernatural causes, or changes in physical reality.

## GitHub setup

**Suggested repository name:** `BSC-BS-F006-The-Order-Fracture`

**Repository description:**

> Black Star Codex F006 asks: If the evidence stays the same, why would changing its order change the answer? A controlled AI evaluation using synthetic data, fixed prompts, repeated trials, and an auditable Evidence Gate ledger. Protocol ready; results pending. Independent replication welcome.

Upload this document as `README.md`. Add the saved schedule, raw responses, and results only after conducting the trials. External independent replication is welcome; publish disagreements and failed runs alongside successes.

> The Black Star remembers what the system once got wrong.
