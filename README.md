# Skin Cancer Prediction Using Machine Learning  
### Predictive Analysis of Benign vs. Malignant Skin Cancer

## Overview
This project investigates how **machine learning models can predict skin cancer status** (benign vs. malignant) using demographic, environmental, biological, and behavioral features.

Using a supervised learning framework, we:
- Analyze relationships between risk factors and cancer status  
- Engineer meaningful features using domain knowledge  
- Compare multiple models to optimize predictive performance  

## Research Questions
1. Which factors are most predictive of skin cancer risk?  
2. How do different modeling approaches compare in performance?  
3. Does increasing model complexity improve generalization?  

## Dataset
We use a Kaggle dataset consisting of:
- **50,000 training observations**  
- **20,000 test observations**  
- ~50 predictors

Each observation includes:
- Demographic information (`age`, etc.)  
- Environmental exposure (`UV levels`)  
- Biological traits (`skin tone`, `immunosuppression`)  
- Behavioral factors (`sun protection habits`)  
- Medical history (`family history`, `lesions`)

### Data Cleaning
- Identified substantial missing data (~196k missing values)  
- Missingness pattern consistent with **MCAR**  
- Avoided row deletion due to high data loss  

### Imputation
- Used **MissForest (Random Forest–based imputation)**  
- Captures nonlinear relationships  
- Outperformed MICE, KNN, and median imputation in test performance  

### Engineered Features
- Log transformations for skewed variables  
- Square-root transformation for UV exposure  
- Polynomial features (e.g., age²)  
- Interaction terms (e.g., UV × skin sensitivity)  
- Noise variable filtering using correlation + PCA  

## Exploratory Data Analysis
<img width="5600" height="3600" alt="missingness_plot_highres" src="https://github.com/user-attachments/assets/6b3aaebc-b9b3-4894-bb59-e1e19e6e96e4" />
<img width="826" height="418" alt="Screenshot 2026-04-02 at 12 45 47" src="https://github.com/user-attachments/assets/2e86c80a-0e0d-4d8f-95e7-2df19fcf92d6" />
<img width="773" height="423" alt="Screenshot 2026-04-02 at 12 46 50" src="https://github.com/user-attachments/assets/e438305d-d223-428f-86a8-f7fd59073c4e" />
<img width="734" height="428" alt="Screenshot 2026-04-02 at 12 47 09" src="https://github.com/user-attachments/assets/c1186b3f-d5e7-44a7-a255-907fa46ca29f" />
<img width="775" height="422" alt="Screenshot 2026-04-02 at 12 47 20" src="https://github.com/user-attachments/assets/02b5ed93-25bd-4417-9f95-b5fec193ff7a" />

### Key Insights
- missing data revealed a uniformly distributed pattern across all predictors, and there is no evidence of systematic clustering. 
- Dataset is **balanced (~50% benign / 50% malignant)**  
- **Age** positively correlates with cancer risk  
- **Fair skin tones** have higher malignancy rates  
- **Immunosuppression** is a strong predictor  
- **Family history** significantly increases risk  

## Modeling Approach

We trained and compared multiple classification models:

### Models Tested
- Logistic Regression  
- LASSO / Ridge  
- Random Forest  
- XGBoost  

### Final Model
Logistic Regression with:
- Engineered nonlinear features  
- Interaction terms  
- Threshold tuning (0.495)  
- Bagging (100 iterations)  

### Performance Progression
- Baseline: 0.60420  
- + MissForest: 0.60485  
- + Feature Engineering: 0.60520  
- + Threshold Tuning: 0.60565  
- + Bagging: **0.60620**  

### Key Findings
- **Negative result:** complex models did NOT outperform simpler ones  
- Logistic regression generalized best  
- Performance plateau (~60%) suggests high noise in dataset  

## Limitations
- Dataset likely **synthetic** (balanced classes, uniform missingness)  
- Missing key clinical variables (e.g., images, genetic markers)  
- High noise limits achievable accuracy  
- Model evaluated on a single test distribution  

## Tech Stack
- **R**
  - `tidyverse`
  - `missForest`
  - `glmnet`
  - `randomForest`
- Methods:
  - Logistic Regression
  - Ensemble Learning (Bagging)










