🧬 Tri-Modal Glioblastoma Survival Prediction

This project presents a multimodal framework for predicting survival outcomes in glioma patients by integrating clinical data, genomic mutations, and MRI-derived features. The goal is to improve prognostic accuracy using a combination of machine learning and deep learning techniques.

📌 Overview

Glioblastoma is an aggressive brain tumor with highly variable patient outcomes. Traditional models often rely on a single type of data, which limits their predictive capability.
In this project, a tri-modal approach is used to combine:

Clinical features (age, gender, tumor type, race)
Genomic mutation data (IDH1, TP53, ATRX, EGFR, PTEN, NF1)
MRI features extracted using a pretrained 3D deep learning model

The final prediction is obtained using a late fusion survival model based on Cox proportional hazards.

🏗️ Methodology
1. Data Collection
Clinical and genomic data: TCGA (GBM + LGG)
MRI data: RSNA-MICCAI Brain Tumor Radiogenomic Dataset
2. Preprocessing
Clinical data cleaned and encoded
Genomic data converted into binary mutation matrix
MRI scans resized to 64 × 128 × 128
3. Feature Extraction
MRI features extracted using MedicalNet (3D ResNet-18)
Global average pooling applied
Reduced to 512 features, then PCA → 30 features
4. Modeling
Separate Cox models trained for:
MRI features
Clinical features
Genomic features
Risk scores combined using weighted late fusion:
R_final = w_mri * R_mri + w_clin * R_clin + w_gen * R_gen
5. Evaluation
5-fold cross-validation
Metrics:
Concordance Index (C-index)
Kaplan–Meier survival analysis
Log-rank test
Time-dependent AUC
📊 Results
Model	C-index
MRI Only	0.52
Clinical Only	0.65
Genomic Only	0.53
Clinical + Genomic	0.66
Clinical + MRI	0.66
MRI + Genomic	0.58
Tri-modal	0.67
Significant survival separation observed (log-rank p ≈ 1.7 × 10⁻¹⁵)
Hazard Ratio ≈ 2.07
Time-dependent AUC:
1-year: 0.71
2-year: 0.76
3-year: 0.81
📁 Project Structure
├── data/
│   ├── clinical_genomic.csv
│   ├── mri_features.csv
│
├── notebooks/
│   ├── preprocessing.ipynb
│   ├── feature_extraction.ipynb
│   ├── modeling.ipynb
│
├── models/
│   ├── cox_models.pkl
│
├── app/
│   ├── app.py  (Streamlit interface)
│
├── results/
│   ├── plots/
│   ├── evaluation_metrics.csv
│
└── README.md
💻 Installation
pip install numpy pandas scikit-learn lifelines scikit-survival torch torchvision streamlit
▶️ Usage
Run model
python model.py
Run interface
streamlit run app.py
📈 Visualizations
Kaplan–Meier survival curves
Risk score distribution
Survival scatter plots
Time-dependent AUC curves
⚠️ Limitations
Dataset size is moderate (N = 585)
Requires all three modalities for prediction
No external validation yet
MRI and TCGA datasets are not perfectly aligned
🔮 Future Work
External validation on independent datasets (e.g., BraTS)
Incorporating transformer-based fusion
Explainability using SHAP / Grad-CAM
Handling missing modalities
📚 References
TCGA Dataset
RSNA-MICCAI Brain Tumor Dataset
MedicalNet (Tencent)
👨‍💻 Author

Ramcharan Reddy Kandhuru
B.Tech Student
Department of Computer Science
