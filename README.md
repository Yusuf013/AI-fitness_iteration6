# AI Fitness Exercise Recognition (PyTorch → ONNX → Flutter)

Dit project bevat een AI-model dat fitnessoefeningen herkent op basis van één afbeelding.  
Het model is getraind met PyTorch (ResNet-18) en geëxporteerd naar het ONNX-formaat voor gebruik in een Flutter mobiele applicatie.

De mobiele app kan hiermee volledig **on-device** (zonder internet) voorspellingen doen, wat goed is voor privacy en prestaties.

---

## Functionaliteit

Het model herkent de volgende oefeningen:

- cable_flyes
- incline_benchpress
- machine_pulldown
- pullup
- romanian_deadlift
- squats

Op basis van een foto geeft de app:

- de naam van de oefening
- (optioneel) aanvullende informatie zoals spiergroepen en uitvoeringstips

---

## Model

- Architectuur: ResNet-18 (pretrained)
- Framework: PyTorch + PyTorch Lightning
- Input: RGB afbeelding 224×224
- Output: klasse-index (0–5)

---

## Projectstructuur (globaal)

/dataset
/data
/inference

/notebooks
training_notebook.ipynb
export_to_onnx.ipynb

/model.pth
/fitness_resnet18.onnx

/flutter_app

yaml
Code kopiëren

---

## Python omgevingen

Dit project gebruikt **twee aparte Python-omgevingen**. Dit is bewust gedaan om stabiliteit en reproduceerbaarheid te garanderen.

### 1. Training environment

Gebruikt voor:

- dataset laden
- model trainen
- evaluatie
- opslaan van `model.pth`

**Python versie:** 3.14

#### Setup

```bash
python -m venv train-env
train-env\Scripts\activate
pip install -r requirements-training.txt
2. Export environment (ONNX)
Gebruikt voor:

laden van model.pth

exporteren naar fitness_resnet18.onnx

Python versie: 3.10
(ONNX Runtime ondersteunt Python 3.14 momenteel niet op Windows)

Setup
bash
Code kopiëren
py -3.10 -m venv onnx-env
onnx-env\Scripts\activate
pip install -r requirements-export.txt
Dependencies
requirements-training.txt
txt
Code kopiëren
torch
torchvision
pytorch-lightning
torchmetrics
matplotlib
pandas
numpy
requirements-export.txt
txt
Code kopiëren
torch
torchvision
onnx
onnxruntime
onnxscript
numpy
ONNX export proces
Laad het PyTorch model (model.pth)

Strip Lightning prefix (model.)

Bouw ResNet-18 opnieuw

Exporteer naar ONNX:

Output:

Code kopiëren
fitness_resnet18.onnx
Deze file wordt gebruikt in de Flutter app.

Flutter integratie (samenvatting)
Plaats het model in:

bash
Code kopiëren
assets/models/fitness_resnet18.onnx
Voeg toe aan pubspec.yaml

Installeer dependency:

bash
Code kopiëren
flutter pub add onnxruntime
Preprocessing in de app:

resize → 224×224

RGB → float (0–1)

tensor shape → [1, 3, 224, 224] (CHW)

Output index → map naar class name:

dart
Code kopiëren
const classes = [
  'cable_flyes',
  'incline_benchpress',
  'machine_pulldown',
  'pullup',
  'romanian_deadlift',
  'squats',
];
Belangrijk
De preprocessing in Flutter moet exact gelijk zijn aan de preprocessing tijdens training.

De ONNX export moet worden uitgevoerd met Python 3.10.

Training notebooks mogen Python 3.14 blijven gebruiken.

Bekende beperkingen
Model herkent slechts 6 oefeningen

Werkt op basis van één frame (geen video)

Geen pose-validatie (alleen classificatie)

Toekomstige verbeteringen
Meer oefeningen toevoegen

Pose estimation integreren

Confidence thresholding

Model quantization voor kleinere bestanden

Real-time video ondersteuning
```
