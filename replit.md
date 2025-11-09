# AI Trust & Explainability Platform - Replit Project

## Project Overview
This is an enterprise-grade AI Trust & Explainability Platform designed to provide transparency, compliance, and audit capabilities for AI decision-making systems across regulated industries (finance, healthcare, HR).

## Current Status
- **Complete:** Full-stack MVP implementation
- **Backend:** Express.js API with TypeScript
- **Frontend:** React + Vite with Tailwind CSS
- **Demo Data:** Pre-loaded with 8 sample AI decisions

## Architecture
- **Backend:** Node.js/Express on port 3000 (API & explainability services)
- **Frontend:** React/Vite on port 5000 (webview)
- **ML Service:** Python/Flask on port 8000 (scikit-learn models)
- **Data Storage:** In-memory singleton DataStore (ready for PostgreSQL migration)

## Key Features Implemented
1. AI Decision Logging API
2. Explainability Engine (feature importance, decision paths, counterfactuals)
3. Risk Assessment (bias detection, risk scoring)
4. Compliance Checking (GDPR, SOC2, HIPAA)
5. Interactive Dashboard
6. Decision Explorer with detailed views
7. Audit Sandbox for simulation
8. Compliance Center with framework documentation

## Project Structure
```
├── backend/          # Express TypeScript API
├── frontend/         # React TypeScript UI
├── ml-service/       # Python Flask ML models
├── README.md         # Comprehensive documentation
└── replit.md         # This file
```

## Recent Changes (2025-11-01)
- Created full project structure (backend, frontend, ML service)
- Implemented backend API with all endpoints
- Built React frontend with 4 main pages
- Added explainability and compliance services
- **NEW:** Built Python ML Service with 3 scikit-learn models:
  - Loan Approval (RandomForest) for finance domain
  - Patient Risk Assessment (GradientBoosting) for healthcare domain
  - Candidate Screening (LogisticRegression) for HR domain
- ML models automatically log predictions to Trust Platform
- Seeded demo data (8 decisions + live ML predictions)
- Fixed DataStore singleton pattern
- Created comprehensive README with ML API documentation

## Development Commands
**Backend:** `cd backend && npm run dev` (port 3000)
**Frontend:** `cd frontend && npm run dev` (port 5000)
**ML Service:** `cd ml-service && python app.py` (port 8000)

## API Endpoints
- POST /api/decisions - Log AI decision
- GET /api/decisions - Get all decisions
- GET /api/decisions/:id - Get specific decision
- GET /api/stats - Get statistics
- POST /api/simulate - Simulate decision (sandbox)
- GET /api/compliance/templates - Get compliance frameworks

## User Preferences
None specified yet.

## Next Steps (If Needed)
- PostgreSQL database integration
- PDF report generation
- Advanced analytics
- Custom compliance rule builder
