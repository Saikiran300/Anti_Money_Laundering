# 💸 Anti-Money Laundering Detection System (Big Data Pipeline)

This project builds a scalable and efficient Big Data pipeline to detect suspicious financial transactions using Apache Spark, machine learning models (GBT, XGBoost), and an interactive Streamlit dashboard. Designed for high-volume data, the system can process, classify, and visualize large-scale transactional behavior in real-time or batch mode.

---

## 📌 Key Features

- **High-Volume Data Processing**: Built with PySpark to handle and transform millions of records.
- **Advanced ML Models**: Trained with both Spark MLlib’s Gradient Boosted Trees and XGBoost for classification.
- **Real-Time Predictions**: Streamlit interface allows single transaction evaluation on-the-fly.
- **Batch Risk Analysis**: Upload large CSVs (up to 2GB+) and get immediate risk classifications.
- **Deployment-Ready**: Modular code, model serialization, and environment setup included.

---

## 🧰 Technology Stack

| Layer              | Tools / Libraries                            |
|--------------------|-----------------------------------------------|
| **Data Pipeline**   | Apache Spark (PySpark), Spark SQL             |
| **Feature Engineering** | PySpark window functions, aggregations   |
| **ML Modeling**     | Spark MLlib (GBTClassifier), XGBoost         |
| **Frontend**        | Streamlit (Real-time + Batch Interface)      |
| **Model Persistence** | joblib, scikit-learn                       |
| **Storage**         | CSV files (2GB+ supported)                   |
| **Version Control** | Git, GitHub                                  |

---

## 📂 Folder Layout

```
.
├── app.py                          # Streamlit dashboard
├── requirements.txt               # Project dependencies
├── code/
│   ├── feature_engineering_pipeline.py
│   ├── extract_laundering_transactions.py
│   ├── xgb_aml_model.pkl          # Serialized XGBoost model
│   ├── gbt_aml_model.pkl          # Serialized Spark MLlib model
│   └── HI-Small_Trans.csv         # Sample transaction data
├── data/
│   └── final_ml_dataset.csv       # Processed dataset with features + labels
└── docs/
    └── architecture_diagram.png  # Project architecture
```

---

## 🔄 Workflow Breakdown

### 1️⃣ Data Ingestion
- Reads the IBM HI-Small AML dataset using `SparkSession.read.csv()` with inferred schema.

### 2️⃣ Feature Engineering
- Groups data by account ID and applies custom aggregations.
- Derives features like:
  - Transaction count
  - Average/standard deviation of amounts
  - Hour-based time buckets
  - Custom metrics via `percentile_approx`

### 3️⃣ Labeling Suspicious Transactions
- Parses semi-structured `.txt` logs using regex to identify laundering tags.
- Joins labels to main dataset to create a complete training matrix.

### 4️⃣ Model Training
- Models used:
  - `GBTClassifier` from Spark MLlib
  - `XGBoostClassifier` (using joblib for persistence)
- Training on PySpark-generated features.

### 5️⃣ Streamlit Dashboard
- **Single Transaction Mode**: Enter values to get instant classification
- **Batch Mode**: Upload full transaction files (CSV) for scoring
- Model switcher to compare GBT vs. XGBoost results

---

## 🚀 Getting Started

### Step 1: Environment Setup
```bash
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### Step 2: Run Spark Feature Pipeline
Run the preprocessing and feature engineering code from the `code/` folder using PySpark.

### Step 3: Launch Streamlit App
```bash
streamlit run app.py
```

---

## 🧠 Contributors

- Sai Kiran Reddy Pothuganti
---

## 📸 App Previews

![Screenshot 1](https://github.com/user-attachments/assets/e691cdcc-555c-4399-96e5-476f661860fc)
![Screenshot 2](https://github.com/user-attachments/assets/3f0faf27-e99f-4865-b20f-7a3fd4b09149)
![Screenshot 3](https://github.com/user-attachments/assets/bdb3b9d5-847d-4c15-b1f2-8283dd1fb4e6)

---

## 📚 References

- [Apache Spark](https://spark.apache.org/)
- [Streamlit Docs](https://docs.streamlit.io/)
- [XGBoost](https://xgboost.readthedocs.io/)
- [IBM AML Dataset](https://www.kaggle.com/datasets/ibm/anti-money-laundering-dataset)
