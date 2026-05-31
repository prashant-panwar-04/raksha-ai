# Pothole Detection

A lightweight image-based pothole detection pipeline built on colour-feature extraction and a scikit-learn classifier. Part of the **Raksha AI** platform.

---

## Project Structure

```text
pothole_detection/
├── model.py                   # Wrapper around the saved sklearn model
├── predict.py                 # CLI inference script for a single image
├── train.py                   # Training script using image-derived features
├── demo.py                    # End-to-end demo (train + score in one shot)
├── generate_sample_image.py   # Generates a sample PNG for quick testing
├── sample_training_data.csv   # Small synthetic dataset, ready to use
└── requirements.txt           # Python dependencies
```

---

## Quick Start

**1. Install dependencies**

```bash
pip install -r requirements.txt
```

**2. Generate a sample image and run inference**

```bash
python generate_sample_image.py
python predict.py sample_image.png
```

**3. Train a model on the sample dataset**

```bash
python train.py sample_training_data.csv --output artifacts/sample_pothole_model.joblib
```

**4. Run the full end-to-end demo**

```bash
python demo.py
```

Trains a classifier from `sample_training_data.csv` and scores a sample feature vector in one step — no setup required.

---

## How It Works

Images are represented as **colour statistics** extracted from RGB channels. These six features are fed into a trained sklearn classifier to predict whether a road surface contains a pothole.

### Training Data Schema

| Feature      | Description                         |
|--------------|-------------------------------------|
| `mean_red`   | Mean red channel intensity          |
| `mean_green` | Mean green channel intensity        |
| `mean_blue`  | Mean blue channel intensity         |
| `std_red`    | Standard deviation of red channel   |
| `std_green`  | Standard deviation of green channel |
| `std_blue`   | Standard deviation of blue channel  |
| `label`      | `1` = pothole, `0` = no pothole     |

> `label` is only required in the training CSV — not at inference time.

---

## Run Both AI Demos Together

From the repository root:

```bash
python ai-models/run_demos.py
```

Launches the risk prediction and pothole detection demos in sequence.

---

## Notes & Limitations

- Uses **hand-crafted colour features** — fast and dependency-light, but less robust than deep learning approaches (e.g. YOLOv8, CNNs).
- `sample_training_data.csv` is **synthetic** — replace with real labelled road imagery for production use.
- Trained model artifacts are saved as `.joblib` files under `artifacts/`.

---

## Roadmap

- [ ] Replace colour features with CNN embeddings or YOLOv8 detection
- [ ] Add video stream inference support
- [ ] Integrate with Raksha AI geolocation reporting pipeline
- [ ] Add severity classification (low / medium / high)

---

## Part of Raksha AI

This module is one component of the [Raksha AI](https://github.com/IshanSirohi/raksha-ai) platform — an intelligent road safety system combining risk analysis, pothole detection, and real-time reporting.
