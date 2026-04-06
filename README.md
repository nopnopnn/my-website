# ESD-Predictor: An Online Early Warning and Evaluation System for Electrostatic Discharge Parameters

## 1. Project Overview

**ESD-Predictor** is a lightweight, Browser/Server (B/S) architecture-based online early warning and evaluation tool for Electrostatic Discharge (ESD) parameters. This system is designed to bridge the gap between underlying algorithmic research and practical Electromagnetic Compatibility (EMC) engineering applications by encapsulating complex feature extraction pipelines and high-dimensional predictive models in a localized web service.

Users simply upload raw dynamic discharge current waveform files (in CSV format) via the front-end interface. The server automatically executes early truncation, denoising, multi-dimensional feature extraction, and tensor reconstruction. Utilizing built-in machine learning and deep temporal networks, the system achieves high-precision proactive prediction of the "Peak Current" and "Rise Rate" during the very early stages of the discharge event.

## 2. Core Features

* **Multi-Modal Algorithm Matrix**
  The system integrates multiple hyperparameter-optimized predictive models to meet varying computational and accuracy requirements:
  * **Traditional Machine Learning Baselines:** Support Vector Machine (SVM), Random Forest (RF).
  * **End-to-End Deep Temporal Networks:** 1D Convolutional Neural Network (1D-CNN), Long Short-Term Memory (LSTM).
* **Flexible Data Preprocessing Manifolds**
  Provides two industry-standard data normalization scaling options:
  * `StandardScaler` (Z-score Normalization): Optimizes gradient propagation for deep neural networks.
  * `MinMaxScaler`: Adapts to shallow geometric margin models.
* **Rigorous Anti-Leakage Feature Pipeline**
  During feature tensor reconstruction, the server strictly strips global extreme values. It extracts only 10 core statistical and morphological features (including mean, standard deviation, skewness, kurtosis, RMS, fitted trend slope, spectral dominant frequency, and spectral centroid) from the truncated leading edge of the waveform, ensuring the physical rigor of the early warning mechanism.
* **High-Concurrency Asynchronous Processing & Visualization**
  Supports concurrent batch uploading of multiple waveform files. The front-end utilizes the Fetch API to intercept submission events, enabling non-blocking asynchronous requests and JSON data parsing. Prediction results (including feature comparisons and predicted extremes) are rendered in real-time within a Data Grid without requiring a page refresh.

## 3. Technology Stack

The system adopts a front-end and back-end separation design, ensuring cross-platform deployment flexibility and scalability:

### Backend (Server-Side)
* **Core Framework:** `Flask` (Python)
* **Scientific Computing & Feature Extraction:** `NumPy`, `Pandas`, `SciPy` (FFT domain analysis and statistical features)
* **Model Deserialization & Inference Engine:**
  * `scikit-learn` / `joblib` (Loading `.pkl` weights for traditional machine learning)
  * `TensorFlow` / `Keras` (Loading `.h5` computational graph models for deep learning)

### Frontend (Client-Side)
* **Page Structure & Styling:** `HTML5`, `Bootstrap 5` (Responsive UI and card-based layout)
* **Interactive Logic:** Native `JavaScript` (Dynamic DOM rendering and AJAX asynchronous communication)

## 4. Installation & Usage Guide

This tool is designed to be run as a local web service. Please follow the instructions below to configure the environment and start the application.

### 4.1 Local Environment Setup

1. **Download the Repository:** Clone the project from GitHub (or download the ZIP file and extract it).
   ```bash
   git clone <your-github-repo-url>
   cd <repository-folder-name>
