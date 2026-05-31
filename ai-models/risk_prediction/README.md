## Project Structure

```text
risk_prediction/
├── model.py                   # Explainable risk scoring module
├── predict.py                 # CLI for producing a risk score from input values
├── train.py                   # Optional training script for a tabular classifier
├── demo.py                    # End-to-end demo (train + predict in one shot)
├── sample_training_data.csv   # Small synthetic dataset, ready to use
└── requirements.txt           # Python dependencies
```

---

## Quick Start

**1. Install dependencies**

```bash
pip install -r requirements.txt
```

**2. Run a risk prediction**

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

**3. Train a model on the sample dataset**

```bash
python train.py sample_training_data.csv --output artifacts/sample_risk_model.joblib
```

**4. Run the full end-to-end demo**

```bash
python demo.py
```

Trains a model from `sample_training_data.csv` and prints a risk prediction in one step — no setup required.

---

## How It Works

The risk scorer evaluates a combination of contextual signals — location, time of day, weather, road condition, traffic density, and road zone — to output a risk score. The `model.py` module is designed to be **explainable**, meaning individual feature contributions can be surfaced alongside the final score.

### Input Features

| Feature          | Description                                      | Example Values               |
|------------------|--------------------------------------------------|------------------------------|
| `lat`            | Latitude of the location                         | `28.61`                      |
| `lng`            | Longitude of the location                        | `77.20`                      |
| `time_of_day`    | Traffic period                                   | `peak`, `off-peak`, `night`  |
| `weather`        | Current weather condition                        | `rain`, `fog`, `clear`       |
| `road_condition` | Surface state of the road                        | `pothole`, `wet`, `good`     |
| `traffic_level`  | Congestion level                                 | `heavy`, `moderate`, `light` |
| `zone`           | Road/highway identifier                          | `NH-48`, `urban`, `rural`    |
| `label`          | `1` = high risk, `0` = low risk (training only)  | `0`, `1`                     |

> `label` is only required in the training CSV — not at inference time.

---

## Training on Custom Data

Prepare a CSV with the columns listed above, then run:

```bash
python train.py path/to/training_data.csv --output artifacts/my_risk_model.joblib
```

---

## Run Both AI Demos Together

From the repository root:

```bash
python ai-models/run_demos.py
```

Launches the risk prediction and pothole detection demos in sequence.

---

## Notes & Limitations

- `sample_training_data.csv` is **synthetic** — replace with real labelled incident data for production use.
- The current feature set is tabular; integrating real-time weather or traffic APIs would substantially improve accuracy.
- Trained model artifacts are saved as `.joblib` files under `artifacts/`.

---

## Roadmap

- [ ] Integrate live weather and traffic APIs as feature sources
- [ ] Add per-feature risk contribution breakdown in prediction output
- [ ] Support batch prediction from a CSV of locations
- [ ] Expose a REST endpoint for integration 
