# Resumo — baselines, ablação de clima, GARCH e seleção de features

Protocolo comum a todos os modelos: alvo em **log-retorno** do fechamento (estacionário),
validação **walk-forward** (5 folds, janela de treino expansiva a partir de 50% dos dados),
`LOOKBACK=45`, `EMBARGO=45`, `StandardScaler` ajustado **por fold apenas no treino**.
Modelos de nível avaliados nos **mesmos dias-alvo** (`te_idx[LOOKBACK:]` de cada fold).

> Convenção Diebold–Mariano: `DM = mean(e_modelo² − e_ref²) / sd`.
> **DM < −1,96 ⇒ modelo significativamente melhor** que a referência; **DM > 1,96 ⇒ pior**.

## Tabela comparativa (nível / média)

| model                  |    RMSE |     MAE |   sMAPE |   MASE |   DirAcc |   DM_vs_naive |   DM_oos_vs_naive |   DM_oos_vs_ARIMA |
|:-----------------------|--------:|--------:|--------:|-------:|---------:|--------------:|------------------:|------------------:|
| RandomWalk             | 0.02325 | 0.01814 |  198.45 |  0.724 |    0.008 |          0    |            nan    |            nan    |
| ARIMA                  | 0.02325 | 0.01814 |  185.08 |  0.724 |    0.501 |         -0.2  |             -0.11 |            nan    |
| LSTM_a_market          | 0.02358 | 0.01846 |  170.31 |  0.737 |    0.479 |          0.92 |              2.31 |              2.22 |
| LSTM_b_market_climaRaw | 0.0235  | 0.01821 |  161.77 |  0.727 |    0.534 |          0.49 |              1.38 |              1.37 |
| LSTM_c_market_climaLag | 0.0236  | 0.01847 |  164    |  0.738 |    0.5   |          0.62 |              1.57 |              1.54 |

## Baseline GARCH(1,1) — volatilidade (não o nível)

QLIKE médio (menor = melhor): **GARCH −6.508** vs **variância constante −6.518**.
GARCH vence em 2 dos 5 folds; na média a variância constante empata/leva vantagem marginal.
→ Não há ganho consistente de um GARCH(1,1) sobre o benchmark de variância constante neste
período — coerente com a autocorrelação da variância existir, mas ser difícil de explorar 1-passo.

## Estabilidade da seleção de features (RF dentro do fold, top-12)

Presentes no top-12 em **todos** os folds: `ret_cafe`, `sma_10`, `vol_5`, `vol_21`,
`ret_cambio`, `sin_doy` e **`umidade_pct_mean_Manhuacu`** (única climática 100% estável).
Logo abaixo (≥60% dos folds): `temp_ar_C_mean_Patrocinio`, `precip_mm_sum_Manhuacu`,
`umidade_pct_mean_Machado`, `temp_min_C_min_Patrocinio`, `cos_doy`, `temp_ar_C_mean_Manhuacu`.

## Veredito

- **Melhor LSTM**: LSTM_b_market_climaRaw (RMSE 0.02350).
- **vs random walk** (RMSE 0.02325): DM_oos = 1.38 (**sem diferença significativa**).
- **vs ARIMA** (RMSE 0.02325): DM_oos = 1.37 (**sem diferença significativa**).
- **LSTM só-mercado** é **significativamente pior** que o random walk (DM_oos = 2.31 > 1.96);
  adicionar clima bruto a traz de volta ao empate e é a **única** configuração com
  acurácia direcional > 0.5 (0.534).
- **Clima ajuda?** RMSE: só-mercado 0.02358 | +clima bruto 0.02350 | +clima defasado 0.02360.
  → adicionar clima **bruto** reduziu o RMSE médio e melhorou o acerto direcional;
  o clima **defasado agregado** não. Nenhum modelo bate o random walk de forma significativa
  — resultado honesto, esperado em log-retorno diário de commodity (mercado ~eficiente).
