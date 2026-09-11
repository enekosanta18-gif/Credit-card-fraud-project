
# 💳 Credit Card Fraud Detection

A Random Forest-based classification model to detect fraudulent credit card transactions, trained on the Credit Card Fraud Detection 2023 dataset.

📋 Table of Contents
Project Overview
Dataset
Technologies Used
Project Structure
Installation
Usage
Methodology
Results
Future Improvements
Author
License
📖 Project Overview

This is my first Machine Learning project focused on a real-world, high-impact use case: credit card fraud detection. The goal is to build a model capable of distinguishing between legitimate and fraudulent transactions using anonymized numerical variables (result of PCA transformation) and transaction amount.

The project covers the complete supervised classification pipeline:

Data loading and initial exploration.
Preparation of predictive variables and target variable.
Splitting into training and test sets.
Variable scaling.
Training a RandomForestClassifier model.
Cross-validation.
Evaluation using classification metrics, confusion matrix, and ROC curve.
Analysis of feature importance and correlation between features.
📊 Dataset
Name: creditcard_2023.csv
Size: 568,630 transactions
Columns: 31 (id, V1–V28, Amount, Class)
V1 to V28: anonymized numerical variables obtained via PCA.
Amount: transaction amount.
Class: target variable (0 = legitimate transaction, 1 = fraudulent transaction).
Class Balance: The dataset is nearly balanced (~50% / 50%), which simplifies training and eliminates the need for additional balancing techniques like SMOTE or undersampling.

⚠️ The original dataset is not included in this repository due to its size. It can be downloaded from Kaggle - Credit Card Fraud Detection Dataset 2023 and should be placed in the data/ folder before running the notebook.

🛠 Technologies Used
Python 3
pandas — data manipulation
NumPy — numerical computing
scikit-learn — modeling and evaluation (train_test_split, StandardScaler, RandomForestClassifier, metrics)
Matplotlib / Seaborn — data visualization
Jupyter Notebook

📁 Project Structure
credit-card-fraud-detection/
│
├── data/
│   └── creditcard_2023.csv        # (not included, download separately)
│
├── PRIMER_PROYECTO_CREDIT_CARD_FRAUD.ipynb
├── README.md
└── requirements.txt

⚙️ Installation
Clone the repository:
bash
git clone https://github.com/<your-username>/credit-card-fraud-detection.git
cd credit-card-fraud-detection
Create and activate a virtual environment (optional but recommended):
bash
python -m venv venv
source venv/bin/activate    # Linux / macOS
venv\Scripts\activate       # Windows
Install dependencies:
bash
pip install -r requirements.txt

Suggested requirements.txt:

pandas
numpy
scikit-learn
seaborn
matplotlib
jupyter
Download the dataset and place it in data/creditcard_2023.csv.
▶️ Usage
Open the notebook:
bash
jupyter notebook PRIMER_PROYECTO_CREDIT_CARD_FRAUD.ipynb
Adjust the CSV file path to your local dataset location:
python
df = pd.read_csv("data/creditcard_2023.csv")
Execute cells in order to reproduce the complete analysis: data loading, model training, and results evaluation.
🔬 Methodology
Step	Description
1. Data Preparation	Drop id and Class columns from predictive variables (X); separate Class as target variable (y).
2. Train/Test Split	train_test_split with test_size=0.2 and random_state=42 (80% training / 20% test).
3. Scaling	Standardize variables using StandardScaler, fit on training set, apply to both train and test.
4. Model	RandomForestClassifier with n_estimators=100, max_depth=10, min_samples_split=5, n_jobs=-1.
5. Cross-Validation	5-fold cross-validation on training set, using f1 as the scoring metric.
6. Evaluation	classification_report, confusion matrix, and ROC/AUC curve on test set.
7. Interpretability	Feature importance (feature_importances_) and correlation matrix between features.
   
📈 Results

Data Split:

Set	Samples	Features
Train	454,904	29
Test	113,726	29

Cross-Validation (5-fold, F1 metric):

F1 scores: [0.9847, 0.9864, 0.9847, 0.9843, 0.9839]
Average F1 score: 0.9848

Classification Report (test set):

Class	Precision	Recall	F1-score	Support
0 (Legitimate)	0.97	1.00	0.99	56,750
1 (Fraud)	1.00	0.97	0.99	56,976
Accuracy			0.99	113,726

Top Features by Model Importance:

Feature	Importance
V10	0.172
V4	0.159
V14	0.146
V12	0.114
V11	0.090

The model achieves an F1-score of 0.99 on both classes with a global precision of 99%, and the ROC curve confirms strong discrimination capacity between legitimate and fraudulent transactions. Variables V10, V4, V14, V12, and V11 contribute most to predictions.

🚀 Future Improvements
 Test alternative algorithms (XGBoost, LightGBM, Logistic Regression) for performance comparison.
 Optimize hyperparameters using GridSearchCV / RandomizedSearchCV.
 Evaluate with fraud-specific metrics (Precision-Recall AUC, false negative cost).
 Package the trained model (joblib/pickle) and expose via API (Flask/FastAPI).
 Add unit tests and scikit-learn Pipeline for production deployment.
👤 Author

Eneko First practical Machine Learning project applied to fraud detection.

📄 License

This project is distributed under the MIT License. The dataset used is subject to the license terms specified by its original source (Kaggle).

