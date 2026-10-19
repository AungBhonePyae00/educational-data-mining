# Early Prediction of Student Academic Outcomes Using Learning Analytics

A machine learning research project investigating whether early student engagement and demographic information can help identify students who may fail or withdraw from a course.

## Research Question

Can students at risk of failing or withdrawing be identified using early learning activity and assessment-related information?

The goal is to explore whether information available early in a course can support earlier student outreach and academic support.

## Project Overview

This project uses the Open University Learning Analytics Dataset (OULAD) to investigate the early prediction of student academic outcomes. I developed and compared three logistic regression models using different feature sets and engagement windows.

The target variable groups final outcomes into two categories:

- **At risk (1):** Fail or Withdrawn
- **Not at risk (0):** Pass or Distinction

The dataset contains 32,593 student-course records. Approximately 52.8% belong to the at-risk category.

## Dataset

**Source:** [Open University Learning Analytics Dataset (OULAD)](https://analyse.kmi.open.ac.uk/open_dataset)

The dataset contains information about student demographics, course registrations, assessments, and interactions with online learning materials.

This project focuses on student information and early engagement activity. Final outcomes are used to construct the target label and are excluded from model input features to prevent target leakage.

The original and processed datasets are excluded from this repository. Download the dataset from the official source to reproduce the analysis.

## Methods

The project follows these steps:

1. Explore the dataset and examine student outcome distributions.
2. Create early engagement features based on online learning activity.
3. Define a binary target for students who fail or withdraw.
4. Split the data into training and test sets while preventing student overlap between the sets.
5. Build three logistic regression pipelines with appropriate preprocessing.
6. Evaluate the models using accuracy, precision, recall, F1-score, and ROC-AUC.
7. Examine performance differences across gender and age groups.
8. Discuss limitations and the responsible use of predictive models in education.

### Models Compared

| Model | Features |
|---|---|
| Model 1: Early engagement | Click activity during the first 14 days, previous attempts, studied credits, course module, and presentation |
| Model 2: Extended features | Model 1 features plus gender, region, highest education, IMD band, age band, and disability |
| Model 3: Earlier prediction | Click activity during the first 7 days, previous attempts, studied credits, course module, and presentation |

The preprocessing and logistic regression steps are combined into pipelines. The models are evaluated on held-out student groups to reduce the risk of information leakage between training and test data.

## Results

| Model | Accuracy | Precision | Recall | F1-score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Model 1: 14-day engagement | 0.682 | 0.689 | 0.720 | 0.704 | 0.737 |
| Model 2: Extended features | 0.692 | 0.706 | 0.711 | 0.708 | 0.757 |
| Model 3: 7-day engagement | 0.663 | 0.676 | 0.688 | 0.682 | 0.715 |

Model 2 achieved the strongest overall performance in accuracy, F1-score, and ROC-AUC. Compared with Model 1, it improved accuracy, precision, F1-score, and ROC-AUC, although recall decreased slightly.

Model 3 used engagement data from only the first seven days and performed less well than the 14-day model. This suggests that the additional engagement window may provide useful predictive information in this dataset.

These results indicate predictive associations, not causal relationships. They do not establish that the selected features cause students to fail or withdraw.

## Fairness Analysis

I examined Model 2 performance across gender and age groups to explore whether the model identified at-risk students equally well across these groups.

**Gender**

- Female students: recall of approximately 0.665.
- Male students: recall of approximately 0.747.
- Difference in recall: approximately 8.2 percentage points.

**Age**

- Ages 0–35: recall of approximately 0.741.
- Ages 35–55: recall of approximately 0.633.
- Ages 55 and older: recall of approximately 0.500.

The oldest age group contained only 42 test records, making its performance estimates particularly uncertain. These observed differences warrant further investigation, but they do not by themselves establish that the model is discriminatory.

This analysis is exploratory. A more complete fairness evaluation would require additional metrics, uncertainty estimates, and validation on other datasets.

## Limitations

- **Limited generalizability:** The analysis uses historical data from a particular educational setting, so the results may not generalize to other institutions, courses, or student populations.
- **Target definition:** The binary target combines failing and withdrawing, although these outcomes may have different causes.
- **Feature selection:** Predictive performance depends on the selected features, target definition, and evaluation procedure.
- **Fairness uncertainty:** Group-level metrics can be unstable when sample sizes are small.
- **Interpretability:** Predictive associations do not explain why a student may struggle academically.
- **Practical use:** A predictive model should not be used as the sole basis for consequential decisions about students.

Any real-world application would require external validation, privacy protections, ongoing performance and fairness monitoring, and meaningful human oversight.

## Repository Structure

```text
educational-data-mining/
├── notebooks/
│   ├── 01_data_understanding.ipynb
│   ├── 02_early_engagement.ipynb
│   └── 03_risk_prediction.ipynb
├── report/
│   └── research_question.md
├── data/       # Local datasets, excluded from Git
├── results/    # Generated results, excluded from Git
├── src/
├── README.md
└── .gitignore

## Tools and Technologies

- Python
- Pandas and NumPy
- Scikit-learn
- Matplotlib and Seaborn
- Jupyter Notebook
- Git and GitHub


## Reproducing the Analysis

1. Clone this repository.
2. Download the [Open University Learning Analytics Dataset (OULAD)](https://analyse.kmi.open.ac.uk/open_dataset).
3. Place the required raw CSV files in the local `data/raw/` directory.
4. Create and activate a Python virtual environment:

   ```powershell
   python -m venv .venv
   .\.venv\Scripts\Activate.ps1
   ```

5. Install the required dependencies:

   ```bash
   python -m pip install -r requirements.txt
   ```

6. Open the notebooks in Jupyter Notebook or VS Code and run them in order, following any documented data preparation steps.

The notebooks document data exploration, feature engineering, model evaluation, and interpretation.

## Conclusion

This project demonstrates a workflow for investigating the early prediction of student academic outcomes using learning analytics. Comparing different engagement windows and feature sets illustrates how model design affects predictive performance.

The fairness analysis also highlights why overall performance metrics alone are not sufficient when evaluating models that could influence student support.

The intended use of this research is to explore how predictive analytics might inform supportive outreach, not to label students or replace academic judgment.