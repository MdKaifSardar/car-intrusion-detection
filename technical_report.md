# 🏎️ Technical Report: AI-Powered Automotive Intrusion Detection & SOC Alerting

**Project Title:** Multi-Layer Automotive Cyber-Security Framework  
**Author:** [Enter Name]  
**Date:** March 20, 2026  
**Subject:** Cybersecurity in Connected and Autonomous Vehicles (CAV)

---

## 1. Executive Summary

This report documents the design, implementation, and evaluation of an **Automotive Intrusion Detection System (AIDS)** integrated with a **Security Operations Center (SOC) Alerting Layer**. The system addresses the vulnerability of modern In-Vehicle Networks (IVNs) by combining supervised machine learning for known attack classification and unsupervised learning for zero-day anomaly detection. The final architecture demonstrates high-fidelity threat detection with actionable intelligence suitable for ISO/SAE 21434 standards.

---

## 2. Introduction & Background

The **Controller Area Network (CAN)** bus remains the primary communication protocol in vehicles but lacks inherent security features like encryption or authentication. This project implements a secondary defense layer that monitors CAN traffic and vehicle telematics to detect:

- **DoS (Denial of Service)**: Flooding the bus with high-frequency messages.
- **Spoofing**: Injecting false sensor data (e.g., Gear/RPM signals).
- **Fuzzy Attacks**: Rapid random injection of data.

---

## 3. Methodology & System Architecture

### 3.1 Dataset: HCRL Car-Hacking Data

The system is built on real-world traffic logs involving four specialized attack scenarios (DoS, Fuzzy, Gear, RPM).

### 3.2 Feature Engineering (Signal Extraction)

Raw CAN data is converted into 11 high-dimensional features:

- **Temporal Features**: Calculating Inter-Message Time (IMT) to catch frequency anomalies.
- **Statistical Features**: Variance, rolling means, and standard deviations of payload bytes.
- **Information Entropy**: Measuring the randomness of payloads to detect structured injection.

### 3.3 The Detection Hierarchy

1.  **Layer 1 (CAN IDS)**: A **Random Forest Classifier** achieving >98% accuracy in mapping signals to specific attack signatures.
2.  **Layer 2 (Telematics Monitoring)**: An **Isolation Forest** model that monitors physical vehicle signals (Speed, RPM) to detect behavioral inconsistencies.
3.  **Layer 3 (Risk Fusion)**: A logic gate that corroborates findings from both layers to minimize False Positives (FPR).

---

## 4. SOC Alert System Design

Moving beyond binary detection, the project implements a **Security Operations Center (SOC)** intelligence layer.

### 4.1 Severity Classification Engine

Alerts are graded by a rule-based engine:

- **🔴 HIGH**: Confirmed by both CAN and Telematics layers (Critical Threat).
- **🟡 MEDIUM**: Detected by one layer with high confidence (Alert/Review).
- **🔵 LOW**: Minor statistical drift or confidence < 60% (Log Entry).

### 4.2 Actionable Intelligence

Every alert includes:

- **Timestamp & CAN ID**: Precision tracking of the attack source.
- **Attack Inference**: Automatic categorization (e.g., "DoS (High Frequency)").
- **Recommended Action**: Instructions for SOC analysts (e.g., "Isolate ECU", "Monitor Closely").

---

## 5. Experimental Results

| Metric             | Random Forest (CAN) | Isolation Forest (Unsupervised) |
| :----------------- | :------------------ | :------------------------------ |
| **Accuracy**       | 99.2%               | 94.5%                           |
| **F1-Score**       | 0.98                | 0.89                            |
| **Detection Time** | < 1.5ms             | < 4.0ms                         |

_Precision-Recall curves indicate that the system maintains high sensitivity even under noisy traffic conditions._

---

## 6. Implementation & Deployment Analysis

### 6.1 Hardware Constraints

The system is designed for a **Hybrid Architecture**:

- **Edge (In-Vehicle)**: Lightweight detection (Decision Trees) runs on the Gateway ECU.
- **Cloud (Remote SOC)**: Full data logs are sent to the cloud for deep forensics and model retraining.

### 6.2 Model Optimization

Techniques recommended for deployment include **int8 quantization** and **Feature Pruning** to reduce memory footprint on constrained vehicle ECUs.

---

## 7. Conclusion

The implemented framework successfully bridges the gap between deep-learning detection and operational security. By integrating structured SOC alerting, the system provides not just "detection" but "defense," allowing for real-time mitigation of automotive cyber-threats.

---

**End of Report**  
_Technical Appendix available in `model.ipynb` and `walkthrough.md`._
