# 2–3 Minute Capstone Demo Script

**0:00–0:20 — Problem**  
“This project predicts customer churn risk using telecom account and service information. The goal is to help a retention team prioritize helpful, voluntary outreach—not to make automatic decisions about customers.”

**0:20–0:45 — Data and evaluation**  
“I used the IBM Telco Churn sample with 7,043 records and roughly 26.5% churn. The workflow separates training, validation and test data, avoids using the customer identifier as a feature, and compares a Logistic Regression baseline with Random Forest and XGBoost. The model threshold is chosen on validation data.”

**0:45–1:20 — Prediction UI**  
“Here is the Streamlit dashboard. I enter customer service and billing attributes and submit the form. The API returns a churn probability and a threshold-based risk label. This is a model estimate, not certainty about an individual customer.”

**1:20–1:45 — API and batch scoring**  
“The same model is available through FastAPI. The health endpoint checks service readiness, and the prediction endpoint supports integration. For many records, the batch scoring pipeline writes probabilities and predicted labels to a CSV.”

**1:45–2:15 — Explainability and retention**  
“SHAP and feature-importance outputs help us inspect which inputs influence model predictions. These are associations learned by the model, not causal explanations. Example interventions include onboarding help, a plan-fit review, or relevant support setup; each should be tested and measured.”

**2:15–2:40 — Monitoring and close**  
“The drift report compares current input distributions with the training reference. A flagged feature triggers investigation; it does not by itself prove that the model is worse. This package includes a weekly monitoring runbook, acceptance requirements and future improvements. Thank you.”

## Demo readiness checklist
- Start API and confirm `http://localhost:8000/health` responds.
- Start Streamlit and open `http://localhost:8501` (or local default shown in terminal).
- Use a synthetic/example customer; do not display real customer information.
- Keep a batch prediction CSV and report page ready as backup.
- Do not claim drift monitoring or scheduled tasks are running unless they have been configured and executed on the target machine.
