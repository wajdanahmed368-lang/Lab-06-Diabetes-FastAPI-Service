# Laboratory 6 — Diabetes Risk Prediction FastAPI Service

**Course:** Introduction to Artificial Intelligence (AI–101L)  
**Instructor:** Dr. Muhammad Awais  
**Duration:** 3 hours · **Block:** Phase C — Model Deployment & Serving  

---

## 📌 Project Overview
This project packages a machine learning model into a production-ready web service. It features:
- A high-performance **FastAPI** REST backend.
- A pre-trained scikit-learn **Logistic Regression** model (`Mymdoel.pkl`) trained on clinical diagnostic features.
- An interactive, responsive **HTML/JavaScript Frontend** (`index.html`) for real-time patient risk evaluation.

---

## 🏗️ Architecture
```
[ User Browser / Web Client ]
              │  HTTP POST /predict (JSON)
              ▼
    [ FastAPI Application (main.py) ]
              │  Feature Validation (Pydantic)
              ▼
   [ Scikit-Learn Model (Mymdoel.pkl) ]
              │
              ▼  Prediction (0 / 1) + Probability Score
  { "prediction": "Diabetic", "probability": 0.939 }
```

---

## 📂 Repository Structure
```
├── main.py            # FastAPI REST application routes and ML inference logic
├── index.html         # Responsive web interface for end users
├── Mymdoel.pkl        # Serialized pre-trained Logistic Regression classifier
├── requirements.txt   # Python service dependencies
├── .gitignore         # Git ignore rules
└── README.md          # Project documentation
```

---

## 🔌 API Endpoints

### 1. `GET /`
Returns service status and link to interactive Swagger documentation.
```json
{ "message": "Diabetes API is Running. /docs for API documentation." }
```

### 2. `GET /health`
System health check endpoint.
```json
{ "status": "ok" }
```

### 3. `POST /predict`
Evaluates diabetes onset risk based on 6 patient features.

**Request Payload:**
```json
{
  "Glucose": 160.0,
  "BloodPressure": 80.0,
  "Insulin": 150.0,
  "BMI": 33.5,
  "DiabetesPedigreeFunction": 0.65,
  "Age": 45.0
}
```

**Response Payload:**
```json
{
  "predicted_label": 1,
  "prediction": "Diabetic",
  "probability": 0.812
}
```

---

## 🚀 Running the Service Locally

### 1. Install Dependencies
```bash
pip install -r requirements.txt
```

### 2. Start the FastAPI Server
```bash
python -m uvicorn main:app --reload --port 8000
```
Server runs at: `http://localhost:8000`  
Interactive Swagger docs: `http://localhost:8000/docs`

### 3. Open the Frontend
Double-click `index.html` or open it in your browser. Enter clinical numbers and click **Predict** to receive instantaneous diagnostic results!
