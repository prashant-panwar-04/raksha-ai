# ⚠️ Risk Prediction

An explainable accident-risk scoring engine that combines geolocation, environmental, and traffic signals to produce a real-time risk score. Designed as a modular AI component within the **Raksha AI** platform.

---

## 📁 Project Structure

```
risk_prediction/
├── model.py                    # Explainable risk scoring module
├── predict.py                  # CLI for producing a risk score from input values
├── train.py                    # Optional training script for a tabular classifier
├── demo.py                     # End-to-end demo (train + predict in one shot)
├── sample_training_data.csv    # Small synthetic dataset, ready to use
└── requirements.txt            # Python dependencies for training and inference
```

---

## 🚀 Quick Start

### 1. Install dependencies

```bash
pip install -r requirements.txt
```

### 2. Run a risk prediction

```bash
python predict.py \
  --lat 28.61 \
  --lng 77.20 \
  --time peak \
  --weather rain \
  --road pothole \
  --traffic heavy \
  --zone "NH-48"
```

### 3. Train a model on the sample dataset

```bash
python train.py sample_training_data.csv --output artifacts/sample_risk_model.joblib
```

### 4. Run the full end-to-end demo

```bash
python demo.py
```

This trains a model from `sample_training_data.csv` and prints a risk prediction in one step — no setup required.

---

## 🧠 How It Works

The risk scorer evaluates a combination of **contextual signals** — location, time of day, weather, road condition, traffic density, and road zone — to output a risk score. The `model.py` module is designed to be **explainable**, meaning individual feature contributions can be surfaced alongside the final score.

### Input Features

| Feature          | Description                                         | Example Values                    |
|------------------|-----------------------------------------------------|-----------------------------------|
| `lat`            | Latitude of the location                            | `28.61`                           |
| `lng`            | Longitude of the location                           | `77.20`                           |
| `time_of_day`    | Traffic period                                      | `peak`, `off-peak`, `night`       |
| `weather`        | Current weather condition                           | `rain`, `fog`, `clear`            |
| `road_condition` | Surface state of the road                           | `pothole`, `wet`, `good`          |
| `traffic_level`  | Congestion level                                    | `heavy`, `moderate`, `light`      |
| `zone`           | Road/highway identifier                             | `NH-48`, `urban`, `rural`         |
| `label`          | Risk class — **training only** (`1` = high risk, `0` = low risk) | `0`, `1`          |

> **Note:** `label` is only required in the training CSV — not at inference time.

---

## 🏋️ Training on Custom Data

Prepare a CSV with the columns listed in the table above, then run:

```bash
python train.py path/to/training_data.csv --output artifacts/my_risk_model.joblib
```

Trained model artifacts are saved as `.joblib` files under the `artifacts/` directory.

---

## 🔁 Running All AI Demos Together

From the **repository root**, run both the risk and pothole demos in sequence:

```bash
python ai-models/run_demos.py
```

---

## 📌 Notes & Limitations

- The included `sample_training_data.csv` is **synthetic** — for production use, replace it with real labeled incident data sourced from traffic authorities or field sensors.
- The current feature set is **tabular and rule-adjacent**; integrating real-time traffic APIs or weather feeds would substantially improve accuracy.
- Model artifacts are saved as `.joblib` files and loaded automatically by `predict.py` at inference time.

---

## 🗺️ Roadmap

- [ ] Integrate live weather and traffic APIs as feature sources
- [ ] Add per-feature risk contribution breakdown in prediction output
- [ ] Support batch prediction from a CSV of locations
- [ ] Expose a REST endpoint for integration with the Raksha mobile app
- [ ] Time-series risk trend analysis per zone

---

## 🤝 Part of Raksha AI

This module is one component of the broader [Raksha AI](https://github.com/IshanSirohi/raksha-ai) platform — an intelligent road safety system combining risk analysis, pothole detection, and real-time reporting.
