# Low-Resource Protein Function Prediction: Tokenization and Sparsity Analysis

This project studies how **protein language models behave when labeled biological data is scarce**, and how **sequence tokenization choices** affect model performance under such low-resource conditions.

The work is inspired by challenges in real-world bioinformatics, where most protein sequences lack reliable functional annotations.

---

## 🧬 Motivation

Modern protein language models (e.g., ProtBERT) are pretrained on millions of unlabeled protein sequences and achieve strong performance on downstream tasks.  
However, in practice:

- Functional labels are **limited or missing**
- Tokenization choices (amino acids vs k-mers) are often **assumed**, not analyzed

This project asks:

> **Does tokenization help or hurt protein models when labeled data is extremely limited?**

---

## 🔍 Key Research Questions

1. How robust are protein language models under **1%–10% labeled data**?
2. How does **tokenization (AA vs 3-mer vs 4-mer)** affect performance?
3. How does **vocabulary size and sparsity** influence learning?
4. Can **simple k-mer baselines** outperform deep models in low-resource settings?

---

## 🧪 Dataset

- **Source:** UniProt Swiss-Prot
- **Labels:** Gene Ontology (GO) terms
- **Filtering:** Classes with ≥ 50 proteins
- **Total Proteins:** ~12,000
- **Task:** Multi-class protein function classification

---

## 🧠 Models and Representations

### 1. ProtBERT Embeddings
- Pretrained ProtBERT model
- Mean-pooled sequence embeddings
- Classifier: Logistic Regression
- Tokenizations:
  - Amino Acid (AA)
  - Overlapping 3-mers
  - Overlapping 4-mers

### 2. K-mer-only Baseline
- Bag-of-k-mers (3-mer, 4-mer)
- No pretrained model
- Classifier: Logistic Regression

---

## 📉 Vocabulary & Sparsity Analysis

| Tokenization | Vocabulary Size | Avg Tokens / Sequence | Rare Token % |
|-------------|----------------|----------------------|--------------|
| AA          | 21             | 399.14               | 0.00%        |
| 3-mer       | 8,047          | 397.14               | 1.06%        |
| 4-mer       | 137,493        | 396.14               | 44.49%       |

**Insight:**  
Higher-order k-mers drastically increase vocabulary size and sparsity, especially harmful under low-resource supervision.

---

## 📊 Results: ProtBERT + Tokenization

| Split | Train Size | AA F1 | 3-mer F1 | 4-mer F1 |
|------|-----------|------|----------|----------|
| 100% | 12,265    | 0.7123 | 0.0920 | 0.1005 |
| 10%  | 1,226     | 0.2986 | 0.0498 | 0.0564 |
| 5%   | 613       | 0.1595 | 0.0353 | 0.0350 |
| 1%   | 122       | 0.0452 | 0.0188 | 0.0179 |

---

## 📊 Results: K-mer-only Baseline

| Split | Train Size | 3-mer F1 | 4-mer F1 |
|------|-----------|----------|----------|
| 100% | 12,265    | 0.7897   | 0.7920   |
| 10%  | 1,226     | 0.4920   | 0.4520   |
| 5%   | 613       | 0.3965   | 0.3398   |
| 1%   | 122       | 0.1141   | 0.0913   |

---

## 🧠 Key Observations

- Amino-acid tokenization is **far more robust** than k-mer tokenization in ProtBERT under low-resource conditions.
- Large k-mer vocabularies introduce severe **data sparsity**, harming deep models when labels are limited.
- Surprisingly, **simple k-mer baselines outperform ProtBERT embeddings** in extreme low-data regimes.
- Pretraining does not guarantee robustness when tokenization conflicts with data availability.

---

## 📌 Why This Matters

This study highlights that:

- Tokenization is a **critical design choice**, not a trivial preprocessing step.
- Under realistic low-resource biological settings, **simpler models may outperform complex pretrained models**.
- Vocabulary sparsity can negate the benefits of large-scale pretraining.

These insights are important for applying protein language models in real-world biological discovery.

---

## 🛠 How to Run

This project was developed in Google Colab.

1. Open the notebook
2. Run all cells in order
3. Datasets are automatically downloaded
4. Results are cached for reproducibility

---

## 📚 Future Work

- Per-class error analysis
- Hybrid tokenization strategies
- Adapter-based fine-tuning
- Integration with biological knowledge graphs

---

## 📄 License

This project is released under the MIT License.
