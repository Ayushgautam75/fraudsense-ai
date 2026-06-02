# 🔌 FraudSense AI - API Reference Guide

## Base URL

```
http://localhost:5000
```

## Authentication

All endpoints (except `/login`) require an active session. Include credentials in requests.

---

## 📊 Dashboard & Statistics

### Get Dashboard Statistics

**Endpoint:** `GET /api/dashboard-stats`

**Authentication:** Required (Session)

**Response:**

```json
{
  "status": "success",
  "data": {
    "total_transactions": 45,
    "fraud_detected": 8,
    "safe_transactions": 37,
    "fraud_rate": 17.78,
    "fraud_by_day": {
      "2024-04-23": 2,
      "2024-04-24": 1,
      "2024-04-25": 0,
      "2024-04-26": 3,
      "2024-04-27": 2,
      "2024-04-28": 0,
      "2024-04-29": 0
    },
    "location_distribution": {
      "Delhi": 20,
      "Mumbai": 15,
      "Bangalore": 10
    },
    "avg_confidence": 78.45
  }
}
```

**Example Usage (Python):**

```python
import requests

response = requests.get('http://localhost:5000/api/dashboard-stats')
data = response.json()
print(f"Total: {data['data']['total_transactions']}")
print(f"Fraud Rate: {data['data']['fraud_rate']}%")
```

---

## 🤖 Smart Predictions

### Smart Fraud Prediction

**Endpoint:** `POST /api/predict-smart`

**Authentication:** Required (Session)

**Request Body:**

```json
{
  "amount": 5000,
  "hour": 22,
  "device": "mobile",
  "location": "Delhi"
}
```

**Response:**

```json
{
  "status": "success",
  "result": "Safe Transaction",
  "confidence": 92,
  "reasons": [
    "✅ Normal amount: ₹5,000",
    "⏰ Working hours transaction",
    "✅ Known device: mobile"
  ],
  "risk_level": "Low"
}
```

**Possible Risk Levels:**

- `"Low"` - No risk flags
- `"Medium"` - 1-2 risk flags
- `"High"` - 3+ risk flags

**Example Usage (cURL):**

```bash
curl -X POST http://localhost:5000/api/predict-smart \
  -H "Content-Type: application/json" \
  -d '{
    "amount": 5000,
    "hour": 22,
    "device": "mobile",
    "location": "Delhi"
  }'
```

**Example Usage (Python):**

```python
import requests
import json

data = {
    "amount": 5000,
    "hour": 22,
    "device": "mobile",
    "location": "Delhi"
}

response = requests.post(
    'http://localhost:5000/api/predict-smart',
    json=data
)

result = response.json()
print(f"Result: {result['result']}")
print(f"Confidence: {result['confidence']}%")
print("Reasons:")
for reason in result['reasons']:
    print(f"  {reason}")
```

**Device Options:**

- `"mobile"`
- `"laptop"`
- `"tablet"`
- `"atm"`

---

## 👤 Risk Profile

### Get Customer Risk Profile

**Endpoint:** `GET /api/risk-profile`

**Authentication:** Required (Session)

**Response:**

```json
{
  "status": "success",
  "risk_score": 35,
  "category": "🟢 Low Risk",
  "fraud_history": {
    "count": 2,
    "total_transactions": 45,
    "fraud_rate": 4.44
  },
  "spending_pattern": {
    "average": 8500.5,
    "maximum": 45000.0,
    "total_transactions": 45
  }
}
```

**Risk Score Scale:**

- `0-39` → 🟢 Low Risk
- `40-69` → 🟡 Medium Risk
- `70-100` → 🔴 High Risk

**Example Usage (JavaScript):**

```javascript
fetch("/api/risk-profile")
  .then((response) => response.json())
  .then((data) => {
    console.log(`Risk Score: ${data.risk_score}`);
    console.log(`Category: ${data.category}`);
    console.log(`Fraud Rate: ${data.fraud_history.fraud_rate}%`);
  });
```

---

## 🔄 Model Comparison

### Compare Multiple Models

**Endpoint:** `POST /api/model-comparison`

**Authentication:** Required (Session)

**Request Body:**

```json
{
  "amount": 5000,
  "hour": 22,
  "device": "mobile",
  "location": "Delhi"
}
```

**Response:**

```json
{
  "status": "success",
  "models": {
    "Random Forest": {
      "pred": 0,
      "prob": 92.0,
      "result": "Safe"
    },
    "Logistic Regression": {
      "pred": 0,
      "prob": 87.5,
      "result": "Safe"
    }
  },
  "consensus": "Safe",
  "avg_confidence": 89.75
}
```

**Interpretation:**

- `pred`: 0 = Safe, 1 = Fraud
- `prob`: Confidence percentage
- `consensus`: Final prediction based on all models
- `avg_confidence`: Average confidence across all models

---

## 📜 Transaction Export

### Export Transactions (with optional filters)

**Endpoint:** `GET /api/transactions-export`

**Authentication:** Required (Session)

**Query Parameters:**

```
?type=fraud&result=fraud&limit=100
```

| Parameter | Type    | Description      | Example                                        |
| --------- | ------- | ---------------- | ---------------------------------------------- |
| `type`    | string  | Transaction type | `fraud`, `loan`, `risk`, `anomaly`, `spending` |
| `result`  | string  | Result filter    | `fraud`, `safe`, `default`, `approved`         |
| `limit`   | integer | Max records      | `100` (default 1000)                           |

**Response:**

```json
{
  "status": "success",
  "count": 8,
  "data": [
    {
      "id": 1,
      "user_id": "admin",
      "trans_type": "fraud",
      "amount": 15000,
      "location": "Mumbai",
      "device": "laptop",
      "result": "⚠️ Fraud Detected",
      "confidence": 92.5,
      "date": "2024-04-29 22:15:30",
      "details": {}
    },
    ...
  ]
}
```

**Example Usage (Python - Export as CSV):**

```python
import requests
import csv

response = requests.get('http://localhost:5000/api/transactions-export?type=fraud')
data = response.json()

# Write to CSV
with open('fraud_transactions.csv', 'w', newline='') as f:
    writer = csv.DictWriter(f, fieldnames=['id', 'amount', 'location', 'device', 'result', 'confidence', 'date'])
    writer.writeheader()
    writer.writerows(data['data'])
```

---

## 🚨 Anomaly Detection

### Get Anomaly Detection Data

**Endpoint:** `POST /api/anomaly-detection`

**Authentication:** Required (Session)

**Request Body:**

```json
{
  "amount": 5000,
  "hour": 22,
  "device": "mobile",
  "location": "Delhi"
}
```

**Response:**

```json
{
  "status": "success",
  "anomalies": [
    {
      "amount": 45000,
      "confidence": 95,
      "is_anomaly": true,
      "date": "2024-04-28 02:30:15"
    },
    {
      "amount": 5000,
      "confidence": 12,
      "is_anomaly": false,
      "date": "2024-04-28 14:22:45"
    }
  ]
}
```

**Data Structure:**

- `amount`: Transaction amount
- `confidence`: Anomaly confidence (0-100)
- `is_anomaly`: Boolean indicating if anomaly detected
- `date`: Timestamp of transaction

---

## 🔐 Authentication

### Login

**Endpoint:** `POST /login`

**Request Body:**

```json
{
  "user": "admin",
  "pwd": "demo123"
}
```

**Demo Users:**

```
admin / demo123 (Admin role)
user / user123 (User role)
```

### Logout

**Endpoint:** `POST /logout`

**Authentication:** Required (Session)

---

## 📝 Error Responses

### Error Format

```json
{
  "status": "error",
  "message": "Invalid amount"
}
```

### Common Error Codes

| Status Code | Error             | Solution            |
| ----------- | ----------------- | ------------------- |
| 400         | Invalid amount    | Use positive number |
| 401         | Not authenticated | Login first         |
| 404         | Not found         | Check endpoint URL  |
| 500         | Server error      | Check server logs   |

---

## 🛠️ Integration Examples

### Example 1: Dashboard Integration (JavaScript)

```javascript
async function loadDashboardData() {
  const response = await fetch("/api/dashboard-stats");
  const data = await response.json();

  document.getElementById("totalTrans").textContent =
    data.data.total_transactions;
  document.getElementById("fraudCount").textContent = data.data.fraud_detected;
  document.getElementById("fraudRate").textContent =
    data.data.fraud_rate.toFixed(1) + "%";
}

loadDashboardData();
```

### Example 2: Prediction Form (JavaScript)

```javascript
document
  .getElementById("predictionForm")
  .addEventListener("submit", async (e) => {
    e.preventDefault();

    const formData = {
      amount: parseFloat(document.getElementById("amount").value),
      hour: parseInt(document.getElementById("hour").value),
      device: document.getElementById("device").value,
      location: document.getElementById("location").value,
    };

    const response = await fetch("/api/predict-smart", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(formData),
    });

    const result = await response.json();
    displayResult(result);
  });
```

### Example 3: Data Export (Python)

```python
import requests
import pandas as pd

# Get fraud transactions
response = requests.get('http://localhost:5000/api/transactions-export?type=fraud')
data = response.json()

# Convert to DataFrame
df = pd.DataFrame(data['data'])

# Save to Excel
df.to_excel('fraud_transactions.xlsx', index=False)
```

### Example 4: Risk Monitoring (Python)

```python
import requests
import time

def monitor_risk():
    while True:
        response = requests.get('http://localhost:5000/api/risk-profile')
        profile = response.json()['risk_score']

        if profile['risk_score'] > 70:
            print(f"⚠️ Alert: High Risk Score {profile['risk_score']}")

        time.sleep(3600)  # Check every hour

monitor_risk()
```

---

## 📊 Rate Limiting & Performance

**Current Limits:**

- No rate limiting (can be added)
- Recommended: 100 requests/minute per user
- Query optimization: Indexed on user_id, date

**Caching:**

- Dashboard stats cached for 30 seconds
- API responses not cached by default
- Can implement Redis for production

---

## 🔒 Security Considerations

✅ **Implemented:**

- Session-based authentication
- SQL injection prevention (SQLAlchemy)
- CORS protection
- Input validation

⚠️ **Recommendations:**

- Add rate limiting
- Implement API keys for production
- Use HTTPS/SSL
- Add request signing
- Enable audit logging

---

## 📈 Monitoring & Logging

**Current Logging:**

- Startup logs in console
- Prediction logs: User, amount, result
- Error logs: Exceptions and tracebacks

**Recommended Enhancements:**

- ELK Stack (Elasticsearch, Logstash, Kibana)
- Prometheus metrics
- Sentry error tracking
- Application performance monitoring

---

## 🚀 Deployment Considerations

**Production Ready Checklist:**

- [ ] Migrate to PostgreSQL
- [ ] Add Redis caching
- [ ] Implement rate limiting
- [ ] Add API versioning
- [ ] Setup CI/CD pipeline
- [ ] Add comprehensive logging
- [ ] Setup monitoring/alerting
- [ ] Add API documentation (Swagger)

---

## 📞 Support

For questions or issues:

1. Check logs in console
2. Verify database connection
3. Ensure models are loaded
4. Check authentication status

---

**Last Updated:** April 30, 2026
**API Version:** 1.0
**Status:** Production Ready ✅
