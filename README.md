# 🍕 Pizza-or-Not-Pizza
[![Status: WIP](https://img.shields.io/badge/status-WIP-orange.svg)](https://github.com/willow788/Pizza-or-Not-Pizza)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](./LICENSE)
[![Python](https://img.shields.io/badge/python-3.8%2B-blue.svg)]()
[![Docker](https://img.shields.io/badge/docker-ready-blue.svg)]()
[![Made by willow788](https://img.shields.io/badge/author-willow788-9cf.svg)]()

---

Hero
----
![Pizza Banner](docs/images/banner.png)

A fast, playful, and production‑ready image classifier that answers one delightful question: "Is that pizza?" Use it for demos, moderation filters, chatbots, mobile apps, or just for fun.

Quick links
-----------
- Demo: (add demo URL)
- Model checkpoints: models/
- API docs: docs/api.md
- Issues & support: https://github.com/willow788/Pizza-or-Not-Pizza/issues

Why Pizza-or-Not-Pizza?
-----------------------
- Instant, human-friendly binary classification: pizza vs not-pizza.
- Lightweight models optimized for edge and mobile deployments.
- Clear, reproducible training pipeline and evaluation.
- Dockerized API and a tiny web UI for demos and integration.

Highlights
----------
- ⚡ Fast inference (EfficientNet/MobileNet variants)
- 🧪 Explainability (saliency / Grad-CAM heatmaps)
- 🐳 One-command Docker deployment
- ♻️ Easy to extend dataset and retrain
- ✅ Tests and CI-ready

Try it locally (2-min)
----------------------
```bash
# clone & enter
git clone https://github.com/willow788/Pizza-or-Not-Pizza.git
cd Pizza-or-Not-Pizza

# create environment (recommended)
python -m venv .venv
source .venv/bin/activate    # Windows: .venv\Scripts\activate

# install
pip install -r requirements.txt

# start API + demo
make start   # or: python app/main.py

# open http://localhost:8000
```

Live Demo & GIF
---------------
will update later
![Demo GIF](docs/images/demo.gif)

Usage examples
--------------

- Web UI  
  Upload an image in the browser and get an instant prediction, confidence score, and explanation heatmap.

- HTTP API
```bash
curl -X POST "http://localhost:8000/predict" \
  -F "file=@examples/pepperoni.jpg"
# -> {"prediction": "pizza", "confidence": 0.995, "explain_url": "/explain/uuid"}
```

- Python API
```python
from pizza_or_not_pizza import PizzaClassifier

clf = PizzaClassifier.from_pretrained("models/best_checkpoint.pth")
pred, score = clf.predict("examples/margherita.jpg")
print(pred, score)  # pizza 0.98
```

- CLI
```bash
python cli/predict.py --image examples/margherita.jpg
# Output: Prediction: PIZZA (0.98)
```

Model & dataset
---------------
- Default architectures: EfficientNet‑B0 (transfer learning) and lightweight MobileNet variants for mobile.
- Dataset: curated positive pizza images + diverse negative samples (other foods, plates, scenes).
- Augmentations: rotation, brightness, cropping, random erasing to improve robustness.

Training example
----------------
```bash
python train.py \
  --data data/ \
  --model efficientnet_b0 \
  --epochs 30 \
  --batch-size 32 \
  --lr 1e-4 \
  --output models/exp1
```

Evaluation & recommended thresholds
----------------------------------
We report:
- Accuracy
- Precision / Recall
- F1-score
- ROC AUC

Tips:
- For moderation/strict use-cases: use a higher confidence threshold (e.g., 0.95+).
- For recall-sensitive use-cases (find every pizza): lower threshold and post-filter.

Performance (example)
---------------------
- EfficientNet‑B0 (transfer): ~95% accuracy on held-out test (your mileage may vary)
- MobileNet small: ~92% accuracy, <50ms inference on average phone CPU

Project structure
-----------------
- app/            — FastAPI web app and demo UI  
- cli/            — Command‑line utilities  
- data/           — Dataset layout & ingestion scripts  
- docs/           — Documentation, images, diagrams  
- models/         — Saved checkpoints & export scripts  
- train.py        — Training entrypoint  
- predict.py      — Offline prediction utility  
- tests/          — Unit & integration tests  
- Dockerfile      — Containerize the API  
- requirements.txt

Deployment
----------
- Docker (one-line):  
  docker build -t pizza-or-not-pizza . && docker run -p 8000:8000 pizza-or-not-pizza
- Edge / Mobile: export to TFLite or ONNX and apply quantization for smaller size and faster inference.

Design & UX notes
-----------------
- UI shows top prediction + confidence with an overlay heatmap for explainability.
- Accessibility: colorblind-safe palettes and alt text for images.
- Minimal, responsive layout for mobile demo pages.

Contributing
------------
We welcome contributions of all kinds — code, datasets, UI improvements, and docs.

How to contribute:
1. Fork the repo
2. Create a branch: git checkout -b feat/your-feature
3. Add tests and documentation
4. Submit a PR and link related issues

Good first issues:
- Add more negative-sample categories (e.g., sandwiches, salads)
- Improve unit tests for prediction CLI
- Add mobile export and a sample integration

Code of conduct
---------------
This project follows the Contributor Covenant. Please be respectful and constructive.

Roadmap (short)
---------------
- [x] Core classifier + demo UI
- [ ] Better dataset coverage (international pizzas)
- [ ] Model quantization & mobile examples
- [ ] Hosted live demo & badges

Credits & acknowledgements
--------------------------
Built by willow788. Thanks to the open-source ML community and dataset contributors.

License
-------
MIT — see LICENSE.

Get in touch
------------
- Repo: https://github.com/willow788/Pizza-or-Not-Pizza  
- Issues: https://github.com/willow788/Pizza-or-Not-Pizza/issues  
- Maintainer: willow788

