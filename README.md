# Dynamic-Pricing-for-Urban-Parking-Lots

**Summer Analytics 2025 Capstone Project**  
By Hrick Bose • GitHub: HrickBose9

---

## ▶️ How to Run the Code

To run the full pipeline and generate real-time visualizations:

1. **Open the notebook** [`Urban_parking_lot_pricing_CLEAN.ipynb`](./Urban_parking_lot_pricing_CLEAN.ipynb) in [Google Colab](https://colab.research.google.com/)
2. **Upload the included dataset**: `dataset.csv`
3. Run all cells from top to bottom
4. Bokeh plots will appear inline for:
   - Model 0 (Daily window)
   - Model 1 (Occupancy + Queue)
   - Model 2 (Demand function)
5. Optional: Right-click each plot → Save as PNG for analysis

📌 Note: Outputs are intentionally cleared for GitHub rendering. You must execute the notebook to view model results.


## 🧠 Project Overview

Urban parking lots face congestion and underutilization due to static pricing. This project builds a **real-time dynamic pricing engine** for 14 urban parking lots using live streaming data and the **Pathway framework**.  

We implement three pricing models of increasing sophistication, integrating real-time features like:
- Occupancy rate
- Queue length
- Traffic congestion
- Vehicle type
- Special day indicators

---
## 🛠️ Tech Stack

| Tool             | Purpose                                |
|------------------|----------------------------------------|
| **Python**       | Preprocessing, modeling, pipeline logic |
| **Pathway**      | Real-time data streaming & processing   |
| **Pandas / NumPy** | Data manipulation and math             |
| **Bokeh + Panel**| Interactive visualizations              |
| **Google Colab** | Notebook execution                      |
| **GitHub**       | Version control and submission          |

---

## 🏗️ Architecture

```mermaid
flowchart TD
    A[Raw Dataset (CSV)] --> B[Preprocessing with pandas]
    B --> C[parking_stream.csv]
    C --> D[Pathway Streaming Input]
    D --> E[Model 0: Daily Window]
    D --> F[Model 1: Occupancy + Queue]
    D --> G[Model 2: Demand-based Function]
    E & F & G --> H[Bokeh Plotting with Panel]
    H --> I[Visual Dashboard Output]
```

---

## 🔢 Models Used

### 🔷 Model 0 – Daily Window (Baseline)

**Formula:**  
Price = 10 + (Max Occupancy - Min Occupancy) / Capacity

- Captures daily demand volatility
- Smooth but not responsive to real-time changes

---

### 🟠 Model 1 – Row-wise (Occupancy + Queue)

**Formula:**  
Price = 10 + 0.6 * (Occupancy / Capacity) + 0.4 * QueueLength^1.5

(Clipped between ₹5 and ₹20)

- Real-time reactive model
- Scales pricing with both usage and congestion

---

### 🟢 Model 2 – Demand-Based Sigmoid Model

**Formula (Simplified):**  
x = w1*OccupancyRatio + w2*Queue + w3*Traffic +
    w4*(IsSpecialDay * Traffic) + w5*VehicleRisk

Demand = 1 / (1 + exp(-k * (x - μ)))
Price = 10 * (1 + Demand)

- Most dynamic and adaptive model
- Smooth sigmoid response to multiple features
- Robust to noisy inputs and spikes

---
