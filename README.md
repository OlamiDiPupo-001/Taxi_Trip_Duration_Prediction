# 🚕 AI-Driven Taxi Trip Duration Prediction

**Course:** Introduction to Artificial Intelligence

**Topic:** Regression Analysis for Urban Mobility  

**Developer:** Azeez Oladipupo Akinlade -> 151486, Haithem Ladj -> 156006

---

## 01 — Introduction: The Driver’s Perspective

### 🎯 The Goal
The objective of this project is to build a high-precision **regression model** that predicts the total travel time of a taxi trip in **New York City**.  
By analyzing **GPS coordinates, timestamps, and passenger data**, the system estimates how many seconds a trip will last **before the vehicle even starts moving**.

---

### 💡 Personal Motivation
This project goes beyond academics. Alongside studies, Azeez also work as a **part-time taxi driver in Poznań**. Whether navigating rush-hour traffic near **Most Teatralny** or driving toward **Stary Rynek**, one metric matters most: **ETA (Estimated Time of Arrival)**.

In the taxi industry, **time is money**. Accurate duration prediction helps:

- **Drivers:**  
  Better shift planning and smarter decisions about accepting long or short trips.
- **Passengers:**  
  Reduced uncertainty and stress during congested traffic.
- **Platforms:**  
  Smarter dispatching—assigning the closest driver in *time*, not just distance.

---
## 📂 **Repository Structure**


```
Taxi_Trip_Duration_Prediction/
│
├── run_demo/                              # Demo applications
│   ├── run_demo.py                        # python file to run demo
│   └── run_demo.ipynb                     # notebook file
│
├── src/                                   # Project Files
│   ├── ai_taxi_duration_prediction.ipynb  # EDA, Feature Engineering, Model Training & Tuning (notebook)
│   └── ai_taxi_duration_prediction.py     # python file
│
├── taxi_duration_model_test/              # Model and testing 
│   ├── taxi_duration_model.pkl/           # Trained model file
│   └── taxi_test_data.zip/                # Test data file
│
├── Images/                                # Images from model training and validation 
│
└── README.md                              # Project documentation
```


## 📊 Input Data
The project uses the **NYC Taxi Trip Duration dataset** (NYC TLC).

**Features include:**
- Pickup & drop-off GPS coordinates  
- Exact pickup date and time  
- Passenger count and vendor ID  

---

## 🤖 AI Domain & Task Type
- **Domain:** Artificial Intelligence → Machine Learning  
- **Learning Type:** Supervised Learning  
- **Task:** Regression  
- **Target Variable:** `trip_duration` (in seconds)

---
## 02 — State of the Art

Before selecting a model, We evaluated three industry-standard approaches:

### 2.1 Linear Regression (Traditional Statistics)
**Strengths**
- Extremely fast
- Easy to explain and interpret

**Weaknesses**
- Assumes linearity
- Performs poorly in cities where traffic patterns vary drastically by time, It thinks 5km at 3 PM is the same as 5km at 3 AM.

---

### 2.2 Deep Learning (RNNs)
**Strengths**
- Highly accurate with massive sequential datasets
- Captures temporal dependencies

**Weaknesses**
- As a driver, I want to know why a trip is long (is it the time? the holiday? the bridge?). Neural networks don't tell  that easily.
- Computationally expensive for a simple ETA problem

---

### 2.3 Ensemble Learning (XGBoost / Gradient Boosting)
**Strengths**
- It’s the gold standard for tabular data. It builds a forest of decision trees that correct each other's mistakes, which is perfect for the messy reality of city traffic.
- Excellent with tabular data
- Handles outliers and non-linear relationships well
- Industry standard for Kaggle-style problems

**Weaknesses**
- Requires thoughtful **feature engineering**

---

## 03 — Method & Design: The *Holiday & Haversine* Approach

### 3.1 Chosen Model: XGBoost
Traffic behaves like a series of **if–then rules**:
> *If it's Monday at 8:00 AM → expect congestion.*

XGBoost models this behavior naturally using ensembles of decision trees.

---

### 3.2 Solving the Traffic Data Limitation
Our challenge is missing live maps, unlike real-world platforms (Uber, Bolt), the AI uses live traffic data from Google Maps. As a student, we don't have that.

**Solution:**

We use driver instinct and custom **Holiday Feature**.

Traffic patterns change dramatically on holidays. By integrating a **US Federal Holiday calendar**, the model learns that:
- A Monday ≠ a regular Monday if it’s **Labor Day**

This significantly improves prediction accuracy.

---

### 3.3 Feature Engineering Pipeline
- **Haversine Distance:**  
  Converts GPS coordinates into straight-line distance (km)
- **Time Decomposition:**  
  - Hour of day  
  - Day of week  
  - `Is_Holiday` flag
- **Data Cleaning:**  
  Removed impossible trips (e.g., 1 second or 24 hours)
- **Log Transformation:**  
  Applied `log(1 + trip_duration)` to reduce skew from extreme outliers

---

## 04 — Proof of Concept & Experiments

### 4.1 Testing Strategy
A strict dataset split was used:

- **60% Training** – Model learning  
- **20% Validation** – Hyperparameter tuning  
- **20% Test** – Final evaluation (never seen before by the model)

---

### 4.2 Results
- **Metric:** Root Mean Squared Error (RMSE)  
- **Final Test RMSE:** `0.0138 on log scale` and on average prediction is off by 51.91 seconds

**Key Insights**
- Distance, hour and weekend are the most important feature
- The holiday feature reduces late-year prediction errors
<img src="Images/important_features.png"> 


---

### 4.3 Model Demonstration
<img src="Images/model_perfomances.png"> 

**5 Good and worst predictions**


<img src="Images/model_demonstration.png">

---
### 4.4 Data source and training
To replicate this project, download the raw data from Kaggle
- Go to the [NYC Taxi Trip Duration Competition](https://www.kaggle.com/competitions/nyc-taxi-trip-duration).
- Download train.csv.
- Place it in the same folder as the notebook.
- The script will automatically perform a 60/20/20 split (Train/Validate/Test) to ensure the model isn't just memorizing data.




---

## 05 — Discussion & Challenges

### 🚧 Real-World Limitations
Even with **85%+ accuracy**, real driving experience reveals limitations, Driving in Poznań taught me that. One broken-down bus on a bridge can destroy an AI's prediction. The model is strong, but without real-time weather data and live road closure feeds, there will always be a 5-10% error rate caused by "unseen chaos.":

- **Accidents:** Sudden crashes cannot be predicted
- **Weather:** Rain can slow a city by ~20% (not yet modeled)
- **Human Behavior:** Passenger delays introduce noise into the data

**Future Improvement:**  
Integrate a weather API to enhance realism.

---

## ▶️ How to Run the Demo
1. Load `taxi_duration_model.pkl`(brain) and `taxi_test_data.csv`(test cases)
2. Open the notebook
3. Run the run_demo cell in the notebook
4. Input a trip index to compare:
   > *AI prediction vs. real NYC taxi outcome*

---
### Final Summary
This project proves that with the right "hand-crafted" features (like holiday logic and Haversine math), a lightweight model can provide high-value predictions that are useful for real-world taxi operations.
