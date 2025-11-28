# Previsão de Custos de Infraestrutura Cloud Utilizando Modelos Baseados em Métricas Reais

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

---

# Modelo Conceitual

O custo total de infraestrutura cloud é influenciado diretamente por métricas de uso como CPU, memória, volume de requisições e armazenamento.  
Modelos matemáticos podem prever esse custo futuro com base em padrões históricos.  
Assim, o tipo de modelo de previsão influencia o erro predito, sendo o principal foco do experimento.

---

# Hipóteses

### Hipótese Nula (H0)
Não existe diferença significativa na precisão entre os modelos de previsão analisados.

### Hipótese Alternativa (H1)
Existe diferença significativa na precisão entre os modelos de previsão.

### Hipóteses específicas:
- **H1.1:** A regressão linear apresenta erro diferente dos modelos de séries temporais.  
- **H1.2:** ARIMA apresenta menor erro em comparação com modelos simples.  
- **H1.3:** O exponential smoothing gera previsões mais estáveis em dados com tendência.  

---

# Variáveis

### Variáveis Independentes (Fatores)
- Modelo de previsão utilizado.

### Variáveis Dependentes
- MAE (Mean Absolute Error)  
- RMSE (Root Mean Square Error)  
- MAPE (Erro percentual)  
- Erro de validação (dados fora do treino)

### Variáveis de Controle
- Mesma série temporal de entrada.  
- Período analisado.  
- Mesmas métricas utilizadas (CPU, requisições etc.).  
- Mesma janela de amostragem.

---

# Tabela 1 – Variáveis e Descrições

| Variável | Tipo | Descrição |
|----------|------|------------|
| Modelo de Previsão | Independente | Modelo aplicado: regressão linear, média móvel, ARIMA, exponential smoothing |
| MAE | Dependente | Erro absoluto médio entre valor real e previsto |
| RMSE | Dependente | Raiz do erro quadrático médio |
| MAPE | Dependente | Erro percentual médio |
| Erro de Validação | Dependente | Acurácia em dados nunca utilizados no treino |
| CPU Média | Controle | % médio de processamento |
| Requisições | Controle | Número de requisições por período |
| Armazenamento | Controle | Volume em GB |
| Memória | Controle | Consumo médio em MB |
| Janela Temporal | Controle | Período usado na previsão (ex.: últimos 7 dias) |

---

# Fatores e Tratamentos

### Fator Principal
**Modelo de previsão**

### Tratamentos:
- **T1:** Regressão Linear  
- **T2:** Média Móvel  
- **T3:** ARIMA  
- **T4:** Exponential Smoothing  

---

# Tabela 2 – Fatores, Tratamentos e Combinações

| Fator | Tratamento | Descrição |
|-------|------------|-----------|
| Modelo | T1 | Regressão Linear |
| Modelo | T2 | Média Móvel Simples |
| Modelo | T3 | ARIMA |
| Modelo | T4 | Exponential Smoothing |

Como há apenas um fator, existem **4 combinações possíveis**.

---

# Desenho Experimental

### Tipo de desenho:
**Desenho completamente aleatorizado**, com repetição de experimentos para reduzir variância.

### Etapas do experimento:

1. Coletar métricas reais de consumo cloud (CPU, requisições, storage).  
2. Montar dataset histórico com custo real por período.  
3. Dividir dataset em treino (70%) e validação (30%).  
4. Aplicar cada modelo de previsão sobre os mesmos dados.  
5. Gerar séries previstas.  
6. Medir MAE, RMSE, MAPE e erro de validação.  
7. Repetir o experimento com diferentes janelas temporais:  
   - 7 dias  
   - 14 dias  
   - 30 dias  
8. Comparar resultados utilizando ANOVA ou testes estatísticos equivalentes.  
9. Validar hipóteses:  
   - Se p < 0.05 → rejeita H0, modelos são significativamente diferentes.

---
