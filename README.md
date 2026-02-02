# Finding the Most Natural Protein Sequence using ProteinBERT

## Overview

This repository contains a bioinformatics pipeline for identifying the most natural protein sequences using ProteinBERT, a deep learning model trained on large-scale protein sequence data.
The workflow evaluates candidate protein sequences and ranks them based on their naturalness score, reflecting how closely a sequence resembles naturally occurring proteins.

This project is part of an evolutionary-inspired in-silico protein engineering framework, where ProteinBERT is used as a final filtering step after sequence optimization.

---

## Key Idea

> Not all stable sequences are biologically natural.
> ProteinBERT helps quantify how natural-like a protein sequence is by leveraging contextual amino acid probabilities learned from real protein data.

---

## Methodology

### 1. Input Sequences

* Candidate protein sequences are provided in FASTA format
* These sequences are typically generated from:

  * Consensus sequence construction
  * In-silico mutagenesis
  * Genetic Algorithm optimization

---

### 2. ProteinBERT Model

ProteinBERT is a transformer-based protein language model that:

* Separates local (convolutional layers) and global (fully connected layers) representations
* Uses global attention instead of self-attention
* Achieves linear complexity with respect to sequence length

This makes it efficient and well-suited for long protein sequences.

---

### 3. Naturalness Scoring

Each protein sequence is scored using the pretrained ProteinBERT model:

1. Sequences are tokenized into amino acid representations
2. The model predicts the probability of each amino acid given its context
3. A naturalness score is computed as:

[
\text{Score} = \sum \log(\text{probability} + \epsilon)
]

Where:

* Higher scores indicate more biologically natural sequences
* ϵ is a small constant to avoid numerical instability

---

### 4. Ranking and Selection

* All sequences are ranked by their naturalness scores
* The top N sequences (default: 10) are selected
* These sequences are strong candidates for:

  * Structural prediction
  * Functional validation
  * Experimental testing

---
## Output

* `naturalness_scores.csv`
  Contains:

  * Sequence ID
  * Naturalness score
  * Rank

* `top_natural_sequences.fasta`
  FASTA file of the highest-scoring sequences

---

## Interpretation of Results

* Higher (less negative) scores → sequences closer to natural proteins
* Sequences with similar scores indicate:

  * Comparable biological plausibility
  * Consistent ProteinBERT confidence

These sequences can be confidently forwarded to structure prediction (for example, Phyre2) or wet-lab validation.

---

## Applications

* Protein engineering
* Stability-optimized enzyme design
* Filtering GA-generated sequences
* Synthetic biology
* Industrial enzyme optimization

---


