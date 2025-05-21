# 📈 Stock Prediction Model (3-Strategy Screener)

This project is an end-to-end machine learning pipeline that predicts which stocks are likely to go up based on three trading strategies: short-term, breakout, and swing trades. The system uses engineered technical indicators, a TensorFlow classification model, and live data from Yahoo Finance to generate daily predictions for over 6000 tickers.

---

## 🔧 Project Structure

```
stock-prediction-project/
├── data/
│   ├── stock_data/                    # Raw CSVs per ticker (6000+ tickers)
│   ├── engineered_stock_data.csv      # Final dataset with features + targets
│   ├── target_a_top_20_tickers.csv    # Prediction output for Strategy A
│   ├── target_b_top_20_tickers.csv    # Prediction output for Strategy B
│   └── target_c_top_20_tickers.csv    # Prediction output for Strategy C
│
├── notebooks/
│   ├── 1_data_preparation.ipynb       # Loads and combines raw CSVs
│   ├── 2_data_engineering.ipynb       # Adds technical indicators + targets
│   └── 3_model_training.ipynb         # Trains model and outputs top 20 picks
│
├── .gitignore
└── README.md
```

---

## 📥 Setup Instructions

1. **Clone this repository**
   ```bash
   git clone https://github.com/SaamSani/stock-prediction-project.git
   cd stock-prediction-project
   ```

2. **Add Raw Ticker Data**
   Place all stock CSVs (one per ticker) into:
   ```
   data/stock_data/
   ```

3. **Install Dependencies**
   Ensure Python ≥ 3.8 is installed. Then run:
   ```bash
   pip install pandas numpy scikit-learn tensorflow yfinance
   ```

4. **Run the Notebooks in Order**
   - `1_data_preparation.ipynb`: Combines raw CSVs and prepares base dataset
   - `2_data_engineering.ipynb`: Adds technical features and target labels
   - `3_model_training.ipynb`: Trains TensorFlow model and predicts top 20 tickers

---

## 📊 Trading Strategies

When prompted in Notebook 3, you’ll choose a strategy:

| Option | Strategy Name       | Description                                      |
|--------|---------------------|--------------------------------------------------|
| A      | Short-Term Pick     | Stock is expected to go up tomorrow             |
| B      | Breakout Opportunity| Stock is expected to jump 10%+ in the next 3 days|
| C      | Swing Trade         | Stock is expected to close higher in 5 days     |

---

## ✅ Example Output

```
Top 20 stocks the model predicts will go UP based on: Target_B

 1.  NVDA   — Confidence: 93.21% — Live Price: $950.12
 2.  AMD    — Confidence: 91.74% — Live Price: $134.87
 ...
20.  META   — Confidence: 82.45% — Live Price: $477.30
```

Predictions are saved as CSV files inside the `/data/` folder.

---

## 🧠 Features Used

| Feature       | Description                                  |
|---------------|----------------------------------------------|
| SMA_10        | 10-day simple moving average                 |
| EMA_10        | 10-day exponential moving average            |
| RSI_14        | Relative strength index                      |
| ATR_14        | Average true range (volatility)              |
| Range         | High − Low (daily range)                    |
| Change        | (Close − Open) ÷ Open (daily return)        |
| SMA_ratio     | Close ÷ SMA_10 (momentum signal)             |
| Volatility    | ATR ÷ Close                                  |
| LogVolume     | Log-transformed trading volume               |

---

## 🧠 Model Details

- **Framework**: TensorFlow (Keras Sequential)
- **Model Type**: Binary Classification
- **Target**: 1 = stock predicted to go up, 0 = otherwise
- **Architecture**:
  - Dense(64, ReLU)
  - Dense(32, ReLU)
  - Dense(1, Sigmoid)

Each trading strategy (A, B, C) uses its own target column (`Target_A`, `Target_B`, `Target_C`) for training and evaluation.

---

## 📌 Notes

- Over **6000 tickers** used from the stock market
- Live prices pulled in real time via the `yfinance` API
- Results are ranked by model confidence and saved to CSV
- Supports daily updates and re-training with new data

---

## 📬 Contact

Created by [Saam Sani](https://github.com/SaamSani)  
For questions or contributions, open an issue or connect via [LinkedIn](https://linkedin.com/in/SaamSani)
