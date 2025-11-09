# AUDITMIND 

A comprehensive enterprise-grade platform for ensuring AI model transparency, fairness, and compliance. This platform provides robust tools for model explainability, bias detection, fairness assessment, and regulatory compliance monitoring.

## 🎯 Overview

As AI systems become increasingly critical in enterprise operations, organizations face mounting pressure around trust, transparency, and accountability. This platform addresses these challenges by:

- **Capturing and explaining** every AI decision with human-readable analysis
- **Assessing risk** through automated bias detection and fairness metrics
- **Ensuring compliance** with GDPR, SOC2, HIPAA, and other regulatory frameworks
- **Providing audit trails** for complete transparency and accountability

## ✨ Key Features

### 1. **AI Decision Logging**
- Real-time capture of AI decisions via REST API
- Comprehensive metadata tracking (model name, confidence, inputs/outputs)
- Automatic versioning and timestamping

### 2. **Explainability Engine**
- Feature importance analysis showing which factors influenced decisions
- Decision path visualization
- Counterfactual analysis ("what-if" scenarios)
- Human-readable explanations for every decision

### 3. **Risk Assessment**
- Automated bias detection (age, gender, race, etc.)
- Risk scoring (low/medium/high)
- Confidence interval analysis
- Real-time alerts for high-risk decisions

### 4. **Compliance Center**
- Pre-built templates for GDPR, SOC2, and HIPAA
- Automated compliance checking for every decision
- Audit report generation (PDF/CSV)
- Configurable compliance rules

### 5. **Interactive Audit Sandbox**
- Simulate AI decisions without logging to production
- Instant explainability analysis
- Test compliance before deployment
- Example scenarios for finance, healthcare, and HR

### 6. **Governance Dashboard**
- Real-time metrics and analytics
- Risk distribution visualization
- Recent decision feed
- Compliance rate tracking

### 7. **ML Service (Python)**
- Production-ready ML models using scikit-learn
- Automatic decision logging to Trust Platform
- Three pre-trained models:
  - **Loan Approval** (RandomForest) - Finance domain
  - **Patient Risk Assessment** (GradientBoosting) - Healthcare domain
  - **Candidate Screening** (LogisticRegression) - HR domain

## 🏗️ Tech Stack

**Backend (Trust Platform API):**
- Node.js + Express + TypeScript
- In-memory data store (production-ready for PostgreSQL)
- RESTful API architecture

**Frontend:**
- React 18 + TypeScript
- Vite for fast development
- Tailwind CSS for styling
- Recharts for data visualization

**ML Service:**
- Python 3.11 + Flask
- scikit-learn for ML models
- NumPy & Pandas for data processing
- Automatic integration with Trust Platform

## 🚀 Getting Started

### Prerequisites
- Node.js 18+ installed
- Python 3.11+ installed (for ML service)

### Installation

1. **Install backend dependencies:**
```bash
cd backend
npm install
```

2. **Install frontend dependencies:**
```bash
cd frontend
npm install
```

3. **Install ML service dependencies:**
```bash
cd ml-service
pip install -r requirements.txt
```

### Running the Application

**Start backend server:**
```bash
cd backend
npm run dev
```
Backend runs on `http://localhost:3000`

**Start frontend server:**
```bash
cd frontend
npm run dev
```
Frontend runs on `http://localhost:5000`

**Start ML service:**
```bash
cd ml-service
python app.py
```
ML Service runs on `http://localhost:8000`

Note on database defaults:
- The ML service now defaults to SQLite for development when `DATABASE_URL` is not set, so it runs without requiring PostgreSQL locally.
- To use PostgreSQL, set `DATABASE_URL` (or `DEV_DATABASE_URL` for development) to your connection string in the environment or `.env`.
- The database health check is dialect-aware and works across PostgreSQL and SQLite.

The platform will automatically load demo data showcasing decisions from finance, healthcare, and HR domains.

## 📡 API Documentation

### Base URL
```
http://localhost:3000/api
```

### Endpoints

#### Log AI Decision
```http
POST /api/decisions
Content-Type: application/json

{
  "modelName": "loan_approval_v3",
  "modelType": "XGBoost",
  "domain": "finance",
  "inputData": {
    "credit_score": 720,
    "annual_income": 85000,
    "debt_to_income": 0.22
  },
  "output": "approved",
  "confidence": 0.89
}
```

**Response:**
```json
{
  "success": true,
  "decision": {
    "id": "uuid",
    "timestamp": "2025-11-01T10:30:00Z",
    "modelName": "loan_approval_v3",
    "output": "approved",
    "confidence": 0.89,
    "explanation": {
      "summary": "Decision approved was primarily influenced by...",
      "featureImportance": [...],
      "decisionPath": [...],
      "counterfactuals": [...]
    },
    "riskScore": {
      "level": "low",
      "score": 0.15,
      "factors": [],
      "biasIndicators": [...]
    },
    "complianceChecks": [
      {
        "framework": "GDPR",
        "passed": true,
        "requirements": [...]
      }
    ]
  }
}
```

#### Get All Decisions
```http
GET /api/decisions?domain=finance&riskLevel=high
```

#### Get Decision by ID
```http
GET /api/decisions/:id
```

#### Get Statistics
```http
GET /api/stats
```

#### Simulate Decision (Audit Sandbox)
```http
POST /api/simulate
Content-Type: application/json

{
  "modelName": "test_model",
  "domain": "healthcare",
  "inputData": {
    "age": 45,
    "bmi": 27.5
  }
}
```

#### Get Compliance Templates
```http
GET /api/compliance/templates
```

### ML Service API

#### Base URL
```
http://localhost:8000
```

#### Get Available Models
```http
GET /models
```

**Response:**
```json
{
  "models": [
    {
      "name": "loan_approval_sklearn_v1",
      "type": "RandomForest",
      "domain": "finance",
      "endpoint": "/predict/loan",
      "features": ["credit_score", "annual_income", "debt_to_income", "employment_years"],
      "trained": true
    },
    ...
  ]
}
```

#### Train Models
```http
POST /train/all
```

```http
POST /train/{model_name}
```

Supported `model_name` values:
- `loan`, `loan_approval_sklearn_v1`
- `patient-risk`, `patient_risk_sklearn_v1`
- `candidate`, `candidate_screening_sklearn_v1`

Notes:
- Models are not trained at startup. Predictions will auto-train on first use if needed.
- Use these endpoints to pre-train models for production readiness.

#### Loan Approval Prediction
```http
POST /predict/loan
Content-Type: application/json

{
  "credit_score": 720,
  "annual_income": 85000,
  "debt_to_income": 0.22,
  "employment_years": 7
}
```

**Response:**
```json
{
  "prediction": "approved",
  "confidence": 0.89,
  "feature_importance": {
    "credit_score": 0.35,
    "annual_income": 0.30,
    "debt_to_income": 0.20,
    "employment_years": 0.15
  },
  "logged_to_platform": true,
  "platform_decision_id": "uuid"
}
```

#### Patient Risk Prediction
```http
POST /predict/patient-risk
Content-Type: application/json

{
  "age": 62,
  "bmi": 31.2,
  "blood_pressure": 145,
  "cholesterol": 240,
  "smoking": true
}
```

#### Candidate Screening Prediction
```http
POST /predict/candidate
Content-Type: application/json

{
  "years_experience": 8,
  "education_level": "masters",
  "skills_match": 0.88,
  "previous_companies": 4
}
```

**Note:** All ML Service predictions are automatically logged to the Trust Platform for explainability analysis and compliance checking.

## 💡 Usage Examples

### Example 1: Finance - Loan Approval
```javascript
const response = await fetch('http://localhost:3000/api/decisions', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    modelName: 'loan_approval_model',
    domain: 'finance',
    inputData: {
      credit_score: 720,
      annual_income: 75000,
      debt_to_income: 0.25,
      employment_years: 5
    },
    output: 'approved',
    confidence: 0.87
  })
});

const { decision } = await response.json();
console.log(decision.explanation.summary);
console.log(decision.riskScore.level); // 'low'
console.log(decision.complianceChecks); // GDPR, SOC2, HIPAA status
```

### Example 2: Healthcare - Patient Risk Assessment
```javascript
const response = await fetch('http://localhost:3000/api/decisions', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    modelName: 'patient_risk_model',
    domain: 'healthcare',
    inputData: {
      age: 62,
      bmi: 31.2,
      blood_pressure: 145,
      cholesterol: 240,
      smoking: true
    },
    output: 'high_risk',
    confidence: 0.82
  })
});
```

### Example 3: HR - Candidate Screening
```javascript
const response = await fetch('http://localhost:3000/api/decisions', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    modelName: 'candidate_screening_ai',
    domain: 'hr',
    inputData: {
      years_experience: 8,
      education_level: 'masters',
      skills_match: 0.88,
      previous_companies: 4
    },
    output: 'qualified',
    confidence: 0.85
  })
});
```

## 📁 Project Structure

```
├── backend/
│   ├── src/
│   │   ├── controllers/      # API request handlers
│   │   ├── models/            # TypeScript interfaces
│   │   ├── routes/            # API route definitions
│   │   ├── services/          # Business logic
│   │   │   ├── dataStore.ts           # In-memory storage
│   │   │   ├── explainabilityService.ts  # AI explanation engine
│   │   │   └── complianceService.ts   # Compliance checking
│   │   ├── utils/             # Utility functions
│   │   └── server.ts          # Express app setup
│   └── package.json
├── frontend/
│   ├── src/
│   │   ├── components/        # React components
│   │   ├── pages/             # Page components
│   │   │   ├── Dashboard.tsx
│   │   │   ├── DecisionExplorer.tsx
│   │   │   ├── AuditSandbox.tsx
│   │   │   └── ComplianceCenter.tsx
│   │   ├── services/          # API client
│   │   └── App.tsx
│   └── package.json
└── README.md
```

## 🎨 UI/UX Features

- **Professional Design:** Enterprise-grade interface with clean, modern aesthetics
- **Real-time Updates:** Dashboard auto-refreshes every 10 seconds
- **Interactive Visualizations:** Pie charts, bar charts, and progress indicators
- **Color-coded Risk Levels:** Instant visual feedback (green/yellow/red)
- **Responsive Layout:** Works on desktop, tablet, and mobile
- **Navigation:** Intuitive navigation between Dashboard, Decision Explorer, Audit Sandbox, and Compliance Center

## 🔒 Compliance Frameworks

### GDPR (General Data Protection Regulation)
- Data minimization checks
- Transparency requirements
- Fairness and non-discrimination

### SOC 2 (Service Organization Control 2)
- Audit trail verification
- Data integrity checks
- Availability monitoring

### HIPAA (Health Insurance Portability and Accountability Act)
- Protected Health Information (PHI) security
- Minimum necessary data usage
- Accountability and traceability

## 🚧 Roadmap

**Phase 1 (Current):** ✅
- Core explainability engine
- Decision logging and tracking
- Compliance templates (GDPR, SOC2, HIPAA)
- Audit sandbox
- Governance dashboard

**Phase 2 (Future):**
- PostgreSQL database integration
- Multi-agent system support
- Advanced bias detection algorithms
- Custom compliance rule builder
- PDF/CSV audit report generation
- Real-time alerting system

**Phase 3 (Future):**
- Decentralized architecture support
- Spatial computing integration
- IoT device decision tracking
- Enterprise SSO integration
- Advanced analytics and ML insights

## 📄 License

This project is available for enterprise evaluation and demonstration purposes.

## 🤝 Support

For questions, issues, or enterprise licensing inquiries, please contact your platform administrator.

---

**Built to ensure AI systems are transparent, fair, and accountable.**
