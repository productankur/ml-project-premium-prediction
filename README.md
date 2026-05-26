# 🏥 Health Insurance Cost Predictor

> An end-to-end Machine Learning web application that predicts personalized health insurance premiums based on demographic, lifestyle, and medical risk factors.

[![Live App](https://img.shields.io/badge/Live%20App-Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)](https://ml-project-premium-prediction-by-ankur.streamlit.app/)
[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-1.6.1-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
[![XGBoost](https://img.shields.io/badge/XGBoost-2.1.4-006600?style=for-the-badge)](https://xgboost.readthedocs.io/)

---

## 📌 Overview

Determining an appropriate health insurance premium is a complex, time-consuming process that traditionally requires consultation with agents and manual assessment of individual risk profiles. This application streamlines that experience by leveraging supervised machine learning to deliver instant, data-driven premium estimates.

The system accepts twelve input parameters spanning demographics, lifestyle habits, and medical history, and returns a predicted annual insurance cost — enabling individuals and insurers alike to make informed, objective decisions.

---

## 🚀 Live Demo

🔗 **[Launch the App](https://ml-project-premium-prediction-by-ankur.streamlit.app/)**

---

## 🧠 How It Works

The prediction pipeline employs a **dual-model architecture** to handle the distinct risk profiles of younger versus older applicants:

- **Model Young** — Applied when the applicant's age is **≤ 25 years**
- **Model Rest** — Applied when the applicant's age is **> 25 years**

Each model has a corresponding dedicated **StandardScaler** fitted on its respective population segment, ensuring accurate normalization of continuous features.

### Prediction Flow

```
User Input (12 features)
        │
        ▼
Feature Engineering
  ├── One-hot encoding of categorical variables
  ├── Ordinal encoding of Insurance Plan (Bronze=1, Silver=2, Gold=3)
  └── Normalized Risk Score from Medical History
        │
        ▼
Age-based Routing
  ├── Age ≤ 25 → scaler_young → model_young
  └── Age  > 25 → scaler_rest  → model_rest
        │
        ▼
Predicted Insurance Premium (₹)
```

### Medical Risk Scoring

Medical history is translated into a normalized risk score using a domain-informed scoring scheme:

| Condition | Risk Score |
|---|---|
| Heart Disease | 8 |
| Diabetes | 6 |
| High Blood Pressure | 6 |
| Thyroid | 5 |
| No Disease / None | 0 |

Composite conditions (e.g., *Diabetes & Heart Disease*) are summed and normalized against a maximum possible score of 14.

---

## 📊 Dataset

The models were trained on a structured insurance dataset with the following profile:

| Property | Detail |
|---|---|
| Total Records | 50,000 rows |
| Features | 13 columns (12 input features + 1 target) |
| Target Variable | Annual health insurance premium (₹) |
| Segments | Young cohort (Age ≤ 25) · Rest cohort (Age > 25) |

The dataset covers a diverse population across demographic, lifestyle, and medical dimensions, enabling the model to learn complex, non-linear relationships between individual risk factors and insurance costs.

---

## 📥 Input Parameters

| Parameter | Type | Options / Range |
|---|---|---|
| Age | Numeric | 18 – 100 |
| Number of Dependants | Numeric | 0 – 20 |
| Income in Lakhs | Numeric | 0 – 200 |
| Genetical Risk | Numeric | 0 – 5 |
| Insurance Plan | Categorical | Bronze, Silver, Gold |
| Employment Status | Categorical | Salaried, Self-Employed, Freelancer |
| Gender | Categorical | Male, Female |
| Marital Status | Categorical | Married, Unmarried |
| BMI Category | Categorical | Normal, Obesity, Overweight, Underweight |
| Smoking Status | Categorical | No Smoking, Occasional, Regular |
| Region | Categorical | Northwest, Southeast, Northeast, Southwest |
| Medical History | Categorical | No Disease, Diabetes, Heart Disease, and combinations |

---

## 🛠️ Technology Stack

| Layer | Technology | Version |
|---|---|---|
| Frontend / UI | Streamlit | 1.45.1 |
| ML Framework | scikit-learn | 1.6.1 |
| Boosting Algorithm | XGBoost | 2.1.4 |
| Data Manipulation | Pandas | 2.2.2 |
| Numerical Computing | NumPy | 2.0.2 |
| Model Serialization | Joblib | 1.5.0 |
| Deployment | Streamlit Community Cloud | — |

---

## 📁 Project Structure

```
ml-project-premium-prediction/
│
├── main.py                  # Streamlit UI — input form and prediction trigger
├── prediction_helper.py     # Core ML logic — preprocessing, scaling, and prediction
│
├── model_young.joblib       # Trained model for applicants aged ≤ 25
├── model_rest.joblib        # Trained model for applicants aged > 25
├── scaler_young.joblib      # Feature scaler for young segment
├── scaler_rest.joblib       # Feature scaler for rest segment
│
└── requirements.txt         # Python dependencies
```

---

## ⚙️ Local Setup

### Prerequisites

- Python 3.10 or above
- pip package manager

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/productankur/ml-project-premium-prediction.git
cd ml-project-premium-prediction

# 2. Install dependencies
pip install -r requirements.txt

# 3. Run the application
streamlit run main.py
```

The app will be available at `http://localhost:8501` in your browser.

---

## 📊 Model Architecture

The project uses **XGBoost Regressors** trained separately on two population segments. Key design decisions include:

- **Segment-wise modelling** to capture the non-linear relationship between age and premium cost
- **Normalized risk scoring** to quantify medical history as a continuous feature
- **StandardScaler** applied per segment to ensure feature distributions are correctly normalized before inference
- **One-hot encoding** for all nominal categorical variables; baseline categories are dropped to avoid multicollinearity

---

## 🔒 Disclaimer

This application is intended for **educational and demonstrative purposes only**. The predictions generated should not be used as a substitute for professional actuarial assessment or formal insurance quotations.

---

## 👤 Author

**Ankur**
- 🌐 [Live App](https://ml-project-premium-prediction-by-ankur.streamlit.app/)
- 💻 [GitHub Repository](https://github.com/productankur/ml-project-premium-prediction)

---

*Built with ❤️ using Python and Streamlit*
