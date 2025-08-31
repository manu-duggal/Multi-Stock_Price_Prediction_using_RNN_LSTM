# Multi-Stock_Price_Prediction_using_RNN_LSTM

### **1. Data Preparation**
- Combined stock data from multiple companies into a single master DataFrame.
- Created **windowed sequences** (sliding windows) for time-series modeling.
- Applied **MinMaxScaler** for normalization to improve training stability.
- Chose a **window size of 22** (approx. monthly trading days) for capturing short-term trends.

---

### **2. Model Development**
- **Baseline: Simple RNN**
  - Hyperparameter tuning for `units`, `dropout`, `learning_rate`.
  - **Best parameters**:
    - `units = 64`, `dropout = 0.3`, `learning_rate = 0.01`
  - Achieved **Val Loss ≈ 0.00015**, but showed limitations in long-term dependency handling.

- **Advanced Model: LSTM**
  - Implemented **LSTM** with dropout and tuned hyperparameters.
  - **Hyperparameter search space**:
    - `units`: [32, 64, 128]
    - `dropout`: [0.1, 0.2, 0.3]
    - `learning_rate`: [0.01, 0.001]
  - **Best configuration**:
    - `units = 128`, `dropout = 0.2`, `learning_rate = 0.01`
  - Used **EarlyStopping** and **ReduceLROnPlateau** for regularization and adaptive learning.

---

### **3. Model Evaluation (Single Stock: GOOGL)**
- **Simple RNN**:
  - R² Score: **0.9870**  
- **LSTM**:
  - R² Score: **0.9831**  

**Observations**:
- **Simple RNN achieved the highest R² for GOOGL (0.9870)**, indicating better predictive performance compared to LSTM for this single-stock scenario.
- LSTM still performed well but had slightly lower variance explanation (~98.3%). A difference of 0.4%

---

### **4. Multi-Stock Prediction (GOOGL, AMZN, MSFT, IBM using LSTM)**
- **AMZN**: R² = **0.9800**  
- **GOOGL**: R² = **0.9646**  
- **MSFT**: R² = **0.9246**  
- **IBM**: R² = **0.9154**  

**Observations**:
- **AMZN had the highest R² among multi-stock predictions (0.9800)**.
- **IBM showed the weakest R² (0.9154)**, which is still very good but comparitively weaker
- **AMZN and GOOGL maintained strong R² (>0.96)**, confirming LSTM’s ability to generalize well for large-cap stocks.

---

### **5. Key Insights**
- R² comparison clearly shows:
  - For **single stock**, **Simple RNN > LSTM** (0.9870 vs 0.9831).
  - For **multi-stock**, **LSTM performs best on AMZN and GOOGL** and reasonably well on IBM and MSFT.
- **IBM remains a challenge**, possibly due to lower volatility or different price dynamics.

---

### **6. Final Outcome**
- **Single-Stock Scenario (GOOGL)**:
  - **Simple RNN achieved the best R² (0.9870)**, slightly outperforming LSTM (0.9831).
- **Multi-Stock Scenario (LSTM)**:
  - **AMZN performed best (R² = 0.9800)**, followed by GOOGL (0.9646) and MSFT (0.9246).
  - **IBM lagged slightly (R² = 0.9154)**, suggesting the need for model customization per stock.
- Overall:
  - Models are **highly effective for high-R² stocks (MSFT, GOOGL, AMZN)**.
  - Future improvements should focus on **stock-specific modeling** or **adaptive architectures** for weaker stocks like IBM.


