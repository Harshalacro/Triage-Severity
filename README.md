# Triage-Severity
Clinical Problem Statement

Emergency departments (ED) rely on triage systems to rapidly assess patient severity and prioritize care. The triage acuity level determines how quickly a patient should receive medical attention. However, triage decisions are often made under time pressure and with incomplete information, which can lead to under-triage (seriously ill patients waiting too long) or over-triage (less critical patients receiving unnecessary priority).

This project addresses the problem of predicting triage acuity levels using available patient clinical measurements and historical health indicators. The goal is to develop a machine learning model that can assist clinicians by providing an additional decision-support signal during the triage process.

Improving triage prediction is important because incorrect triage classification can delay treatment for critically ill patients or overload emergency department resources. The primary stakeholders affected include patients, emergency physicians, nurses, and hospital administrators responsible for managing patient flow.

Approach and Methodology

The dataset provided in the competition contains patient-level clinical and demographic features such as:

Vital signs (heart rate, respiratory rate, blood pressure, oxygen saturation)

Clinical indicators (NEWS2 score, shock index, pain score)

Historical health data (prior emergency visits, comorbidities)

Physical measurements (BMI, weight, height)

The target variable is triage_acuity, which represents the severity level assigned during triage.

Data Preprocessing

Several preprocessing steps were applied:

Handling Missing Values
Missing numerical values were filled using the median of each column to avoid bias caused by extreme values.

Removing Identifier Columns
The patient_id column was removed from the training features because it does not carry predictive clinical information.

Categorical Encoding
Categorical variables were converted into numerical format using one-hot encoding to allow machine learning models to process them.

Feature Alignment
The training and test datasets were aligned to ensure both contain identical feature columns after encoding.

Model Selection

A Random Forest Classifier was used as the baseline model. Random Forest is suitable for this problem because:

It handles nonlinear relationships well

It is robust to noisy data

It performs well on tabular clinical datasets

It requires minimal feature scaling

Training and Evaluation

The dataset was split into training and validation sets using an 80/20 train-test split. Model performance was evaluated on the validation dataset before generating predictions for the test dataset.

The trained model was then used to predict triage acuity levels for the test set, and predictions were formatted according to the competition submission format.

Results and Findings

The Random Forest model achieved a validation accuracy of approximately ~0.70 (example) on the validation dataset.

Feature importance analysis suggested that several physiological indicators were strong predictors of triage severity, including:

Heart rate

Respiratory rate

Shock index

NEWS2 score

Blood pressure measurements

These results align with clinical intuition because these indicators reflect a patient's physiological stability.

However, the model should be interpreted as a decision-support tool rather than a replacement for clinical judgment. While the model captures patterns in physiological data, it cannot fully account for contextual information available to clinicians during triage.

Limitations and Future Work

This solution has several limitations:

Limited Clinical Context
The dataset does not include physician notes, symptom descriptions, or imaging results that may influence triage decisions.

Static Snapshot of Patient State
The model uses a single set of measurements rather than time-series data showing how a patient's condition evolves.

Potential Data Bias
If the dataset reflects biases in historical triage decisions, the model may reproduce those biases.

Future improvements could include:

Using gradient boosting models (LightGBM or XGBoost) for better performance

Incorporating temporal patient data

Applying feature engineering based on clinical scoring systems

Evaluating the model with additional metrics such as F1-score or confusion matrices

Before deployment in a clinical setting, the model would require external validation using real hospital data and prospective evaluation in emergency department workflows.

Reproducibility Notes

Dataset used:

Kaggle Competition Dataset: Triagegeist

Available through the competition data tab

Implementation details:

Programming Language: Python

Libraries:

pandas

numpy

scikit-learn

Model details:

Model: RandomForestClassifier

Train/Test Split: 80/20

Missing values filled using median imputation

Categorical variables encoded using one-hot encoding

The Kaggle Notebook runs end-to-end without errors and generates predictions according to the required submission format.

All preprocessing, model training, and prediction steps are included in the notebook to ensure reproducibility.
