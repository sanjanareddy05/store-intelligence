# Store Intelligence

End-to-end Store Intelligence system for offline retail analytics using CCTV footage, YOLOv8, FastAPI, PostgreSQL, Docker, and real-time analytics.

This project converts raw CCTV footage into structured behavioural events and exposes real-time store intelligence metrics through a production-style API.

---

# Features

* CCTV person detection using YOLOv8
* Visitor tracking and session handling
* Entry / Exit detection
* Re-entry detection
* Zone-based visitor analytics
* Dwell-time tracking
* Billing queue detection
* Real-time Store Intelligence API
* Heatmap and funnel analytics
* Health monitoring
* Dockerized deployment
* Live dashboard for real-time metrics
* Automated testing with coverage

---

# System Architecture

Raw CCTV Footage

↓

Detection Pipeline (YOLOv8 + Tracking)

↓

Structured Event Stream (`events.jsonl`)

↓

FastAPI + PostgreSQL Intelligence API

↓

Real-Time Metrics Dashboard

---

# Tech Stack

* Python
* YOLOv8 (Ultralytics)
* OpenCV
* ByteTrack
* FastAPI
* PostgreSQL
* Docker Compose
* Pytest
* Rich (Terminal Dashboard)

---

# Project Structure

```text
store-intelligence/
│
├── app/
│   ├── main.py
│   ├── analytics.py
│   ├── db.py
│   ├── models.py
│   └── schemas.py
│
├── pipeline/
│   ├── detect.py
│   ├── tracker.py
│   ├── emit.py
│   ├── replay_events.py
│   └── output/
│
├── dashboard/
│   └── live_dashboard.py
│
├── tests/
│   └── test_api.py
│
├── docs/
│   ├── DESIGN.md
│   └── CHOICES.md
│
├── docker-compose.yml
├── requirements.txt
├── pytest.ini
└── README.md
```

---

# Dataset Note

Raw CCTV clips are NOT included in this repository due to challenge licensing restrictions and repository size limitations.

Place the challenge CCTV videos inside:

```text
data/videos/
```

Expected format:

```text
data/videos/CAM 1.mp4
data/videos/CAM 2.mp4
data/videos/CAM 3.mp4
data/videos/CAM 4.mp4
data/videos/CAM 5.mp4
```

---

# Setup Instructions

## 1. Clone Repository

```bash
git clone <repository-url>

cd store-intelligence
```

---

## 2. Start API + PostgreSQL

```bash
docker compose up --build
```

This starts:

* FastAPI backend
* PostgreSQL database

Swagger documentation becomes available at:

```text
http://localhost:8000/docs
```

---

## 3. Add CCTV Videos

Place challenge videos inside:

```text
data/videos/
```

---

## 4. Run Detection Pipeline

Generate behavioural events from CCTV footage:

```bash
python pipeline/detect.py
```

This creates:

```text
pipeline/output/events.jsonl
```

Generated events include:

* ENTRY
* EXIT
* REENTRY
* ZONE_ENTER
* ZONE_DWELL
* BILLING_QUEUE_JOIN

---

## 5. Replay Events into API

Replay generated events into the Store Intelligence API:

```bash
python pipeline/replay_events.py
```

This populates analytics data in PostgreSQL.

---

## 6. Open API Documentation

Swagger/OpenAPI documentation:

```text
http://localhost:8000/docs
```

Available endpoints:

### Health

```text
GET /health
```

Returns:

* service health
* database connectivity
* timestamp

### Event Ingestion

```text
POST /events/ingest
```

Ingest behavioural events.

### Metrics

```text
GET /stores/{store_id}/metrics
```

Returns:

* unique visitors
* conversion rate
* queue depth
* dwell analytics
* abandonment rate

### Funnel

```text
GET /stores/{store_id}/funnel
```

Returns visitor funnel analytics.

### Heatmap

```text
GET /stores/{store_id}/heatmap
```

Returns zone-level activity.

### Anomalies

```text
GET /stores/{store_id}/anomalies
```

Returns operational anomalies.

---

# Live Dashboard

Run:

```bash
python dashboard/live_dashboard.py
```

Dashboard displays:

* Unique Visitors
* Conversion Rate
* Queue Depth
* Abandonment Rate

Metrics update in near real time while events are replayed.

---

# Running Tests

Run tests:

```bash
pytest
```

Run coverage:

```bash
pytest --cov=app
```

Expected:

* API tests passing
* > 70% coverage

Current project coverage:

```text
96%
```

---

# Example Flow

1. Start API

```bash
docker compose up --build
```

2. Run detection

```bash
python pipeline/detect.py
```

3. Replay events

```bash
python pipeline/replay_events.py
```

4. View API

```text
http://localhost:8000/docs
```

5. Run dashboard

```bash
python dashboard/live_dashboard.py
```

---

# AI Usage

AI tools were used to accelerate implementation, architecture exploration, testing, and debugging.

Generated outputs were reviewed, modified, validated, and tested manually during implementation.

See:

* `docs/DESIGN.md`
* `docs/CHOICES.md`

for details about AI-assisted engineering decisions.

---

# License

Challenge use only.

Dataset ownership and licensing remain with the challenge provider and are not redistributed in this repository.
