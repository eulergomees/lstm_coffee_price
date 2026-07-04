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

- **Period:** December 2018 – December 2025 (1,763 daily observations)
- **Frequency:** Daily (business days — aligned with exchange calendar)
- **Target:** log-return `r_t = ln(P_t / P_{t-1})` — stationary (confirmed by ADF), avoiding the out-of-`[0,1]` extrapolation that a level-fitted MinMaxScaler causes under a chronological split
- **Climate representation:** Opção B — each city contributes its own set of features (wide format), allowing the model to learn region-specific weights
- **Missing values:** none in the merged dataset; climate is forward-filled on non-trading days
- **Validation:** walk-forward with an **expanding** train window (5 folds, from 50% of the data), `LOOKBACK=45`, `HORIZON=1`, and a **45-day embargo** between train and test to purge leakage
- **Normalization:** `StandardScaler` fitted **per fold on the train core only** (no leakage)
- **Feature selection:** Random Forest importance **inside each fold** (top-k) + stability across folds; EDA uses Pearson/Spearman
- **Architecture:** LSTM (1 layer, hidden 48, dropout 0.2) in PyTorch, Adam + early stopping
- **Baselines:** Random Walk, ARIMA (order by AIC per fold), GARCH(1,1) for volatility
- **Metrics:** RMSE, MAE, sMAPE, MASE, directional accuracy, Diebold–Mariano test

---

## Requirements

```bash
pip install -r requirements.txt
```

---

## Results (summary)

Nenhum modelo bate o random walk de forma significativa (Diebold–Mariano) — resultado
esperado e honesto em log-retorno diário de commodity. A LSTM só-mercado é significativamente
pior que o random walk; **adicionar variáveis climáticas brutas** reduz o RMSE (0.02358 →
0.02350), empata com o random walk e é a **única** configuração com acurácia direcional > 0.5
(0.534). O clima defasado agregado não ajudou. Detalhes em [`results/resumo.md`](results/resumo.md).

## Status

| Stage | Status |
|---|---|
| Climate data collection & processing | ✅ Complete |
| Market data collection | ✅ Complete |
| Dataset merge | ✅ Complete |
| EDA | ✅ Complete |
| LSTM training (walk-forward) | ✅ Complete |
| Baselines + climate ablation + feature selection | ✅ Complete |
| Evaluation & results | ✅ Complete |

---

## Author

**Euler Gomes**

Computer Engineering — IFMG Campus Bambuí

**Antonio Ambrosio**

Computer Engineering — IFMG Campus Bambuí

**Dr. Marcos Roberto**

Ph.D. in Computer Science — IFMG Campus Bambuí

---

## License

This project is intended for academic and portfolio purposes.