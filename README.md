## Industrial Data Analytics Project

### Project Title: **Predictive Maintenance in CNC Milling Machines**

---

### Overview

Tool wear in machining processes critically impacts product quality, production efficiency, and operational costs. This project focuses on developing a predictive model to estimate **flank wear (VB)** in cutting tools using sensor data and machining parameters. The system enables proactive maintenance, reducing downtime and preventing excessive tool wear, ultimately enhancing manufacturing efficiency.

---

### Dataset Description

The dataset provides operational insights from a CNC milling machine under **16 different operating conditions**. Each condition represents a unique combination of **depth of cut (DOC), feed rate, and material type**, with multiple runs containing **9000 sensor readings** per case. 

- **Features:**
  - Operating conditions: Time, Depth of Cut, Feed Rate, Material Type
  - Sensor data: 
    - `smcDC` (Spindle Motor Current)
    - `vib_spindle` (Spindle Vibration Data)
- **Target Variable:**
  - Flank wear (VB)

---

### Objective

To develop a predictive model capable of:
1. Accurately estimating flank wear (VB).
2. Identifying optimal parameter configurations for minimizing wear.
3. Enhancing operational efficiency and reducing tool failure.

---

### Data Processing Workflow

1. **Preprocessing:**
   - Missing data removed.
   - Features standardized using `StandardScaler`.
   - Signal processing techniques applied:
     - **Rectification**: Converting values to absolute for uniform analysis.
     - **Low-pass filtering**: Removing high-frequency noise.
     - **Smoothing**: Applying a moving average for a cleaner signal.
![WhatsApp Image 2024-11-18 at 20 16 22_38f843db](https://github.com/user-attachments/assets/5ec73e5a-9449-4412-87e3-2833c2c39131)
2. **Feature Engineering:**
   - **Operating Conditions:** Weighted higher (1.5x) for critical importance.
   - **Frequency-Domain Features:** Using FFT to capture periodic patterns.
   - **Time-Domain Features:** Extracting statistical measures (mean, standard deviation, RMS).
   - **Dimensionality Reduction:** Recursive Feature Elimination (RFE) to identify top 10 features.
![WhatsApp Image 2024-11-18 at 20 45 19_3cd17cf0](https://github.com/user-attachments/assets/b8a8564c-4c67-4f4f-b639-cde21828b561)

---

### Model Architectures

#### **Model 1: XGBoost Regressor**
- Gradient-boosted decision trees for regression.
- Hyperparameter tuning via `RandomizedSearchCV`.
- 5-fold cross-validation with RMSE as the evaluation metric.
- **RMSE:** 0.10

#### **Model 2: Hybrid Neural Network + XGBoost**
- Feature extraction using:
  - Dense layers for operating conditions.
  - FFT and time-domain features for sensor data.
  - Conv1D for temporal patterns.
- Features fed into XGBoost for regression.
- **RMSE:** 0.0751

#### **Model 3: Multi-Branch Neural Network**
- Branches for:
  - Dense layers (operating conditions).
  - FFT (frequency-domain features).
  - Time-domain features.
  - Conv1D layers (sensor data).
- Concatenated outputs for regression.
- **RMSE:**  0.0719

---

### Evaluation Metrics

- **Root Mean Squared Error (RMSE):**
  - Model 1: **0.10**
  - Model 2: **0.0751**
  - Model 3: **0.0719** 
- **Visualization:** Predicted vs. Actual line plots highlight model accuracy and consistency.
![image](https://github.com/user-attachments/assets/ab1b56fb-413d-44b4-a18b-ca86e288f0e5)

---

### Future Scope

1. Enhance adaptation to time-dependent and condition-specific patterns.
2. Include additional features for better handling of machining variability.
3. Optimize operational efficiency by further reducing tool failure rates.

---

### Team Members
- **Varad S. Pendse**
- **Tejas Bhavekar**

--- 

### Acknowledgment
This project was completed as part of the **ME-217 Industrial Data Analytics** course.
