# End-to-End Customer Churn Prediction System

An end-to-end machine learning project that predicts customer churn, explains the factors influencing churn risk, and helps businesses develop data-driven customer retention strategies.

## Project Overview

Customer churn occurs when customers stop using a company's products or services. Identifying customers who are likely to leave helps businesses take proactive steps to improve customer satisfaction and retention.

This project uses the IBM Telco Customer Churn dataset to build a machine learning pipeline for data analysis, preprocessing, model training, evaluation, explainability, and deployment through FastAPI and Streamlit.

## Objectives

- Perform Exploratory Data Analysis (EDA) to identify churn patterns.
- Clean and preprocess customer data.
- Engineer features and build machine learning pipelines.
- Train and compare Logistic Regression, Random Forest, and XGBoost models.
- Evaluate model performance using classification metrics.
- Explain model predictions using SHAP.
- Generate batch churn predictions.
- Serve predictions through a FastAPI endpoint.
- Provide an interactive Streamlit dashboard.
- Establish a foundation for model and data drift monitoring.

## Technology Stack

| Area | Technologies |
|---|---|
| Programming | Python |
| Data analysis | Pandas, NumPy |
| Visualization | Matplotlib |
| Machine learning | Scikit-learn, XGBoost |
| Explainability | SHAP |
| API | FastAPI, Uvicorn |
| Dashboard | Streamlit |
| Model persistence | Joblib |
| Deployment | Docker |
| Testing | Pytest |
| Version control | Git, GitHub |

## Dataset

**Dataset:** IBM Telco Customer Churn

The dataset contains customer information such as tenure, monthly charges, contract type, payment method, internet service, and churn status.

- Total records: 7,043
- Customers who churned: 1,869
- Customers who did not churn: 5,174
- Churn rate: approximately 26.5%

Place the dataset at `data/raw/churn.csv` before running the data preparation workflow. The raw dataset is not intended to be committed to Git.

## Project Structure

```text
customer-churn-capstone/
├── app_ui/
│   └── streamlit_app.py
├── data/
│   ├── raw/
│   └── processed/
├── docs/
├── models/
├── notebooks/
│   ├── 01_data_understanding.ipynb
│   ├── 02_cleaning_splitting.ipynb
│   ├── 03_features_baseline.ipynb
│   ├── 04_modeling_tuning.ipynb
│   └── 05_explainability.ipynb
├── reports/
│   ├── figures/
│   ├── monitoring/
│   └── batch_predictions.csv
├── slides/
├── src/
│   ├── features/
│   ├── models/
│   ├── monitoring/
│   ├── pipeline/
│   ├── serving/
│   └── utils/
├── tests/
├── .gitignore
├── Dockerfile
├── requirements.txt
└── README.md
```

## Installation

### 1. Clone the repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd customer-churn-capstone
```

Replace the placeholder with your actual GitHub repository URL.

### 2. Create a virtual environment

```bash
python -m venv .venv
```

Activate it on Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

### 3. Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Add the dataset

Download the IBM Telco Customer Churn dataset and save the CSV file as:

```text
data/raw/churn.csv
```

## Running the Project

Run these commands from the project root directory.

### Data analysis and preparation

```bash
python -m src.utils.eda
python -m src.utils.prepare_data
```

### Train and evaluate models

```bash
python -m src.models.train
```

### Generate explainability outputs

```bash
python -m src.models.explain
```

### Generate batch predictions

```bash
python -m src.pipeline.batch_score --in data/processed/test.csv --out reports/batch_predictions.csv
```

### Launch the FastAPI service

```bash
uvicorn src.serving.app:app --host 0.0.0.0 --port 8000
```

API documentation is available at:

`http://localhost:8000/docs`

### Launch the Streamlit dashboard

Open a second terminal in the project root and run:

```bash
streamlit run app_ui/streamlit_app.py
```

The dashboard is available at:

`http://localhost:8501`

If the dashboard uses the API, ensure the API is running and that the configured API URL is reachable from the environment running Streamlit.

## Docker Deployment

Build the Docker image:

```bash
docker build -t customer-churn-capstone .
```

Example API container:

```bash
docker run -d --name churn-api -p 8000:8000 customer-churn-capstone
```

Example dashboard container:

```bash
docker run -d --name churn-ui -p 8501:8501 customer-churn-capstone streamlit run app_ui/streamlit_app.py --server.address=0.0.0.0
```

When running the dashboard and API in separate containers, configure the dashboard to use a hostname that can reach the API container, rather than assuming `127.0.0.1` refers to the API container.

## Model Evaluation

Recorded results from the existing project run:

| Model | Validation ROC-AUC | Validation F1 |
|---|---:|---:|
| Logistic Regression | 0.8447 | 0.6329 |
| Random Forest | 0.8306 | 0.6325 |
| XGBoost | 0.8426 | 0.6405 |

XGBoost was selected based on validation F1 in that run.

**Recorded test performance:**

- ROC-AUC: 0.8370
- F1-score: 0.6026
- Precision: 0.5481
- Recall: 0.6690

These are recorded results from the existing model run, not a guarantee that every retraining run will produce identical values.

## Explainability and Business Value

SHAP is used to investigate which customer characteristics influence model predictions. These insights can help teams investigate potential churn drivers and design targeted retention experiments.

Possible retention initiatives include:

1. Reviewing support experiences for customers showing elevated churn risk.
2. Testing suitable contract or pricing options for at-risk customer segments.
3. Offering targeted engagement and retention campaigns and measuring their effectiveness.

Predictions should support human decision-making rather than automatically determine customer eligibility or treatment.

## Monitoring

The project includes a monitoring component intended to compare reference data with newer inference data and help identify potential data drift.

Monitoring should include:
- Reviewing data quality and feature distributions.
- Generating and interpreting drift reports.
- Recording monitoring results.
- Investigating material changes before retraining a model.

Automated weekly scheduling and a freshly generated drift report should be verified in the target environment before being described as operational.

## Testing

Run the automated test suite from the project root:

```bash
pytest -q
```

## Git and Data Safety

Before publishing the repository:

- Keep `.venv/`, secrets, environment files, and raw customer data out of Git.
- Avoid committing large generated datasets or model files unless explicitly required.
- Never commit passwords, API keys, or private credentials.
- Review `.gitignore` before the first push.

## Project Deliverables

The project is organized to include:

- Data understanding, preprocessing, baseline, modeling, and explainability notebooks.
- Model training and batch prediction workflows.
- FastAPI prediction service.
- Streamlit user interface.
- Docker deployment configuration.
- Model evaluation reports and visualizations.
- Requirements documentation, monitoring guidance, and capstone presentation materials.

## Limitations

Model quality depends on the dataset, preprocessing, model configuration, and decision threshold. The dataset may not represent all real-world customers. Churn predictions are estimates, and retention interventions should be evaluated using measurable business outcomes.

## Author

**Ariyan Khan**  
B.Tech — Computer Science Engineering  
Dr. Sudhir Chandra Sur Institute of Technology and Sports Complex

## License

Add an appropriate license before redistributing this project. Confirm the dataset's applicable usage terms separately.
