# FraudShield

## 🚀 Overview
FraudShield is a financial fraud detection system designed to identify suspicious transactions using anomaly detection and risk scoring techniques. The system simulates real-world financial transaction workflows by analyzing transaction behavior and flagging high-risk activity.

## 🧠 Problem
Financial institutions must detect fraudulent transactions in real time while minimizing false positives. Traditional rule-based systems often fail to adapt to evolving fraud patterns.

## 💡 Solution
FraudShield combines data preprocessing, feature engineering, and machine learning to analyze transaction patterns and assign fraud risk scores. A Flask-based API enables real-time predictions and integration with external systems.

## ⚙️ Features
- Transaction data preprocessing and cleaning  
- Feature engineering for behavioral pattern analysis  
- Machine learning model training and prediction  
- Risk scoring system for fraud detection  
- REST API for real-time fraud predictions  
- SQL database schema for transaction storage  
 - Explainable AI outputs with feature-level contribution analysis

## 🛠️ Tech Stack
- Python (Pandas, NumPy, Scikit-learn)
- Flask (API development)
- SQL (data storage)

## 📁 Project Structure

```
fraudshield/
│── api/
│   └── app.py          # Flask API for predictions
│── src/
│   ├── data_preprocessing.py
│   ├── feature_engineering.py
│   ├── train_model.py
│   ├── predict.py
│   └── fraud_scoring.py
│── database/
│   └── schema.sql
│── requirements.txt
│── README.md
```

## ▶️ Running Locally

```bash
pip install -r requirements.txt
python api/app.py
```

Then send a POST request to:

```
http://localhost:5000/predict
```

## 🔌 API Endpoints
- `POST /predict` → Returns fraud score, risk tier, and actionable decision for a transaction

## 🧪 System Architecture
1. Data preprocessing  
2. Feature engineering  
3. Model training  
4. Prediction + fraud scoring  
5. API layer  

## 📊 Future Improvements
- Real-time streaming detection  
- Advanced ML models (XGBoost, Isolation Forest)  
- Dashboard for fraud monitoring  

## Example: POST /predict

A minimal example showing how to call the fraud detection endpoint with transaction data and what a typical JSON response looks like.

### Request
- **Endpoint:** `POST /predict`
- **Content-Type:** `application/json`

Body (JSON):
```json
{
	"transaction_id": "txn_00012345",
	"user_id": "user_789",
	"timestamp": "2026-03-28T14:32:00Z",
	"amount": 249.99,
	"currency": "USD",
	"merchant_id": "merch_456",
	"merchant_category": "electronics",
	"card_present": false,
	"payment_method": "card",
	"card_bin": "411111",
	"last4": "1111",
	"device_id": "dev_234",
	"ip_address": "203.0.113.45",
	"billing_country": "US",
	"shipping_country": "US",
	"customer_age": 34,
	"customer_tenure_days": 400,
	"previous_transactions_24h": 5,
	"avg_transaction_amount_30d": 120.50,
	"shipping_velocity_hours": 1.2,
	"velocity_score": 0.8
}
```

Curl example:
```bash
curl -s -X POST http://localhost:5000/predict \
	-H "Content-Type: application/json" \
	-d '{
		"transaction_id":"txn_00012345",
		"user_id":"user_789",
		"timestamp":"2026-03-28T14:32:00Z",
		"amount":249.99,
		"currency":"USD",
		"merchant_id":"merch_456",
		"merchant_category":"electronics",
		"card_present":false,
		"payment_method":"card",
		"card_bin":"411111",
		"last4":"1111",
		"device_id":"dev_234",
		"ip_address":"203.0.113.45",
		"billing_country":"US",
		"shipping_country":"US",
		"customer_age":34,
		"customer_tenure_days":400,
		"previous_transactions_24h":5,
		"avg_transaction_amount_30d":120.50,
		"shipping_velocity_hours":1.2,
		"velocity_score":0.8
	}'
```

### Response
- **Content-Type:** `application/json`
- **Description:** The API returns a numeric fraud score, an actionable label/tier, a concise human-readable reason, per-feature contributions for explainability, and timing metadata.

Body (JSON):
```json
{
	"request_id": "req_abc123",
	"model_version": "v1.2.0",
	"fraud_score": 0.87,
	"threshold": 0.5,
	"predicted_label": "fraud",
	"risk_tier": "high",
	"risk_reason": "Transaction amount unusually high for user and rapid shipping velocity from a new device/IP.",
	"action": "block",
	"explanation": [
		{ "feature": "amount", "contribution": 0.35 },
		{ "feature": "velocity_score", "contribution": 0.30 },
		{ "feature": "ip_address_risk", "contribution": 0.15 }
	],
	"human_readable": {
		"score_text": "87% fraud risk",
		"tier_text": "High risk — recommend blocking"
	},
	"latency_ms": 42
}
```

---

If you want, I can add a small note showing how `threshold` maps to `risk_tier` values.