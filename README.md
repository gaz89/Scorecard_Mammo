
# 🧮 SMD ScoreCard: A 7C Evaluation Framework for Synthetic Medical Data

Synthetic Medical Data (SMDs) are increasingly used in research, development, and evaluation of AI/ML systems in healthcare. However, their **quality, reliability, and safety** must be carefully assessed before deployment in clinical or regulatory settings.  

The **SMD ScoreCard** provides a systematic, multi-dimensional evaluation framework based on **seven criteria ("7Cs")** that matter both technically and clinically:

1. Congruence – Similarity to patient datasets  
2. Coverage – Diversity and novelty of samples  
3. Constraint – Clinical plausibility and adherence to rules  
4. Completeness – Availability of task-related metadata  
5. Comprehension – Explainability of the data generation process  
6. Compliance – Alignment with privacy, security, and standards  
7. Consistency – Uniformity of data quality across subgroups and over time  

---

## 📊 Framework Overview

<img width="1440" height="900" alt="Screenshot 2025-08-25 at 9 05 35 PM" src="https://github.com/user-attachments/assets/5431944c-e254-4d4c-aa3f-fece0c4d058e" />

Each dimension is evaluated using a combination of statistical, topological, and clinical metrics. The scorecard provides **transparent, interpretable reports** that can guide dataset developers, modelers, and regulators.

---

## 🔧 Installation

Clone the repository and install the required dependencies:

```bash
git clone https://github.com/[your-org-or-username]/SMD_ScoreCard.git
cd SMD_ScoreCard
pip install -r requirements.txt
```

---

## 🚀 Usage

Run the evaluation on your dataset by providing paths to real and synthetic data:

```bash
python run_scorecard.py \
  --real_data ./data/real_dataset/ \
  --synthetic_data ./data/synthetic_dataset/ \
  --output ./results/scorecard_report/
```

Options:
- `--features` : Specify handcrafted (intensity, texture, topology) or deep embeddings (SimCLR, ResNet)  
- `--criteria` : Select subset of the 7Cs (default = all)  
- `--output`   : Path to save generated reports and figures  

---

## 📈 Outputs

The tool generates:
- **ScoreCard Reports** – aggregated summary tables for each dataset  
- **Visualizations** – distribution plots, constraint boundary checks, subgroup violin plots  
- **Supplementary Analysis** – detailed metrics and expanded figures  

Example outputs include:
- Congruence plots (JSD, Cosine, SSIM)  
- Coverage metrics (diversity indices, convex hull volume)  
- Constraint validation against clinically plausible ranges  
- Consistency checks across demographic or protocol subgroups  

---

## 🩺 Interpretation

The scorecard highlights strengths and weaknesses across datasets:
- High Congruence but low Coverage/Consistency → model memorization risk  
- Low Constraint → unrealistic or implausible samples (hallucinations)  
- Low Completeness → missing metadata that reduces downstream utility  
- High Compliance → dataset aligns with privacy and regulatory standards  

---

## 📚 Citation

If you use this framework in your work, please cite:

```
@article{zamzmi2025smdscorecard,
  title={A Seven-Criteria Evaluation Framework for the Responsible Use of Synthetic Medical Data},
  author={Zamzmi, Ghada and colleagues},
  journal={(Pending)},
  year={2025}
}
```

---

## 🤝 Contributing

We welcome contributions! Please open an issue or submit a pull request for:
- Additional metrics  
- Support for new data modalities (e.g., CT, MRI, clinical text)  
- Extended visualization modules  

---

## 📄 License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.  

---

## ✨ Acknowledgments

This framework was developed as part of ongoing work in responsible AI for medical imaging. We thank the broader research and regulatory science community for constructive feedback that shaped this work.
