# 🚨 Accident Detection System

A full-stack intelligent accident detection system that uses **YOLOv8** computer vision to analyze video footage, detect road accidents in real-time, and log incident reports to a cloud dashboard — with Firebase-backed authentication and Firestore storage.

---

## 📸 Overview

This system is built across three layers:

| Layer | Technology | Purpose |
|-------|-----------|---------|
| **Frontend** | React + Vite + MUI | Dashboard, live feed, incident viewer |
| **Backend** | Node.js + Express | API gateway, video upload, Firebase logging |
| **Detection Service** | Python + FastAPI + YOLOv8 | AI-powered accident analysis |

---

## 🏗️ Project Structure

```
Accidentdetection/
├── accident-frontend/          # React frontend (Vite)
│   ├── src/
│   │   ├── components/         # Navbar, LiveFeed, MapView, Stats, etc.
│   │   ├── pages/              # Dashboard, Incidents, Login, Signup, Stats
│   │   ├── firebase.js         # Firebase config
│   │   └── App.jsx             # Routing (protected routes)
│   └── package.json
│
├── accident-backend/           # Node.js backend
│   ├── index.js                # Express server (upload, analyze, Firestore)
│   ├── uploads/                # Temp video storage
│   └── detect-service/         # Python FastAPI microservice
│       ├── app.py              # YOLOv8 detection endpoint
│       ├── best.pt             # Trained YOLOv8 model weights
│       ├── detect.py           # Detection utilities
│       └── requirements.txt    # Python dependencies
```

---

## ✨ Features

- 🎥 **Video Upload & Analysis** — Upload CCTV/dashcam footage and detect accidents automatically
- 🤖 **YOLOv8 Detection** — Custom-trained object detection model for accident classification
- 📊 **Live Dashboard** — Real-time statistics, incident map, and recent alerts
- 🗺️ **Map View** — Geo-tagged incident locations
- 🔐 **Firebase Auth** — Secure login/signup with protected routes
- ☁️ **Firestore Logging** — All incidents stored with timestamp, confidence score, severity, and location
- 📸 **Auto Screenshot** — Captures a frame from the video when an accident is detected

---

## 🚀 Getting Started

### Prerequisites

- Node.js v18+
- Python 3.9+
- A Firebase project (Firestore + Authentication enabled)

---

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/iammuhammedyasir/Accidentdetection.git
cd Accidentdetection
```

---

### 2️⃣ Firebase Setup

1. Go to [Firebase Console](https://console.firebase.google.com/) and create a project
2. Enable **Firestore Database** and **Authentication** (Email/Password)
3. Download your **Service Account Key** (`serviceAccountKey.json`) from Project Settings → Service Accounts
4. Place it in `accident-backend/serviceAccountKey.json`
5. Copy your Firebase web config into `accident-frontend/src/firebase.js`

---

### 3️⃣ Start the Detection Service (Python/FastAPI)

```bash
cd accident-backend/detect-service

# Create a virtual environment (recommended)
python -m venv venv
source venv/bin/activate        # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Start the FastAPI server
uvicorn app:app --host 0.0.0.0 --port 8000 --reload
```

> The detection service will be available at `http://localhost:8000`

---

### 4️⃣ Start the Backend (Node.js)

```bash
cd accident-backend

# Install dependencies
npm install

# Start the server
node index.js
```

> The backend API will run on `http://localhost:5000`

---

### 5️⃣ Start the Frontend (React)

```bash
cd accident-frontend

# Install dependencies
npm install

# Start the development server
npm run dev
```

> The frontend will be available at `http://localhost:5173`

---

## 🔌 API Reference

### Node.js Backend (`localhost:5000`)

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/` | Health check |
| `GET` | `/api/incidents` | Fetch all incidents from Firestore |
| `POST` | `/api/analyze` | Upload a video and trigger detection |

### FastAPI Detection Service (`localhost:8000`)

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/analyze` | Receives video, runs YOLOv8, returns result |

**Sample Response from `/api/analyze`:**
```json
{
  "success": true,
  "result": {
    "timestamp": "2025-03-11T10:30:00Z",
    "accident_detected": true,
    "confidence": 0.91,
    "location": "Main Street Junction, Kochi",
    "severity": "Unknown",
    "status": "Reported",
    "screenshot_path": "screenshots/snap_1234567890.jpg"
  }
}
```

---

## 🧠 Model

The YOLOv8 model (`best.pt`) is a custom-trained object detection model for accident detection. To retrain or replace:

1. Prepare a labelled dataset (YOLO format)
2. Train using [Ultralytics YOLOv8](https://docs.ultralytics.com/)
3. Replace `best.pt` in `accident-backend/detect-service/`

---

## 🛠️ Tech Stack

**Frontend:** React 19, Vite, React Router v7, MUI v7, Tailwind CSS, Lucide Icons, Firebase

**Backend:** Node.js, Express v5, Multer, Axios, Firebase Admin SDK

**Detection:** Python, FastAPI, Ultralytics YOLOv8, OpenCV, PyTorch

**Database & Auth:** Firebase Firestore, Firebase Authentication

---

## ⚠️ Important Notes

- **Never commit** `serviceAccountKey.json` to version control — add it to `.gitignore`
- The `best.pt` model file may be large; consider using [Git LFS](https://git-lfs.github.com/) if needed
- The `location` field in the detection service is currently mocked — integrate a real geolocation API for production use

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).

---

## 👤 Author

**Muhammed Yasir**  
GitHub: [@iammuhammedyasir](https://github.com/iammuhammedyasir)
