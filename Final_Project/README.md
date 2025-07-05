# Dynamic Pricing Engine for Urban Parking Lots

---

## 🚀 Project Overview

This project develops an **intelligent, data-driven dynamic pricing engine** for urban parking lots. Our primary goal is to optimize parking space utilization and revenue by adjusting prices in real-time based on predicted demand. Traditional static pricing models often lead to inefficiencies, like overcrowding during peak hours or underutilization during off-peak times. This system leverages **machine learning** and **real-time stream processing** to create a responsive, dynamic pricing strategy.

At its core, the project utilizes an **LSTM (Long Short-Term Memory) model**, trained on historical parking data, to forecast future occupancy rates. This prediction then feeds into a rule-based pricing engine that calculates an optimal price. The entire workflow is orchestrated within a **real-time streaming pipeline**, simulating how the system would operate in a live environment.

---


## 🛠️ Tech Stack

* **Programming Language**: Python
* **Data Manipulation & Analysis**: `pandas`, `NumPy`
* **Machine Learning**: `TensorFlow` (Keras), `Scikit-learn`
* **Real-time Data Streaming**: `Pathway`
* **Data Visualization**:
    * Historical Analysis: `Matplotlib`, `Seaborn`
    * Real-time Dashboard: `Bokeh`
* **Development Environment**: Google Colab / Jupyter Notebook

---

## 🏛️ Architecture & Workflow

Our system is designed as a streaming pipeline that processes parking data in real-time, from ingestion to price visualization.

### Architecture Diagram
<img src="https://github.com/user-attachments/assets/6cd25b34-7029-4150-a80a-9c30a39ccdd9" alt="Architecture Diagram" width="400px" />
