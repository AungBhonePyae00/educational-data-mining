# Early Prediction of Student Academic Outcomes Using Learning Analytics

## Project Overview

This project investigates whether early student learning activity and student/course characteristics can help identify students at risk of failing or withdrawing from a course.

Using the Open University Learning Analytics Dataset (OULAD), I developed and compared three logistic regression models with different feature sets and early activity observation windows.

## Research Question

Can students at risk of failing or withdrawing be identified using early learning activity and student/course information?

## Dataset

This project uses the Open University Learning Analytics Dataset (OULAD), which contains information about students, courses, assessments, and interactions with an online learning platform.

The analysis includes 32,593 student-course records.

## Methodology

Three logistic regression models were evaluated:

- **Model 1: 14-day activity.** Uses early online activity, previous attempts, studied credits, and course information.
- **Model 2: Extended features.** Adds demographic characteristics to the features used in Model 1.
- **Model 3: 7-day activity.** Uses online activity from the first seven days, along with previous attempts, studied credits, and course information.

The models use numerical preprocessing, categorical encoding, and class-weighted logistic regression. Model performance was evaluated using accuracy, precision, recall, F1-score, and ROC-AUC.

## Results

| Model | Accuracy | F1-score | ROC-AUC |
|---|---:|---:|---:|
| Model 1: 14-day | 68.2% | 0.704 | 0.737 |
| Model 2: Extended | 69.2% | 0.708 | 0.757 |
| Model 3: 7-day | 66.3% | 0.682 | 0.715 |

Model 2 achieved the strongest overall performance across most metrics. Model 1 achieved the highest recall at 72.0%, while Model 3 had the lowest performance across the reported metrics.

## Fairness Analysis

I evaluated recall and precision across gender and age groups. The results showed differences in recall between groups, highlighting the importance of evaluating subgroup performance alongside overall model metrics.

The oldest age group had only 42 test records, so its results should be interpreted cautiously.

## Limitations

The models achieved moderate predictive performance and did not identify every at-risk student. The study also uses a single dataset, and the models may not generalize to other educational settings. Observed differences across demographic groups do not establish their cause or prove discrimination.

## Future Work

Potential improvements include testing additional machine learning algorithms, incorporating early assessment information, evaluating performance on other datasets, and investigating differences in model performance across demographic groups.

## Tools and Technologies

- Python
- pandas and NumPy
- scikit-learn
- Matplotlib
- Jupyter Notebook

## Project Status

The initial modeling, evaluation, comparison, and fairness analysis are complete. Further validation and documentation will help prepare the project for broader research use.