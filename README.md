# rsomics-fasta-digest

In-silico enzymatic digestion of a protein FASTA into peptides, with
missed-cleavage and peptide-length filtering.

## Install

```
cargo install rsomics-fasta-digest
```

## Usage

```
# tryptic digest, fully cleaved, default 6-50 aa peptides
rsomics-fasta-digest proteins.fa

# allow up to 1 missed cleavage, write a peptide table
rsomics-fasta-digest proteins.fa -e trypsin -m 1 -o peptides.tsv

# LysC digest keeping shorter peptides
rsomics-fasta-digest proteins.fa -e lysc --min-len 4 --max-len 60
```

- `-e, --enzyme` — `trypsin`, `lysc`, or `chymotrypsin` (default `trypsin`).
- `-m, --missed-cleavages` — max missed cleavages (default `0`).
- `--min-len` / `--max-len` — peptide length bounds (default `6` / `50`).
- `-o, --output` — output path (`-` = stdout); one peptide per line.

## Origin

Independent Rust implementation of in-silico enzymatic protein digestion.
Cleavage follows the standard per-enzyme rules (trypsin and LysC cut after
K/R and K respectively; chymotrypsin after aromatic residues), combined with
the missed-cleavage and peptide-length filtering used in proteomics workflows.
No single upstream CLI is used as a byte-level oracle; the enzyme rules follow
the widely published conventions (e.g. ExPASy PeptideCutter).

License: MIT OR Apache-2.0.
Upstream credit: standard proteomic cleavage rules (ExPASy PeptideCutter and
common MS-proteomics digestors).
