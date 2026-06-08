# ☕ LSTM Coffee Price Prediction

> Forecasting arabica coffee futures prices using deep learning, climate data, and market indicators.

---

## Overview

This project develops a **Long Short-Term Memory (LSTM)** neural network to predict the daily closing price of arabica coffee futures (**KC=F**) traded on the ICE Futures exchange.

The model combines financial market data with meteorological observations from the four main coffee-producing microregions of Minas Gerais, Brazil — the state responsible for the majority of the country's arabica production.


---

## Motivation

Brazil is the world's largest coffee producer and exporter. Coffee price volatility directly impacts millions of producers, exporters, and traders. Accurate price forecasting can support better decision-making across the entire supply chain.

Unlike most financial forecasting approaches that rely solely on market indicators, this project incorporates **regional climate variables** as input features — reflecting the agronomic reality that weather events such as frost, drought, and temperature extremes are among the strongest drivers of coffee supply and price.

---

## Data Sources

| Source | Description | Frequency |
|---|---|---|
| [Yahoo Finance](https://finance.yahoo.com) via `yfinance` | KC=F closing price (USD/lb) and BRL/USD exchange rate | Daily |
| [INMET BDMEP](https://bdmep.inmet.gov.br) | Historical climate data from 4 weather stations | Hourly → Daily |

**Weather stations (INMET automatic network):**

| City | Station Code | Altitude | Region |
|---|---|---|---|
| Varginha | A515 | 942 m | Sul de Minas |
| Patrocínio | A523 | 931 m | Alto Paranaíba |
| Manhuaçu | A556 | 674 m | Zona da Mata |
| Machado | A567 | 871 m | Sul de Minas |

**Climate variables retained per station:**

- Mean, max, and min air temperature (°C)
- Total precipitation (mm)
- Global solar radiation (kJ/m²)
- Mean relative humidity (%)
- Mean and max wind speed (m/s)
- Frost flag (1 if min temperature < 0°C)

---

## Methodology

- **Period:** January 2019 – December 2025
- **Frequency:** Daily (business days — aligned with exchange calendar)
- **Climate representation:** Opção B — each city contributes its own set of features (wide format), allowing the model to learn region-specific weights
- **Missing values:** Linear interpolation within each station's time series (~4%)
- **Feature selection:** Random Forest feature importance + Pearson/Spearman correlation
- **Normalization:** MinMaxScaler fitted on training set only
- **Architecture:** Multi-layer LSTM with dropout (PyTorch)
- **Train/Val/Test split:** 70% / 15% / 15% — chronological, no shuffling

---

## Requirements

```bash
pip install -r requirements.txt
```

---

## Status

| Stage | Status |
|---|---|
| Climate data collection & processing | ✅ Complete |
| Market data collection | ✅ Complete |
| Dataset merge | ✅ Complete |
| LSTM training | ⏳ Pending |
| Evaluation & results | ⏳ Pending |

---

## Author

**Euler Gomes**

Computer Engineering — IFMG Campus Bambuí

---

## License

This project is intended for academic and portfolio purposes.