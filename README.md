# 🧠 Content Moderation ML Engine  
### Automated Comment Category Prediction

This repository contains an end-to-end machine learning solution for the **Comment Category Prediction Challenge**. The project focuses on building a robust classification engine to automatically categorize user-generated comments into four moderation categories using text, engagement metrics, and system signals.

---

## 📌 Project Overview

The objective is to predict the internal handling category (**labels 0, 1, 2, or 3**) assigned to online comments.

This system serves as an **automated moderation tool**, enabling platforms to efficiently process large volumes of user-generated content.

### 🚧 Key Challenges

- **Severe Class Imbalance**  
  - Label 0: **57.7%**  
  - Label 3: **2.8%**

- **High-Dimensional Text Data**  
  - Required transformation using NLP techniques

- **Missing Data**  
  - Identity-related features had **73% missing values**

---

## 📊 Dataset Description

- **Total Records:** 198,000

### 🔑 Features

- **Primary Feature**
  - `comment` → Raw text input

- **Engagement Metrics**
  - `upvotes`, `downvotes`

- **System Signals**
  - `if_1`, `if_2`

- **Identity / Categorical Signals**
  - `race`, `religion`, `gender`, `disability`

- **Temporal Feature**
  - `created_date` (timestamps)

---

## 🛠️ Technical Workflow

### 1️⃣ Exploratory Data Analysis (EDA)

- **Missing Value Handling**
  - Filled identity columns with `'none'`  
  - Interpreted missing values as *“no identity detected”*

- **Correlation Analysis**
  - Studied relationship between engagement signals and moderation labels

---

### 2️⃣ Feature Engineering

- **Temporal Features**
  - Extracted: `year`, `month`, `day`, `hour`

- **Engagement Metrics**
  - `net_votes = upvotes - downvotes`
  - `vote_ratio`

- **Text Metadata**
  - `comment_len` (length of text)

---

### 3️⃣ Preprocessing Pipeline

Implemented using **Scikit-learn `ColumnTransformer`**

| Branch        | Technique                          | Purpose |
|--------------|-----------------------------------|--------|
| Text         | TF-IDF Vectorizer (`ngram=(1,2)`) | Capture contextual meaning |
| Numeric      | StandardScaler                    | Normalize values |
| Categorical  | OneHotEncoder                     | Encode identity/system features |

---

## 🤖 Modeling & Performance

### 📊 Models Trained
- Logistic Regression 2x
- Random Forest
- LightGBM 2x

### 📊 Model Comparison

| Aspect              | Logistic Regression | LightGBM (Final Model) |
|---------------------|--------------------|-------------------------|
| Algorithm           | Linear             | Gradient Boosting       |
| Non-linearity       | ❌ No              | ✅ Yes                  |
| Class Imbalance     | `class_weight`     | `sample_weight`         |
| Avg Accuracy        | ~60%               | **~82.4%**              |

---

## ⚖️ Handling Class Imbalance

- Applied **Balanced Class Weights**
- Minority classes received up to **7x more importance**
- Prevented model bias toward majority class (Label 0)

---

## 📈 Evaluation Metrics

Due to imbalance, accuracy alone was insufficient.

### Metrics Used:

- **Macro-Average F1 Score**
  - Equal importance to all classes

- **Precision**
  - Controls false positives

- **Recall**
  - Controls false negatives


---

## 📁 Data Setup

Place the following files in the root directory:

train.csv
test.csv
--- 
## ▶️ Execution
Open the Jupyter Notebook
Run all cells to:
Train the model
Generate predictions
Output submission.csv
---
##⚠️ Important Note

Always use:
prep.transform(test_data)
instead of fit_transform on test data to ensure consistency with training preprocessing.
---
## 📅 Project Timeline

Comment Category Prediction Challenge
📆 January 2026 – March 2026
---
## 💡 Key Highlights
- End-to-end ML pipeline with real-world applicability
- Advanced feature engineering combining NLP + metadata
- Effective handling of class imbalance
- Production-ready preprocessing pipeline

---
## 📌 Future Improvements
Deep learning models (BERT / Transformers)
Real-time moderation API deployment
