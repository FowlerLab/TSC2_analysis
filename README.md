# TSC2 Manuscript Files

## Data Files

| File | Description |
|------|-------------|
| `20260217_TSC2_lib1_scores.csv` | Averaged abundance scores for Library 1 (3,951 variants) |
| `20260217_TSC2_lib2_scores.csv` | Averaged abundance scores for Library 2 (6,017 variants) |

## CountESS Files:

The files below were used to generate the input files using CountESS V 0.1.16 (https://github.com/CountESS-Project/CountESS/tree/main)

| File                           | Description                                                                                              |
| ------------------------------ | -------------------------------------------------------------------------------------------------------- |
| `20260217_final_TSC2_lib1.ini` | CountESS config file for counting and scoring using .fastq files and a variant barcode map for library 1 |
| `20260217_final_TSC2_lib2.ini` | CountESS config file for counting and scoring using .fastq files and a variant barcode map for library 2 |
| 'TSC2_lib1_map.csv'            | Variant to barcode map generated using Pacybara (Weile et al., 2024) for library 1                       |
| 'TSC2_lib2_map.csv'            | Variant to barcode map generated using Pacybara for library 2                                            |

## References:

Weile, J., Ferra, G., Boyle, G., Pendyala, S., Amorosi, C., Yeh, C.-L., Cote, A.G., Kishore, N., Tabet, D., Loggerenberg, W. van, et al. (2024). Pacybara: accurate long-read sequencing for barcoded mutagenized allelic libraries. Bioinformatics _40_, btae182. https://doi.org/10.1093/bioinformatics/btae182.
