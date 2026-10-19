# Research Question

## Working Title
Early Prediction of Student Academic Outcomes Using Learning Analytics

## Main Research Question
Can students at risk of failing or withdrawing be identified using learning activity and assessment information available during the early stages of a course?

## Subquestions
1. How is early engagement with online learning materials associated with final academic outcomes?
2. How accurately can machine learning models identify students who later fail or withdraw?
3. Which early engagement and assessment features contribute most to predictive performance?

## Proposed Outcome Definition
For the initial binary classification experiment, students whose final result is `Fail` or `Withdrawn` will be labeled as at risk. Students whose final result is `Pass` or `Distinction` will be labeled as not at risk.

## Research Considerations
The analysis will use only information available by the chosen prediction point. Final results and future activity must not be used as predictive features. Model performance will be evaluated using more than accuracy, including precision, recall, and F1-score.

The analysis will examine limitations related to class balance, repeated student records, and the generalizability of results.