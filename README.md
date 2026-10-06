# Machine Learning and Deep Learning for RNA-Seq Metadata Completion

This repository contains the data, R/RMarkdown scripts, processed metadata, model outputs, and figures used for my master's thesis on machine-learning-based completion of missing biological metadata in public barley RNA-seq datasets.

The main analysis focused on predicting missing metadata for three biological variables:

- Tissue
- Developmental stage
- Treatment

Random Forest models were used for all three metadata variables, while a Multilayer Perceptron (MLP) was additionally evaluated for treatment prediction.

## Repository Structure

### `barley_rna_seq_data`

This is the main folder containing most of the barley RNA-seq data and machine-learning scripts.

It includes:

- standardized and aligned metadata
- SRA RunTable metadata
- transcript abundance files
- PCA component extraction scripts
- Random Forest modelling scripts
- study-aware cross-validation scripts
- developmental-stage prediction scripts
- tissue prediction scripts
- treatment prediction scripts
- model-generated metadata predictions
- intermediate and final prediction files

Important analysis files include:

- `10_pca_components.Rmd`
- `20_pca_components.Rmd`
- `100_pca_components.Rmd`
- `tissue_50pcs_rf_cv.Rmd`
- `developmental_stage_pca_rf_cv.Rmd`
- `treatment_pca_rf_cv.Rmd`

### `barley_rna_seq_analysis`

This folder contains additional analysis and visualization scripts.

It includes:

- RNA-seq preprocessing and normalization
- PCA and UMAP analysis
- ANOVA/statistical analysis
- metadata summary plots
- PCA component preparation
- figures
- intermediate R data objects used during analysis

Examples include:

- `barley_rna_seq_n.Rmd`
- `barley_rna_seq_pca_umap.Rmd`
- `pca_components.Rmd`
- `Tissue_summary_plot.Rmd`
- `treatment_summary_plots.Rmd`

### Final Annotated Metadata

The final metadata table generated for this thesis is:

`metadata_with_all_predictions_final_clean.csv`

This file contains:

- original metadata annotations
- model-generated metadata predictions
- prediction confidence values
- provenance information indicating whether an annotation was original or model-predicted

The final dataset contains 10,096 RNA-seq samples.

## RNA-Seq Processing

RNA-seq samples were obtained from the NCBI Sequence Read Archive (SRA).

Transcript abundance was quantified using kallisto against the *Hordeum vulgare* cv. Morex V3 transcriptome reference.

Expression values were represented as TPM and transformed using:

`ln(TPM + 1)`

Transcripts with zero variance were removed before dimensionality reduction.

## Dimensionality Reduction

Principal Component Analysis (PCA) was performed on the transformed transcript-expression matrix.

Different numbers of principal components were evaluated for machine-learning prediction:

- 10 PCs
- 20 PCs
- 50 PCs
- 100 PCs

## Machine-Learning Models

### Random Forest

Random Forest models were used for:

- Tissue prediction
- Developmental-stage prediction
- Treatment prediction

The main implementation used:

- R 4.5.2
- `randomForest` 4.7-1.2
- 500 trees
- random seed 123

Both sample-wise and study-aware evaluation strategies were investigated.

### Multilayer Perceptron

An MLP model was additionally evaluated for treatment prediction using the R `nnet` package.

Main settings included:

- R 4.5.2
- `nnet` 7.3-20
- one hidden layer
- 10 hidden units
- softmax output
- weight decay = 0.001
- maximum iterations = 300
- random seed = 123

## Study-Aware Evaluation

To evaluate generalization across independent experiments, SRA studies were separated between training and testing datasets.

In addition to standard sample-wise evaluation, study-aware hold-out testing and study-aware 10-fold cross-validation were performed.

This approach prevents samples from the same SRA study from appearing in both training and test sets.

## Reproducibility

The RMarkdown files provided in this repository document the main preprocessing, dimensionality-reduction, statistical-analysis, machine-learning, cross-validation, and metadata-prediction procedures used in the thesis.

## Data Availability

The processed metadata, prediction outputs, analysis scripts, and final annotated metadata table are provided in this repository.

The final annotated metadata table is:

`metadata_with_all_predictions_final_clean.csv`

## License

License information is provided in the `LICENSE` file.
