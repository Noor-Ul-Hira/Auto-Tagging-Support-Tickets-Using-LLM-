# Auto-Tagging-Support-Tickets-Using-LLM-


## Problem Statement
Automatically classify support tickets into predefined categories using a large language model (LLM).  
The goal is to reduce manual effort in tagging support tickets and to explore how different approaches — zero-shot, few-shot, and fine-tuned models — perform on the same dataset.

## Objective
- Automatically tag free-text support tickets into categories.
- Compare **zero-shot, few-shot, and fine-tuned LLM** approaches.
- Output **top 3 most probable categories** per ticket.

## Dataset
- **Banking77**: Free-text support ticket dataset containing 77 categories.  
- For this task, we selected **8 important categories**:
  - card_arrival
  - card_payment_wrong_exchange_rate
  - cash_withdrawal_charge
  - chargeback
  - card_payment_fee_charged
  - transfer_failed
  - passcode_forgotten
  - request_refund

## Skills Gained
- Prompt engineering for zero-shot and few-shot learning
- LLM-based text classification
- Multi-class prediction and ranking
- Fine-tuning transformer models (DistilBERT) for domain-specific tasks

## Methodology / Approach

### Step 1: Dataset Loading & Preprocessing
- Load dataset using Hugging Face `datasets` library.
- Convert to pandas DataFrame for filtering and sampling.
- Map label names to numeric IDs for model compatibility.
- Filter dataset to selected categories and sample 300 tickets for experimentation.

### Step 2: Zero-Shot Classification
- Use **Facebook BART large MNLI** model.
- Predict ticket categories without training (multi-label support disabled).
- Evaluate using **accuracy score**.
- Output top 3 predicted labels per ticket.

### Step 3: Few-Shot Classification
- Use **FLAN-T5 small** model with a prompt containing 5–6 examples.
- Convert generated text into predicted category.
- Evaluate accuracy and compare with zero-shot performance.

### Step 4: Fine-Tuning
- Split filtered dataset into **train (80%) and test (20%)** sets.
- Tokenize text using `AutoTokenizer` (DistilBERT).
- Convert data to Hugging Face `Dataset` format with `labels`.
- Fine-tune **DistilBERT** model for multi-class classification over 3 epochs.
- Evaluate using accuracy against test set.

### Step 5: Evaluation & Output
- Compare **zero-shot, few-shot, and fine-tuned model accuracies**.
- Display top-3 predictions for each ticket (from zero-shot model).
- Summarize findings and insights.

## Key Results / Observations
1. **Zero-Shot Classification**
   - Provides reasonable predictions without any training.
   - Accuracy lower than fine-tuned model due to domain-specific context.

2. **Few-Shot Classification**
   - Slightly improves over zero-shot when examples in the prompt are informative.
   - Useful when dataset is small or fine-tuning is not feasible.

3. **Fine-Tuned Model (DistilBERT)**
   - Achieves the **highest accuracy** among all approaches.
   - Learns domain-specific patterns and terminology.
   - Requires labeled dataset and training time.

4. **Top-3 Predictions**
   - Zero-shot model outputs top-3 labels per ticket, helpful in cases of ambiguity.
   - Provides a ranked list for potential automation or human-in-the-loop review.

## Insights & Conclusion
- Fine-tuning transformer models is the most reliable approach for domain-specific ticket classification.
- Zero-shot and few-shot learning are useful when labeled data is scarce or for rapid prototyping.
- Combining LLM outputs (top-3 predictions) with human review can reduce manual effort while maintaining accuracy.
- The task demonstrates practical use of LLMs in **support automation, prompt engineering, and multi-class text classification**.


