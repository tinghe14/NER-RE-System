
# 🔗 End-to-End NER and Relation Extraction System
This project provides a complete system to train and apply Named Entity Recognition (NER) and Relation Extraction (RE) models. It uses BERT-based models from the HuggingFace Transformers library to first identify entities in text and then extract the relationships between them.

## Tech Stack
*   Python, PyTorch, HuggingFace Transformers
*   `seqeval` for NER evaluation
*   Pandas, Scikit-learn

## Example Input / Output
**Input (raw text):**
`"Steve Jobs was the co-founder of Apple Inc."`

**Output (extracted relations):**
*   **NER Step:** `[PER: Steve Jobs]`, `[ORG: Apple Inc.]`
*   **RE Step:** `(Head: Steve Jobs, Relation: found, Tail: Apple Inc.)`


## How to Run

**1. Setup Environment**

First, create a directory for your models and install the required packages.

```bash
mkdir models
pip install -r requirements.txt
```

**2. Train the NER Model**

Use the run_ner.py script with the provided sample data to train and save an NER model.
```bash
python bert-ner/run_ner.py \
  --data_dir sample_data/ner_data \
  --model_type bert \
  --model_name_or_path bert-base-cased \
  --output_dir models/ner_model \
  --do_train \
  --do_eval
```

**3. Train the RE Model**
Similarly, train and save an RE model.
```bash
python bert-re/run_re.py \
  --data_dir sample_data/re_data \
  --model_type bert \
  --model_name_or_path bert-base-cased \
  --output_dir models/re_model \
  --do_train \
  --do_eval
```

**4. Run End-to-End Inference**
Use the main inference script to run the full pipeline on new text. This script will load both fine-tuned models.
```bash
python ner_re_inference.py \
  --input_file sample_data/sample_input.txt \
  --ner_model_dir models/ner_model \
  --re_model_dir models/re_model
```
