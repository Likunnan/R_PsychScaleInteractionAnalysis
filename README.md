# PsychScaleInteractionAnalysis: R Code for Psychometric Evaluation and Interaction Effect Analysis

This repository contains an R script for a comprehensive analysis of psychological scale data. The script performs:
1.  Psychometric evaluation of measurement scales (KMO, Bartlett's Test, Cronbach's Alpha, CFA, CR, AVE).
2.  Principal Component Analysis (PCA) to derive composite scores for selected scales (H, J, K).
3.  Linear regression modeling to examine main effects of groups and their interaction effects with PCA-derived scores.
4.  Generation of interaction plots and tables.

## Prerequisites

* **R:** Version 4.0 or higher recommended.
* **RStudio:** Recommended for ease of use.
* **R Packages:** The script attempts to automatically install missing packages:
    * `tidyr`
    * `dplyr`
    * `ggplot2`
    * `psych`
    * `interactions`
    * `broom`
    * `lavaan`
    * `semTools`
* **Data File:** A CSV file named `Data_Preprocessing.csv` is required. It should be in the same directory as the R script, or the script's file path must be updated.

## Data Structure

The `Data_Preprocessing.csv` file is expected to contain:
* Items for scales C, D, E, G (e.g., C1, C2, C3, etc.), used as outcome variables after pivoting.
* Items for scales H, J, K (e.g., H1, H2, H3, H4, etc.), used for PCA.
* Each row in the original wide-format data is assumed to represent an independent observation or participant.

## Script Workflow

The R script (`analysis_script.R` - *please replace with your actual script filename*) executes the following:

1.  **Setup:** Installs (if needed) and loads required R packages.
2.  **Data Loading:** Loads `Data_Preprocessing.csv`. **Important:** Modify `read.csv()` path if your file is located elsewhere.
3.  **Psychometric Evaluation:**
    * KMO and Bartlett's Test.
    * Cronbach's Alpha.
    * Confirmatory Factor Analysis (CFA) with model summary and fit indices.
    * Composite Reliability (CR) and Average Variance Extracted (AVE).
4.  **Principal Component Analysis (PCA):** Extracts first principal component scores for H, J, and K scales (H\_pca, J\_pca, K\_pca).
5.  **Data Preparation for Regression:**
    * Transforms data to long format. `value` column holds item scores for C, D, E, G; `group` variable (C, D, E, G) derived from item names.
    * Filters for specified groups (default: C, D, E, G). Modify `filter()` for different groups.
    * Sets group "C" as the reference level for regression.
6.  **Regression Modeling and Interaction Analysis:**
    * Builds a linear model: `value ~ group * H_pca + group * J_pca + group * K_pca`.
    * Outputs model summary.
    * Visualizes interactions for `group` with H\_pca, J\_pca, and K\_pca. Plots are saved as PNG files (e.g., `interaction_plot_H.png`) in the working directory.
    * Creates a table of interaction effects.
7.  **Session Information:** Prints R and package versions for reproducibility.

## How to Run

1.  Ensure R and RStudio (recommended) are installed.
2.  Download the R script and `Data_Preprocessing.csv` into the same directory.
3.  Open the R script in RStudio.
4.  Update the `read.csv()` path in the script if needed.
5.  Run the entire script. Plots are saved to your R working directory (check with `getwd()`).

## Interpreting Output

* **Psychometric Section:** Check for KMO > 0.6, significant Bartlett's test, Cronbach's Alpha > 0.7, good CFA fit (e.g., CFI/TLI > 0.90-0.95, RMSEA < 0.06-0.08, SRMR < 0.08), CR > 0.7, and AVE > 0.5.
* **Regression Summary:** Analyze coefficients, p-values, and magnitudes for main and interaction effects.
* **Interaction Plots (Saved PNGs):** Visualize how the relationship between PCA scores and `value` varies across `group`s.
* **Working Directory for Plots:** Run `getwd()` in R console to find the save location for plots.

## Customization

* **File Path:** Update `read.csv()` for `Data_Preprocessing.csv`.
* **Group Filtering:** Modify `filter()` in Step 5 for different analytical groups.
* **CFA Model:** Update `cfa_model_string` in Step 3.3 for different scale items or factor structures.
* **Plot Saving:** Customize `ggsave()` parameters (filenames, dimensions, DPI) in Step 6.1.

## License

This project is licensed under the MIT License. See the `LICENSE.md` file for details.

Copyright (c) 2025 Rongyi Chen

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

## Citation
If you use this code in your research, please consider citing this repository.
