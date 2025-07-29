# Product Substitution System with Siamese BERT

This project predicts substitute products based on product descriptions using a two-phase process:
1. **Baseline using SBERT + cosine similarity**
2. **Supervised fine-tuning using a Siamese BERT model trained on human-labeled pairs**

---

## 📈 Model Performance

After training the Siamese BERT model on ~900 human-labeled product substitution pairs:

| Metric | Value |
|--------|--------|
| ✅ Accuracy | **67.2%** |
| ✅ Valid Substitution Recall (Label = 1) | **75.0%** |
| ✅ AUC Score | **0.727** |

> The model significantly improves over naive cosine similarity by learning what makes two products truly substitutable in a B2B context.

---

## 📦 Project Structure

| Phase | Description |
|-------|-------------|
| 🧠 **Phase 1 – Baseline** | Use pre-trained SBERT to calculate cosine similarity between all product descriptions. The top 3 most similar products are selected as candidate substitutes. |
| ✅ **Human Review** | Substitution candidates are manually labeled as valid or invalid (1 / 0) in `Labeled_Substitution_Pairs.csv`. |
| 🔁 **Phase 2 – Fine-tuned Siamese BERT** | Train a Siamese network using sentence-transformers on labeled pairs to better capture domain-specific substitution logic. |

---

## 📊 Data Files

- `substitution_table_cleaned_for_labeling.csv`: Full original product data and initial 3 candidate substitutes.
- `Labeled_Substitution_Pairs.csv`: Human-reviewed product substitution pairs with labels.
- `siamese_top3_recommendations.csv`: Final output – 3 top-ranked substitutes per product (with scores).

---

## 🧪 Notebooks

- `01_tf-idf_baseline.ipynb`: Cosine similarity baseline.
- `02_siamese_bert.ipynb`: Siamese model training + Top-3 recommendations.

---

## 📂 Final Output

Each product is recommended 3 most semantically similar substitute products using the trained Siamese BERT model, exported in:

`data/siamese_top3_recommendations.csv`

---

## 📌 Example Output

| Item | Sub_1 | Sub_1_Desc | Score_1 |
|------|--------|-------------|---------|
| 1106 | 1106003 | GREEN LID... | 0.91 |

