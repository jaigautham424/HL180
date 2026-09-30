# KANKANI — Multimodal Industrial Quality Intelligence Platform

## 🚀 Start the Platform

### Frontend (Next.js)
```powershell
cd d:\HL180\kankani
npm run dev
# Open: http://localhost:3000
```

### Backend (FastAPI + Ultralytics YOLO)
```powershell
cd d:\HL180\kankani\backend
py -m pip install -r requirements.txt
py server.py
# API: http://localhost:8000
# Docs: http://localhost:8000/docs
```

---

## Connect Your YOLO Model

1. Open **Model Center**: http://localhost:3000/app/model-center
2. Click **+ REGISTER MODEL**
3. Enter: version name, architecture (e.g. `yolo11n`), absolute `.pt` path
4. Click **REGISTER** — class names auto-extracted from the model
5. Click **APPROVE** then **DEPLOY**
6. Model is now live for inspection

---

## Connect Your Dataset

1. Open **Dataset Center**: http://localhost:3000/app/dataset-center
2. Click **+ REGISTER DATASET**
3. Point to your dataset root (where `data.yaml` lives)
4. Click **VALIDATE** to check images/labels/yaml

Required YOLO structure:
```
dataset/
├── images/train/  val/  test/
├── labels/train/  val/  test/
└── data.yaml
```

---

## Run Training

1. Go to **Training**: http://localhost:3000/app/training
2. Select dataset, architecture, epochs, device
3. Click **START TRAINING** — live epoch/mAP metrics stream in real time
4. After: Model Center → Approve → Deploy

---

## Run Live Inspection

1. Deploy a model in Model Center
2. Go to **Live Inspection**: http://localhost:3000/app/live-inspection
3. Upload a product image
4. Click **RUN INSPECTION**
5. Real YOLO inference runs — bounding boxes appear on detected defects
6. Fusion engine evaluates all evidence — decision recorded to database

---

## Platform Pages

| Page | URL | Purpose |
|---|---|---|
| Landing | / | Freeflow 12-frame inspection story |
| Control Center | /app/control-center | System status, model, metrics |
| Live Inspection | /app/live-inspection | Real YOLO inference workstation |
| Production Line | /app/production-line | Conveyor & station visualization |
| Batch Inspection | /app/batch-inspection | Multi-image batch processing |
| Defect Analysis | /app/defect-analysis | Defect intelligence workspace |
| Thermal Intel | /app/thermal | Thermal heatmap workspace |
| Records | /app/records | Inspection record database |
| Analytics | /app/analytics | Quality KPIs |
| Model Center | /app/model-center | Lifecycle: Train→Approve→Deploy |
| Dataset Center | /app/dataset-center | Dataset registration & validation |
| Training | /app/training | YOLO training pipeline |
| Config | /app/config | Product & process engineering specs |
| System | /app/system | Hardware & service status |

---

## Key Architecture

```
Frontend (Next.js :3000)
    ↓
Backend (FastAPI :8000)
    ↓
Ultralytics YOLO (real inference)
    ↓
Multimodal Fusion Engine
    ↓
Quality Decision (PASS/REJECT/HOLD/REWORK/HUMAN_REVIEW)
    ↓
SQLite Database (inspection records)
```

---

## API Reference

Full interactive docs: http://localhost:8000/docs

Key endpoints:
- `POST /api/inspection/live` — run single inspection
- `POST /api/inspection/batch` — batch inspection
- `GET  /api/records` — inspection history
- `GET  /api/analytics/summary` — quality KPIs
- `POST /api/training` — start training run
- `POST /api/models/{id}/deploy` — deploy model
- `POST /api/datasets/{id}/validate` — validate dataset
- `GET  /api/system/status` — platform status
