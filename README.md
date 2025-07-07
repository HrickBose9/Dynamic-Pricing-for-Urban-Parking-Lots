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
## 🔢 Models Used

We implemented and evaluated three pricing models to respond to real-time urban parking dynamics:

---

### 🔷 Model 0 – Daily Window (Baseline)

**Formula:**  
\[
\text{Price} = 10 + \frac{\text{Max Occupancy} - \text{Min Occupancy}}{\text{Capacity}}
\]

- Captures daily fluctuation in occupancy
- Works on a tumbling time window (1 day)
- Serves as a baseline for volatility detection

---

### 🟠 Model 1 – Row-wise Occupancy + Queue

**Formula:**  
\[
\text{Price} = 10 + 0.6 \cdot \left(\frac{\text{Occupancy}}{\text{Capacity}}\right) + 0.4 \cdot \text{QueueLength}^{1.5}
\]  
(Clipped between ₹5 and ₹20)

- Row-wise dynamic pricing based on real-time occupancy and congestion
- Queue growth is modeled non-linearly
- Smooth and responsive to live demand conditions

---

### 🟢 Model 2 – Demand-Based Sigmoid Function

**Formula (simplified):**  
\[
x = \text{weighted sum of occupancy, queue, traffic, events, vehicle risk}
\]  
\[
\text{Demand} = \frac{1}{1 + e^{-k(x - \mu)}}, \quad \text{Price} = 10 \cdot (1 + \text{Demand})
\]

- Most sophisticated model
- Incorporates multiple real-time features
- Uses a sigmoid to smooth price response and prevent overreaction
- Best performance in visual testing

---

✅ Model 2 is the most robust and recommended for real-world deployment.


## 🛠️ Tech Stack

| Tool        | Purpose                      |
|-------------|------------------------------|
| **Python (pandas, numpy)** | Data wrangling & modeling logic |
| **Pathway**  | Real-time data stream processing |
| **Bokeh + Panel** | Interactive visualizations |
| **Google Colab** | Execution environment |
| **GitHub**   | Submission + version control |

---

## 🏗️ Architecture

```mermaid
flowchart TD
    A[Raw Dataset (CSV)] --> B[Preprocessing with pandas]
    B --> C[parking_stream.csv]
    C --> D[Pathway replay_csv stream]
    D --> E[Model 0: Daily Tumbling Window]
    D --> F[Model 1: Row-wise Linear Model]
    D --> G[Model 2: Demand Function]
    E & F & G --> H[Bokeh Visualization (Real-Time)]
    H --> I[Final Dashboard]
