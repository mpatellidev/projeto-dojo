# Documentação do projeto

## Objetivo

O projeto analisa dados de imóveis e treina um modelo de regressão para prever preços.
O fluxo foi mantido curto, sequencial e baseado em recursos conhecidos das bibliotecas usadas.

## Ordem de execução

1. Execute `notebook/tratamento.ipynb` para limpar e exportar `dataset/limpo.csv`.
2. Execute `notebook/EDA.ipynb` para conhecer os dados por tabelas e gráficos.
3. Execute `notebook/machine-learning.ipynb` para treinar e avaliar o modelo.

## Tratamento

São removidos valores ausentes, duplicados e registros com medidas essenciais não positivas.
Também é removido o 1% de preços mais extremos, reduzindo a influência de valores muito distantes.

Nenhuma coluna é criada, removida ou renomeada durante a limpeza.
A base final possui 4.503 registros e as mesmas 18 colunas da base original.

## Análise exploratória

A EDA apresenta resumo numérico, histograma, dispersão, barras, boxplot e correlação.
Os gráficos usam instruções diretas, sem cópias da base, filtros escondidos ou laços automáticos.

## Preparação do modelo

O alvo é `price`; `date`, `street` e `price_per_sqft` não entram no treino.
As colunas `city` e `statezip` são codificadas com `pd.get_dummies` sem alterar a base salva.

Os dados são separados em 80% para treino e 20% para teste.
O `StandardScaler` é ajustado no treino e aplicado somente às variáveis numéricas.

## Modelo e tunagem

O `RandomForestRegressor` combina várias árvores e calcula a média de suas previsões.
Ele representa relações não lineares sem exigir fórmulas ou transformações complexas.

O `GridSearchCV` testa oito combinações com validação cruzada de três partes.
São ajustados número de árvores, profundidade máxima e mínimo de amostras para divisão.

## Resultado

| Métrica | Resultado |
| --- | ---: |
| MAE | 92.400,79 |
| RMSE | 149.843,86 |
| R² | 0,716 |

O MAE indica um erro médio de cerca de 92 mil unidades monetárias.
O R² indica que o modelo explica aproximadamente 71,6% da variação dos preços de teste.
Essas métricas representam os 99% de imóveis mantidos e não o grupo de preços mais extremos.
