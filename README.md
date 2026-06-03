# Plant Disease Detection

[![GitHub stars](https://img.shields.io/github/stars/your-repo.svg)](https://github.com/your-username/Plant-Disease-Detection)  
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

## 📖 Overview

**Plant Disease Detection** is a lightweight web application built with **Flask** and **TensorFlow** that identifies diseases in various plant leaves (Mango, Brinjal, Onion, Guava, Papaya, etc.) from uploaded images. It provides:
- A **prediction API** powered by a pre‑trained MobileNetV2 model.
- Detailed disease information, prevention steps, and recommended supplements.
- A simple UI for end‑users and a market page for browsing supplements.

The repository contains the model, label mapping, CSV data for diseases and supplements, and example images.

---

## ✨ Features

- **Image‑based disease classification** using a MobileNetV2 backbone.
- **Dynamic disease details** fetched from `disease_info.csv`.
- **Supplement recommendations** from `supplement_info.csv`.
- **Responsive UI** built with Jinja2 templates.
- **Docker / Gunicorn ready** for production deployment.

---

## 🗂️ Repository Structure

```
Plant-Disease-Detection-main/
├── app/                     # Flask application source
│   ├── app.py               # Main entry point
│   ├── CNN.py               # Optional CNN model definition (unused in Flask app)
│   ├── requirements.txt     # Python dependencies
│   ├── disease_info.csv      # Disease descriptions & images
│   ├── supplement_info.csv    # Supplement recommendations
│   ├── static/               # CSS, JS, uploaded images, demo images
│   └── templates/           # HTML Jinja2 templates
│       ├── home.html
│       ├── index.html
│       ├── submit.html
│       └── market.html
├── Model/                  # Pre‑trained TensorFlow model
│   ├── keras_model.h5
│   └── labels.txt           # Class label list
├── demo_images/            # Sample leaf images for quick testing
├── test_images/            # Additional images used during development
├── Procfile                # Heroku / Railway entry point (gunicorn)
└── README.md               # **THIS FILE**
```

---

## 📦 Installation

1. **Clone the repo**
   ```bash
   git clone https://github.com/your-username/Plant-Disease-Detection.git
   cd Plant-Disease-Detection
   ```
2. **Create a virtual environment** (optional but recommended)
   ```bash
   python -m venv .venv
   source .venv/Scripts/activate   # Windows PowerShell
   # or
   .venv\Scripts\activate.bat    # Command Prompt
   ```
3. **Install dependencies**
   ```bash
   pip install -r app/requirements.txt
   ```
4. **Verify the model files** – the `Model/` folder already contains `keras_model.h5` and `labels.txt`. No extra download is required.

---

## 🚀 Running the Application

### Development (debug) mode
```bash
python app/app.py
```
Visit `http://127.0.0.1:5000` in your browser.

### Production (Gunicorn)
```bash
gunicorn --bind 0.0.0.0:8000 app.app:app
```
You can also use the provided `Procfile` with platforms such as Heroku, Railway, or Fly.io.

---

## 📡 API Endpoints
| Route | Method | Description |
|------|--------|-------------|
| `/` | GET | Home page – description of the project |
| `/index` | GET | UI for uploading a leaf image |
| `/submit` | POST | Handles image upload, runs prediction, and returns disease details & supplement suggestions |
| `/market` | GET | Shows a searchable list of all supplements |

The core prediction logic lives in `app/app.py` – the function `prediction(image_path: str) -> int` loads the image, preprocesses it, runs the TensorFlow model, and returns the class index.

---

## 🖼️ Demo

Upload an image on the **Upload** page. After submitting, you’ll see:
- Predicted disease name
- Description and prevention steps
- Recommended supplement(s) with buy‑links
- A gallery of alternative supplements

*Feel free to replace the placeholder screenshots below with actual screenshots of your running app.*

![Home page](https://raw.githubusercontent.com/your-username/Plant-Disease-Detection/main/demo_images/home.png)
![Result page](https://raw.githubusercontent.com/your-username/Plant-Disease-Detection/main/demo_images/result.png)

---

## 📚 Dataset & Model Details

- **Model**: MobileNetV2 (alpha = 0.35, no pretrained weights) fine‑tuned on a custom leaf‑disease dataset. The model file (`keras_model.h5`) is ~2.4 MB.
- **Labels**: Stored in `Model/labels.txt` – one label per line.
- **Disease metadata** (`disease_info.csv`): Columns include `disease_name`, `description`, `Possible Steps`, `image_url`.
- **Supplement metadata** (`supplement_info.csv`): Contains `supplement name`, `supplement image`, `buy link`.

Feel free to replace the model with a newer architecture – just update `MODEL_PATH` and adjust the number of classes.

---

## 🤝 Contributing

1. Fork the repository.
2. Create a feature branch (`git checkout -b feature/awesome-feature`).
3. Make your changes and add tests if applicable.
4. Submit a Pull Request with a clear description of the changes.

Please follow the existing code style (PEP 8) and keep the documentation updated.

---

## 📄 License

This project is licensed under the **MIT License** – see the `LICENSE` file for details.

---

## ⭐️ Acknowledgements

- **TensorFlow** and **Flask** teams for the excellent libraries.
- The open‑source community for providing datasets and model checkpoints.
- Icons made by **Freepik** from **www.flaticon.com**.

---

*Happy planting and happy coding!*
