# Causal Relation Extraction from Medical Literature

Fine-tuned **BioClinical ModernBERT** on a **PubMed causal dataset** to extract **cause and effect spans** from biomedical sentences. The model identifies exact cause-effect pairs (e.g., *"Aspirin"* → *"headache relief"*) to support evidence‑based medicine.

##  Overview
Causal relation extraction from medical literature is crucial for building evidence‑based clinical decision support systems. This project fine‑tunes a domain‑specific language model to **automatically extract cause and effect phrases** from single sentences.

## Model & Dataset
- **Model:** [`thomas-sounack/BioClinical-ModernBERT-base`](https://huggingface.co/thomas-sounack/BioClinical-ModernBERT-base) – a state‑of‑the‑art biomedical language model with an 8192‑token context window.
- **Dataset:** [`medalpaca/medical_meadow_pubmed_causal`](https://huggingface.co/datasets/medalpaca/medical_meadow_pubmed_causal) – contains biomedical sentences labeled with causal relations (causative, correlative, etc.).
- **Task:** Token‑level sequence labeling (BIO tagging) for **cause** and **effect** spans.

## Project Pipeline
1. **Load dataset & model** from Hugging Face.
2. **Identify cause/effect spans** using causal trigger words (e.g., *"causes"*, *"leads to"*).
3. **Generate BIO tags** (`B-CAUSE`, `I-CAUSE`, `B-EFFECT`, `I-EFFECT`, `O`).
4. **Tokenize & align** labels with subword tokens (handling WordPiece tokenization).
5. **Fine‑tune** BioClinical ModernBERT for 6 epochs with early stopping.
6. **Evaluate** on test set – extract cause/effect from new sentences.

## Results
- **Validation F1 Score:** `0.88` 
- **Test set performance:** The model successfully extracts cause and effect phrases from unseen sentences, though some disease terms (e.g., *"fever"*) may be misclassified as chemicals due to dataset imbalance.

| Class      | Precision | Recall | F1-score |
|------------|-----------|--------|----------|
| Chemical   | 0.90      | 0.90   | 0.90     |
| Disease    | 0.78      | 0.82   | 0.80     |
| **Micro avg** | 0.87   | 0.89   | **0.88** |

## How to Run

### Option 1: Google Colab (Recommended)
1. Open the provided notebook `.ipynb` file in Colab.
2. Enable **GPU** (Runtime → Change runtime type → T4 GPU).
3. Run all cells sequentially.

### Option 2: Local Machine
1. git clone https://github.com/Muqaddasjamil/causal-relation-extraction.git
2. cd causal-relation-extraction
3. pip install -r requirements.tx
