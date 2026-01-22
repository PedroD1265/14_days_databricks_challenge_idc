# Day 14 — AI-Powered Analytics: Genie & Mosaic AI

## Focus
- Natural language → SQL exploration with **Databricks Genie**
- Intro to **Mosaic AI / GenAI workflows**
- Simple NLP task (sentiment analysis) + logging results to **MLflow**
- Turning “AI outputs” into something trackable (params/metrics/artifacts)

---

## What I Used (My Setup)
- **Workspace:** Databricks (Serverless)
- **Data source:** Unity Catalog tables created earlier (`ecommerce.*`)
- **Experiment tracking:** MLflow (workspace experiment under my user)
- **NLP approach:** Hugging Face Transformers `pipeline("sentiment-analysis")`
- **Notes:** Initially hit a missing dependency (`transformers`), then ran successfully after the environment had the package available and downloaded the default sentiment model.

---

## Tasks Completed (Checklist)
- [x] Attempted NLP sentiment analysis with Transformers
- [x] Resolved missing dependency issue (`ModuleNotFoundError: transformers`)
- [x] Ran sentiment inference on sample reviews
- [x] Logged an MLflow run with parameters + a simple metric derived from the predictions
- [x] Confirmed the model download/inference ran on CPU in Serverless

---

## What Happened (Step-by-step)

### 1) Initial error: `ModuleNotFoundError: No module named 'transformers'`
- Meaning: the Python environment running your notebook **didn’t have** the Transformers library installed/available at that moment.
- Why it matters: `pipeline(...)` is part of the `transformers` package, so the import fails immediately.

### 2) Second run: model downloaded + inference succeeded
- The notebook output shows:
  - It **defaulted** to `distilbert-base-uncased-finetuned-sst-2-english` (the default sentiment model for that pipeline if you don’t specify one).
  - It downloaded files like `config.json`, `model.safetensors`, tokenizer files, etc.
  - “Device set to use cpu” → it ran on CPU (normal in many serverless setups unless GPU is enabled).

### 3) MLflow logging
- You used `mlflow.start_run(...)` and logged:
  - **Params** like task/model
  - A simple **metric** such as number of positives
- This is the key “MLOps habit”: every experiment is reproducible and comparable later.

---

## Quick Validation (Recommended)
To be 100% sure everything is correct, run these quick checks in the notebook:

- Confirm you got **2 predictions** (one per review):
  - `len(results)`
- Print the full results clearly:
  - `for r in results: print(r)`

Expected output: 2 dictionaries (likely one POSITIVE and one NEGATIVE, given the example reviews).

---

## Evidence
- Notebook: `day_14_AI_poweredanalytics.ipynb`
- MLflow:
  - 1 run created for sentiment baseline (params + metric logged)
- Output:
  - Transformers pipeline ran and returned sentiment predictions
  - Model artifacts downloaded in the session (seen in notebook output)

---

## Notes / Improvements for “Production-like” Quality
- Specify the model explicitly to avoid defaults:
  - e.g., `pipeline("sentiment-analysis", model="distilbert-base-uncased-finetuned-sst-2-english")`
- Log richer metrics:
  - `positives`, `negatives`, average confidence, etc.
- (Optional) Log the raw prediction output as an MLflow artifact (JSON) for traceability.
