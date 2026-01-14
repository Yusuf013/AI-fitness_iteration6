# AI Fitness Exercise Recognition (PyTorch → ONNX → Flutter)

Dit project bevat een AI-model dat fitnessoefeningen herkent op basis van één afbeelding.  
Het model is getraind met PyTorch (ResNet-18) en geëxporteerd naar ONNX voor gebruik in een Flutter mobiele app.

De app voert herkenning volledig **on-device** uit (zonder internet).

---

## Herkende oefeningen

- cable_flyes  
- incline_benchpress  
- machine_pulldown  
- pullup  
- romanian_deadlift  
- squats  

---

## Model

- Architectuur: ResNet-18 (pretrained)
- Input: 224×224 RGB afbeelding
- Output: oefeningsklasse (0–5)

---

## Python omgevingen

Dit project gebruikt twee Python-versies:

### Training
- Python 3.14  
- Voor model training en evaluatie

### Export naar ONNX
- Python 3.10  
- Nodig vanwege ONNX Runtime compatibiliteit

---

## Dependencies

### Training
torch
torchvision
pytorch-lightning
torchmetrics
matplotlib
pandas
numpy

shell
Code kopiëren

### Export
torch
torchvision
onnx
onnxruntime
onnxscript
numpy

yaml
Code kopiëren

---

## Export pipeline

PyTorch (.pth) → ONNX (.onnx) → Flutter app

yaml
Code kopiëren

Het ONNX-bestand `fitness_resnet18.onnx` wordt direct in de app geladen.

---

## Flutter integratie (kort)

- Model in `assets/models/fitness_resnet18.onnx`
- Dependency: `onnxruntime`
- Preprocessing:
  - resize → 224×224
  - pixelwaarden → 0–1 floats
  - tensor shape → [1, 3, 224, 224]

---
