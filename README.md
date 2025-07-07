# Dynamic-Pricing-for-Urban-Parking-Lots

**Summer Analytics 2025 Capstone Project**  
By Hrick Bose • GitHub: HrickBose9

---

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
