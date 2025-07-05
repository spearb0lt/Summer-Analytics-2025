Dynamic Pricing Engine for Urban Parking Lots
🚀 Project Overview
This project develops an intelligent, data-driven dynamic pricing engine for urban parking lots. The primary goal is to optimize parking space utilization and revenue by adjusting prices in real-time based on predicted demand. Traditional static pricing models often lead to inefficiencies like overcrowding during peak hours or underutilization during off-peak times. This system leverages machine learning and real-time stream processing to create a responsive pricing strategy.

The core of the project is an LSTM (Long Short-Term Memory) model trained on historical parking data to forecast future occupancy rates. This forecast is then fed into a rule-based pricing engine that calculates an optimal price. The entire workflow is orchestrated within a real-time streaming pipeline, simulating how the system would operate in a live environment.

🛠️ Tech Stack
Programming Language: Python

Data Manipulation & Analysis: pandas, NumPy

Machine Learning: TensorFlow (Keras), Scikit-learn

Real-time Data Streaming: Pathway

Data Visualization:

Historical Analysis: Matplotlib, Seaborn

Real-time Dashboard: Bokeh

Development Environment: Google Colab / Jupyter Notebook

🏛️ Architecture & Workflow
The system is designed as a streaming pipeline that processes parking data in real-time, from ingestion to price visualization.

Architecture Diagram
Code snippet

graph TD
    A[Data Source: CSV Stream] -->|Simulated Real-time Events| B(Pathway: Data Ingestion);
    B -->|Raw Data Records| C{Pathway: Real-time Preprocessing & Feature Engineering};
    C -->|Engineered Features| D[Windowing: Create Sequences];
    D -->|Time-based Sequences (e.g., last 24 hrs)| E[ML Model Prediction];
    subgraph ML Inference
        E(Trained LSTM Model);
    end
    E -->|Predicted Occupancy Rate| F[Dynamic Pricing Logic];
    F -->|Calculated Price & Tier| G(Pathway: Output Stream);
    G -->|Live Pricing Data| H[Bokeh Real-time Dashboard];

    style A fill:#f9f,stroke:#333,stroke-width:2px
    style H fill:#bbf,stroke:#333,stroke-width:2px
Detailed Workflow Explanation
Data Ingestion (A -> B):
The system simulates a live data feed by reading historical data from a CSV file in streaming mode. In a production environment, this would be replaced with a direct connection to a message queue (like Kafka or RabbitMQ) or an IoT data source from the parking lots. Pathway ingests each row as a separate event in the stream.

Real-time Preprocessing & Feature Engineering (B -> C):
As each data record (event) flows through the Pathway pipeline, it undergoes immediate transformation. This includes:

Parsing timestamps.

Calculating the occupancy_rate from Occupancy and Capacity.

Extracting time-based features like hour_of_day and day_of_week.

One-hot encoding categorical variables like TrafficConditionNearby.
These steps are crucial for preparing the data for the machine learning model.

Windowing & Sequencing (C -> D):
The LSTM model requires a sequence of historical data (e.g., data from the last 24 time steps) to make a prediction. Pathway's powerful windowing capabilities are used here. The stream is grouped by SystemCodeNumber (the parking lot ID), and a sliding window collects the most recent sequence of data for each lot.

Demand Forecasting (D -> E):
Once a complete sequence is formed for a specific parking lot, it is passed to a User-Defined Function (UDF). Inside this UDF:

The data sequence is scaled using the pre-fitted MinMaxScaler.

The pre-trained Keras LSTM model (model.predict()) is invoked to forecast the occupancy_rate for the next time step.

Dynamic Pricing Logic (E -> F):
The predicted occupancy rate from the model is then fed into the get_dynamic_price function. This function contains the core business logic, translating the demand forecast into a concrete price. It uses a tiered system (e.g., Discount, Standard, High Demand, Surge) to set the price based on predefined occupancy thresholds.

Output Stream & Visualization (F -> G -> H):
The final output, containing the timestamp, parking lot ID, predicted occupancy, and the calculated dynamic price, is published to an output stream. This stream is connected to a Bokeh server using pw.io.bokeh.write. The Bokeh dashboard subscribes to this stream and automatically updates the plots in real-time as new pricing data is generated, providing a live monitoring tool for parking lot operators.

📋 How to Run
Setup: Ensure all dependencies listed in the notebook are installed.

Train Model: Run the initial cells of the notebook to preprocess the data and train the LSTM model. This only needs to be done once.

Run Simulation: Execute the final cells containing the Pathway and Bokeh code to start the real-time pricing simulation and view the live dashboard.
