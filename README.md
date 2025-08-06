# 🧠 Modulation of *Bacteroides fragilis*-Driven Bile Acid Metabolism in Stroke-Associated Enterotypes by *Eucommia ulmoides* Extract and *Limosilactobacillus reuteri* 🌿💊

[![DOI](https://img.shields.io/badge/DOI-10.xxxx%2Fxxxx-blue.svg)](https://doi.org/10.xxxx/xxxx) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) <p align="center">
  <img src="https://raw.githubusercontent.com/Benjamin-JHou/BioDeepNat/main/images/icon.png" alt="icon" width="120">
</p>

<h1 align="center">Modulation of *Bacteroides fragilis*-Driven Bile Acid Metabolism in Stroke-Associated Enterotypes by *Eucommia ulmoides* Extract and *Limosilactobacillus reuteri*</h1>

<p align="center">
  <em>🔬 Exploring the association between specific gut enterotypes, bile acids, and ischemic stroke (IS), and evaluating the interventional effects of *Eucommia ulmoides* (EU) extract and *Limosilactobacillus reuteri* (*L. reuteri*).</em>
</p>

<p align="center">
  <img src="https://github.com/WXG920713/Stroke-and-B.fragilis-EU/blob/main/graph%20abstract.png" alt="Graphical Abstract" width="800"> 
</p>

---

## 📜 Table of Contents

- [Overview](#overview)
- [Analysis Workflow](#analysis-workflow)
  - [1. Personalized Metabolic Modeling (COBRA)](#1-personalized-metabolic-modeling-cobra)
    - [📄 `create_panmodel_code.txt`](#create_panmodel_codetxt)
    - [📄 `initMgPipe_code.txt`](#initmgpipe_codetxt)
  - [2. Machine Learning Analysis (XGBoost-SHAP)](#2-machine-learning-analysis-xgboost-shap)
    - [💻 `xgboost_shap.ipynb`](#xgboost_shapipynb)
- [Data Availability](#data-availability)
- [How to Cite](#how-to-cite)
- [Acknowledgements](#acknowledgements)

---

## 💡 Overview

Gut microbiota dysbiosis influences the risk of ischemic stroke (IS)[cite: 2]. Diet and natural products can modulate the microbiota to prevent disease[cite: 3]. This study focuses on the association of specific enterotypes and bile acids with IS, and evaluates the interventional effects of *Eucommia ulmoides* (EU) extract and *Limosilactobacillus reuteri* (*L. reuteri*)[cite: 4]. Public metagenomic data from IS patients and healthy controls were used to classify the gut microbiota[cite: 5]. Constraint-based metabolic models (COBRA) were employed to predict microbial metabolic features[cite: 6]. Machine learning (XGBoost-SHAP) was utilized to identify key microbes and metabolites[cite: 7]. In vitro experiments and a PC12 and Caco-2 co-culture cell model were used to validate their effects on the gut-brain axis[cite: 8, 9].

The Bacteroidaceae-dominant enterotype (ET-B) is associated with a higher risk of IS, while the Lachnospiraceae-dominant enterotype (ET-L) is associated with a lower IS risk[cite: 10]. ET-B, enriched with *B. fragilis*, increases the production of deoxycholic acid (DCA), thereby impairing brain and gut function[cite: 11]. The combined intervention of *L. reuteri* and EU extract, particularly the addition of EU, significantly inhibited *B. fragilis* growth and DCA production, improved intestinal barrier function by upregulating p-AMPKα and ZO-1, and demonstrated neuroprotective effects via the upregulation of p-AKT[cite: 12].

---

## ⚙️ Analysis Workflow

The analysis workflow and corresponding scripts used in this study are as follows:

### 1. 🧬 Personalized Metabolic Modeling (COBRA)

Personalized gut microbiota community metabolic models were constructed using the constraint-based metabolic modeling (COBRA) toolbox, integrating the assembly of gut organisms through reconstruction and analysis (AGORA)2 model and species-level relative abundance data[cite: 57].

#### 📄 `create_panmodel_code.txt`

This MATLAB script is used to **convert strain-level AGORA2 models to species-level pan-genome models**[cite: 58]. This is a key preprocessing step for personalized metabolic modeling.

- **📖 Relevant Paper Section:** 2.3. Personalized metabolic modeling and flux analysis [cite: 57]
- **▶️ Main Function:** Calls the `createPanModels` function[cite: 492, 500].
- **➡️ Inputs:**
    - `modPath`: Path to the folder containing strain models[cite: 485, 486].
    - `taxTable`: Path to the AGORA2 information file containing taxonomic information for strains[cite: 490, 491].
- **⬅️ Outputs:**
    - `panPath`: Output path for the corresponding level pan-genome model[cite: 487].
- **🛠️ Core Tools:** MATLAB, AGORA2 model data.

#### 📄 `initMgPipe_code.txt`

This MATLAB script is used to **construct personalized gut microbiota community metabolic models** and perform flux analysis[cite: 57, 513]. It integrates the species-level pan-models and species relative abundance data, considering dietary compositions[cite: 57, 59, 507, 508].

- **📖 Relevant Paper Section:** 2.3. Personalized metabolic modeling and flux analysis [cite: 57]
- **▶️ Main Function:** Calls the `initMgPipe` function[cite: 513, 530].
- **➡️ Inputs:**
    - `modPath`: Path to the species pan-models (generated by `create_panmodel_code.txt`)[cite: 505, 506, 516].
    - `abunFilePath`: Path to the OTU table or similar abundance input file[cite: 501, 502, 503, 504, 517].
    - `dietFilePath`: Path to the file containing diet constraints[cite: 507, 508, 519, 520].
- **⬅️ Outputs:**
    - `netSecretionFluxes`: Net secretion fluxes of metabolites by the community[cite: 524].
    - `netUptakeFluxes`: Net uptake fluxes of metabolites by the community[cite: 525].
    - And other model statistics and summary data[cite: 523, 526, 527, 528, 529].
- **🛠️ Core Tools:** MATLAB, COBRA toolbox, AGORA2 model data, IBM CPLEX solver[cite: 62].
- **📄 Paper Mention:** This script is also referenced in Section 2.5. "Metabolic Model Simulations of bile acid" for simulating metabolic capabilities and interactions of *B. fragilis* and *L. reuteri*, especially concerning bile acid metabolism[cite: 79, 84].

### 2. 🤖 Machine Learning Analysis (XGBoost-SHAP)

An XGBoost classifier was developed using species-level OTUs to differentiate between Ischemic Stroke (IS) and Healthy Control (HC) patients[cite: 63]. SHAP (SHapley Additive exPlanations) analysis was utilized to interpret feature contributions and identify important microbial predictive metabolites[cite: 71].

#### 💻 `xgboost_shap.ipynb`

This Jupyter Notebook contains the Python code for **building the XGBoost classifier and performing SHAP analysis**.

- **📖 Relevant Paper Section:** 2.3. Extreme Gradient Boosting (XGBoost) Classifier Construction and SHapley Additive exPlanations (SHAP) Interpretation (Note: The paper text mentions this as section 2.3, but its content and placement suggest it might be 2.4 in a revised version, as it follows metabolic modeling).
- **▶️ Main Functions:**
    - Data preprocessing (filtering OTUs[cite: 65], Mann-Whitney U test [cite: 65]).
    - XGBoost hyperparameter optimization using `RandomizedSearchCV`[cite: 66].
    - Model training and 10-fold cross-validation[cite: 69].
    - Model performance evaluation using Receiver Operating Characteristic (ROC) curves and Area Under the Curve (AUC) values[cite: 70].
    - Application of SHAP analysis to identify important microbial species and predictive metabolites[cite: 71].
- **🛠️ Core Tools:** Python, pandas, numpy, scikit-learn, XGBoost, SHAP.
- **📄 Paper Mention:** This analysis was used to identify key gut microbial features in the ET-B and ET-L cohorts (Figures 3a,b and 4a,b) [cite: 175, 181] and key gut microbial metabolites (Supplementary Figures S1b,c)[cite: 173, 174]. The code is available in the GitHub repository[cite: 72].


---

## ✍️ How to Cite

If you use these codes or data in your research, please cite our paper:

Wu, X., Zhang, T., Zhang, T., Jian, F., & Park, S. (Year). Modulation of *Bacteroides fragilis*-Driven Bile Acid Metabolism in Stroke-Associated Enterotypes by *Eucommia ulmoides* Extract and *Limosilactobacillus reuteri*. *Journal Name*, *Volume(Issue)*, Pages. 
DOI: [Insert DOI Here](https://doi.org/XXXX)

---

## 🙏 Acknowledgements

This study was supported by a grant from the National Research Foundation of Korea (NRF) funded by the Ministry of Science and ICT (RS-2023-00208567)[cite: 307].
