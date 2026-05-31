# 🕳️ Pothole Detection

A lightweight image-based pothole detection pipeline built on color-feature extraction and a scikit-learn classifier. Designed as a modular AI component within the **Raksha AI** platform.

---

## 📁 Project Structure

```
pothole_detection/
├── model.py                    # Wrapper around the saved sklearn model
├── predict.py                  # CLI inference script for a single image
├── train.py                    # Training script using image-derived features
├── demo.py                     # End-to-end demo (train + score in one shot)
├── generate_sample_image.py    # Generates a sample PNG for quick testing
├── sample_training_data.csv    # Small synthetic dataset, ready to use
└── requirements.txt            # Python dependencies
```

---

## 🚀 Quick Start

### 1. Install dependencies

```bash
pip install -r requirements.txt
```

### 2. Generate a sample image and run inference

```bash
python generate_sample_image.py
python predict.py sample_image.png
```

### 3. Train a model on the sample dataset

```bash
python train.py sample_training_data.csv --output artifacts/sample_pothole_model.joblib
```

### 4. Run the full end-to-end demo

```bash
python demo.py
```

This trains a classifier from `sample_training_data.csv` and scores a sample feature vector in one step — no setup required.

---

## 🧠 How It Works

Images are represented as **color statistics** extracted from RGB channels. These six features are passed to a trained sklearn classifier to predict whether a road surface contains a pothole.

### Feature Schema

| Feature     | Description                        |
|-------------|------------------------------------|
| `mean_red`  | Mean red channel intensity         |
| `mean_green`| Mean green channel intensity       |
| `mean_blue` | Mean blue channel intensity        |
| `std_red`   | Std deviation of red channel       |
| `std_green` | Std deviation of green channel     |
| `std_blue`  | Std deviation of blue channel      |
| `label`     | `1` = pothole, `0` = no pothole    |

> **Note:** `label` is only required in the training CSV — not at inference time.

---

## 🔁 Running All AI Demos Together

From the **repository root**, run both the risk and pothole demos in sequence:

```bash
python ai-models/run_demos.py
```

---

## 📌 Notes & Limitations

- This pipeline uses **hand-crafted color features**, making it fast and dependency-light but less robust than deep learning approaches (e.g. YOLOv8, CNN).
- The included `sample_training_data.csv` is **synthetic** — for production use, replace it with real labeled road imagery.
- Model artifacts are saved as `.joblib` files under the `artifacts/` directory.

---

## 🗺️ Roadmap

- [ ] Replace color features with CNN embeddings or YOLOv8 detection
- [ ] Add support for video stream inference
- [ ] Integrate with Raksha AI geolocation reporting pipeline
- [ ] Severity classification (low / medium / high)

---

## 🤝 Part of Raksha AI

This module is one component of the broader [Raksha AI](https://github.com/IshanSirohi/raksha-ai) platform — an intelligent road safety system combining risk analysis, pothole detection, and real-time reporting.
