# 🧠 Hybrid Semantic–Graph Speech Analysis for Early Detection of Alzheimer’s Disease

This project explores how AI can analyze **what people say** (semantic content) and **how they organize their speech** (graph structure) to detect early signs of Alzheimer’s disease — using only **non-invasive, text-based transcripts**.

---

## 📘 Overview
We combine:
- **Semantic embeddings** using `all-mpnet-base-v2` (SentenceTransformers)
- **Structural graph features** using NVG (Natural Visibility Graph) and HVG (Horizontal Visibility Graph)
- **Hybrid modeling** with Random Forests and BiLSTM + Attention

---

## 📊 Dataset
- **Source:** DementiaBank Pitt Corpus (Cookie Theft Picture Description Task)
- **Access:** Restricted academic dataset (not publicly shareable)
- **Used Data:** Transcripts only (no audio)
- **Note:** Due to data-use agreement, this repository includes *no raw or derived data*.  
  To reproduce results, please request access directly from DementiaBank:  
  🔗 https://dementia.talkbank.org/

You may substitute your own speech or text dataset following the same format:

---

## ⚙️ Methods
| Step | Description |
|------|--------------|
| Preprocessing | Sentence tokenization and cleaning of CHAT transcripts |
| Semantic Embedding | SentenceTransformer (`all-mpnet-base-v2`) |
| Structural Features | HVG & NVG from sentence-length time series |
| Models | Random Forest (feature ablation) and BiLSTM + Attention (sequence learning) |

---

## 🧩 Graph Feature Example
Two sentences connect if they are “visible” to each other in the sequence of sentence lengths.

- **HVG rule:** connect if all in-between are shorter than both ends  
  \[
  x_k < \min(x_i, x_j)
  \]
- **NVG rule:** connect if line-of-sight passes above intermediates  
  \[
  x_k < x_i + \frac{x_j - x_i}{j - i}(k - i)
  \]

---

## 📈 Results
| Model | Features | Test AUC | F1 | Accuracy |
|--------|-----------|----------|----|-----------|
| Random Forest | Semantic + HVG | 0.79 | 0.74 | 0.70 |
| BiLSTM + Attention | Semantic + HVG | **0.85** | **0.79** | **0.76** |

🟢 Structural (graph) features improved results across both models.

---

## 💬 Takeaways
- Semantic meaning is the strongest signal.  
- Graph structure adds complementary insight into **thought organization**.  
- The hybrid model improves early, explainable detection — using text only.

⚠️ **Data Disclaimer**
This repository does not include any DementiaBank data, transcripts, or derived features.
All rights belong to the original data custodians.  
Only reproducible code and sample placeholders are provided for research transparency.
