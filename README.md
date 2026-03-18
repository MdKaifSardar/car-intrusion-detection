# 🛡️ Automotive Intrusion Detection System (AIDS)

[![Python](https://img.shields.io/badge/Python-3.12-blue.svg)](https://www.python.org/)
[![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-Latest-orange.svg)](https://scikit-learn.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)

A robust, multi-layer security framework for modern vehicles. This system combines **CAN Bus traffic analysis** with **Telematics anomaly detection** to provide a comprehensive defense-in-depth against cyber attacks.

---

## ⚡ Core Features

- **Real-world Data Integration**: Built and validated using the HCRL Car-Hacking Dataset.
- **Multi-Model Analysis**: Utilizes Random Forest for high-accuracy classification and Isolation Forest for unsupervised anomaly detection.
- **Telematics Behavioral Monitoring**: A secondary detection layer that monitors vehicle speed, RPM, and sensor data for secondary validation.
- **SOC Alert Engine**: Automatically converts mathematical anomalies into structured, human-readable security alerts (JSON & DataFrames).
- **Deployment Optimized**: Includes detailed analysis for Edge/Cloud hybrid architectures and resource-constrained ECU environments.

---

## 📊 Detection Pipeline

The system processes raw vehicle data through a sophisticated multi-stage pipeline:

```mermaid
graph TD
    A[Raw CAN Bus Traffic] --> B[Streaming Data Loader]
    B --> C[Feature Engineering]
    C --> D{Detection Layers}

    subgraph "Detection Logic"
    D --> D1[CAN IDS: Random Forest]
    D --> D2[Telematics: Isolation Forest]
    end

    D1 --> E[Multi-Layer Risk Fusion]
    D2 --> E

    E --> F[SOC Alert Generator]

    subgraph "Response Layer"
    F --> G[Structured JSON Alerts]
    F --> H[Actionable Dashboard Viz]
    end

    G --> I((SOC Analyst))
    H --> I
```

---

## 🛠️ Installation & Setup

1.  **Clone the Repository**:

    ```bash
    git clone https://github.com/your-username/car-intrusion.git
    cd car-intrusion
    ```

2.  **Download the Dataset**:
    - Place the HCRL CSV files (DoS, Fuzzy, Gear, RPM) in the `data/` folder.

3.  **Install Dependencies**:

    ```bash
    pip install pandas numpy scikit-learn matplotlib seaborn
    ```

4.  **Run the Analysis**:
    - Open `model.ipynb` in VS Code or Jupyter and execute all cells.

---

## 🚦 Alert Severity Engine

The SOC module classifies alerts based on the combined confidence of all detection layers:

| Severity      | Description                   | Recommended Action                        |
| :------------ | :---------------------------- | :---------------------------------------- |
| **🔴 HIGH**   | Confirmed multi-layer anomaly | Immediate investigation; Isolate ECU.     |
| **🟡 MEDIUM** | Single-layer trigger          | Monitor closely; Verify telemetry.        |
| **🔵 LOW**    | Minor signal irregularity     | Log for review; Check sensor calibration. |

---

## 📂 Project Structure

- `model.ipynb`: Core research and implementation notebook.
- `alerts.json`: Generated output for SIEM integration.
- `data/`: (Ignored) HCRL raw dataset folder.
- `.gitignore`: Optimized for large-scale ML project pushes.

---

_Project developed for Advanced Automotive Cybersecurity Research._
