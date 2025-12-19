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

