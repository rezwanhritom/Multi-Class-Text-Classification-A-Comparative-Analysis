# Multi-Class Text Classification: A Comparative Analysis

This repository contains the implementation and analysis for the project **"Multi-Class Text Classification: A Comparative Analysis"**. The work investigates how text preprocessing strategies and feature representations affect multi-class news headline classification across classical machine learning and deep sequence models.

The study classifies headlines into four topics — **Business**, **Science and Technology**, **Sports**, and **World News** — and systematically compares **TF-IDF** and **Skip-gram Word2Vec** representations under three preprocessing regimes across eight model architectures.

---

## 📌 Key Contributions

- A controlled comparison of **three preprocessing strategies** (*none*, *extreme*, *optimum*) on short-form news text.

- Evaluation of **TF-IDF** vs. **Skip-gram Word2Vec** representations for multi-class headline classification.

- Benchmarking of **eight models**, spanning Logistic Regression, Deep Neural Networks, and unidirectional/bidirectional RNN variants (SimpleRNN, GRU, LSTM).

- A full experimental grid of **24 final experiments** and **132 hyperparameter tuning runs**, scored primarily by **macro-F1**.

---

## 📊 Dataset Overview

- **Task:** Multi-class topic classification of news headlines

- **Training set:** 88,829 headlines (`Training_data_9.csv`)

- **Test set:** 12,000 headlines, balanced at 3,000 per class (`Test_data.csv`)

- **Classes:** Business, Science and Technology, Sports, World News

- **Split:** Stratified 85/15 train–validation split from the training file (75,504 / 13,325), with a held-out test set for final evaluation

The training distribution is **imbalanced** (Sports and World News dominate), while the test set is balanced — making **macro-F1** the primary evaluation metric.

---

## 🔧 Preprocessing & Representations

### Preprocessing Variants

| Variant | Description |
|---|---|
| **none** | Raw headline text |
| **extreme** | HTML cleaning, stopword removal, lemmatization, and stemming |
| **optimum** | Same cleaning as *extreme*, but retains negations and skips stemming |

### Feature Representations

- **TF-IDF** – Sparse bag-of-words features with n-gram search
- **Skip-gram Word2Vec** – 100-dimensional embeddings (window 5), frozen as a sequence embedding layer (vocab 30k, sequence length 60)

---

## 🤖 Models Implemented

### TF-IDF Models

- **Logistic Regression** – Interpretable linear baseline
- **Deep Neural Network (DNN)** – Multi-layer dense network with dropout and early stopping

### Skip-gram Sequence Models

- **SimpleRNN / BiSimpleRNN**
- **GRU / BiGRU**
- **LSTM / BiLSTM**

Hyperparameters were selected via grid search on validation macro-F1. Full tuning logs are available in [`Result/tuning_logs_table.csv`](Result/tuning_logs_table.csv).

---

## 📈 Results Summary

- **Best model:** Extreme preprocessing + TF-IDF + Deep Neural Network
- **Test accuracy:** **91.16%**
- **Macro-F1:** **0.911**

| Rank | Setup | Accuracy | Macro-F1 |
|---|---|---|---|
| 1 | extreme · TF-IDF · DeepNN | **0.9116** | **0.9111** |
| 2 | extreme · Skip-gram · BiLSTM | 0.9086 | 0.9082 |
| 3 | optimum · TF-IDF · DeepNN | 0.9084 | 0.9079 |
| 4 | optimum · Skip-gram · BiLSTM | 0.9083 | 0.9078 |

Complete rankings for all 24 experiments are in [`Result/final_results_table.csv`](Result/final_results_table.csv).

### Key Observations

- Preprocessing substantially improves neural sequence models; gains are largest for weaker architectures.
- *Extreme* and *optimum* preprocessing perform nearly identically on this task.
- Gated RNNs (GRU/LSTM) strongly outperform plain SimpleRNN on 60-token sequences.
- For short, keyword-heavy headlines, a TF-IDF Deep NN matches or beats heavier sequence models at lower training cost.
- Business vs. Science/Technology remains the hardest class pair across all models.

---

## 🧠 Practical Implications

- Careful text cleaning remains a high-leverage step for noisy, HTML-wrapped short text.
- Strong classical/neural bag-of-words pipelines can be competitive with recurrent models on headline-length inputs.
- Macro-F1 and confusion-matrix analysis are essential when class imbalance and semantic overlap are present.

These findings support practical NLP pipelines where preprocessing and representation choice should be validated jointly with model selection.

---

## 📜 License

This repository is licensed under the **Creative Commons Attribution–NonCommercial 4.0 International (CC BY-NC 4.0)** license.

- ✔️ Academic and research use permitted
- ❌ Commercial use prohibited
- 📌 Proper attribution and citation required

See the `LICENSE` file for full terms.

---

## 📚 Citation (APA)

If you use this work in academic or research contexts, please cite:

Hritom, R. (2026). *Multi-Class Text Classification: A Comparative Analysis* https://github.com/rezwanhritom/Multi-Class-Text-Classification-A-Comparative-Analysis

---

## 💬 Connect

If you find this repository helpful or would like to discuss the project, feel free to open an issue or start a discussion.

Created and maintained by: [Rezwanur Rahman](https://github.com/rezwanhritom)
