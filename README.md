# DriveGuard — Student Edition

DriveGuard is a Computer Vision project focused on driver monitoring. It leverages **YOLOv8** and **MediaPipe** to detect risky driving behaviors such as drowsiness, distraction, and phone use in real-time.

Designed as a modern full-stack application, the project features a Python/FastAPI backend and a Vue.js frontend, orchestrated via Docker.

## 1. Features

* **Drowsiness Detection**: Uses Eye Aspect Ratio (EAR) to detect prolonged eye closure.
* **Yawn Detection**: Uses Mouth Aspect Ratio (MAR) to detect fatigue.
* **Distraction Detection**: Tracks head pitch and yaw to ensure the driver's eyes are on the road.
* **Phone Usage**: Utilizes a YOLOv8 object detection model to identify cell phone usage.
* **Risk Scoring**: Evaluates the session dynamically and assigns a normalized risk score (0-100).
* **Web Dashboard**: View live sessions, session history, and detailed analytics.

## 2. Architecture Overview

* **Computer Vision Engine**: Python-based pipeline utilizing OpenCV, MediaPipe (Face Mesh), and YOLOv8 (Object Detection).
* **Backend API**: FastAPI application connected to an SQLite database via SQLAlchemy, managing jobs and persisting session results.
* **Frontend**: Vue.js Single Page Application (SPA) providing an interactive operations dashboard.
* **Deployment**: Configured via Docker Compose for easy evaluation and scaling.

## 3. Getting Started

### Prerequisites

* Python 3.10+
* Node.js 18+ (for frontend development)
* Docker & Docker Compose (optional, but recommended for full-stack deployment)
* Standard webcam (for live monitoring)

### Installation (Local Development)

#### 1. Clone the Repository

```bash
git clone https://github.com/AmeyaShukla503/Cv24bai10495driveguard.git
cd DriveGuard
```

#### 2. Set Up Python Environment

```bash
python -m venv venv
```

Activate the virtual environment:

**Windows:**

```bash
venv\Scripts\activate
```

**macOS/Linux:**

```bash
source venv/bin/activate
```

Install the required Python packages:

```bash
pip install -r requirements.txt
```

#### 3. Database Setup

DriveGuard defaults to SQLite for easy local setup, but can be configured for PostgreSQL via `config.yaml`.

#### 4. Start the Backend

```bash
uvicorn backend.app.main:app --reload --port 8000
```

#### 5. Start the Frontend

Open another terminal:

```bash
cd frontend
npm install
npm run dev
```

Navigate to:

```text
http://localhost:5173
```

to access the dashboard.

## 4. Testing

To run the test suite for the computer vision pipeline and backend API:

```bash
pytest
```

Make sure the Python virtual environment is activated before running the tests.

## 5. Running via CLI

DriveGuard provides a headless CLI for rapid video analysis without starting the web dashboard.

### Analyze a Pre-recorded Video

```bash
python main.py run samples/demo.mp4
```

### Run Live Analysis via Webcam

```bash
python main.py run 0
```

## 6. Docker Deployment

To launch the entire stack (FastAPI Backend, Vue Frontend, and SQLite Database) using Docker:

```bash
docker compose up --build
```

Access the application at:

```text
http://localhost:5173
```

## 7. Project Structure

```text
DriveGuard/
│
├── cv_engine/       # Core algorithms
│   ├── YOLO
│   ├── MediaPipe
│   ├── Tracking
│   └── Risk Scoring
│
├── backend/         # FastAPI server and database
│
├── frontend/        # Vue 3 application
│
├── models/          # YOLOv8 and MediaPipe model files
│
├── docs/            # Architecture, UML diagrams, and reports
│
├── tests/           # Pytest test suite
│
├── config.yaml      # Application configuration
├── requirements.txt # Python dependencies
└── README.md        # Project documentation
```

## 8. Configuration

Behavior thresholds, scoring weights, and infrastructure endpoints are managed through `config.yaml`.

Refer to `.env.example` for overriding sensitive environment variables.

## 9. License

This project is licensed under the **MIT License**.
