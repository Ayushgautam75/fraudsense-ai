# ⚡ Quick Start Guide - FraudSense AI

## 🚀 Get Started in 5 Minutes

### Step 1: Install Dependencies

```bash
pip install -r requirements.txt
```

**New packages installed:**

- Flask-CORS (API support)
- Plotly (Interactive charts)
- shap (ML explainability - optional)

### Step 2: Start the Server

```bash
python app.py
```

**Expected Output:**

```
 * Serving Flask app...
 * Running on http://127.0.0.1:5000

 [✅] Database initialized
 [✅] Models loaded successfully
 [✨] Dashboard and prediction features are READY!
```

### Step 3: Open in Browser

```
http://localhost:5000
```

### Step 4: Login

```
Username: admin
Password: demo123
```

---

## 📊 What's New - Quick Overview

| Feature              | Where                         | What It Does                            |
| -------------------- | ----------------------------- | --------------------------------------- |
| **Dashboard**        | `/dashboard`                  | See fraud trends, stats, real-time data |
| **Smart Prediction** | Dashboard → "Make Prediction" | Get fraud prediction + AI reasoning     |
| **Risk Profile**     | `/risk-profile`               | View your customer risk score           |
| **History**          | `/history`                    | Filter, search, export transactions     |
| **Dark Mode**        | 🌙 icon                       | Toggle dark/light theme                 |
| **APIs**             | `/api/*`                      | Programmatic access to all features     |

---

## 🎯 Quick Test Cases

### Test 1: Make a Safe Prediction

```
Amount: 1000
Hour: 14 (2 PM)
Device: mobile
Location: Delhi

Expected Result: ✅ SAFE
Confidence: 90-95%
```

### Test 2: Make a Fraud Prediction

```
Amount: 50000
Hour: 23 (11 PM)
Device: laptop
Location: Unknown

Expected Result: ⚠️ FRAUD
Confidence: 85-92%
```

### Test 3: Check Risk Profile

1. Go to `/risk-profile`
2. See your risk score and recommendations
3. Check fraud statistics

### Test 4: Filter Transactions

1. Go to `/history`
2. Select type: "fraud"
3. Click "Filter"
4. Export as CSV

---

## 🔥 Cool Features to Try

### 1. Dark Mode

Click the moon icon 🌙 in navbar

### 2. Real-Time Dashboard

Statistics auto-update every 30 seconds

### 3. AI Reasoning

See WHY the model thinks it's fraud:

- "💰 High amount: ₹25,000"
- "🌙 Unusual time: Late night transaction"
- "📍 Location change: Mumbai"

### 4. Multi-Device Test

Try on mobile, tablet, laptop - fully responsive!

### 5. Data Export

Download all transactions as CSV or JSON

---

## 📊 API Quick Test

### Using Python:

```python
import requests
import json

# Login first (if needed)
# requests.post('http://localhost:5000/login', data={'user': 'admin', 'pwd': 'demo123'})

# Get dashboard stats
response = requests.get('http://localhost:5000/api/dashboard-stats')
print(json.dumps(response.json(), indent=2))

# Make prediction
response = requests.post(
    'http://localhost:5000/api/predict-smart',
    json={
        'amount': 5000,
        'hour': 22,
        'device': 'mobile',
        'location': 'Delhi'
    }
)
print(json.dumps(response.json(), indent=2))
```

### Using cURL:

```bash
# Get stats
curl http://localhost:5000/api/dashboard-stats

# Make prediction
curl -X POST http://localhost:5000/api/predict-smart \
  -H "Content-Type: application/json" \
  -d '{"amount":5000,"hour":22,"device":"mobile","location":"Delhi"}'
```

### Using Postman:

1. Create new POST request
2. URL: `http://localhost:5000/api/predict-smart`
3. Body (JSON):

```json
{
  "amount": 5000,
  "hour": 22,
  "device": "mobile",
  "location": "Delhi"
}
```

4. Click Send

---

## 📁 Project Structure Overview

```
📦 Financial Fraud Detection
├── 📄 app.py                     ⭐ Main application
├── 📄 utils.py                   ✨ Helper functions & ML logic
├── 📄 models.py                  💾 Database models
├── 📄 config.py                  ⚙️ Configuration
├── 📄 requirements.txt            📦 Dependencies
│
├── 📂 templates/
│   ├── dashboard_enhanced.html   ✨ NEW - Main dashboard
│   ├── history_enhanced.html     ✨ NEW - Transaction history
│   ├── risk_profile.html         ✨ NEW - Risk scoring
│   ├── login_modern.html         Login page
│   └── base.html                 Base template
│
├── 📂 static/
│   ├── css/                      Stylesheets
│   ├── js/                       JavaScript files
│   └── chart.js                  Chart library
│
├── 📂 model/
│   └── project3/                 ML Models
│       ├── cc_fraud_rf.pkl
│       ├── loan_default_rf.pkl
│       ├── iso_forest.pkl
│       └── spend_kmeans.pkl
│
├── 📄 FEATURE_UPGRADE_GUIDE.md   📚 Complete feature guide
├── 📄 API_REFERENCE.md           📚 API documentation
└── 📄 README.md                  📚 Project overview
```

---

## 🎓 Learning Path

### Beginner (5 minutes)

1. Start server
2. Login
3. Make a prediction
4. View results

### Intermediate (15 minutes)

1. Explore dashboard
2. Check risk profile
3. Filter transaction history
4. Export data

### Advanced (30 minutes)

1. Test API endpoints with Python/cURL
2. Review model comparison
3. Check database records
4. Study code in `app.py` and `utils.py`

### Expert (1-2 hours)

1. Modify model parameters
2. Add custom ML models
3. Implement email alerts
4. Deploy to production

---

## 🐛 Troubleshooting

### Problem: "Models not found"

**Solution:** Ensure models are in `model/project3/` directory with correct names

### Problem: "Database error"

**Solution:** Delete `instance/database.db` and restart (will recreate)

### Problem: "Port already in use"

**Solution:** Change port in `app.py`

```python
app.run(debug=True, port=5001)  # Use port 5001 instead
```

### Problem: "Dark mode not saving"

**Solution:** Check if browser allows localStorage (Settings → Privacy)

### Problem: "Charts not showing"

**Solution:** Ensure Plotly CDN is accessible (check internet connection)

---

## 🎬 Live Demo Script (2 minutes)

```
"Good morning! This is FraudSense AI - an intelligent fraud detection system.

Let me show you the key features:

1. [Go to Dashboard]
   "Here's our real-time dashboard with fraud statistics"

2. [Scroll to Prediction Form]
   "Let me make a fraud prediction..."
   - Amount: 50000
   - Time: 23 (late night)
   - Device: laptop
   - Location: Unknown
   [Submit]

   "See? The AI detected it as fraud with 92% confidence and showed
    clear reasons: high amount, late night, unknown location"

3. [Go to Risk Profile]
   "Our customers get a risk score and recommendations"

4. [Go to History]
   "Advanced filtering and export capabilities for analysis"

5. [Show Dark Mode]
   "Modern UI with dark mode support"

Questions? Check API_REFERENCE.md for technical details!"
```

---

## 📈 Performance Tips

### For Faster Loading:

1. Clear browser cache (Ctrl+Shift+Delete)
2. Disable browser extensions
3. Use modern browser (Chrome, Firefox, Edge)

### For Better Charts:

1. Ensure good internet connection
2. Disable VPN if having issues
3. Clear DNS cache: `ipconfig /flushdns` (Windows)

### For Faster Predictions:

1. Ensure models are loaded (check server logs)
2. Database indexed on user_id
3. API caching can be implemented

---

## 🔒 Security Reminders

✅ **Safe to Do:**

- Test with demo accounts
- Make bulk uploads with sample data
- Export transaction data
- Share the code on GitHub (models are local)

⚠️ **Don't Do:**

- Share password (demo123)
- Upload real customer data
- Deploy without HTTPS
- Use admin account for regular users

---

## 📱 Mobile Access

The app is fully responsive! Access from phone:

1. Find your computer's IP:
   - Windows: `ipconfig` → Look for IPv4 Address (e.g., 192.168.x.x)
   - Mac/Linux: `ifconfig` → Look for inet

2. On phone browser:

   ```
   http://YOUR_IP:5000
   ```

3. Enjoy responsive design!

---

## 🎉 You're All Set!

✅ Dashboard with real-time data
✅ Smart predictions with AI reasoning
✅ Risk profiling
✅ Transaction management
✅ API access
✅ Dark mode
✅ Responsive design

**Start presenting and ace your project! 🚀**

---

## 📞 Quick Help

| Need Help With | Location                      |
| -------------- | ----------------------------- |
| **Features**   | FEATURE_UPGRADE_GUIDE.md      |
| **APIs**       | API_REFERENCE.md              |
| **Setup**      | README.md                     |
| **This Guide** | QUICK_START.md (you are here) |

---

**Happy coding! Good luck with your project! 💪**
