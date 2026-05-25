# LSTM para predição do preço do café
## Objetivo Geral
Desenvolver e validar um modelo de LSTM para a predição do preço do café, 
utilizando variáveis de mercado e climáticas das principais regiões produtoras 
da café do Brasil. 

## Objetivos Específicos:

1. Coletar e organizar dados
2. Realizar o pré-processamento dos dados
3. Desenvolver um modelo de RNA para predição do preço do café
4. Avaliar o desempenho do modelo utilizando métricas estatísticas

## Origem dos dados

- Dados mercadologicos são originarios do Yahoo Finance, via biblioteca yfinance, sendo os ativos utilizados: 
  1. *KC=f*: código de negociação (ticker) do Café Arábica (Coffee C) para contratos futuros no mercado internacional de commodities.
  2. *BRL=X*: o código (ticker) utilizado no Yahoo Finance para representar a taxa de câmbio entre o Dólar Americano (USD) e o Real Brasileiro (BRL). 
- Dados climáticos são originarios do Instituto Nacional de Meteorologia (INMET), disponibilizados publicamente em: https://bdmep.inmet.gov.br/. As estações escolhidas para coleta foram:
  1. Varginha - MG
  2. Lavras - MG
  3. Machado - MG