Heart Disease Analysis

Exploratory data analysis of a clinical dataset of 918 patients, aimed at finding which patient characteristics are most associated with heart disease.

Tools: Python, Pandas, NumPy, Matplotlib, Seaborn (Google Colab) Data: Heart Failure Prediction Dataset (Kaggle, fedesoriano), heart.csv


Key Findings
ST slope was the strongest separator. Disease rate was 19.7% with an upsloping ST segment (n = 395) vs 82.8% with a flat one (n = 459).
Exercise-induced angina: 85.2% disease rate with angina (n = 371) vs 35.0% without (n = 546).
Asymptomatic chest pain had the highest disease rate (79.0%, n = 496) vs 13.9% for atypical angina (n = 173), so reported symptoms alone look like a poor signal in this sample.
Max heart rate: patients with disease averaged 127.6 bpm vs 148.2 bpm without. The gap held in every age band (about 12 to 19 bpm), so it is not just an age effect.
Cholesterol barely separated the groups (median 246.0 vs 231.5 mg/dl, valid rows only, n = 746).

<img width="2400" height="1350" alt="image" src="https://github.com/user-attachments/assets/42462cac-4d96-47e7-8d42-4f00bc8989bd" />



Data Quality Problem

The dataset has no null values, but 172 cholesterol values (18.7%) were recorded as 0, which is physiologically impossible, and one patient had a resting blood pressure of 0.

I checked whether the zeros were random before deciding what to do. They were not: 88% of those patients had heart disease vs 48% of patients with valid cholesterol, and 74% of them had asymptomatic chest pain. So I did not impute a median, because that would hide this pattern. Instead I flagged those rows, excluded them from cholesterol-specific analysis, and dropped the single impossible blood pressure row (final n = 917).



Correlation

Oldpeak (r = 0.40) and MaxHR (r = -0.40) had the strongest correlations with heart disease. No numeric variable exceeded 0.40, and the strongest categorical findings above do not appear in the heatmap.

<img width="1200" height="900" alt="image" src="https://github.com/user-attachments/assets/52b8c7c4-6af9-489d-97ca-559e49858ccc" />


Limitations:   

Single, mostly male clinical sample (724 M, 193 F); results do not generalize.
Observational data shows association, not causation.
Cholesterol results cover a subset with a lower disease rate than the full data (47.7% vs 55.3%).
Small groups: TA chest pain (n = 46) and downsloping ST segment (n = 63).
No significance tests or predictive model were built.

How to Run:   

Open heart_disease_analysis.ipynb in Google Colab.
Upload heart.csv to the Colab session (folder icon in the left sidebar, then the upload icon).
Run all cells (Runtime > Run all).

Files:

text
heart-disease-analysis/
├── heart_disease_analysis.ipynb
├── heart.csv
├── eda_summary.png
├── correlation_heatmap.png
└── README.md
