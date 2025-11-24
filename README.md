# Entrega 2 – Escopo e Estrutura

## Escopo
Desenvolver e avaliar modelos de previsão de custos cloud utilizando métricas reais de uso de infraestrutura, comparando algoritmos simples (média móvel, regressão linear) e técnicas de séries temporais (ARIMA, exponential smoothing).

---

## Objetivo Geral
Criar um modelo de previsão de custos cloud com base em métricas reais, analisando sua acurácia em diferentes cenários.

---

## Objetivos Específicos
1. Coletar métricas reais de uso (CPU, memória, requisições, armazenamento).  
2. Construir pelo menos três modelos de previsão.  
3. Avaliar a acurácia dos modelos.  
4. Comparar qual modelo apresenta menor erro médio absoluto.  
5. Identificar variáveis que mais impactam o custo final.

---

## Stakeholders
- **Empresas:** redução de gastos inesperados.  
- **DevOps:** planejamento de escalabilidade e otimização.  
- **Desenvolvedores:** compreensão do impacto financeiro das decisões técnicas.  
- **Times financeiros:** previsões mais confiáveis.

---

## Riscos
- Coleta de dados insuficiente.  
- Inconsistência no período analisado.  
- Custos reais variando por mudanças externas (ex.: promoções, regiões).  
- Modelos matemáticos com baixo poder preditivo.

---

## Premissas
- Dados de uso serão coletados de forma estruturada.  
- Período analisado representará o comportamento típico do sistema.  
- O cálculo de custo será feito com base nas tabelas oficiais dos provedores.  

---

## Critérios de Sucesso
- Gerar pelo menos três modelos funcionais.  
- Identificar o modelo com menor erro.  
- Atingir erro médio < 20% em ao menos um modelo.  
- Demonstrar relação entre métricas e custos.

---

# Tabela GQM

| Objetivo | Perguntas | Métricas |
|----------|-----------|----------|
| O1: Criar modelo de previsão | Q1: Qual modelo apresenta menor erro? | M1: MAE |
| | Q2: Como o modelo se comporta em diferentes janelas? | M2: RMSE |
| O2: Avaliar variáveis | Q3: Quais métricas mais influenciam o custo? | M3: Correlação (%) |
| | Q4: Como variações de tráfego afetam o custo? | M4: Custo por requisição |
| O3: Validar precisão | Q5: O modelo generaliza para novos períodos? | M5: Erro de validação (%) |
| O4: Comparar modelos | Q6: Algum modelo apresenta overfitting? | M6: Diferença treino/teste |

---

# Tabela de Métricas

| Métrica | Descrição | Unidade |
|--------|-----------|---------|
| M1 | Mean Absolute Error | valor |
| M2 | Root Mean Square Error | valor |
| M3 | Correlação entre variável e custo | % |
| M4 | Custo médio por requisição | R$ |
| M5 | Erro de validação cruzada | % |
| M6 | Diferença treino/teste | % |
| M7 | Consumo médio de CPU | % |
| M8 | Consumo médio de memória | MB |
| M9 | Volume de armazenamento | GB |
| M10 | Quantidade de requisições | req/s |

