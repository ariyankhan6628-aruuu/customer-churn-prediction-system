# Monitoring Runbook

## Purpose
The drift utility compares a reference feature sample (normally the training split) with a recent inference sample. It creates an HTML report and a CSV table. It is a **screening tool**, not a direct measure of predictive performance.

## Routine
1. Export a representative, privacy-reviewed sample of recent input rows to `data/inference/current_week.csv`.
2. Run from the project root: `python -m src.monitoring.drift_report --current data/inference/current_week.csv`.
3. Review `reports/monitoring/drift_report.html` and `.csv`.
4. Investigate flagged features, data pipeline changes, category shifts, and whether current data resembles the training population.
5. If labels later become available, evaluate model performance separately (ROC-AUC/PR-AUC, calibration, recall, precision, business outcomes).
6. Record date, sample size, findings, owner and follow-up in a monitoring log. Avoid recording customer identifiers.

## Heuristic thresholds in the included script
- Numeric features: flag if absolute standardized mean difference is at least 0.5.
- Categorical features: flag if total variation distance is at least 0.2.
These thresholds are pragmatic alerts, not statistical significance tests. A flag warrants investigation; it does not automatically mean retraining is required. A clean drift report does not guarantee good model performance.

## Weekly schedule on Windows
A PowerShell helper is included at `docs/weekly_drift_check.ps1`. Schedule it with Windows Task Scheduler to run weekly after placing a fresh file at `data/inference/current_week.csv`. Configure the task to start in the repository root and use the Python executable from `.venv`. If no current file exists, the job should fail visibly rather than silently report “no drift.”

## Incident response
- **Large numeric shift:** check units, parsing, data freshness, and upstream schema changes.
- **New/missing categories:** confirm expected product/customer mix and encoding compatibility.
- **Model/API errors:** check `/health`, application logs, model artifact and input schema.
- **Performance deterioration:** obtain matured labels and compare metrics to a documented baseline before retraining.
- **Before retraining:** preserve the current model, retrain only on approved data, compare on a temporal or held-out evaluation set, and document approval.
