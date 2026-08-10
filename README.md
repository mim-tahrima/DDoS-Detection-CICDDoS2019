# Evaluating the Efficacy of Machine Learning Algorithms in Detecting DDoS Attacks Using the CIC-DDoS2019 Dataset

**Group 2**
Suchitra Kairi (212056) · Tahrima Arif Mim (220205) · Jessica Sen (220241)
Asian University for Women

---

## Problem Statement and Research Objectives

Distributed Denial-of-Service (DDoS) attacks are one of the most disruptive threats to modern network infrastructure. Traditional signature-based intrusion detection systems struggle to keep pace with fast-evolving, multi-vector attacks. This project empirically evaluates whether machine learning classifiers can offer a more adaptive alternative, using the CIC-DDoS2019 benchmark dataset.

**Research Objectives:**
1. Implement and compare four classifiers — Decision Tree, Random Forest, XGBoost, and LightGBM — on accuracy, false-positive rate, and computational overhead.
2. Apply a three-stage (Filter → Wrapper → Embedded) feature selection pipeline and measure its effect on accuracy and efficiency.
3. Evaluate how well the best classifier generalises to a completely unseen DDoS attack type, and how much lightweight fine-tuning improves detection.

**Research Questions:**
- **RQ1:** How do Decision Tree, Random Forest, XGBoost, LightGBM algorithms compare the accuracy and false-positive rates when classifying DDoS attack traffic in the CIC-DDoS2019 dataset, and how do these algorithms compare in terms of training time and computational overhead?
- **RQ2:** How does a three-stage feature selection approach affect the detection accuracy and computational efficiency of different machine learning classifiers compared with using the complete feature set?
- **RQ3:** How does the performance of best classifiers vary when detecting unseen DDoS attack types, and to what extent can fine tuning this classifier with a little amount of target-specific malicious data improve detection performance?

## Dataset Description

This project uses the **CIC-DDoS2019** dataset, a large-scale, labelled benchmark of network flow records extracted via CICFlowMeter (77 features per flow). Six known attack types were used for training/testing (LDAP, MSSQL, NetBIOS, Syn, UDP, UDP-Lag), and a seventh attack type (DNS reflection) was deliberately withheld as an unseen attack for the generalisation experiment (RQ3).

> The raw dataset is not included in this repository due to its size. Download it from the [official CIC-DDoS2019 source](https://www.unb.ca/cic/datasets/ddos-2019.html) and place the Parquet files in a local `data/` folder before running the pipeline (see Execution steps below).

## Folder Structure

```
├── src/              # Source code (the main Jupyter notebook)
├── Models/            # Saved trained model files (.pkl)
├── Results/            # Output CSV tables (metrics, comparisons)
├── Figures/            # Output charts and confusion matrices (.png)
├── Presentation/         # Final presentation slides
├── Report/             # Final written report
├── requirements.txt        # Python dependencies
└── README.md            # This file
```

## Installation and Execution

**1. Clone the repository**
```bash
git clone https://github.com/<your-username>/<your-repo-name>.git
cd <your-repo-name>
```

**2. Create a virtual environment (recommended)**
```bash
python -m venv venv
source venv/bin/activate      # Mac/Linux
venv\Scripts\activate         # Windows
```

**3. Install dependencies**
```bash
pip install -r requirements.txt
```

**4. Add the dataset**
Download the CIC-DDoS2019 Parquet files (see Dataset Description above) and place them in a `data/` folder in the project root.

**5. Run the pipeline**
Open `src/Cyber_project_code.ipynb` in Jupyter Notebook, JupyterLab, or VS Code, update the dataset path variable at the top of the notebook to point to your local `data/` folder, and run all cells in order. The notebook is sectioned into Setup → Data Cleaning → RQ1 → RQ2 → RQ3, and will regenerate all tables (into `Results/`), figures (into `Figures/`), and trained models (into `Models/`).

## Summary of Results

| Research Question | Key Finding |
|---|---|
| **RQ1** | Decision Tree, Random Forest, and XGBoost achieved comparable accuracy (~0.74); LightGBM underperformed (0.18) under default hyperparameters. Decision Tree offered the best speed/false-positive-rate trade-off. |
| **RQ2** | A three-stage feature selection pipeline reduced the feature set from 77 to 15 (an 81% reduction) with negligible accuracy loss and up to 64% faster training. |
| **RQ3** | The best classifier generalised to a fully unseen DNS attack with 95.5% zero-shot accuracy, improving to 98.4% after fine-tuning with only 20% of target-domain data. |

Full methodology, results, and discussion are available in [`Report/`](./Report).

## License

This project was completed for academic purposes as part of a university coursework requirement.
