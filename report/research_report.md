# Early Prediction of Student Academic Outcomes Using Learning Analytics

## Abstract

This project investigates whether students at risk of failing or withdrawing from an online course can be identified using early learning activity and student information. Using the Open University Learning Analytics Dataset (OULAD), I developed and compared three machine learning models based on student engagement during the first 7 or 14 days of a course. Logistic regression was used to predict whether a student would fail or withdraw. The models were evaluated using accuracy, precision, recall, F1-score, and ROC-AUC. The extended model, which included demographic and educational background information, achieved the highest ROC-AUC of approximately 0.757. The results suggest that early learning activity can provide useful signals for identifying students who may need additional support. However, the models have limitations and should not be used as the sole basis for decisions about individual students.

## 1. Introduction

Students may experience academic difficulties before their final course results become available. Identifying early signs of difficulty could help instructors and educational institutions provide support before students fail or withdraw.

Learning analytics uses data generated during learning activities to better understand student behavior and academic progress. Online learning platforms record information such as student clicks, assessment results, and course participation. These data can be used to investigate whether early engagement patterns are associated with later academic outcomes.

The goal of this project is to explore how machine learning can support the early identification of students who may be at risk of unsuccessful academic outcomes.

### Research Question

Can students at risk of failing or withdrawing be identified using early learning activity and assessment information?

## 2. Dataset

This project uses the Open University Learning Analytics Dataset (OULAD), a publicly available dataset containing information about students, courses, assessments, and interactions with an online learning platform.

The analysis uses student-course records and learning activity information to construct early engagement features. The final modeling dataset contains 32,593 student-course records.

The target variable, `at_risk`, was defined as follows:

- **At risk (1):** Students whose final result was Fail or Withdrawn.
- **Not at risk (0):** Students whose final result was Pass or Distinction.

The dataset contains approximately 52.8% at-risk records and 47.2% not-at-risk records.

### Feature Engineering

The main engagement features were created by counting student clicks during the first 7 or 14 days of a course. Additional predictors included the number of previous attempts, studied credits, course module, and course presentation.

The extended model also included demographic and educational background features, such as gender, region, highest education level, deprivation band, age band, and disability status.

Final course outcomes were used only to construct the target variable. They were not included as model predictors.

## 3. Methodology

### Model 1: Early Engagement Using the First 14 Days

The first model used the number of clicks during the first 14 days, previous attempts, studied credits, course module, and course presentation.

This model established a baseline for evaluating how well early engagement and basic course information could identify at-risk students.

### Model 2: Extended Feature Set

The second model used the same predictors as Model 1, with additional demographic and educational background information.

The purpose was to investigate whether these additional features improved predictive performance and to examine whether model performance differed across demographic groups.

### Model 3: Early Engagement Using the First 7 Days

The third model used clicks from only the first 7 days, together with previous attempts, studied credits, course module, and course presentation.

This model explored the trade-off between earlier predictions and predictive performance.

### Data Preparation and Evaluation

The models used logistic regression with preprocessing pipelines. Numeric features were imputed and standardized, while categorical features were imputed and one-hot encoded.

Data were divided into training and testing sets. To reduce the risk of information leakage between records belonging to the same student, student-level separation was checked during the splitting process.

Each model was evaluated using:

- **Accuracy:** The proportion of predictions that were correct.
- **Precision:** The proportion of predicted at-risk records that were actually at risk.
- **Recall:** The proportion of actual at-risk records that the model identified.
- **F1-score:** A combined measure of precision and recall.
- **ROC-AUC:** A measure of how well the model distinguishes between the two outcome groups across classification thresholds.

## 4. Results

### Model Performance Comparison

| Metric | Model 1: 14-day | Model 2: Extended | Model 3: 7-day |
|---|---:|---:|---:|
| Accuracy | 0.682 | 0.692 | 0.663 |
| Precision | 0.689 | 0.706 | 0.676 |
| Recall | 0.720 | 0.711 | 0.688 |
| F1-score | 0.704 | 0.708 | 0.682 |
| ROC-AUC | 0.737 | 0.757 | 0.715 |

*Figure 1. Comparison of predictive performance across the three models.*

Model 2 achieved the highest accuracy, precision, F1-score, and ROC-AUC. Its ROC-AUC was approximately 0.757, indicating better discrimination between at-risk and not-at-risk records than the other two models in this evaluation.

Model 1 achieved the highest recall at approximately 0.720. This means it identified a larger proportion of at-risk records than the other models at their evaluated classification thresholds.

Model 3 had the lowest scores across the reported metrics. Its results suggest that using only the first 7 days of engagement information reduced predictive performance compared with using 14 days of engagement information.

Although Model 2 performed best overall on several metrics, the differences should be interpreted in the context of the dataset, feature selection, and evaluation procedure. These results do not establish that the same performance would generalize to other institutions or student populations.

## 5. Fairness Analysis

Model 2 was examined to see whether recall differed between female and male records.

| Group | Number of test records | Recall | Precision |
|---|---:|---:|---:|
| Female | 2,887 | 0.665 | 0.694 |
| Male | 3,584 | 0.747 | 0.714 |

The model's recall was approximately 0.665 for female records and 0.747 for male records, a difference of about 8.2 percentage points.

This difference indicates that the model identified different proportions of at-risk records across these groups in the test data. In a real educational setting, such differences could matter because missed students might not receive timely support.

However, a difference in recall alone does not prove that a model is discriminatory. Additional investigation would be needed to understand the causes of the gap, examine other fairness measures, and assess performance across different student groups.

The age-group analysis also showed differences in recall. Results for the oldest age group should be interpreted cautiously because that group contained only 42 test records.

The fairness analysis highlights the importance of evaluating predictive systems beyond overall accuracy.

## 6. Limitations

This project has several limitations.

First, the models use historical data from a particular online learning environment. Student behavior and course structures may differ at other institutions, so the results may not generalize.

Second, early click counts provide only a partial view of student engagement. Clicks do not necessarily measure understanding, motivation, or the quality of learning.

Third, the target combines failing and withdrawing into one at-risk category. These outcomes may have different causes and may require different types of support.

Fourth, the analysis identifies associations in historical data. It does not establish that low engagement causes an unsuccessful outcome.

Fifth, the fairness analysis focuses on a limited set of group comparisons. Further evaluation would be needed before any real-world deployment.

Finally, a model with moderate predictive performance will make errors. Any practical system should support human judgment rather than automatically determine a student's academic opportunities.

## 7. Conclusion and Future Work

This project examined whether early learning activity and student information could help identify students at risk of failing or withdrawing.

The extended model achieved the strongest overall results on several evaluation metrics, with a ROC-AUC of approximately 0.757. The 14-day baseline achieved the highest recall, while the 7-day model offered the possibility of earlier predictions at the cost of lower predictive performance.

The findings suggest that early engagement data may be useful for identifying students who could benefit from additional support. However, model errors, differences in group performance, and limits to generalizability must be considered.

Future work could include testing additional machine learning algorithms, evaluating different classification thresholds, investigating the causes of group performance differences, and validating the models on a separate dataset. It would also be valuable to determine whether using the predictions to offer supportive interventions improves student outcomes.

## 8. References

Kuzilek, J., Hlosta, M., & Zdrahal, Z. (2017). Open University Learning Analytics dataset. *Scientific Data, 4*, 170171. https://doi.org/10.1038/sdata.2017.171

Open University Learning Analytics Dataset. https://analyse.kmi.open.ac.uk/open_dataset

Scikit-learn documentation. https://scikit-learn.org/stable/

## Reproducibility

The analysis notebooks and project files are available in this GitHub repository:

https://github.com/AungBhonePyae00/educational-data-mining

The project uses Python and scikit-learn. See the repository README for setup instructions and information about obtaining the dataset.