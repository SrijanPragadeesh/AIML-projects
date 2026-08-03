# Real-Time Context-Aware Text Classification & Live Stream Routing

An automated message routing system that classifies unstructured, high-velocity
customer feedback and routes each message to the right team in real time — with
priority scoring layered on top of the raw category, not just a static lookup table.

## Overview

Customer support teams receive feedback through many channels at high volume.
Manually reading and forwarding every message to the right department is slow and
error-prone. This project builds an end-to-end pipeline that:

1. Learns a language representation of incoming feedback text.
2. Classifies each message into one of five categories.
3. Scores **priority** using both the category and the urgency language in the
   message itself (context-aware, not just a fixed rule per category).
4. Simulates a **live stream** of incoming messages, classifying and routing each
   one the instant it "arrives," then reports a routing dashboard.

## Dataset

`customer_feedback.csv` — 1,000 customer feedback messages, evenly split across five
categories (200 each), with no missing values:

| Category | Routed To |
|---|---|
| Billing | Finance Team |
| Delivery | Logistics Team |
| Product | Quality Assurance Team |
| Technical Support | IT Support Team |
| General Inquiry | Customer Care Team |

## Pipeline

### 1. Data exploration
Class balance check, message length distribution, and per-category word clouds to
understand the vocabulary that separates each category.

### 2. Text preprocessing
Light normalization only — lowercasing and whitespace/punctuation cleanup — since the
feedback is already short, clean natural language. Heavy stemming or stopword removal
would strip out useful signal like negations ("not working") or order IDs.

### 3. Feature engineering
**TF-IDF** over unigrams + bigrams (instead of a raw word-count vectorizer). TF-IDF
down-weights common words and up-weights category-distinctive ones, and bigrams
capture short phrases ("payment failed", "not working") instead of isolated words.

### 4. Model training & comparison
Three classifiers are trained on the same TF-IDF features and compared with 5-fold
cross-validation:

| Model | Notes |
|---|---|
| Multinomial Naive Bayes | Fast, strong baseline for text |
| Logistic Regression | Linear, well-calibrated probabilities |
| Linear SVM (calibrated) | Wrapped in `CalibratedClassifierCV` for confidence scores |

The best-performing model is selected automatically by macro F1 score.

### 5. Evaluation
Accuracy, precision/recall/F1 per class, and a confusion matrix heatmap.

### 6. Context-aware priority layer
Category alone doesn't tell you how urgent a message is. Priority is computed as:

- **Base priority by category** — `Billing` and `Technical Support` start higher than
  `General Inquiry`.
- **Urgency escalation** — messages containing urgency/frustration language ("urgent",
  "immediately", "unacceptable", "charged twice", "still not"...) get bumped up one
  priority level, capped at `Critical`.
- **Confidence fallback** — if the model isn't confident about the category (max
  predicted probability below a threshold), the message is routed to a **manual
  triage queue** instead of being auto-assigned, so low-confidence guesses never get
  silently mis-routed.

### 7. Live stream simulation
A shuffled batch of held-out test messages (plus a few hand-written urgent examples)
is fed through the routing function one at a time with simulated arrival latency —
the same pattern a real consumer reading off a message queue (Kafka / RabbitMQ /
Kinesis) would run continuously in production. Each message prints its classification,
confidence, priority, and destination team as it "arrives."

### 8. Live dashboard
After the stream finishes, two summary charts show message volume per team and per
priority level.

### 9. Model persistence
The fitted TF-IDF + classifier pipeline is saved with `joblib` so it can be loaded by
a real streaming consumer without retraining.

## Results

The best model reached **100% test accuracy**. This is expected rather than a red
flag: the feedback messages are short, templated, and highly category-distinctive
(e.g. delivery complaints and billing complaints use almost entirely non-overlapping
vocabulary), so a linear/Naive Bayes model over TF-IDF features separates them
perfectly. The interesting behavior to look at isn't the accuracy number — it's the
stream simulation, where an ambiguous, low-confidence message is correctly deferred
to manual review instead of being force-classified.

## Tech Stack

- Python, pandas, NumPy
- scikit-learn (TF-IDF, Naive Bayes, Logistic Regression, Linear SVM, model selection & metrics)
- matplotlib, seaborn, wordcloud (visualization)
- joblib (model persistence)

## Project Structure

```
.
├── ML_TASK_4_solution.ipynb     # Full pipeline: EDA -> training -> routing -> stream simulation
├── customer_feedback.csv        # Dataset (1,000 labeled feedback messages)
├── feedback_router_model.joblib # Saved trained pipeline (TF-IDF + classifier)
└── README.md
```

## How to Run

```bash
pip install pandas numpy scikit-learn matplotlib seaborn wordcloud joblib
jupyter notebook ML_TASK_4_solution.ipynb
```

Run all cells top to bottom. The last classification cell accepts live input so you
can test your own feedback message and see it classified and routed on the spot.

To reuse the trained model without retraining:

```python
import joblib
model = joblib.load("feedback_router_model.joblib")
model.predict(["My payment failed and I was charged twice"])
```

## Future Improvements

- Swap TF-IDF for sentence embeddings (e.g. `sentence-transformers`) if feedback text
  becomes more varied or informal.
- Add a feedback loop where manually-triaged "Uncertain" messages are relabeled and
  used to periodically retrain the model.
- Connect `route_message()` to an actual message broker (Kafka/RabbitMQ) instead of
  the in-notebook simulation.

## Author

**Samrabinson P**
