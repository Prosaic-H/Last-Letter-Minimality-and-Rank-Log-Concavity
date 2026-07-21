# Last-Letter Minimality and Rank Log-Concavity

This repository accompanies the paper **"Last-Letter Minimality and Rank
Log-Concavity in Universal Coxeter Groups."** It provides the computational
verification code and machine-readable summaries corresponding to Sections 6
and 7.

The computations are regression evidence only and are not used as proofs.
Every count is a count of **distinct reduced scattered words**. Position
embeddings are used only internally to generate candidates before
deduplication.

## Requirements

- Python 3.11 or later
- No third-party Python packages

Run every command below from the repository root.

## Repository Structure

```text
.
|-- README.md
|-- code/
|   |-- verification_core.py
|   |-- verify_append_gain_failure.py
|   |-- verify_diagonal_transfer_failure.py
|   |-- verify_alternating_suffix_injection.py
|   |-- verify_half_sandwich.py
|   |-- verify_main_invariants.py
|   |-- verify_transfer_polynomials.py
|   `-- verify_section7_conjectures.py
|-- examples/
|   `-- README.md
`-- data/
    `-- README.md
```

`verification_core.py` contains deterministic lexicographic enumeration,
direct distinct-word counting, and the append-gain recurrence shared by the
seven command-line checks. All arithmetic is exact integer arithmetic.

## Correspondence With the Paper

| Paper location | Mathematical object | Command |
|---|---|---|
| Example 6.1 | An append-gain polynomial that is not log-concave | `python code/verify_append_gain_failure.py` |
| Example 6.2 | Failure of the diagonal transfer analogue | `python code/verify_diagonal_transfer_failure.py` |
| Lemma 3.3 and Theorem 4.8 | Recurrence validation, continuation log-concavity, last-letter ratio minimum, and rank log-concavity | `python code/verify_main_invariants.py` |
| Lemma 4.3 and the half-sandwich identities | Alternating-suffix injection and the two denominator-free defects | `python code/verify_alternating_suffix_injection.py` and `python code/verify_half_sandwich.py` |
| Corollary 5.8 | Off-diagonal transfer-polynomial log-concavity | `python code/verify_transfer_polynomials.py` |
| Corollaries 5.2 and 5.3 | Return- and open-path ratio sandwiches | `python code/verify_half_sandwich.py` |
| Section 7 | Previous-terminal maximizer and adjacent compensation conjectures | `python code/verify_section7_conjectures.py` |

## Reproducing the Paper Ranges

The following commands use the full ranges recorded in Sections 6 and 7:

```console
python code/verify_append_gain_failure.py --output data/example_6_1.json
python code/verify_diagonal_transfer_failure.py --output data/example_6_2.json
python code/verify_alternating_suffix_injection.py --output data/alternating_suffix_injection.json
python code/verify_half_sandwich.py --output data/half_sandwich.json
python code/verify_main_invariants.py --output data/main_invariants.json
python code/verify_transfer_polynomials.py --output data/transfer_polynomials.json
python code/verify_section7_conjectures.py --output data/section7_conjectures.json
```

Expected headline totals include:

| Check | Expected total |
|---|---:|
| Alternating-suffix source instances | 2,346 |
| Instances for each structural half-sandwich identity | 2,304 |
| Words in the main-invariant regression | 1,006,729 |
| Previous-letter inequalities in Section 7 | 10,088,798 |
| Terminal/maximizer events in Section 7 | 2,548,760 |
| Adjacent compensation inequalities in Section 7 | 2,548,760 |

The full runs are exhaustive within the stated finite ranges and can take
several minutes. For a faster installation check, use `--quick` on the four
large regression scripts:

```console
python code/verify_half_sandwich.py --quick
python code/verify_main_invariants.py --quick
python code/verify_transfer_polynomials.py --quick
python code/verify_section7_conjectures.py --quick
```

## Output Format

Each script prints a concise deterministic summary. Passing `--output PATH`
also writes the same summary as UTF-8 JSON with sorted keys. A failed assertion
stops at the first lexicographic counterexample and includes the ambient word,
letters, degree, and relevant coefficient data in the exception message.

## Scope

Finite regression cannot replace the proofs in the paper. In particular, the
Section 7 scripts report evidence for conjectural refinements only; a zero
failure count in the tested range is not a proof.
