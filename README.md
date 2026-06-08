## 🏥 Survival Super Learner for 30-Day Hospital Readmission

*A clinical machine learning pipeline that uses an advanced Survival Super Learner (Stacked Ensemble) framework to predict 30-day hospital readmission risk.
The system handles the multiple target classes (<30, >30, NO) native to Electronic Health Record (EHR) data by framing them as an interval-censored survival task. This approach helps hospital care teams safely allocate resource coordination budgets where they are needed most.*

------------------------------
## 🚀 Performance & Core Architecture

* Target Chronic Conditions: Type 2 Diabetes Mellitus, Chronic Kidney Disease (CKD), and Essential Hypertension.
* Dataset Pool: 53,000 unique patient rows extracted from 68,000 raw encounter rows of the [UCI Diabetes 130-US Hospitals Dataset](http://archive.ics.uci.edu/dataset/296/diabetes+130-us+hospitals+for+years+1999-2008).
* Validation Performance: Achieved a Harrell's Concordance Index (C-Index) of 0.7022 using patient-stratified 5-fold cross-validation.
* Meta-Model Weight Highlights: The pipeline utilizes your proposed method of taking a weighted score of different base survival models using a regularized linear-style Cox model. The meta-learner assigned 95.66% of its trust allocation to the Random Survival Forest, mathematically proving that medical records are driven by highly non-linear feature interactions rather than simple linear risk paths.

------------------------------
## 📈 Pipeline Visualization
The pipeline outputs an interactive dashboard displaying your model's trust breakdown, a stratified time-to-event survival curve, and top-driver clinical feature importances:
## The Visual Story Behind the Curves
<img width="5971" height="1906" alt="readmissions_pipeline_dashboard" src="https://github.com/user-attachments/assets/03083d2c-11f8-4470-94ab-eb78d9625e3f" />


* Tier A (Top 10% | High Risk): Experiences a steep vertical drop at Day 15, capturing the subset of patients suffering from acute post-discharge complications or sudden drops in stability.
* Tier B (Next 20% | Moderate Risk): Experiences a delayed drop at Day 45, capturing patients who handle the immediate transition home but gradually destabilize due to difficulties managing long-term chronic conditions.
* Tier C (Bottom 70% | Low Risk): Projects a highly stable flat line out past 60 days, identifying patients who can safely return home on standard follow-up paths.

------------------------------
## Repo Architecture

├── preprocess_eda.ipynb      # Stage 1: EHR data cleaning, leakage filtering, and feature extraction<br>
├── modeling.ipynb            # Stage 2: Stacking Super Learner, RSF training, and visual dashboard generation<br>
├── report.pdf            # Detailed Report<br>
├── readmissions_pipeline_dashboard.png   <br>
└── README.md                 # Strategic project summary and technical documentation

------------------------------
## 🔮 Deployment Proposals
To take this validated engine from code to real-world hospital utility, the report outlines a roadmap for two downstream integration proposals:

   1. Automated Clinical Workflow Mapping: Continuous scores are binned into percentile tiers. Tier A (Top 10% of high scores) automatically triggers an EHR alert to deploy home health nurse nurse dispatches within 48 hours of discharge, saving premium beds for the highest-risk patients.
   2. MLOps Model Governance & Drift Auditing: Implementation of monthly automated Population Stability Index (PSI) monitors. If changes in population features or diagnostic code densities push the tracking index past 0.20, the engineering team is instantly alerted to trigger the 6-month automated model recalibration loop.
