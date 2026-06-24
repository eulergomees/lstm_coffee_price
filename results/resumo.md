# Resumo Fase 2 — baselines, ablação e seleção

## Tabela comparativa

| model                  |    RMSE |     MAE |   sMAPE |   MASE |   DirAcc |   DM_vs_naive |   DM_oos_vs_naive |   DM_oos_vs_ARIMA |
|:-----------------------|--------:|--------:|--------:|-------:|---------:|--------------:|------------------:|------------------:|
| RandomWalk             | 0.02325 | 0.01814 |  198.45 |  0.724 |    0.008 |          0    |            nan    |            nan    |
| ARIMA                  | 0.02325 | 0.01814 |  185.08 |  0.724 |    0.501 |         -0.2  |             -0.11 |            nan    |
| LSTM_a_market          | 0.02358 | 0.01846 |  170.31 |  0.737 |    0.479 |          0.92 |              2.31 |              2.22 |
| LSTM_b_market_climaRaw | 0.0235  | 0.01821 |  161.77 |  0.727 |    0.534 |          0.49 |              1.38 |              1.37 |
| LSTM_c_market_climaLag | 0.0236  | 0.01847 |  164    |  0.738 |    0.5   |          0.62 |              1.57 |              1.54 |

## Verdicto

- **Melhor LSTM**: LSTM_b_market_climaRaw (RMSE 0.02350).
- **vs random walk** (RMSE 0.02325): DM_oos = 1.38 (sem diferença significativa).
- **vs ARIMA** (RMSE 0.02325): DM_oos = 1.37 (sem diferença significativa).
- **Clima ajuda?** RMSE: só-mercado 0.02358 | +clima bruto 0.02350 | +clima defasado 0.02360.
  → adicionar clima (bruto) **reduziu** o RMSE médio.
