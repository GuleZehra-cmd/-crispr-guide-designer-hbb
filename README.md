# CRISPR Guide RNA Designer for the HBB Gene

## What is this?
A Python tool that finds and ranks CRISPR-Cas9 guide RNAs for the human
HBB gene (the gene mutated in sickle cell anaemia).

## Why?
CRISPR edits a gene, but you need to tell it the address where to cut. That address is the 20-letter RNA guide. My tool takes a gene and produces a ranked list of good addresses.

## How it works
1. Scans for NGG PAM sites (the "sticker" Cas9 needs)
2. Takes the 20 letters before each PAM as the guide
3. Keeps guides with 40-60% GC content, ranked by closeness to 50%
4. Repeats on the reverse strand, because Cas9 reads both

## Results
| Strand | Guides passing filter |
|---|---|
| Forward | 34 |
| Reverse | 25 |
| Total | 59 |

Scanning only the forward strand finds 34 guides, while scanning both strands finds 59. So a forward-only scan would miss 25 usable guides (about 42% of the total). This matters because Cas9 can bind an NGG site on either strand of the DNA.

![chart](guide_chart.png)

## Limitations
- Only checks GC content. It doesn't predict cutting efficiency.
- It doesn't check for off-target cuts elsewhere in the genome.
- Guides could also match the nearly identical HBD gene (not checked).

## Data
HBB coding sequence, RefSeq NM_000518.4 (444 bases).

## Run it
Open in Google Colab or run `python guide_designer.py`.
