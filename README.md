# Global Solution 2026 — CitizenTech
## Análise estatística da poluição do ar (PM2.5) em Pequim

**Disciplina:** Modelagem Linear para Aprendizado de Máquina (MLAM)

## 1. Integrantes

| Nome completo | RM |
|---|---|
| Arthur Araujo Massarioli | 573308 |
| Daniel Alejandro Pupo Martinez | 573075 |
| Wendel Pedro Rezende | 573126 |

## 2. Problema e objetivo

A poluição atmosférica é um desafio ambiental e de saúde pública. Este trabalho investiga **em que medida variáveis meteorológicas (temperatura, ponto de orvalho, pressão, vento, chuva e neve) explicam e permitem prever a concentração de partículas finas PM2.5** em Pequim, no contexto do desafio CitizenTech.

Objetivos: descrever a distribuição do PM2.5, testar hipóteses sobre a média, medir associações (bivariada e multivariada), ajustar regressões linear e logística, avaliar sua adequação e declarar as limitações.

## 3. Base de dados

- **Nome:** Beijing PM2.5 Data
- **Fonte:** UCI Machine Learning Repository — https://archive.ics.uci.edu/dataset/381/beijing+pm2+5+data
- **Conteúdo:** 43.824 medições horárias reais (01/01/2010 a 31/12/2014), 12 colunas: `year`, `month`, `day`, `hour`, `pm2.5`, `DEWP` (ponto de orvalho), `TEMP` (temperatura), `PRES` (pressão), `cbwd` (direção do vento), `Iws` (velocidade acumulada do vento), `Is` (horas de neve), `Ir` (horas de chuva).
- **Limpeza:** remoção das 2.067 linhas sem valor de PM2.5, restando 41.757 registros. Nenhum outro dado foi alterado. A limpeza é feita pelo próprio notebook.
- **Arquivos .csv:** `beijing_pm25_original.csv` (base original) e `beijing_pm25_limpo.csv` (base após a limpeza). Os dois são gerados pelo notebook.

## 4. Arquivos do repositório

| Arquivo | Descrição |
|---|---|
| `Global_Solution_MLAM.ipynb` | Notebook com todos os cálculos, gráficos, testes, modelos, previsões e classificações (saídas preservadas) |
| `beijing_pm25_original.csv` | Base original da UCI |
| `beijing_pm25_limpo.csv` | Base utilizada nas análises (sem registros sem PM2.5) |
| `Relatorio_Estatistico_GS_MLAM.pdf` | Relatório estatístico |
| `README.md` | Este arquivo |

## 5. Como executar

1. Abra `Global_Solution_MLAM.ipynb` no **Google Colab** (ou Jupyter) e execute **Ambiente > Executar tudo**.
2. A base é baixada automaticamente da UCI pela biblioteca `ucimlrepo` (é necessário acesso à internet). A primeira célula de código instala essa biblioteca.
3. Os arquivos `.csv` são salvos na pasta de trabalho do notebook (no Colab, o painel de arquivos à esquerda).

**Ordem do notebook:** identificação da base → importação e exploração → limpeza → salvamento dos `.csv` → análise exploratória → distribuição normal (item 02) → testes de hipóteses (item 03) → análise bivariada (item 04) → regressão linear múltipla (item 05) → regressão logística (item 06) → conclusões e limitações.

## 6. Bibliotecas

Python 3 com: `ucimlrepo`, `pandas`, `numpy`, `scipy`, `statsmodels`, `scikit-learn`, `matplotlib` e `seaborn`. No Google Colab todas já vêm instaladas, exceto `ucimlrepo` (instalada pelo notebook).

## 7. Síntese dos principais resultados

| Análise | Resultado |
|---|---|
| Distribuição normal | P(PM2.5 < média) = 50,00%; P(PM2.5 > mediana) = 61,38% |
| Testes Z (α = 6% e 9%) | Não rejeitou H0 em nenhum dos dois testes (p = 0,4485 e 0,6451) |
| Bivariada PM2.5 × ponto de orvalho | r = 0,1714; PM2.5 = 96,70 + 1,09·DEWP; R² = 0,029 (teste F significativo) |
| Regressão múltipla (TEMP, DEWP, PRES, Iws) | R² = 0,224; teste F significativo; maior correlação com o PM2.5: vento (−0,248) |
| Validação (treino/teste) | R² = 0,2255; MAE = 57,79; RMSE = 82,97 |
| Regressão logística (PM2.5 ≥ 100 µg/m³) | Acurácia = 69,23%; 1.530 dos 3.011 registros elevados detectados |

**Conclusão:** a meteorologia, principalmente o vento, ajuda a explicar parte da poluição por PM2.5, mas sozinha não basta para prever bem as concentrações altas.

## 8. Limitações

- Distribuição do PM2.5 assimétrica à direita, o que limita a hipótese de normalidade.
- Dados horários correlacionados no tempo, o que viola a hipótese de independência.
- Testes de hipóteses de caráter didático (referência e amostras da mesma base).
- Forte multicolinearidade entre temperatura, ponto de orvalho e pressão.
- Ausência de dados de emissão (trânsito, indústria, aquecimento).
- Uma única cidade e o período de 2010 a 2014.
- O corte de 100 µg/m³ é um critério operacional do estudo, não uma classificação oficial de qualidade do ar.
- Os resultados indicam associação, não causalidade.
