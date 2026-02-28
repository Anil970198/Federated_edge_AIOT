# Privacy-Preserving AIoT: Federated Learning for Arrhythmia Detection

## 📌 Overview
This repository contains a **Privacy-Preserving Artificial Intelligence of Things (AIoT)** simulation built for smart healthcare applications. The project uses **Federated Learning** to train a global Convolutional Neural Network (CNN) across multiple decentralized edge devices (e.g., smartwatches, health monitors) to detect cardiac arrhythmias, without ever transmitting raw patient telemetry to a central cloud.

## 🏗️ Architecture Stack
* **Federated Engine:** [Flower (flwr)](https://flower.dev/)
* **Deep Learning Framework:** PyTorch
* **IoT Simulation:** Ray (Virtual Client Engine)
* **Dataset:** MIT-BIH Arrhythmia Database

## ⚙️ System Design
1. **The Global Server:** Orchestrates the training process and uses the `FedAvg` (Federated Averaging) strategy to aggregate model weights. It intercepts and saves the final global weights to disk.
2. **The Edge Nodes:** 5 simulated IoT clients. Each client holds a strictly private, local partition of the ECG dataset and never shares it.
3. **The AI Model:** A lightweight 1D-CNN designed to be computationally efficient for resource-constrained edge devices (TinyML).

## 🚀 Results (5 Communication Rounds)
The system generalized and converged beautifully by only securely sharing learned gradients:
* **Round 1 Global Accuracy:** 90.34%
* **Round 5 Global Accuracy:** 96.16%

![Federated Learning Results](federated_AIOT.png.png)
*(Please upload the saved matplotlib graph image to this repository and name it `federated_training_results.png` to display here)*

## 📡 Authentic Real-Time Edge Inference
To prove the end-to-end pipeline, the system simulates an Edge Device downloading the final authentic `global_model.npz` weights from the server and performing real-time inference on new patient signals:

```text
============================================================
🏥 AUTHENTIC IoT EDGE INFERENCE DASHBOARD 🏥
============================================================

📡 Transmitting Patient Signal #03485 from Edge Device...
[✅] Prediction: Normal Beat
    ↳ Model Diagnosis: CORRECT

📡 Transmitting Patient Signal #19794 from Edge Device...
[🚨] ALERT TRIGGERED: Premature Ventricular Contraction detected!
    ↳ Model Diagnosis: CORRECT

📡 Transmitting Patient Signal #18733 from Edge Device...
[❓] ALERT TRIGGERED: Unclassifiable / Paced beat detected!
    ↳ Model Diagnosis: INCORRECT (Actual: Premature Ventricular Contraction)
```

## 🧠 Why This Matters (Erasmus Mundus Context)
As IoT networks expand, sending highly sensitive telemetry (like medical ECGs) to centralized cloud servers poses massive privacy and bandwidth risks. This project demonstrates a mathematically sound, distributed systems approach to **Edge AI**, proving that robust machine learning can occur strictly at the edge while simultaneously building a collaborative global model.
