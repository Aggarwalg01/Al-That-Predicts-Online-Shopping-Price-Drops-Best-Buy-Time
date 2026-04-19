# SmartPrice AI 📉

**SmartPrice AI** is an advanced machine learning platform designed to solve the problem of dynamic pricing in e-commerce. By leveraging Long Short-Term Memory (LSTM) neural networks, the system predicts future price drops on platforms like Amazon and Flipkart, empowering shoppers to transition from reactive to proactive purchasing. Unlike basic price trackers, SmartPrice AI provides a "Buy Now" vs. "Wait" recommendation engine backed by deep learning time-series forecasting.

---

### 🏗️ Tools and Technologies Used

This project integrates data science with modern web deployment. Here is the breakdown:

#### **Frontend & Integration**
* **Flask API:** Serves as the bridge between the Python machine learning model and the user interface.
* **Browser Extension (JavaScript):** Provides a seamless overlay on e-commerce product pages to display real-time price predictions.
* **Matplotlib/Seaborn:** Used for generating performance comparison charts and trend visualizations.

#### **Backend & Data Science**
* **Python (v3.10+):** The primary language for data processing and model training.
* **TensorFlow & Keras:** Used to build and train the LSTM (Long Short-Term Memory) neural network.
* **Scikit-Learn:** Utilized for data scaling (Min-Max Scaler) and baseline comparisons (Random Forest).
* **BeautifulSoup4 & Requests:** The engine for web scraping real-time price and rating data.
* **Pandas & NumPy:** For complex data manipulation and time-series structuring.

---

### ✨ Key Features

* **LSTM Time-Series Forecasting:** A deep learning model specifically tuned to recognize "price memory" and seasonal trends that traditional models (like ARIMA) often miss.
* **Dynamic Recommendation Engine:** A logic-based system that analyzes predicted vs. current prices. It uses a **1.5% sensitivity threshold** to issue "Wait" signals if a significant drop is imminent.
* **Dual-Model Validation:** Includes a "Performance Comparison" module that benchmarks the LSTM model against Random Forest baselines to ensure the highest accuracy.
* **Web Scraping Pipeline:** Automatically extracts price, discount percentage, and customer ratings to build a multi-dimensional view of a product’s value.
* **Automated Metrics Gathering:** Real-time calculation of Mean Absolute Error (MAE) and accuracy percentages (achieving a peak of **92.7% accuracy**).

---

### 🚀 How to Open and Run the Project

Follow these instructions to set up the prediction engine and the testing environment.

#### **Step 0: Prerequisites**
* **Python 3.10+:** Ensure Python is installed and added to your system PATH.
* **Jupyter Notebook / Google Colab:** Required to run the `.ipynb` files provided.
* **Required Libraries:** Install the stack using: 
    ```bash
    pip install pandas numpy scikit-learn tensorflow beautifulsoup4 requests flask
    ```

#### **Step 1: Data Preparation**
1.  Open `Training LSTM Neural Network.ipynb`.
2.  The script will look for your product CSV or initiate a scraping session to gather historical price data.
3.  The data is automatically normalized using **Min-Max Scaling** to ensure the neural network processes the prices efficiently.

#### **Step 2: Training the Model**
1.  Run the training cells in the notebook.
2.  The model uses a **14-day lookback window** (analyzing the last two weeks to predict the next day).
3.  Monitor the **Loss Curve**; the system is optimized using the **Adam Optimizer** to minimize the Mean Squared Error.

#### **Step 3: Performance Benchmarking**
1.  Open `Performance Comparison - LSTM vs. Random Forest.ipynb`.
2.  Run the comparison script to visualize how the Deep Learning model (LSTM) outperforms the Baseline (Random Forest).
3.  View the final **MAE (Mean Absolute Error)** report to confirm the precision of the predictions.

#### **Step 4: Deployment (API)**
1.  Run the Flask application script:
    ```bash
    python app.py
    ```
2.  The server will host the model at `http://localhost:5000`.
3.  The Browser Extension can now send a product URL to this endpoint and receive a "Buy" or "Wait" recommendation.

---

### 📚 How does the algorithm actually work?

1.  **Sequence Learning:** Because prices are sequential, the LSTM stores information from previous days in its "cell state," allowing it to remember if a price is currently in a "downward trend" or a "plateau."
2.  **Threshold Logic:** The system doesn't just predict a number; it calculates the **Delta (Δ)**. If `(Current Price - Predicted Price) / Current Price > 0.015`, the system triggers a **WAIT** alert.
3.  **Accuracy Verification:** The model is tested against a "Hold-out" dataset. It only achieves its **92.7% accuracy** rating by successfully predicting fluctuations it has never seen before during the training phase.
