# Acceleration Reconstruction via Numerical Integration

## Project Overview

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

## Reconstruction Methodology

This project employs a physics-based approach to reconstruct kinematic motion from noisy sensor data. The analysis proceeds in sequential steps: signal smoothing followed by double numerical integration.

### 1. Signal Smoothing
Raw accelerometer data often contains high-frequency noise. To reduce this noise while preserving the shape and height of acceleration peaks, we apply a **Savitzky-Golay filter**.


For each data point $a_i$, the filter fits a polynomial $P(t)$ of order $k$ to a symmetric window of $2M+1$ neighboring points using the method of least squares. The smoothed value is the polynomial evaluated at the central point:

$$
a_i = P(t_i)
$$

### 2. Velocity Reconstruction
Velocity is derived by integrating the smoothed acceleration function over time. This requires an initial velocity constant $v_0$ (velocity at $t=0$):

$$
v(t) = v_0 + \int_{0}^{t} a(\tau) \, d\tau
$$


### 3. Displacement Reconstruction
Displacement is derived by integrating the calculated velocity function over time. This requires an initial position constant $x_0$ (position at $t=0$):

$$
x(t) = x_0 + \int_{0}^{t} v(\tau) \, d\tau
$$


### 4. Discrete Numerical Approximation
Since the sensor data is discrete with a sampling interval $\Delta t$, we approximate the continuous integrals using the **Cumulative Trapezoidal Rule**. This method estimates the area under the curve by dividing it into trapezoids. For the $n$-th data point:

$$
v_n \approx v_{n-1} + \frac{a_{n-1} + a_n}{2} \cdot \Delta t
$$


---

## Getting Started

### Prerequisites
* Python 3.8+
* Jupyter Notebook

### Installation

1.  **Clone the repository** (or download the files):
    ```bash
    git clone https://github.com/mattia-3rne/acceleration-reconstruction-via-numerical-integration.git
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

## Project Structure

* `acceleration_data.csv`: The raw data exported from the Phyphox app.
* `main.ipynb`: The main analysis notebook.
* `requirements.txt`: Python package dependencies.
* `README.md`: Project documentation.
