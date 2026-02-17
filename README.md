# TSC2 Variant Abundance QC Analysis

## Overview

This notebook performs quality control (QC) filtering on TSC2 VAMP-seq variant abundance scores by applying a read-count frequency threshold at the variant level across biological replicates.

## Input Files

| File | Description |
|------|-------------|
| `20260217_Lib1_counts_and_scores.csv` | Per-replicate bin counts and scores for Library 1 (2 replicates, 7,902 rows) |
| `20260217_Lib2_counts_and_scores.csv` | Per-replicate bin counts and scores for Library 2 (3 replicates, 18,050 rows) |
| `20260217_TSC2_lib1_scores.csv` | Averaged abundance scores for Library 1 (3,951 variants) |
| `20260217_TSC2_lib2_scores.csv` | Averaged abundance scores for Library 2 (6,017 variants) |

## QC Method

A frequency-based QC threshold is applied following the approach from [Matreyek et al., 2018](https://doi.org/10.1038/s41588-018-0122-z):

1. **Sum bin counts** — For each variant in each replicate, `count_1` through `count_4` are summed into a total count.
2. **Compute frequency** — Each variant's total count is divided by the replicate's total to get its frequency.
3. **Apply threshold** — Variants must have a frequency above 1×10⁻⁴·⁷⁵ (~1.78×10⁻⁵).
4. **Flag passing variants** — A `QC_flag` boolean column is added to the scores files:
   - **Library 1 (2 replicates):** Variant must pass threshold in **both** replicates.
   - **Library 2 (3 replicates):** Variant must pass threshold in **at least 2 of 3** replicates.

## Output Files

| File                               | Description                                                    |
| ---------------------------------- | -------------------------------------------------------------- |
| `20260217_TSC2_lib1_scores_QC.csv` | Library 1 scores with `QC_flag` column (3,943 / 3,951 passing) |
| `20260217_TSC2_lib2_scores_QC.csv` | Library 2 scores with `QC_flag` column (5,869 / 6,017 passing) |

### Output columns

| Column | Description |
|--------|-------------|
| `variant` | HGVS protein variant identifier (ENSP00000219476.3) |
| `abundance_1`, `abundance_2`, (`abundance_3`) | Per-replicate abundance scores |
| `abundance_avg` | Mean abundance across replicates |
| `variance` | Variance of abundance across replicates |
| `std_dev` | Standard deviation of abundance across replicates |
| `QC_flag` | `True` if the variant passes the frequency threshold in sufficient replicates |
## Also included:

The files below were used to generate the input files using CountESS V 0.1.16 (https://github.com/CountESS-Project/CountESS/tree/main)

| File                           | Description                                                                                              |
| ------------------------------ | -------------------------------------------------------------------------------------------------------- |
| `20260217_final_TSC2_lib1.ini` | CountESS config file for counting and scoring using .fastq files and a variant barcode map for library 1 |
| `20260217_final_TSC2_lib2.ini` | CountESS config file for counting and scoring using .fastq files and a variant barcode map for library 2 |
| 'TSC2_lib1_map.csv'            | Variant to barcode map generated using Pacybara (Weile et al., 2024) for library 1                       |
| 'TSC2_lib2_map.csv'            | Variant to barcode map generated using Pacybara for library 2                                            |


## References:

Matreyek, K.A., Starita, L.M., Stephany, J.J., Martin, B., Chiasson, M.A., Gray, V.E., Kircher, M., Khechaduri, A., Dines, J.N., Hause, R.J., et al. (2018). Multiplex assessment of protein variant abundance by massively parallel sequencing. Nat Genet _50_, 874–882. https://doi.org/10.1038/s41588-018-0122-z.

Weile, J., Ferra, G., Boyle, G., Pendyala, S., Amorosi, C., Yeh, C.-L., Cote, A.G., Kishore, N., Tabet, D., Loggerenberg, W. van, et al. (2024). Pacybara: accurate long-read sequencing for barcoded mutagenized allelic libraries. Bioinformatics _40_, btae182. https://doi.org/10.1093/bioinformatics/btae182.