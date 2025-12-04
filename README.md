# Final_Group_Assignment_ML4HC
ICU Survival Modelling
Kaplan Meier, Cox Proportional Hazards, and Machine Learning for Critical Care Decision Support
1. Project Overview

This repository contains a complete survival modelling pipeline designed for one of the most important decisions in healthcare: estimating short term mortality risk for critically ill adults. Hospitals operate with finite ICU beds, overworked staff, and constant triage pressures. Predictive survival modelling can help clinicians decide who needs urgent escalation, who can be safely stepped down, and how survival evolves over the first days and weeks after admission.

We analyse the SUPPORT dataset of 9,105 high acuity hospital patients and build a structured modelling workflow. It progresses from descriptive survival curves to interpretable statistical models and finally to flexible machine learning classifiers. Each model answers a specific clinical question while following strict requirements on leakage control, fairness, calibration, reproducibility, and stakeholder communication.
This README presents the ideas as clearly as possible so that clinicians, data scientists, and students can follow the reasoning behind every decision.

2. Repository Structure

Primary Notebooks
• 01_ICU_Survival_analysis_KM.ipynb
 Kaplan Meier curves, confidence intervals, restricted mean survival time, cumulative hazard, subgroup survival, and early clinical interpretation.
• 02_ICU_Survival_analysis_CPH.ipynb
 Univariable and multivariable Cox models, hazard ratio interpretation, proportional hazards checks, personalised survival curves, and calibration.
• 03_ICU_Survival_analysis_DT_RF.ipynb
 Thirty day mortality prediction with Decision Trees and Random Forests, preprocessing pipelines, grid searched hyperparameters, test set performance, and risk driver analysis.

Additional Files
• environment.yml for complete reproducibility.
• utils.py (optional) for reusable functions.
• Presentation.pdf for stakeholder communication and recommendations.
• README.md for documentation.

3. Installation and Environment

The entire workflow is reproducible with a single environment file.

conda env create -f environment.yml
conda activate icu_survival_env


Major libraries include lifelines, scikit learn, scikit survival, pandas, numpy, and matplotlib.
All versions are pinned to avoid non reproducible results.

4. Quickstart Guide

Run the notebooks in this order.

Step 1. Load dataset and validate time variables

We clean negative values, confirm that d.time and slos represent valid survival durations, and inspect event and censoring rates. These steps reflect the expected setup in the project guidelines 

HL4HC_GroupAssignment_2_KM

.

Step 2. Kaplan Meier analysis

• Plot survival curves with confidence intervals.
• Compute median survival and RMST to quantify early and late risk windows.
• Use cumulative hazard to capture the steep rise in early mortality.
• Compare survival across diagnosis and severity groups.
• Produce clinical takeaways that connect survival patterns to ICU capacity needs.

Step 3. Cox Proportional Hazards modelling

• Remove leakage variables and restrict predictors to information available at admission.
• Fit univariable and multivariable Cox models.
• Interpret hazard ratios for clinical decision making.
• Check proportional hazards assumptions using Schoenfeld residuals.
• Evaluate model discrimination and calibration.
• Generate personalised survival curves for representative patients.
These steps follow Cox modelling requirements in the assignment instructions 

HL4HC_GroupAssignment_2_CPH

.

Step 4. Fixed horizon Decision Tree and Random Forest

• Define the thirty day mortality label without accessing future data.
• Build preprocessing pipelines with imputers, scalers, and one hot encoding.
• Train Decision Tree and Random Forest models with grid searched hyperparameters.
• Evaluate test set AUROC and Brier score.
• Analyse permutation importance to identify dominant clinical drivers.
This reflects the classification modelling expectations described in the instructions 

HL4HC_GroupAssignment_2_DT_RF

.

5. Dataset Summary

The SUPPORT dataset includes high risk adult inpatients from five United States hospitals. It contains:
• Demographics such as age, sex, and education.
• Physiologic measures such as APS, scoma, creatinine, mean blood pressure, and temperature.
• Diagnosis categories that represent major advanced diseases.
• Length of stay, in hospital mortality status, overall survival time, and long term outcomes.

The outcome structure reveals:
• About 26 percent in hospital mortality.
• About 27 percent thirty day mortality.
• Heavy right censoring due to discharge alive.
• Strong early risk concentration in the first days of admission.

These patterns appear in the Kaplan Meier exploratory section (pages 7 to 12) 

HL4HC_GroupAssignment_2_KM

.

6. Key Findings from Survival Analysis
Kaplan Meier

The Kaplan Meier curves show a steep early drop in survival, confirming that the highest risk window occurs shortly after admission. Subgroup curves reveal large differences across diseases such as coma, ARF and malignancies. Restricted mean survival time highlights actionable time points that align with ICU resource constraints.

Cumulative hazard analysis confirms that risk accumulates rapidly early in the stay, then slows down as patients stabilise. These insights help determine when to intensify monitoring and when discharge becomes safer.

Cox Proportional Hazards

The Cox model quantifies the independent contributions of baseline predictors. Key results include:
• Higher APS and scoma scores significantly increase mortality hazard.
• Diagnosis categories such as coma and cancer exhibit strong elevated risk.
• Higher mean blood pressure reduces hazard, consistent with clinical physiology.
• Age and comorbidities increase risk in a stable and interpretable way.

The model passes proportional hazards checks for most predictors. Calibration curves and Brier scores support clinical deployment. The model also generates personalised survival curves that clinicians can use to communicate prognosis to families.

Decision Tree and Random Forest

The Random Forest model delivers the strongest predictive discrimination with AUROC near 0.744 on the held out test set. The Decision Tree provides a simpler representation with somewhat lower performance but more visibility into decision splits.

Permutation importance indicates that temperature, creatinine, respiratory indicators, blood pressure, and severity scores drive most of the risk signal.

Both models respect horizon definitions and avoid leakage by limiting features to values available at admission.

7. Evaluation Strategy
Discrimination

• Concordance index for Cox models.
• AUROC for fixed horizon classifiers.
• Average precision to reflect class imbalance.

Calibration

• Reliability curves to detect over and under prediction.
• Brier score computed on the test set.
• Optional recalibration if required.

Threshold selection and decision analysis

We study threshold changes under realistic capacity constraints. This analysis explains how clinicians might deploy the model in a real hospital setting that must balance missed detections with resource saturation.

Fairness and subgroup performance

All models are checked across sex, age ranges, and diagnosis classes. These checks follow the grading rubric that prioritises fairness and robustness of clinical models.

8. Clinical Interpretation

Bringing the findings together:

• The first days of hospitalisation represent the most dangerous phase.
• Diagnosis category and physiological severity dominate the risk landscape.
• Cox models provide clear and interpretable effect sizes suitable for clinical guidelines.
• Random Forest improves discrimination and reveals nonlinear interactions not captured by traditional statistical models.
• Model predictions should always complement, not replace, clinical judgement.
• ICU capacity planning benefits from quantifying early survival trajectories and identifying which groups require intensive resources.

These conclusions are aligned with the decision context described in the Kaplan Meier notebook (pages 1 to 4) 

HL4HC_GroupAssignment_2_KM

.

9. Future Extensions

If this project were to be expanded, promising directions include:
• Competing risks analysis to explicitly model discharge.
• Time varying covariates that incorporate physiological changes during admission.
• Gradient boosted survival models.
• Deep neural survival models for richer pattern extraction.
• Integration into a real world triage dashboard.

10. Authors

Nizar Haroun
Juan Sebastian Marcial Piedra
Mateo Perdomo Andrés
Eliza Whitfield
