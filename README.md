# ML Aplicada — Previsão de Visitantes

Projeto acadêmico de Machine Learning Aplicada que utiliza o pipeline **CRISP-DM** para análise, preparação e modelagem de dados reais de visitação em zoológicos. O trabalho combina técnicas de **Regressão Linear**, **Random Forest** e **KNN** para prever a demanda de visitantes e gerar insights voltados ao contexto do **Totem Inteligente FlexMedia**.

---

## Visão Geral

Este projeto é a entrega da **Sprint 2** de uma disciplina de Machine Learning Aplicada. O ponto de partida, definido na Sprint 1, foi a pergunta de negócio:

> *"Como identificar visitantes com maior chance de interagir com o Totem FlexMedia?"*

Na Sprint 2, o foco passou para a construção de um pipeline preditivo completo — da compreensão do domínio até a avaliação dos modelos — usando dados reais de visitação do **Zoológico de Helsinque (2023)** como base empírica.

---

## Objetivo do Trabalho

O professor solicitou a aplicação completa do pipeline **CRISP-DM** sobre um dataset real, contemplando:

- **Entendimento do negócio**: definir o problema e as hipóteses de trabalho
- **Análise exploratória dos dados (EDA)**: compreender a distribuição, qualidade e padrões dos dados
- **Pré-processamento e Feature Engineering**: preparar as variáveis para os modelos
- **Modelagem**: aplicar ao menos dois algoritmos de ML (regressão e classificação)
- **Avaliação**: medir o desempenho com métricas adequadas e comparar os resultados
- **Conclusão**: extrair insights e recomendações práticas para o contexto de negócio

**Hipóteses investigadas:**

1. Dias de fim de semana e feriados concentram maior número de visitantes
2. Estações do ano e mês influenciam diretamente o volume de visitação
3. É possível antecipar o público e ajustar automaticamente o funcionamento do Totem FlexMedia

---

## O que foi Entregue

| Etapa | Descrição | Status |
|---|---|---|
| EDA | Análise descritiva e exploratória dos dados | ✅ Concluído |
| Pré-processamento | Codificação com OneHotEncoder e normalização com StandardScaler | ✅ Concluído |
| Regressão Linear | Previsão do número absoluto de visitantes | ✅ Concluído |
| Random Forest | Regressão com ensemble (1.000 árvores) | ✅ Concluído |
| KNN + GridSearchCV | Classificação de períodos: alta / média / baixa demanda | ✅ Concluído |
| Avaliação | MAE, RMSE, R², Classification Report e Matriz de Confusão | ✅ Concluído |
| Visualizações | Importância de variáveis e matriz de confusão | ✅ Concluído |
| Insights | Recomendações práticas para o Totem Inteligente FlexMedia | ✅ Concluído |

---

## Estrutura do Repositório

```
ML-aplicada-previsao-de-visitantes/
├── Notebook_acadêmico.ipynb   # Pipeline CRISP-DM completo (EDA → Modelagem → Avaliação)
└── README.md                  # Documentação do projeto
```

> **Nota:** O dataset `zoo_visitors_2023_consolidada.xlsx` (Zoológico de Helsinque, 2023) foi utilizado no desenvolvimento mas não está versionado no repositório.

---

## Tecnologias Utilizadas

| Tecnologia | Finalidade |
|---|---|
| Python 3.x | Linguagem principal |
| Jupyter Notebook | Ambiente de desenvolvimento interativo |
| pandas | Manipulação e análise de dados |
| numpy | Operações numéricas |
| matplotlib | Visualização gráfica |
| seaborn | Visualização estatística |
| scikit-learn | Modelos de ML, pré-processamento e métricas |

**Algoritmos de Machine Learning:**

| Algoritmo | Tipo | Finalidade |
|---|---|---|
| `LinearRegression` | Regressão | Prever o número de visitantes |
| `RandomForestRegressor` | Regressão (Ensemble) | Capturar padrões não-lineares |
| `KNeighborsClassifier` + `GridSearchCV` | Classificação | Classificar períodos por nível de demanda |

---

## Como Executar o Projeto

### Pré-requisitos

- Python 3.8 ou superior
- Jupyter Notebook ou JupyterLab

### 1. Clone o repositório

```bash
git clone https://github.com/depaolii/ML-aplicada-previsao-de-visitantes.git
cd ML-aplicada-previsao-de-visitantes
```

### 2. Instale as dependências

```bash
pip install pandas numpy matplotlib seaborn scikit-learn openpyxl jupyter
```

### 3. Adicione o dataset

Coloque o arquivo `zoo_visitors_2023_consolidada.xlsx` na raiz do repositório (mesmo diretório do notebook). O dataset deve conter as colunas:

| Coluna | Tipo | Descrição |
|---|---|---|
| `date` | datetime | Data do registro |
| `weekday` | categórico | Dia da semana (seg–dom) |
| `visitors` | numérico | Número de visitantes — variável alvo (Y) |
| `month` | numérico | Mês (1–12) |
| `year` | numérico | Ano |
| `is_weekend` | binário | 1 = fim de semana, 0 = dia útil |
| `is_holiday` | binário | 1 = feriado, 0 = dia normal |
| `season` | categórico | Estação (Winter, Spring, Summer, Fall) |
| `visitor_class` | categórico | Classe criada: `low` / `medium` / `high` |

### 4. Execute o notebook

```bash
jupyter notebook "Notebook_acadêmico.ipynb"
```

Execute as células sequencialmente ou use **Kernel → Restart & Run All** para reproduzir o pipeline completo.

---

## Exemplos de Uso

### Previsão com Regressão Linear

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_absolute_error, mean_squared_error, r2_score

model = LinearRegression()
model.fit(X_train, y_train)
y_pred = model.predict(X_test)

print(f"MAE:  {mean_absolute_error(y_test, y_pred):.2f}")
print(f"RMSE: {mean_squared_error(y_test, y_pred, squared=False):.2f}")
print(f"R²:   {r2_score(y_test, y_pred):.3f}")
```

### Classificação de Demanda com KNN + GridSearchCV

```python
from sklearn.neighbors import KNeighborsClassifier
from sklearn.model_selection import GridSearchCV

param_grid = {
    'n_neighbors': [3, 5, 7, 9, 11],
    'weights': ['uniform', 'distance'],
    'metric': ['euclidean', 'manhattan']
}

grid = GridSearchCV(KNeighborsClassifier(), param_grid, cv=5, scoring='f1_macro')
grid.fit(X_train_cls, y_train_cls)

print("Melhores parâmetros:", grid.best_params_)
# Resultado: n_neighbors=7, weights='uniform', metric='euclidean'
```

---

## Conclusão / Resultados Obtidos

### Modelos de Regressão — Previsão de Visitantes

| Modelo | MAE | RMSE | R² |
|---|---|---|---|
| **Regressão Linear** | **544,73** | **808,36** | **0,728** |
| Random Forest | 592,91 | 965,30 | 0,612 |

- A **Regressão Linear** apresentou o melhor desempenho global, explicando **72,8% da variância** no número de visitantes (R² = 0,728) — resultado sólido considerando a volatilidade dos dados.
- O **Random Forest** (1.000 árvores) captura bem picos e baixos de visitação, mas com maior RMSE, sugerindo que a relação entre as features e a variável alvo é predominantemente linear.

### Modelo de Classificação — KNN (Otimizado)

| Classe | Precision | Recall | F1-Score |
|---|---|---|---|
| `high` | 0,70 | 0,84 | 0,76 |
| `low` | 0,65 | 0,92 | 0,76 |
| `medium` | 0,67 | 0,25 | 0,36 |
| **Acurácia Geral** | | | **67%** |

- O KNN acerta com consistência os extremos (**alta** e **baixa** demanda), o que é o mais relevante para planejamento operacional.
- A classe **medium** (recall de 25%) é a mais difícil de identificar — comportamento esperado em problemas de classificação com categorias limítrofes.

### Principais Insights

1. **Mês e estação do ano** são os fatores mais determinantes para o volume de visitantes
2. Fins de semana e feriados aumentam o fluxo, porém com impacto menor que o esperado inicialmente
3. **Dias de demanda média são os mais difíceis de prever**, indicando que variáveis adicionais (clima real, eventos especiais, campanhas de marketing) podem aumentar significativamente a acurácia
4. Os modelos permitem ao **Totem Inteligente FlexMedia** antecipar modos de operação (normal, interativo ou pico) com base na data, dia da semana e estação do ano
5. Recomenda-se coletar dados complementares em sprints futuras para evoluir o pipeline e reduzir o erro nas previsões de dias com demanda intermediária

---

## Autores

Projeto desenvolvido como atividade acadêmica da disciplina de **Machine Learning Aplicada**.
