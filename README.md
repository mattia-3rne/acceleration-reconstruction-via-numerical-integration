# Acceleration Reconstruction via Numerical Integration

## 📊 Project Overview

The goal is to reconstruct the velocity and position profiles of a moving object based on raw acceleration data collected via Phyphox. This involves double numerical integration of the accelerometer signal and applying a smoothing algorithm due to sensor noise.
### The Variables
Since this involves integrating time-series data, we track the kinematic state evolution.

| Variable | Symbol | Unit | Description                      |
| :--- | :--- | :--- |:---------------------------------|
| **Time** | **$t$** | $s$ | The timestamp of the sensor recording. |
| **Acceleration** | **$a(t)$** | $m/s^2$ | Raw input data from Phyphox accelerometer. |
| **Velocity** | **$v(t)$** | $m/s$ | First integral of acceleration.  |
| **Position** | **$x(t)$** | $m$ | Second integral of acceleration. |
---

## 🚀 Getting Started

### Prerequisites
* Python 3.8+
* Jupyter Notebook

### Installation

1.  **Clone the repository** (or download the files):
    ```bash
    git clone https://github.com/mattia-3rne/Acceleration-Reconstruction.git
    ```

2.  **Install dependencies**:
    This project requires `numpy`, `pandas`, `matplotlib`, and `scipy`.
    ```bash
    pip install -r requirements.txt
    ```

### Running the Analysis

1.  Start Jupyter Notebook:
    ```bash
    jupyter notebook
    ```

2.  Open the main notebook file (`main.ipynb`).

3.  **Run All Cells**:
    The notebook is self-contained. It will:
    * Load the raw `.csv` data exported from Phyphox.
    * Apply smoothing filter to raw data
    * Perform numerical integration.
    * Plot the final reconstructed paths.

---

## 📂 Project Structure

* `Acceleration_Reconstruction.ipynb`: The main analysis notebook.
* `acceleration_data.csv`: The raw data exported from the Phyphox app.
* `requirements.txt`: Python package dependencies.
* `README.md`: Project documentation.
