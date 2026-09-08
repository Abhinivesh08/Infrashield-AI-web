# Infrashield-AI-web
InfraShield AI — a predictive risk dashboard for infrastructure projects that flags delay and cost-overrun risk before it happens. Self-contained single-file demo (React + Tailwind, no backend) with explainable AI, early-warning alerts, and a swappable prediction engine ready for a real ML backend. Built for SIH26103.
InfraShield AI predicts delay and cost-overrun risk in infrastructure projects before they happen. It classifies each project's risk (LOW/MEDIUM/HIGH/CRITICAL), explains why in plain language with a SHAP-style feature-importance breakdown, and surfaces early warnings for projects that need attention — complete with review/assign/priority workflows and downloadable reports.

This is a self-contained single-file demo (React + Tailwind, no server required) with a secure login flow (including forgot-password) and a prediction engine isolated behind one function, so it's a drop-in slot for a real FastAPI + PostgreSQL + XGBoost/SHAP backend.
