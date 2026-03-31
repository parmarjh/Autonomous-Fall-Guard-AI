# 🛡️ Autonomous Fall Guard AI (v2)

[![Status](https://img.shields.io/badge/Status-Active-brightgreen.svg)](https://github.com/[INSERT_USERNAME]/fall-detection-v2)
[![Language](https://img.shields.io/badge/Language-Python-blue.svg)](https://www.python.org/)
[![Framework](https://img.shields.io/badge/Framework-FastAPI-05998b.svg)](https://fastapi.tiangolo.com/)
[![Model](https://img.shields.io/badge/Model-YOLOv11-red.svg)](https://ultralytics.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**Autonomous Fall Guard AI** is a state-of-the-art, locally-hosted safety monitoring system. Leveraging the power of YOLOv11 and FastAPI, it provides real-time fall detection, automated emergency alerts, and a professional web-based command center.

---

## 📖 Table of Contents
- [Motivation](#-motivation)
- [Key Features](#-key-features)
- [How It Works (2D & 3D Image Base)](#-how-it-works-2d--3d-image-base)
- [Tech Stack](#-tech-stack)
- [Installation](#-installation)
- [Usage](#-usage)
- [Running Tests](#-running-tests)
- [Contributing](#-contributing)
- [License](#-license)

---

## 💡 Motivation
Falls among the elderly and vulnerable populations often go unnoticed for hours, leading to severe health complications. This project was built to provide an **autonomous, affordable, and privacy-focused solution** that runs on standard hardware, offering real-time protection and immediate communication with caregivers via automated alerts.

---

## ✨ Key Features
- **🚀 Real-Time Detection:** Powered by YOLOv11 for high-accuracy human detection and fall classification.
- **📧 Automated Email Alerts:** Sends instant snapshots of the detected fall to emergency contacts using Gmail SMTP.
- **🖥️ Modern Web Dashboard:** A glassmorphism-inspired UI for live monitoring and system status.
- **🔔 Interactive Alarm:** Audible 'Ring Type' alarm triggered directly on the dashboard during incidents.
- **📹 Low-Latency Streaming:** Optimized video feed via FastAPI `StreamingResponse`.
- **🛠️ Self-Optimizing:** Automatically selects the best available camera index (DSHOW support for Windows).

---

## 🧩 How It Works (2D & 3D Image Base)
The system employs a sophisticated detection engine that processes visual data through a multi-stage pipeline:

### 1. 2D Bounding Box Analysis
Standard video frames are processed to identify human figures. The engine monitors:
- **Aspect Ratio:** A sudden shift from a vertical (standing) to a horizontal (lying) ratio.
- **Centroid Displacement:** Tracking the movement of the person's center-point across frames.

### 2. Time-Based 3D Awareness
While the input is a 2D RGB stream, the system creates a "3D Spatial Context" by:
- **Depth Inference:** Using bounding box scale changes to estimate relative distance from the camera.
- **Temporal Analysis:** Analyzing the *velocity* of the person's descent over time (the 'T' axis of visual data), distinguishing a fall from simply sitting or lying down.
- **Pose Correlation:** Preparing for 3D skeleton mapping (compatible with pose-estimation models for fine-grained fall confirmation).

### 3. Automated Response
Once a fall is confirmed (threshold met), the logic triggers:
- Local hardware alarm (audio).
- Remote SMTP alert with an attached `.jpg` snapshot.
- Persistent logging in the dashboard activity feed.

---

## 🛠️ Tech Stack
- **AI Core:** [YOLOv11](https://docs.ultralytics.com/) (Ultralytics)
- **Backend:** [FastAPI](https://fastapi.tiangolo.com/) (Async Python)
- **Computer Vision:** [OpenCV](https://opencv.org/) (DSHOW Integration)
- **Templating:** [Jinja2](https://jinja.palletsprojects.com/)
- **Communication:** [SMTP](https://docs.python.org/3/library/smtplib.html) (MIME-based email)

---

## ⚙️ Installation

### Prerequisites
- Python 3.9+
- A compatible webcam
- (Optional) NVIDIA GPU with CUDA for faster inference

### Step-by-Step Setup
1. **Clone the Repo:**
   ```bash
   git clone https://github.com/[INSERT_USERNAME]/fall-detection-v2.git
   cd fall-detection-v2
   ```

2. **Install Dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Configure Gmail Credentials:**
   Open `app.py` and update the following placeholders:
   ```python
   GMAIL_SENDER    = "your-email@gmail.com"
   GMAIL_APP_PASS  = "your-app-password" # Obtain from Google Account settings
   ALERT_RECIPIENT = "recipient-email@gmail.com"
   ```

4. **Prepare the Model:**
   Ensure `yolo11n.pt` is in the root directory. It will automatically download on the first run if missing.

---

## 🚀 Usage

### Starting the Server
Run the FastAPI application:
```bash
python app.py
```

### Accessing the Dashboard
Open your browser and navigate to:
[http://127.0.0.1:8000](http://127.0.0.1:8000)

- **Live Feed:** Watch the real-time AI processing.
- **Alarm Controls:** Mute/Unmute the audible alarm.
- **Status API:** Check system health at `/status`.

---

## 🧪 Running Tests
To ensure system stability, run the automated test suite:
```bash
# Example using pytest
pytest tests/
```
*(Note: [INSERT details about your test coverage here])*

---

## 🤝 Contributing
Contributions are what make the open-source community an amazing place to learn, inspire, and create.
1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## ⚖️ License
Distributed under the **MIT License**. See `LICENSE` for more information.

---

## 📸 Screenshots/Visuals
*(Add your project GIFs or screenshots in the `docs/assets` folder and link them here)*

| Main Dashboard | Detection Alert |
| :---: | :---: |
| ![Dashboard Placeholder](https://via.placeholder.com/600x400?text=Dashboard+Mockup) | ![Alert Placeholder](https://via.placeholder.com/600x400?text=Detection+Visualization) |

---

> [!TIP]
> **Performance Note:** For optimal real-time performance on high-resolution cameras, it is recommended to run the system on a device with an NVIDIA GPU and `pytorch` with CUDA support.

---
Created with ❤️ by **Antigravity AI**
