# Final_Group_Assignment_ML4HC
ICU Survival Modelling
Understanding short term mortality in critically ill patients through survival analysis and machine learning
1. Project Overview

This project examines how critically ill patients progress during their hospital stay and which factors shape their chances of survival. The clinical motivation is very real: ICU beds are limited, clinicians must make rapid decisions, and early mortality risk is often unclear. By modelling survival, we can support triage, escalation, discharge planning, and conversations with families.

We work with the SUPPORT dataset, which contains detailed information on 9,105 severely ill adults. The workflow mirrors how a clinician or data scientist would approach the problem. We begin with descriptive survival curves, move to interpretable statistical models, and then explore whether machine learning can improve short term predictions.

The goal is straightforward: provide a transparent, end to end analysis that is both technically solid and useful in practice.

2. Repository Structure
Main Notebooks

01_ICU_Survival_analysis_KM.ipynb
Kaplan Meier curves, median survival, restricted mean survival time, cumulative hazard, subgroup comparisons, and early clinical interpretation.

02_ICU_Survival_analysis_CPH.ipynb
Univariable and multivariable Cox models, hazard ratio interpretation, proportional hazards checks, personalised survival curves, and calibration.

03_ICU_Survival_analysis_DT_RF.ipynb
Thirty day mortality modelling with Decision Trees and Random Forests, preprocessing pipelines, hyperparameter tuning, test set evaluation, and feature importance.

Supporting Files

• environment.yml for reproducible setup
• utils.py for shared helper functions
• Presentation.pdf for communicating insights to clinical stakeholders
• README.md (this document)

3. Installation and Environment

Create the environment with:

conda env create -f environment.yml
conda activate icu_survival_env


The environment includes numpy, pandas, scikit learn, lifelines, seaborn, matplotlib, and all required packages. Versions are pinned so the notebooks run consistently on any machine.

4. Quickstart Guide
Step 1. Load the dataset

We start by inspecting the survival variables, correcting invalid values, and confirming event and censoring definitions. This ensures all stages of the analysis are built on clean, reliable inputs.

Step 2. Kaplan Meier analysis

The KM notebook provides the first look at how survival evolves over time. The curves show a steep early decline, which aligns with what clinicians often observe. Subgroup curves reveal meaningful differences across disease categories. Restricted mean survival time and cumulative hazard clarify when risk is highest and when patients begin to stabilise.

Step 3. Cox Proportional Hazards modelling

The Cox model quantifies the effect of baseline variables on mortality. Only admission time predictors are included to prevent leakage. We interpret hazard ratios, check model assumptions, evaluate calibration, and generate personalised survival curves. This step adds structure and clarity to the patterns seen in the KM analysis.

Step 4. Decision Tree and Random Forest modelling

This part focuses on predicting thirty day mortality. We define a clean binary label, build preprocessing pipelines, tune both models, and evaluate their performance using AUROC and Brier score. The Random Forest performs best and highlights important predictive features. The Decision Tree offers a simplified, more interpretable alternative.

5. Summary of the Dataset

The dataset includes patients with advanced conditions such as respiratory failure, heart failure, cirrhosis, coma, and malignancies. Baseline physiological values, comorbidities, demographics, and outcomes are all recorded.

Key observations:
• In hospital mortality is roughly one in four
• Thirty day mortality is slightly higher
• A large portion of patients are discharged alive, creating substantial censoring
• Survival and length of stay are heavily right skewed, with most events occurring early

These patterns guide the modelling choices in the notebooks.

6. Main Results
Kaplan Meier

Survival declines most sharply during the first days after admission. This early period is clinically important and aligns with real practice. Subgroup curves show that some diagnosis categories experience significantly worse outcomes. Cumulative hazard curves support the observation that early risk is concentrated.

Cox Proportional Hazards

The Cox model demonstrates that higher severity scores, specific diagnosis groups, lower blood pressure, older age, and multiple comorbidities all increase mortality risk. The model is reasonably well calibrated and passes most assumption checks. Personalised survival curves provide a practical way to visualise expected outcomes for specific patient profiles.

Decision Tree and Random Forest

For the thirty day task, the Random Forest achieves the strongest performance with an AUROC around 0.74. It identifies several consistent predictors such as temperature, creatinine, respiratory indicators, blood pressure, and severity scores. The Decision Tree is easier to interpret and can be useful when transparency is a priority.

7. Evaluation Approach

Discrimination
Concordance index for survival models and AUROC for classification models. Average precision is also reported to capture class imbalance.

Calibration
Calibration curves and Brier scores are used to check whether predicted probabilities match observed outcomes.

Threshold selection
Different thresholds are evaluated considering real ICU capacity constraints, helping translate model performance into practical decision policies.

Subgroup checks
Performance is compared across age, sex, and disease categories to identify any significant differences or fairness concerns.

8. Clinical Perspective

Bringing all results together, the picture is consistent. Mortality risk is heavily concentrated early in the admission. Physiological severity and diagnosis type drive much of the variation in outcomes. Cox models provide clear, interpretable insights, while the machine learning models capture nonlinear patterns and interactions that traditional models cannot.

These tools can support clinicians as they prioritise care, allocate scarce resources, and communicate prognosis. They should complement clinical judgment rather than replace it.

9. Future Extensions

Possible directions for further work include:
• Modelling discharge as a competing risk
• Incorporating time varying covariates
• Exploring boosted or neural survival models
• Building an interactive dashboard for real time clinical use

10. Authors

Nizar Haroun
Juan Sebastian Marcial Piedra
Mateo Perdomo Andrés
Eliza Whitfield
