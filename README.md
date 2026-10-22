# 📊 Análise Exploratória do PIB por Unidade da Federação (IBGE)

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-4c72b0)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)

Análise exploratória de dados (EDA) do Produto Interno Bruto (PIB) das 27 Unidades da Federação do Brasil, com base em dados do **IBGE**. O projeto examina a estrutura da base, calcula estatísticas descritivas, visualiza a distribuição dos valores e mensura a **concentração econômica regional** por meio da participação percentual de cada estado no total nacional.

---

## 📑 Sumário

- [Objetivo](#-objetivo)
- [Fonte e estrutura dos dados](#-fonte-e-estrutura-dos-dados)
- [Tecnologias utilizadas](#-tecnologias-utilizadas)
- [Metodologia](#-metodologia)
- [Principais resultados](#-principais-resultados)
- [Visualizações](#-visualizações)
- [Como executar](#-como-executar)
- [Estrutura do repositório](#-estrutura-do-repositório)
- [Limitações e cuidados](#-limitações-e-cuidados)
- [Próximos passos](#-próximos-passos)
- [Autor](#-autor)

---

## 🎯 Objetivo

Responder, a partir dos dados de PIB por UF, às seguintes perguntas:

1. Qual é a estrutura e a qualidade da base de dados?
2. Como o PIB se distribui entre os estados (média, mediana, dispersão)?
3. Quais estados concentram a maior parte da riqueza?
4. Qual o grau de desigualdade entre o maior e o menor PIB estadual?

---

## 🗂️ Fonte e estrutura dos dados

- **Fonte:** IBGE (Instituto Brasileiro de Geografia e Estatística) — tabela de PIB por Unidade da Federação.
- **Coleta:** os valores foram **transcritos manualmente** da tabela do IBGE e inseridos diretamente no notebook, em um dicionário Python.
- **Dimensão:** 27 registros × 2 colunas.

| Coluna   | Tipo     | Descrição                                   |
|----------|----------|---------------------------------------------|
| `Estado` | `string` | Nome da Unidade da Federação (26 estados + DF) |
| `PIB`    | `int`    | Valor do PIB da UF conforme informado na base |

Coluna derivada criada na análise:

| Coluna           | Descrição                                           |
|------------------|-----------------------------------------------------|
| `Participacao_%` | Participação percentual da UF no PIB total das 27 UFs |

### ✅ Verificação de qualidade

| Verificação              | Resultado |
|--------------------------|-----------|
| Dimensões da base        | (27, 2)   |
| Estados únicos           | 27        |
| Valores ausentes         | 0         |
| Registros duplicados     | 0         |

---

## 🛠️ Tecnologias utilizadas

- **Python 3**
- **Pandas** — manipulação e estatística descritiva
- **NumPy** — suporte numérico
- **Matplotlib** — customização de gráficos e formatação de eixos
- **Seaborn** — visualizações estatísticas
- **Jupyter Notebook** — ambiente de desenvolvimento e documentação

---

## 🔬 Metodologia

O notebook está organizado em etapas sequenciais:

| Etapa | Descrição |
|-------|-----------|
| **1. Estrutura da base** | Dimensões, unicidade de estados, valores ausentes e duplicados |
| **2. Estatísticas descritivas** | `describe()` com formatação no padrão brasileiro (`.` milhar, `,` decimal) |
| **3. Formatação brasileira** | Função `formato_br()` para padronizar números nos eixos dos gráficos |
| **4. Gráfico de barras** | PIB de todas as UFs, ordenado de forma crescente |
| **5. Top 5** | Cinco maiores PIBs estaduais |
| **6. Histograma** | Distribuição dos valores com curva KDE |
| **7. Participação percentual** | Cálculo da fatia de cada UF no total e ranking das 10 maiores |
| **8. Participação do Top 5** | Gráfico da contribuição percentual das cinco maiores economias |

Cálculo da participação:

```python
base_pib["Participacao_%"] = (base_pib["PIB"] / base_pib["PIB"].sum()) * 100
```

---

## 📈 Principais resultados

### Estatísticas descritivas

| Métrica | Valor |
|---------|------:|
| Contagem | 27 |
| Média | 405.309.090,26 |
| Desvio padrão | 672.650.116,31 |
| Mínimo (Roraima) | 25.124.805,00 |
| 1º quartil (25%) | 85.302.894,00 |
| Mediana (50%) | 209.829.732,00 |
| 3º quartil (75%) | 398.328.480,50 |
| Máximo (São Paulo) | 3.444.814.033,00 |

### Ranking das 10 maiores UFs por participação no total

| # | Estado | PIB | Participação |
|:-:|--------|----:|-------------:|
| 1 | São Paulo | 3.444.814.033 | 31,48% |
| 2 | Rio de Janeiro | 1.172.871.443 | 10,72% |
| 3 | Minas Gerais | 971.977.551 | 8,88% |
| 4 | Paraná | 670.919.162 | 6,13% |
| 5 | Rio Grande do Sul | 650.107.022 | 5,94% |
| 6 | Santa Catarina | 513.392.973 | 4,69% |
| 7 | Bahia | 430.987.853 | 3,94% |
| 8 | Distrito Federal | 365.669.108 | 3,34% |
| 9 | Goiás | 336.746.975 | 3,08% |
| 10 | Mato Grosso | 273.008.586 | 2,49% |

### 💡 Insights

- **Alta concentração econômica:** São Paulo sozinho responde por **31,48%** do PIB somado das UFs — quase um terço do total.
- **Top 3 ≈ metade do total:** São Paulo, Rio de Janeiro e Minas Gerais somam cerca de **51,1%**.
- **Top 5 ≈ dois terços:** as cinco maiores economias (SP, RJ, MG, PR e RS) representam aproximadamente **63,2%**; as 10 maiores, cerca de **80,7%**.
- **Distribuição assimétrica à direita:** a média (≈ 405 milhões) é quase o **dobro da mediana** (≈ 210 milhões), indicando que poucos valores muito elevados puxam a média para cima. O desvio padrão (≈ 673 milhões) supera a própria média, sinal de forte dispersão.
- **Histograma:** a maior parte das UFs (20 de 27) está na primeira faixa de valores, com um *outlier* evidente à direita — São Paulo.
- **Desigualdade entre extremos:** o PIB de São Paulo é cerca de **137 vezes** o de Roraima (menor valor da base).

---

## 🖼️ Visualizações

O notebook gera os seguintes gráficos:

1. **PIB por Unidade da Federação** — barras horizontais com as 27 UFs.
2. **Cinco maiores valores registrados** — barras horizontais do Top 5.
3. **Distribuição dos valores de PIB** — histograma com KDE.
4. **Participação dos cinco maiores valores** — barras com percentual sobre o total.

## 📄 Licença

Este projeto é distribuído sob a licença MIT. Os dados pertencem ao IBGE e estão sujeitos aos seus termos de uso.
