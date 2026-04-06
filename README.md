# Medicare Claim Fraud Detection

## Overview
Healthcare fraud creates major financial and operational inefficiencies. In this project, I built an end-to-end fraud detection solution to identify suspicious Medicare claims using data analysis, feature engineering, and machine learning.

The objective was not only to classify potentially fraudulent claims, but also to design a workflow that could support real-world decision-making through scalable deployment and prediction services.

This project uses Medicare claims data and applies a logistic regression model to classify claims as fraudulent or non-fraudulent. The final solution includes exploratory analysis, feature engineering, model training, performance evaluation, and deployment using FastAPI, Streamlit, Docker, and AWS.

## Business Problem
Fraudulent healthcare claims increase costs, delay legitimate reimbursements, and reduce operational efficiency. Manual review alone is expensive and difficult to scale.

This project addresses a core business question:

**How can we identify high-risk Medicare claims early so investigators can focus their effort where it matters most?**

The goal is to support fraud review teams with a risk-based system that improves detection efficiency while balancing the tradeoff between catching fraud and avoiding too many false positives.

## Dataset
This project uses the Medicare Claims Synthetic Public Use Files published by CMS.

Data sources used in the project include:
- Beneficiary data
- Inpatient claim data
- Outpatient claim data

These datasets were combined and prepared for fraud risk modeling.

## Project Goals
- Analyze Medicare claim patterns and identify signals associated with suspicious activity
- Build a machine learning model to classify fraudulent vs. non-fraudulent claims
- Engineer features that improve fraud detection performance
- Deploy the model in a production-style workflow with API and UI access
- Create an architecture that can support scalable fraud scoring

## End-to-End Workflow
1. Data extraction and integration  
   Combined beneficiary, inpatient, and outpatient datasets for modeling

2. Data cleaning and preprocessing  
   Handled data quality issues, prepared fields for analysis, and standardized input structure

3. Exploratory data analysis  
   Examined claim-level and provider-level patterns to understand fraud behavior

4. Feature engineering  
   Created predictive variables from claim and beneficiary information

5. Model training  
   Trained a logistic regression model for binary classification

6. Evaluation  
   Assessed performance using fraud-focused metrics, especially recall and capture rate

7. Deployment  
   Served predictions using FastAPI and Streamlit, containerized with Docker, and deployed on AWS

## Tech Stack
- **Programming:** Python, SQL
- **Machine Learning:** Logistic Regression
- **Experiment Tracking / Model Management:** MLflow
- **Backend API:** FastAPI
- **Frontend UI:** Streamlit
- **Containerization:** Docker
- **Cloud Services:** AWS ECS, AWS ECR, AWS S3
- **Analysis Environment:** Jupyter Notebook

## Model Performance
The current model is a **Logistic Regression** classifier.

Reported performance:
- **Recall:** 65%
- **Capture Rate:** 72% in the top 3 percentile

This means the model is useful for prioritizing suspicious claims for investigation and can help focus review effort on the highest-risk segment first.

## Why Recall Matters Here
In fraud detection, missing a fraudulent claim is expensive. Because of that, recall is an important metric in this use case.

I prioritized identifying as many suspicious claims as possible, while recognizing that fraud systems must also manage false positives to avoid unnecessary friction and review overhead.

## Key Insights
### 1. Fraud detection is a ranking problem, not just a classification problem
The model captured 72% of fraudulent cases within the top 3 percentile of scored claims. This shows strong value as a prioritization tool, where investigators can review the highest-risk claims first instead of treating all claims equally.

### 2. Feature engineering materially improves fraud detection
The project combines multiple Medicare-related data sources and engineered features from claims and beneficiary information. This reflects that fraud is often better detected through behavioral and relational patterns rather than raw fields alone.

### 3. An effective fraud solution needs both analytics and deployment
This project goes beyond model training by exposing predictions through FastAPI and Streamlit, packaging the solution with Docker, and deploying it through AWS. That makes the work closer to a usable business solution instead of a notebook-only prototype.

## Business Impact
This solution can support healthcare fraud operations in several ways:
- Prioritize high-risk claims for manual investigation
- Reduce review effort by focusing on the most suspicious cases first
- Improve detection efficiency and reduce financial leakage
- Create a scalable scoring workflow that can be integrated into operational review pipelines

## Architecture 

![architecture](https://github.com/user-attachments/assets/b68bc015-87e5-4aab-9fd0-3147f0509db2)


**User Input:** User interacts with the Streamlit web UI for claim data entry.

**Backend API:** FastAPI processes the input, triggering the fraud prediction model.

**ML Model:** Logistic Regression model, loaded via MLflow, predicts if the claim is fraudulent.

**Storage:** All processed data is stored in AWS S3.

**Deployment:** The application is dockerized and deployed on AWS ECS.

## Installation

To run the project locally, follow these steps:

1. Clone the repository:

```bash
git clone https://github.com/rohitkosamkakr18/Medicare-Claim-Fraud-Detection.git
cd Medicare-Claim-Fraud-Detection/src
```

2. Build and run the Docker container:

```bash
docker build -t medicare-fraud-detection .
docker run -p 8501:8501 -p 8000:8000 medicare-fraud-detection
```

3. Install dependencies (if not using Docker):

```bash
pip install -r requirements.txt
```

4. Run FastAPI and Streamlit:

```bash
uvicorn main:app --host 0.0.0.0 --port 8000  # For FastAPI backend
streamlit run app_ui.py --server.port 8501    # For Streamlit frontend
```

## Usage

Access the Streamlit frontend for predictions at: http://localhost:8501

FastAPI documentation is available at: http://localhost:8000/docs

Submit Medicare claim data through the web interface to get predictions on whether a claim is fraudulent.

## Deployment
This project is deployed using AWS Elastic Container Service (ECS) with Docker. The following services are used in the deployment process:

**AWS ECS**: For managing the Docker container cluster.

**AWS S3**: For storing the input/output data.

**AWS ECR**: For storing the Docker images.

## Steps for deployment:

1. Push the Docker image to AWS ECR.

2. Create an ECS cluster and task definition to run the Docker container.

3. Expose ports 8000 (FastAPI) and 8501 (Streamlit) to make the service publicly accessible.

## Model Performance
- Model: Logistic Regression

- Metric: Recall (65%)

- Capture Rate: 72% in the top 3 percentile.

## Demo Video
![Video_Medicare_Fraud_Detection_Interface](https://github.com/user-attachments/assets/d51da451-462e-4db2-b593-41992a2864f4)

