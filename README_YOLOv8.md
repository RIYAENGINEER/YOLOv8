# 🧠 Website Element Detection using YOLOv8

This project uses **Ultralytics YOLOv8** to train, validate, and test an object detection model that recognizes key visual elements on website screenshots — such as buttons, text fields, images, labels, and links.

The dataset was sourced and prepared via **Roboflow**, formatted for YOLOv8, and trained using **Google Colab**.

---

## 📂 Project Structure
```
├── YOLOV8.ipynb                 # Jupyter notebook (training, validation & inference)
├── custom_dataset.yaml           # Dataset config file
├── runs/                         # Training and validation output folders
├── ultralytics/Website-Screenshots-1/
│   ├── train/
│   │   ├── images/
│   │   └── labels/
│   ├── valid/
│   └── test/
└── README.md
```

---

## 🎯 Objective
Detect and classify 8 types of website UI elements:
```
['button', 'field', 'heading', 'iframe', 'image', 'label', 'link', 'text']
```

---

## ⚙️ Setup & Installation

### 1️⃣ Clone the repository
```bash
git clone https://github.com/RIYAENGINEER/YOLOv8.git
cd YOLOv8
```

### 2️⃣ Install dependencies
Use the official Ultralytics package:
```bash
pip install -U ultralytics
```

or install from source:
```bash
pip install -e ./ultralytics
```

### 3️⃣ Verify installation
```bash
yolo version
```

---

## 📘 Dataset Configuration
`custom_dataset.yaml`
```yaml
train: /content/yolov5/image_data/train/images
val:   /content/yolov5/image_data/valid/images
test:  /content/yolov5/image_data/test/images

nc: 8
names: ['button', 'field', 'heading', 'iframe', 'image', 'label', 'link', 'text']
```

---

## 🚀 Training
Run YOLOv8 training:
```bash
yolo task=detect mode=train model=yolov8s.pt data=custom_dataset.yaml epochs=50 imgsz=640 batch=16
```

or inside Python:
```python
from ultralytics import YOLO

model = YOLO("yolov8s.pt")
model.train(data="custom_dataset.yaml", epochs=50, imgsz=640, batch=16)
```

---

## ✅ Validation
To evaluate model performance:
```bash
yolo task=detect mode=val model=runs/train/exp/weights/best.pt data=custom_dataset.yaml imgsz=640
```

or in Python:
```python
metrics = model.val(data="custom_dataset.yaml", imgsz=640)
print(metrics)
```

---

## 🔍 Inference / Detection
Predict on images or folders:
```bash
yolo task=detect mode=predict model=runs/train/exp/weights/best.pt      source=/path/to/image_or_folder imgsz=640 save=True
```

Example (single image):
```python
results = model.predict(source="image_data/train/images/sample.jpg", imgsz=640, save=True)
```

Predicted images will be saved in:
```
runs/detect/exp/
```

---

## 📊 Results
- **Best Model:** `runs/train/exp/weights/best.pt`
- **Validation Metrics:**
  - mAP50: ~0.XX
  - Precision: ~0.XX
  - Recall: ~0.XX
- **Example Predictions:**
  - `runs/detect/exp_yolov8/`

---

## 💡 Future Improvements
- Add data augmentation and hyperparameter tuning.
- Test YOLOv8n / YOLOv8m for performance-speed tradeoff.
- Deploy model as a Streamlit web demo or REST API.

---

## 🧑‍💻 Author
**Priyadharshini Muruganantham**  
🔗 [LinkedIn](https://www.linkedin.com/in/priyadharshinimuruganantham)  
💼 GitHub: [RIYAENGINEER](https://github.com/RIYAENGINEER)

---

## 📜 License
This project is open-source under the [MIT License](LICENSE).
