# Tabela descritiva dos dados

## Visão geral

| métrica               | valor                   |
|:----------------------|:------------------------|
| observações (pregões) | 1763                    |
| período               | 2018-12-31 a 2025-12-30 |
| dias de calendário    | 2556                    |
| datas duplicadas      | 0                       |
| nº de colunas         | 47                      |

## Eventos de risco de geada (toda a amostra)

| estação                  |   dias_risco_geada |
|:-------------------------|-------------------:|
| Varginha                 |                 12 |
| Patrocinio               |                 19 |
| Manhuacu                 |                  1 |
| Machado                  |                  3 |
| ≥1 estação (dias únicos) |                 23 |

## Forward-fill climático (% de dias iguais ao anterior)

| variável            |   pct_repeticao_dia_anterior |
|:--------------------|-----------------------------:|
| precip_mm_sum       |                         55.1 |
| vento_rajada_ms_max |                          6.1 |
| vento_vel_ms_mean   |                          5.5 |
| radiacao_kJm2_sum   |                          3.2 |
| temp_min_C_min      |                          3.1 |
| temp_max_C_max      |                          3   |
| umidade_pct_mean    |                          0.7 |
| pressao_mB_mean     |                          0.6 |
| temp_ar_C_mean      |                          0.4 |

## Estatísticas — mercado

| index      |   count |      mean |      std |      min |       5% |      50% |       95% |       max |     skew |   kurtosis_excess |
|:-----------|--------:|----------:|---------:|---------:|---------:|---------:|----------:|----------:|---------:|------------------:|
| preco_cafe |    1763 | 195.72    | 88.2276  | 86.65    | 95.305   | 182.75   | 390.695   | 438.9     |  0.93179 |           0.07105 |
| cambio_brl |    1763 |   5.08793 |  0.57453 |  3.6428  |  3.8486  |   5.2133 |   5.7772  |   6.3     | -0.93086 |           0.14272 |
| log_ret    |    1762 |   0.0007  |  0.02261 | -0.09021 | -0.03578 |   0      |   0.03816 |   0.09557 |  0.07934 |           0.74359 |

## Estatísticas — clima agregado entre estações

| index            |   count |     mean |      std |     min |       5% |      50% |      95% |       max |
|:-----------------|--------:|---------:|---------:|--------:|---------:|---------:|---------:|----------:|
| temp_min (°C)    |    1763 |    15.34 |     3.51 |    3.6  |     8.98 |    16.33 |    19.9  |     23.92 |
| temp_media (°C)  |    1763 |    20.69 |     2.67 |   10.1  |    15.95 |    21.17 |    24.61 |     28.56 |
| umidade (%)      |    1763 |    71.96 |    10.39 |   33.62 |    52.44 |    73    |    87.08 |     94.9  |
| precip (mm)      |    1763 |     4.03 |     8.23 |    0    |     0    |     0.15 |    19.39 |     69    |
| radiacao (kJ/m²) |    1763 | 26015.8  | 17114.2  | 3290.35 | 10403.7  | 19519.2  | 64377.4  | 100401    |
