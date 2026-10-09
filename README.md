# Synthetic Biodata Sandbox: Generating Privacy-Preserving Lab Records

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/mercymaraba/synthetic-biodata-sandbox/blob/main/Synthetic_Biodata_Sandbox.ipynb)

Patient lab data is useful for research and training, but it is hard to share because it belongs to real people. This project generates synthetic full blood count records and tests whether they are realistic, useful for analysis, safe from re-identification, and clinically believable to a lab scientist.

No real patient data is used. A simulated cohort of 3,000 patients (Normal, iron deficiency anaemia, malaria, AML and CLL) stands in for a confidential lab dataset.

## Methods compared

| Generator | Approach |
|---|---|
| Independent KDE | One density per column, sampled separately (my original approach) |
| Gaussian copula | Keeps correlations across the whole cohort |
| Stratified copula | A separate copula for each diagnosis |
| Noisy copy (unsafe) | Real records plus noise, included to test the privacy checks |

## Key results (mean of 3 runs)

| Method | Utility (F1) | Privacy risk (MIA AUC, 0.5 ideal) | Clinically inconsistent records |
|---|---|---|---|
| Real data (reference) | 0.97 | 0.51 | 0% |
| Independent KDE | 0.13 | 0.51 | 65% |
| Gaussian copula | 0.51 | 0.52 | 27% |
| Stratified copula | 0.97 | 0.53 | 0% |
| Noisy copy (unsafe) | 0.97 | 0.82 | 0% |

* Sampling each column separately keeps the data private but breaks the clinical links, and 44% of its blast values come out negative.
* Fitting one model per diagnosis was the only method that was private, useful and clinically plausible.
* The noisy copy scored high on utility but leaked training patients, which shows that utility alone says nothing about privacy.

## How to run

Click the **Open in Colab** button above, then choose **Runtime > Run all**. It uses only libraries already installed in Colab and takes about a minute.

## Limitations

* The source cohort is simulated. The next step is to run the same checks on de-identified lab data under ethics approval.
* Distance-based privacy tests are a practical screen, not a formal guarantee. Differential privacy would be needed for that.

## Author

Mercy Jerobon Maraba, BSc Medical Laboratory Science
[LinkedIn](https://linkedin.com/in/mercy-maraba)
