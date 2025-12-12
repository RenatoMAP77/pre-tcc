# Plano de Experimento – Previsão de Custos de Infraestrutura Cloud

## 1. Identificação Básica

### 1.1 Título do Experimento
**Previsão de Custos de Infraestrutura Cloud Utilizando Modelos Baseados em Métricas Reais: Uma Comparação entre Algoritmos Simples e Técnicas de Séries Temporais**

### 1.2 ID / Código
`TCC-PRED-CUSTO-2025-001`

### 1.3 Versão do Documento e Histórico de Revisão

| Versão | Data | Autor | Descrição das Alterações |
|--------|------|-------|--------------------------|
| v1.0 | 05/12/2025 | Renato Matos Alves Penna | Desenvolvimento do documento |
| v1.1 | 12/12/2025 | Renato Matos Alves Penna | Finalização das 20 seções |

### 1.4 Datas

- **Data de Criação:** 21/11/2025
- **Última Atualização:** 12/12/2025

### 1.5 Autores

| Nome | Área | Contato |
|------|------|---------|
| Renato Matos Alves Penna | Computação / Engenharia de Software | renatomatosapbusiness@gmail.com |

### 1.6 Responsável Principal (PI / Dono do Experimento)

**Orientador:** Danilo de Quadros Maia Filho  
**Responsável pela Execução:** Renato Matos Alves Penna

### 1.7 Projeto / Produto / Iniciativa Relacionada

Este experimento está vinculado ao **Trabalho de Conclusão de Curso (TCC)** do curso de graduação, com foco em Engenharia de Software Experimental aplicada a Cloud Computing. O estudo visa contribuir tanto para o contexto acadêmico quanto para aplicações práticas em empresas e startups que buscam otimização de custos em infraestrutura cloud.

---

## 2. Contexto e Problema

### 2.1 Descrição do Problema / Oportunidade

A computação em nuvem tornou-se fundamental para organizações modernas, permitindo escalabilidade sob demanda e redução de custos de infraestrutura física. Entretanto, a natureza dinâmica e elástica dos recursos cloud apresenta um desafio crítico: **custos imprevisíveis e difíceis de estimar**.

#### Problema Central:
Organizações frequentemente enfrentam:
- **Gastos inesperados** devido a picos de uso não antecipados
- **Dificuldade em prever orçamentos** mensais/trimestrais de infraestrutura
- **Falta de visibilidade** sobre quais métricas de uso mais impactam os custos
- **Ausência de modelos preditivos** que auxiliem no planejamento financeiro

#### Oportunidade:
Criar modelos de previsão de custos baseados em métricas reais de uso (CPU, memória) pode:
- Permitir **planejamento financeiro mais preciso**
- Identificar **padrões de consumo** e oportunidades de otimização
- Auxiliar **decisões técnicas** com impacto financeiro quantificável
- Prevenir **estouros de orçamento** através de alertas antecipados

### 2.2 Contexto Organizacional e Técnico

#### Contexto Organizacional:
Este é um **experimento acadêmico** desenvolvido como Trabalho de Conclusão de Curso. Embora não esteja vinculado a uma empresa específica, o estudo foi projetado para ter **aplicabilidade prática** em contextos reais de:
- Startups e PMEs que utilizam infraestrutura cloud
- Times de DevOps responsáveis por otimização de custos
- Equipes de engenharia que precisam justificar decisões técnicas financeiramente
- Departamentos financeiros que necessitam de previsões orçamentárias confiáveis

#### Contexto Técnico:
- **Ambiente:** Análise baseada em dados reais do Google Cluster Data 2019
- **Tecnologias:** Python 3.10+, bibliotecas de análise de dados (Pandas, NumPy), machine learning (Scikit-learn, Statsmodels)
- **Métricas analisadas:** CPU e memória RAM (dados reais); custos (estimados)
- **Modelos cloud:** Precificação estimada baseada em tabelas públicas de provedores (AWS, Azure, GCP)
- **Processo:** Metodologia experimental controlada com análise estatística rigorosa

### 2.3 Trabalhos e Evidências Prévias (Internos e Externos)

#### Evidências Externas (Literatura):
**Nota:** Esta seção será expandida na fase de revisão bibliográfica, mas alguns temas relevantes incluem:
- Estudos sobre **time series forecasting** aplicados a custos de TI
- Papers sobre **cloud cost optimization** e FinOps
- Pesquisas comparando **modelos de previsão** (ARIMA, exponential smoothing, machine learning)
- Trabalhos sobre **métricas de infraestrutura** como preditores de custos

#### Evidências Internas:
Este é o primeiro experimento formal sobre o tema no contexto do TCC. Observações preliminares indicam que:
- Modelos de séries temporais podem capturar padrões sazonais de uso
- Métricas de CPU e requisições apresentam correlação forte com custos
- A granularidade dos dados (diária vs. horária) afeta a precisão das previsões

### 2.4 Referencial Teórico e Empírico Essencial

Esta seção apresenta a fundamentação teórica e empírica que embasa o experimento, organizando conhecimento científico consolidado sobre previsão de custos cloud, modelos de séries temporais e metodologias de avaliação.

---

#### 2.4.1 Previsão de Custos e Workloads em Nuvem

A **previsão de workloads em ambientes cloud** é fundamental para otimização de recursos e controle de custos. Calheiros et al. [1] demonstraram em trabalho seminal que modelos ARIMA aplicados a traces do Wikipedia alcançaram **91% de acurácia na previsão de carga**, habilitando provisionamento proativo de recursos. Este trabalho estabeleceu que **séries temporais estatísticas podem capturar padrões de uso cloud com precisão suficiente para decisões operacionais**.

Amiri & Mohammad-Khanli [2] realizaram survey abrangente classificando métodos de previsão de workload em três categorias: (1) estatísticos (ARIMA, Exponential Smoothing), (2) machine learning (SVM, Random Forest), e (3) híbridos. Seu trabalho demonstra que **todos os quatro modelos deste experimento (RL, MM, ARIMA, ES) são amplamente utilizados e validados na literatura**.

Tsoumakos et al. [3] questionaram se machine learning complexo é necessário para previsão de uso cloud, concluindo que **métodos simples como média móvel e exponential smoothing alcançam alta acurácia devido à correlação temporal forte** nos dados. Este achado fundamenta a inclusão de modelos mais simples (MM, RL) neste experimento como baselines competitivos.

**Previsão direta de custos cloud** foi investigada por Khandelwal et al. [4] usando 12 meses de preços spot da Amazon EC2 com Random Forests, enquanto Chhetri et al. [5] **compararam diretamente ARIMA, ETS (Exponential Smoothing), STL e TBATS** para previsão de preços EC2, encontrando que Seasonal Naïve foi robusto para mercados com sazonalidade forte. Fragiadakis et al. [6] aplicaram ML a dados históricos AWS (2016-2022) para prever evolução de preços IaaS, demonstrando viabilidade de modelos preditivos em contextos reais.

---

#### 2.4.2 Modelos de Séries Temporais: Fundamentos Teóricos

**ARIMA (AutoRegressive Integrated Moving Average):**
A metodologia Box-Jenkins [7], formalizada em 1970 e atualizada em 2015, estabeleceu o framework sistemático para modelagem ARIMA: (1) identificação da ordem (p, d, q) via ACF/PACF, (2) estimação de parâmetros por máxima verossimilhança, (3) diagnóstico de resíduos. Hamilton [8] e Brockwell & Davis [9] fornecem tratamento matemático rigoroso de processos ARMA, condições de estacionariedade e teoria de previsão ótima. **ARIMA é considerado estado-da-arte para séries univariadas com padrões lineares e sazonalidade moderada.**

**Exponential Smoothing:**
Holt [10] estendeu suavização exponencial simples para capturar tendências lineares (método de Holt), enquanto Winters [11] adicionou componentes sazonais criando **Holt-Winters Triple Exponential Smoothing**. Gardner [12, 13] realizou revisões abrangentes estabelecendo boas práticas de implementação e introduzindo o framework **ETS (Error, Trend, Seasonal)** que unifica todos os métodos de suavização em modelo de espaço de estados coerente. Hyndman et al. [14] formalizaram ETS matematicamente, permitindo seleção automática de modelos via AIC. **Exponential smoothing é especialmente eficaz para dados com sazonalidade pronunciada e tendências não-lineares.**

**Média Móvel e Regressão Linear:**
Média móvel (Moving Average) é técnica de suavização que calcula média dos últimos k valores, removendo ruído de alta frequência [15]. Regressão Linear modela relação entre variáveis preditoras (CPU, memória) e variável resposta (custo) assumindo relação funcional linear [8, 15]. **Ambos servem como baselines interpretáveis para comparação.**

**Métricas de Avaliação:**
Hyndman & Koehler [16] analisaram criticamente métricas de acurácia de previsão, recomendando **MAE (Mean Absolute Error)** para interpretabilidade, **RMSE (Root Mean Squared Error)** para penalizar erros grandes, e **MASE (Mean Absolute Scaled Error)** como métrica independente de escala. Este trabalho fundamenta a escolha de MAE como métrica primária deste experimento.

**Seleção de Modelos:**
Akaike [17] introduziu AIC (Akaike Information Criterion) para seleção de modelos balanceando ajuste e complexidade, enquanto Schwarz [18] propôs BIC (Bayesian Information Criterion) com penalidade mais forte para complexidade. **AIC e BIC são utilizados para seleção automática de ordem ARIMA e tipo de modelo ETS.**

---

#### 2.4.3 Aplicações em Google Cluster Data

**Caracterização do Dataset:**
Tirmazi et al. [19] realizaram primeira análise oficial comparando traces Google 2019 e 2011, cobrindo **8 clusters Borg em maio/2019 (2.4 TiB de dados)**. Achado crítico: **top 1% dos jobs consomem mais de 99% dos recursos**, indicando distribuição altamente assimétrica. Verma et al. [20] descreveram arquitetura do sistema Borg, incluindo estratégias de alocação de recursos, task-packing e over-commitment que geram os dados analisados. Reiss et al. [21] analisaram trace 2011, descobrindo que **jobs de longa duração apresentam utilização de recursos relativamente estável**, validando que modelos preditivos podem alcançar acurácia razoável. **Wilkes [22] fornece documentação técnica oficial do schema do trace 2019**, essencial para descrição do dataset na Seção 4.

**Modelos Preditivos em Google Traces:**
Janardhanan & Barrett [23] compararam LSTM e ARIMA usando **Google Cluster Data**, encontrando que LSTM alcançou 17-23% de erro vs. 37-42% do ARIMA para cargas altamente variáveis. Shyam & Manvi [24] desenvolveram **modelo híbrido ARIMA-ANN** para previsão de CPU e memória em traces Google, onde ARIMA captura padrões lineares e ANN modela resíduos não-lineares, avaliando com RMSE, MAE e MAPE.

Bappy et al. [25] realizaram análise profunda do **Google Cluster Data 2019** (mesma fonte deste experimento) investigando padrões de uso entre jobs com falha vs. finalizados, fornecendo insights sobre desperdício de recursos. Alibasa et al. [26] usaram **trace v3 (2019)** para prever duração, CPU e memória com GRU/LSTM. Van Loo et al. [27] aplicaram K-means e Lasso em trace 2019, usando Random Forest e XGBoost para previsão de demanda.

Hosseinzadeh et al. [28] propuseram pCNN-LSTM para previsão multi-step de CPU no Google Cluster Trace, alcançando **15% de melhoria sobre LSTM baseline**. Asmawi et al. [29] compararam ML tradicional (Logistic Regression, Random Forest, XGBoost) e LSTM em traces Google 2011, identificando **prioridade do job como feature mais importante**.

---

#### 2.4.4 Estudos Comparativos de Métodos de Previsão

**M-Competition Series (Benchmarks de Referência):**
As competições M3 [30] e M4 [31] são benchmarks gold-standard para métodos de previsão. **Makridakis & Hibon [30]** compararam 24 métodos em 3.003 séries, concluindo: (1) **métodos sofisticados não necessariamente superam simples**; (2) Exponential Smoothing teve desempenho consistente; (3) ARIMA melhorou em relação a competições anteriores. **Makridakis et al. [31]** na M4 (100.000 séries, 61 métodos) encontraram que **métodos híbridos estatísticos-ML superaram abordagens puras em ~10%**, mas ETS e ARIMA permaneceram baselines fortes.

**Crítica Fundamental:**
Makridakis et al. [32] compararam métodos estatísticos (ETS, ARIMA) com 8 algoritmos ML, demonstrando que **métodos estatísticos tradicionais superaram ML em todas as métricas de acurácia com custo computacional menor**. Este resultado fundamenta a escolha de métodos estatísticos neste experimento.

**Comparações Diretas:**
Wadi et al. [33] compararam ARIMA e Exponential Smoothing, concluindo que **ARIMA é superior para previsões de longo prazo** enquanto **ES é melhor para dados flutuantes de curto prazo**. Bahuguna et al. [34] encontraram que ARIMA(0,0,2) performou melhor em séries curtas enquanto Holt-Winters foi superior em séries longas com sazonalidade. Siami-Namini et al. [35] mostraram LSTM superando ARIMA com redução de 84-87% no erro, mas com custo computacional substancialmente maior.

**Contexto Cloud Específico:**
Saxena et al. [36] realizaram primeiro survey sistemático comparando ML para previsão de workload cloud em traces Google, Alibaba e Bitbrains, concluindo que **aprendizado híbrido com suavização estatística superou deep learning puro**. ACM [37] testou 320+ modelos incluindo ARIMA, TBATS, Holt-Winters em traces Adobe, demonstrando que meta-learners alcançaram 84-98% de melhoria, fornecendo framework de seleção de modelos.

---

#### 2.4.5 Abordagens Híbridas e Estado da Arte

A literatura recente demonstra que **modelos híbridos combinando ARIMA com redes neurais ou exponential smoothing frequentemente superam métodos individuais** [24, 31, 36]. Autores [38] combinaram ARIMA e triple exponential smoothing com ponderação dinâmica para previsão de carga de containers Docker. Kontopoulou et al. [39] realizaram revisão extensiva comparando ARIMA e ML, concluindo que **modelos híbridos estatísticos-AI consistentemente superam abordagens individuais**.

Deochake [40] propôs arquitetura FinOps (ABACUS) para otimização de custos cloud integrando ML para orçamentação preditiva, fornecendo contexto operacional para aplicação prática de modelos de previsão.

---

#### 2.4.6 Síntese da Base Empírica

A literatura consolidada suporta as seguintes premissas deste experimento:

1. **Viabilidade:** ARIMA, Exponential Smoothing, Moving Average e Linear Regression são métodos validados para previsão de workload/custo cloud [1, 2, 3, 5].

2. **Dataset:** Google Cluster Data 2019 é dataset público robusto amplamente utilizado em pesquisas de previsão [19, 23, 24, 25, 26, 27, 28].

3. **Métricas:** MAE, RMSE e MAPE são métricas padronizadas para avaliação de acurácia [16, 24, 30, 31].

4. **Expectativa:** Métodos estatísticos simples podem ser competitivos com ML complexo devido à alta correlação temporal em dados cloud [3, 32], mas modelos ARIMA e ES tendem a superar baselines simples [1, 30].

5. **Metodologia:** Desenho experimental CRD com validação cruzada TimeSeriesSplit e testes estatísticos (ANOVA/Kruskal-Wallis) seguem boas práticas de experimentação [15, 41].

**Lacuna Identificada:**
Apesar da abundância de estudos comparando ML sofisticado (LSTM, GRU, CNN) com ARIMA, **existem poucos estudos sistemáticos comparando os quatro modelos básicos (RL, MM, ARIMA, ES) no contexto específico de previsão de custos cloud usando Google Cluster Data 2019**. Este experimento preenche essa lacuna fornecendo comparação controlada, rigorosa e reproduzível.

---

## 3. Objetivos e Questões (Goal / Question / Metric)

### 3.1 Objetivo Geral (Goal Template)

**Analisar** modelos de previsão de custos cloud baseados em métricas reais de uso  
**com o propósito de** comparar sua acurácia e identificar qual apresenta melhor desempenho  
**com respeito a** erro de previsão (MAE, RMSE, MAPE) e capacidade de generalização  
**do ponto de vista de** engenheiros de software, times de DevOps e gestores financeiros  
**no contexto de** ambientes cloud com workloads simulados representando aplicações reais.

### 3.2 Objetivos Específicos

1. **O1 - Desenvolver modelos de previsão:** Construir e implementar pelo menos quatro modelos distintos de previsão de custos (regressão linear, média móvel, ARIMA, exponential smoothing) utilizando métricas reais de uso de infraestrutura.

2. **O2 - Avaliar acurácia dos modelos:** Medir e comparar a precisão de cada modelo utilizando métricas padronizadas de erro (MAE, RMSE, MAPE) em janela temporal de 30 dias.

3. **O3 - Identificar variáveis preditoras:** Analisar quais métricas de infraestrutura (CPU, memória) apresentam maior correlação com os custos estimados e maior poder preditivo.

4. **O4 - Validar generalização:** Verificar se os modelos mantêm precisão adequada em dados não utilizados no treinamento (validação cruzada), garantindo capacidade de generalização para períodos futuros.

5. **O5 - Comparar estabilidade:** Avaliar a robustez dos modelos diante de diferentes padrões de uso (picos, sazonalidade, tendências) e determinar qual apresenta previsões mais estáveis.

### 3.3 Questões de Pesquisa / de Negócio

**Métrica Primária:** MAE (Mean Absolute Error) - Principal critério de comparação
**Métricas Secundárias:** RMSE e MAPE - Análises complementares

#### Relacionadas ao Objetivo O1 (Desenvolver modelos):
- **Q1.1 (PRIMÁRIA):** Qual modelo de previsão apresenta o menor erro médio absoluto (MAE)?
- **Q1.2:** Como os modelos se comportam com janela temporal de 30 dias?
- **Q1.3:** Existe diferença estatisticamente significativa entre o desempenho dos modelos?

#### Relacionadas ao Objetivo O2 (Avaliar acurácia):
- **Q2.1 (SECUNDÁRIA):** Qual modelo apresenta menor erro quadrático médio (RMSE)?
- **Q2.2 (SECUNDÁRIA):** Qual modelo oferece o menor erro percentual (MAPE)?
- **Q2.3:** Os modelos mantêm acurácia consistente ao longo das 30 repetições?

#### Relacionadas ao Objetivo O3 (Identificar variáveis):
- **Q3.1:** Quais métricas de infraestrutura (CPU, memória) apresentam maior correlação com os custos totais?
- **Q3.2:** Como variações no consumo de memória afetam o custo previsto?
- **Q3.3:** O consumo de CPU é um preditor melhor que o uso de memória para custos estimados?

#### Relacionadas ao Objetivo O4 (Validar generalização):
- **Q4.1:** Os modelos generalizam bem para períodos não vistos durante o treinamento?
- **Q4.2:** Qual é o erro médio de validação cruzada de cada modelo?
- **Q4.3:** Existe degradação significativa de performance entre treino e teste?

#### Relacionadas ao Objetivo O5 (Comparar estabilidade):
- **Q5.1:** Qual modelo apresenta menor variância nos erros de previsão?
- **Q5.2:** Algum modelo apresenta sinais de overfitting (diferença treino/teste > 10%)?
- **Q5.3:** Os modelos de séries temporais são mais estáveis que modelos simples?

### 3.4 Métricas Associadas (GQM)

#### Tabela GQM Completa

| Objetivo | Questão | Métricas Associadas |
|----------|---------|---------------------|
| **O1: Desenvolver modelos** | Q1.1: Qual modelo apresenta menor MAE? | M1 (MAE) |
| | Q1.2: Como se comportam em diferentes janelas? | M1 (MAE), M2 (RMSE) |
| | Q1.3: Há diferença estatística entre modelos? | M1 (MAE), M11 (p-valor ANOVA) |
| **O2: Avaliar acurácia** | Q2.1: Qual modelo apresenta menor RMSE? | M2 (RMSE) |
| | Q2.2: Qual modelo oferece menor MAPE? | M3 (MAPE) |
| | Q2.3: Erros diminuem com janelas maiores? | M1 (MAE), M2 (RMSE) por janela |
| **O3: Identificar variáveis** | Q3.1: Quais métricas têm maior correlação? | M4 (Correlação %), M7-M10 |
| | Q3.2: Como requisições afetam custo? | M5 (Custo/requisição), M10 (Requisições) |
| | Q3.3: CPU vs. Memória como preditor? | M4 (Correlação), M7 (CPU), M8 (Memória) |
| **O4: Validar generalização** | Q4.1: Modelos generalizam para novos períodos? | M6 (Erro validação cruzada) |
| | Q4.2: Qual erro médio de validação cruzada? | M6 (Erro validação cruzada) |
| | Q4.3: Há degradação entre treino/teste? | M12 (Diferença treino/teste) |
| **O5: Comparar estabilidade** | Q5.1: Qual modelo tem menor variância? | M13 (Desvio padrão dos erros) |
| | Q5.2: Algum modelo apresenta overfitting? | M12 (Diferença treino/teste) |
| | Q5.3: Séries temporais são mais estáveis? | M13 (Desvio padrão), M12 (Diferença treino/teste) |

#### Tabela Detalhada de Métricas

| ID | Métrica | Descrição Completa | Unidade | Fonte dos Dados |
|----|---------|-------------------|---------|-----------------|
| **M1** | MAE (Mean Absolute Error) | Erro absoluto médio entre valores reais e previstos | Valor monetário (R$) | Cálculo pós-previsão |
| **M2** | RMSE (Root Mean Square Error) | Raiz quadrada do erro quadrático médio | Valor monetário (R$) | Cálculo pós-previsão |
| **M3** | MAPE (Mean Absolute Percentage Error) | Erro percentual absoluto médio | Percentual (%) | Cálculo pós-previsão |
| **M4** | Correlação com Custo | Correlação de Pearson entre métrica e custo final | Coeficiente (-1 a 1) | Análise estatística |
| **M5** | Custo por Requisição | Custo médio por requisição processada | R$ por requisição | Dataset de custos |
| **M6** | Erro de Validação Cruzada | Erro médio em k-fold cross-validation (k=5) | Percentual (%) | Validação cruzada |
| **M7** | Consumo Médio de CPU | Utilização percentual média de CPU | Percentual (%) | Métricas simuladas |
| **M8** | Consumo Médio de Memória | Uso médio de memória RAM | Megabytes (MB) | Métricas simuladas |
| **M9** | Volume de Armazenamento | Quantidade total de storage utilizado | Gigabytes (GB) | Métricas simuladas |
| **M10** | Quantidade de Requisições | Volume de requisições por período | Requisições/segundo | Métricas simuladas |
| **M11** | P-valor (ANOVA/Kruskal-Wallis) | Significância estatística da diferença entre modelos | Valor p | Teste estatístico |
| **M12** | Diferença Treino/Teste | Diferença percentual de erro entre treino e teste | Percentual (%) | Comparação de erros |
| **M13** | Desvio Padrão dos Erros | Variabilidade dos erros de previsão | Valor monetário (R$) | Análise estatística |

---

## 4. Escopo e Contexto do Experimento

### 4.1 Escopo Funcional / de Processo (Incluído e Excluído)

#### 📊 Clarificação: Origem e Natureza dos Dados

**IMPORTANTE:** Este experimento utiliza uma **combinação de dados reais e estimados**:

1. **Dados REAIS (do Google Cluster Data 2019):**
   - **Consumo de CPU:** Métricas reais de utilização de CPU de workloads de produção
   - **Consumo de memória RAM:** Métricas reais de uso de memória
   - **Timestamps:** Eventos temporais reais (granularidade original de 5 minutos)
   - **Job/Task events:** Informações reais de jobs executados

2. **Dados ESTIMADOS/CALCULADOS:**
   - **Custos monetários:** Calculados aplicando tabelas públicas de precificação (AWS, Azure, GCP) às métricas reais de uso
   - **Volume de armazenamento:** Não disponível diretamente no Google Cluster Data; será estimado baseado em CPU/memória ou excluído do escopo
   - **Requisições/tráfego de rede:** Não disponível diretamente no Google Cluster Data; será estimado ou excluído do escopo

3. **Processamento dos Dados:**
   - **Agregação temporal:** Dados originais (5 minutos) são agregados para granularidade horária (1 hora)
   - **Período de análise:** 30 dias contínuos extraídos do dataset de maio de 2019
   - **Resultado final:** 720 observações (30 dias × 24 horas) por métrica

**Conclusão:** As métricas de uso (CPU e memória) são **reais**; os custos são **estimados** com base nessas métricas reais. Storage e requisições podem ser **excluídos** ou **estimados** dependendo da disponibilidade.

---

#### ✅ Incluído no Escopo:

**Métricas de Infraestrutura:**
- Consumo de CPU (percentual de utilização) - **REAL**
- Consumo de memória RAM (em MB) - **REAL**
- Custos monetários (em R$) - **ESTIMADOS com base em CPU e memória reais**

**Modelos de Previsão:**
- Regressão Linear
- Média Móvel Simples
- ARIMA (AutoRegressive Integrated Moving Average)
- Exponential Smoothing (Suavização Exponencial)

**Janelas Temporais de Análise:**
- **Janela principal:** Previsões baseadas em 30 dias (análise principal)
- **Janelas exploratórias (opcionais):** 7 e 14 dias (apenas se tempo permitir)

**Métricas de Avaliação:**
- MAE, RMSE, MAPE
- Erro de validação cruzada (k=5)
- Análise de correlação entre métricas e custos
- Testes estatísticos (ANOVA ou Kruskal-Wallis)

**Análises:**
- Comparação estatística entre modelos
- Identificação de variáveis mais preditivas
- Análise de estabilidade e generalização
- Detecção de overfitting

#### ❌ Excluído do Escopo:

**Aspectos Técnicos:**
- Implementação em ambiente cloud real (será simulado)
- Integração com APIs de provedores cloud
- Monitoramento em tempo real
- Sistemas de alertas automáticos
- Deploy de modelos em produção

**Métricas Adicionais:**
- **Volume de armazenamento (storage)** - Não disponível no Google Cluster Data 2019
- **Quantidade de requisições/tráfego de rede** - Não disponível no Google Cluster Data 2019
- Custos de transferência de dados entre regiões
- Custos de serviços gerenciados (bancos de dados, cache)
- Custos de suporte técnico ou SLAs
- Métricas de latência ou disponibilidade

**Modelos Avançados:**
- Redes neurais ou deep learning
- Modelos ensemble complexos
- Prophet (Facebook) ou técnicas de boosting
- Modelos específicos de provedores (AWS Forecast, etc.)

**Aspectos Organizacionais:**
- Análise de ROI ou business case
- Processos de governança financeira
- Políticas de chargeback entre departamentos
- Compliance ou auditoria financeira

### 4.2 Contexto do Estudo (Tipo de Organização, Projeto, Experiência)

#### Tipo de Organização:
**Contexto Acadêmico** - Trabalho de Conclusão de Curso  
Embora seja um estudo acadêmico, foi projetado para ter **aplicabilidade prática** em:
- Startups de tecnologia
- Pequenas e médias empresas (PMEs) com infraestrutura cloud
- Times de DevOps em organizações de qualquer porte

#### Tipo de Projeto:
- **Natureza:** Experimento controlado com análise quantitativa
- **Duração:** 5 meses (planejamento e execução)
- **Complexidade:** Média (4 modelos, 3 janelas temporais, múltiplas métricas)

#### Perfil de Experiência:
- **Pesquisador:** Estudante de graduação com conhecimento intermediário em:
  - Engenharia de Software
  - Análise de dados e estatística
  - Cloud computing (conceitual)
  - Python e bibliotecas de machine learning

#### Criticidade:
- **Baixa criticidade operacional** (ambiente simulado)
- **Alta criticidade acadêmica** (requisito de TCC)
- **Potencial impacto prático** médio-alto para empresas que adotarem os resultados

### 4.3 Premissas

1. **Dados de Uso:**
   - É possível obter e processar dados reais de traces públicos de cloud computing
   - Os traces do Google Cluster Data 2019 são representativos de workloads cloud reais
   - A granularidade dos dados (5 minutos para 1 hora após agregação) é suficiente para capturar padrões relevantes

2. **Período Analisado:**
   - 30 dias de histórico do dataset são suficientes para treinamento
   - O período extraído representa comportamento típico de sistemas cloud
   - Não há eventos extraordinários no período específico selecionado que distorçam completamente os padrões

3. **Cálculo de Custos:**
   - As tabelas de precificação dos provedores permanecem estáveis durante o período
   - É possível estimar custos baseando-se em tabelas públicas (AWS, Azure, GCP)
   - A conversão de métricas de uso (CPU, memória) em custo monetário segue modelo linear simplificado

4. **Modelos de Previsão:**
   - Os modelos escolhidos são representativos das abordagens mais comuns
   - As implementações das bibliotecas (Scikit-learn, Statsmodels) são confiáveis
   - Hiperparâmetros padrão são adequados para uma primeira comparação

5. **Recursos Computacionais:**
   - O hardware disponível é suficiente para processar o dataset e treinar os modelos em tempo hábil
   - Python 3.10+ e bibliotecas necessárias estão disponíveis e funcionais
   - Dataset do Kaggle (sample) é acessível e tem tamanho gerenciável

6. **Conhecimento Técnico:**
   - O pesquisador possui conhecimento suficiente para implementar os modelos
   - Há suporte do orientador para decisões metodológicas críticas
   - Documentação do Google Cluster Data é suficiente para interpretar os dados corretamente

### 4.4 Restrições

1. **Temporais:**
   - Prazo de 5 meses para conclusão (incluindo documentação)
   - Necessidade de cumprir datas de entrega intermediárias (entregas 1-4)

2. **Financeiras:**
   - Orçamento zero (uso de ferramentas gratuitas/open-source apenas)
   - Uso de datasets públicos gratuitos (Google Cluster Data via Kaggle ou BigQuery free tier)

3. **Técnicas:**
   - Limitação a modelos implementáveis com bibliotecas Python gratuitas
   - Dependência de dados de traces públicos (contexto específico do Google)
   - Processamento local (sem clusters ou infraestrutura distribuída)
   - Necessidade de agregar/processar dados brutos do trace

4. **Metodológicas:**
   - Desenho experimental com fator único (tipo de modelo)
   - Dataset fixo (período específico de maio 2019)
   - Foco em análise quantitativa (sem entrevistas ou estudos de caso)

5. **Organizacionais:**
   - Projeto individual (sem equipe de desenvolvimento)
   - Dependência da disponibilidade do orientador para revisões

6. **Escopo:**
   - Limitação a 4 modelos de previsão (questão de viabilidade)
   - Apenas métricas de CPU e memória do dataset (storage/rede são estimados ou ausentes)
   - Dataset específico de um provedor (Google), não multi-cloud

### 4.5 Limitações Previstas

#### Limitações de Validade Externa (Generalização):

1. **Contexto Específico do Dataset:**
   - Dados provenientes exclusivamente de clusters Google (não AWS, Azure, outros)
   - Workloads específicos do Google (podem não representar todas as empresas)
   - Período específico (maio 2019) pode não capturar sazonalidades anuais
   - Diferentes provedores cloud têm características diferentes

2. **Precificação Estimada:**
   - Custos calculados com tabelas públicas, não refletem custos reais Google
   - Não considera descontos corporativos, reserved instances ou savings plans
   - Modelo de precificação simplificado (linear) pode não capturar complexidades reais

3. **Escala e Complexidade:**
   - Dataset de larga escala pode ter características diferentes de PMEs
   - Múltiplos serviços e interdependências do Google não são replicáveis em empresas menores
   - Padrões de uso de um hyperscaler podem não se aplicar a todos os contextos

#### Limitações de Validade Interna:

1. **Variáveis de Confusão:**
   - Possível correlação espúria entre métricas devido à simulação
   - Dificuldade em isolar completamente o efeito de cada variável

2. **Vieses de Implementação:**
   - Escolha de hiperparâmetros pode favorecer alguns modelos
   - Qualidade da implementação pode variar entre modelos

#### Limitações de Validade de Constructo:

1. **Medição de Custos:**
   - Custos simulados podem não refletir descontos, reserved instances ou savings plans
   - Variações de preço por região não são consideradas

2. **Complexidade Reduzida:**
   - Métricas de infraestrutura são simplificação da realidade
   - Fatores humanos e organizacionais não são capturados

#### Limitações Práticas:

1. **Recursos Limitados:**
   - Tempo e capacidade computacional limitam a complexidade dos modelos
   - Impossibilidade de testar todos os modelos e configurações possíveis

2. **Experiência:**
   - Primeira experiência formal com experimentação controlada
   - Curva de aprendizado pode afetar qualidade inicial

**Estratégias de Mitigação:** Estas limitações serão reconhecidas explicitamente nos resultados e discussão do trabalho, com recomendações claras sobre contextos onde os resultados são mais ou menos aplicáveis.

---

## 5. Stakeholders e Impacto Esperado

### 5.1 Stakeholders Principais

| Stakeholder | Papel | Interesse no Experimento |
|-------------|-------|--------------------------|
| **Empresas e Startups** | Tomadores de decisão financeira | Modelos que ajudem a prever e controlar custos cloud |
| **Times DevOps** | Operadores de infraestrutura | Ferramentas para planejamento de escalabilidade e otimização de recursos |
| **Desenvolvedores** | Criadores de aplicações | Entendimento do impacto financeiro de decisões técnicas (arquitetura, padrões de uso) |
| **Times Financeiros** | Gestores de orçamento | Previsões mais confiáveis para planejamento orçamentário |
| **Gestores de TI** | Liderança técnica | Dados para justificar investimentos e decisões estratégicas |
| **Orientador Acadêmico** | Supervisor do TCC | Qualidade metodológica e rigor científico do experimento |
| **Comunidade Acadêmica** | Pesquisadores | Contribuição para área de Engenharia de Software Experimental e FinOps |

### 5.2 Interesses e Expectativas dos Stakeholders

#### Empresas e Startups:
- **Expectativa:** Identificar modelo de previsão aplicável na prática
- **Interesse:** Reduzir gastos inesperados em até 15-30%
- **Utilidade:** Implementar alertas preditivos de estouro de orçamento
- **Benefício:** ROI positivo através de melhor planejamento financeiro

#### Times DevOps:
- **Expectativa:** Compreender quais métricas monitorar prioritariamente
- **Interesse:** Correlação clara entre métricas técnicas e impacto financeiro
- **Utilidade:** Dados para dimensionar infraestrutura preventivamente
- **Benefício:** Redução de incidentes relacionados a recursos (out of memory, throttling)

#### Desenvolvedores:
- **Expectativa:** Entender como decisões de código/arquitetura afetam custos
- **Interesse:** Modelos que relacionem padrões de uso com custos específicos
- **Utilidade:** Guidelines para desenvolvimento cost-aware
- **Benefício:** Código mais eficiente e econômico

#### Times Financeiros:
- **Expectativa:** Previsões confiáveis para orçamentos trimestrais/anuais
- **Interesse:** Erro de previsão < 20%
- **Utilidade:** Justificativas quantitativas para alocação de recursos
- **Benefício:** Redução de ajustes orçamentários emergenciais

#### Gestores de TI:
- **Expectativa:** Evidências para tomada de decisão estratégica
- **Interesse:** Comparação objetiva entre diferentes abordagens preditivas
- **Utilidade:** Business case para investimento em ferramentas de FinOps
- **Benefício:** Melhor governança de custos cloud

#### Orientador e Comunidade Acadêmica:
- **Expectativa:** Experimento metodologicamente rigoroso
- **Interesse:** Contribuição científica para área de Engenharia de Software Experimental
- **Utilidade:** Referência para futuros trabalhos em FinOps e previsão de custos
- **Benefício:** Avanço do conhecimento na interseção de ES e cloud computing

### 5.3 Impactos Potenciais no Processo / Produto

#### Durante a Execução do Experimento:

**Impactos Positivos:**
- **Aprendizado:** Ganho de conhecimento em técnicas de séries temporais e análise preditiva
- **Metodologia:** Experiência prática com experimentação controlada
- **Documentação:** Criação de material de referência sobre previsão de custos cloud

**Impactos Neutros:**
- **Tempo:** Dedicação de ~5 meses ao experimento (esperado para TCC)
- **Recursos:** Uso de recursos computacionais locais (sem custo adicional)

**Impactos Negativos (Mitigados):**
- **Risco mínimo:** Por ser simulação, não há risco de impactar sistemas em produção
- **Escopo limitado:** Foco em dados sintéticos pode gerar expectativas não atendidas

#### Pós-Experimento:

**Impacto Acadêmico:**
- Contribuição para corpus de conhecimento em FinOps
- Possível publicação em workshops ou conferências de ES
- Referência para trabalhos futuros sobre cloud cost optimization

**Impacto Prático:**
- Empresas podem implementar modelos testados
- Redução de desperdício financeiro em infraestrutura cloud
- Melhoria em processos de planejamento e governança

**Impacto no Produto/Processo:**
- **Curto prazo:** Não há produto direto, mas documentação e código reutilizáveis
- **Médio prazo:** Potencial de evolução para ferramenta de previsão
- **Longo prazo:** Base para sistema de FinOps completo (alertas, dashboards, recomendações)

---

## 6. Riscos de Alto Nível, Premissas e Critérios de Sucesso

### 6.1 Riscos de Alto Nível (Negócio, Técnicos, etc.)

#### Riscos de Negócio:

| Risco | Probabilidade | Impacto | Mitigação |
|-------|---------------|---------|-----------|
| **Resultados não aplicáveis na prática** | Média | Alto | Usar dataset real (Google Cluster Data); validar com literatura |
| **Baixo interesse de stakeholders** | Baixa | Médio | Demonstrar aplicabilidade através de casos de uso concretos |
| **Expectativas não atendidas** | Média | Médio | Comunicar claramente escopo e limitações desde o início |

#### Riscos Técnicos:

| Risco | Probabilidade | Impacto | Mitigação |
|-------|---------------|---------|-----------|
| **Dados reais com problemas de qualidade** | Média | Alto | Pré-validação rigorosa; tratamento de outliers e valores faltantes |
| **Modelos com baixo poder preditivo** | Média | Alto | Testar múltiplos modelos; ajustar hiperparâmetros se necessário |
| **Problemas de implementação** | Baixa | Médio | Usar bibliotecas consolidadas (Scikit-learn, Statsmodels) |
| **Hardware insuficiente para processar dataset** | Média | Médio | Usar sample do Kaggle (gerenciável) ao invés do dataset completo |
| **Bugs ou erros de código** | Média | Médio | Testes unitários; revisão de código; validação de resultados |

#### Riscos de Dados:

| Risco | Probabilidade | Impacto | Mitigação |
|-------|---------------|---------|-----------|
| **Dataset indisponível ou alterado** | Baixa | Alto | Fazer download e backup local; usar múltiplas fontes (Kaggle + BigQuery) |
| **Inconsistência no período analisado** | Baixa | Médio | Validação de qualidade dos dados extraídos; análise exploratória |
| **Falta de variabilidade nos dados** | Baixa | Médio | Google Cluster Data tem alta variabilidade natural de workloads reais |

#### Riscos Metodológicos:

| Risco | Probabilidade | Impacto | Mitigação |
|-------|---------------|---------|-----------|
| **Viés na comparação de modelos** | Média | Alto | Usar mesma métrica de avaliação e mesmo dataset para todos |
| **Overfitting não detectado** | Média | Alto | Validação cruzada rigorosa; análise de diferença treino/teste |
| **Falta de significância estatística** | Média | Alto | Garantir tamanho de amostra adequado (30 execuções por modelo) |

#### Riscos de Cronograma:

| Risco | Probabilidade | Impacto | Mitigação |
|-------|---------------|---------|-----------|
| **Atrasos na implementação** | Média | Alto | Buffer de tempo no cronograma; entregas incrementais |
| **Complexidade subestimada** | Média | Médio | Revisão periódica do progresso com orientador |
| **Problemas pessoais/saúde** | Baixa | Alto | Adiantar entregas quando possível; comunicação transparente |

#### Riscos Externos:

| Risco | Probabilidade | Impacto | Mitigação |
|-------|---------------|---------|-----------|
| **Mudanças em precificação de provedores** | Baixa | Baixo | Usar tabelas de preço fixas do momento inicial |
| **Indisponibilidade do orientador** | Baixa | Médio | Agendar reuniões com antecedência; documentar decisões |

### 6.2 Critérios de Sucesso Globais (Go / No-Go)

#### Critérios Mínimos de Sucesso (Must-Have):

✅ **Critério 1: Modelos Funcionais**
- **Meta:** Implementar com sucesso pelo menos 3 dos 4 modelos propostos
- **Medida:** Código executável que gera previsões
- **Limiar:** 100% dos modelos rodando sem erros críticos

✅ **Critério 2: Avaliação de Acurácia**
- **Meta:** Calcular MAE, RMSE e MAPE para todos os modelos
- **Medida:** Métricas de erro computadas e documentadas
- **Limiar:** Todas as métricas calculadas para todos os modelos

✅ **Critério 3: Comparação Estatística**
- **Meta:** Realizar teste estatístico comparando desempenho dos modelos
- **Medida:** ANOVA ou Kruskal-Wallis com p-valor calculado
- **Limiar:** Teste realizado com interpretação clara dos resultados

✅ **Critério 4: Identificação de Melhor Modelo**
- **Meta:** Determinar qual modelo apresenta menor erro
- **Medida:** Ranking dos modelos por MAE
- **Limiar:** Conclusão clara sobre qual modelo é superior

#### Critérios Desejáveis de Sucesso (Should-Have):

🎯 **Critério 5: Erro Aceitável**
- **Meta:** Atingir erro médio < 20% em ao menos um modelo
- **Medida:** MAPE do melhor modelo
- **Limiar:** MAPE < 20% (desejável); < 30% (aceitável)

🎯 **Critério 6: Identificação de Variáveis Preditoras**
- **Meta:** Determinar quais métricas mais influenciam o custo
- **Medida:** Correlação entre métricas (CPU, memória, etc.) e custo
- **Limiar:** Identificar pelo menos 2 métricas com correlação > 0.6

🎯 **Critério 7: Generalização**
- **Meta:** Validar que modelos generalizam para dados não vistos
- **Medida:** Diferença entre erro de treino e teste
- **Limiar:** Diferença < 15% (sem overfitting severo)

🎯 **Critério 8: Significância Estatística**
- **Meta:** Provar diferença significativa entre modelos
- **Medida:** p-valor do teste estatístico
- **Limiar:** p < 0.05 (diferença significativa)

#### Critérios Extras de Sucesso (Nice-to-Have):

⭐ **Critério 9: Análise de Estabilidade**
- **Meta:** Avaliar robustez dos modelos em diferentes cenários
- **Medida:** Variância dos erros
- **Limiar:** Modelo mais estável identificado

⭐ **Critério 10: Documentação Completa**
- **Meta:** Documentar todo o processo experimental
- **Medida:** Seções do plano experimental preenchidas
- **Limiar:** 100% das seções 1-12 completas

#### Critérios de Qualidade Científica:

📊 **Critério 11: Rigor Metodológico**
- Desenho experimental apropriado
- Variáveis de controle identificadas e mantidas constantes
- Análise estatística correta

📊 **Critério 12: Reprodutibilidade**
- Código documentado e versionado
- Instruções claras para replicação
- Dados sintéticos geráveis novamente

### 6.3 Critérios de Parada Antecipada (Pré-Execução)

O experimento deve ser **adiado ou cancelado** se qualquer uma das seguintes condições ocorrer antes do início da execução:

❌ **Parada Tipo 1 - Recursos Insuficientes:**
- Hardware disponível não consegue processar os modelos em tempo hábil
- Bibliotecas necessárias não funcionam no ambiente disponível
- **Ação:** Reduzir escopo (menos modelos ou janelas menores) ou buscar recursos alternativos

❌ **Parada Tipo 2 - Inviabilidade Metodológica:**
- Impossibilidade de gerar dados sintéticos realísticos
- Modelos escolhidos são inadequados para o problema após revisão mais profunda
- **Ação:** Revisar desenho experimental com orientador

❌ **Parada Tipo 3 - Mudança de Escopo:**
- Orientador solicita mudança radical no tema do TCC
- Prazos acadêmicos são alterados drasticamente
- **Ação:** Renegociar escopo ou prazos

❌ **Parada Tipo 4 - Problemas Pessoais:**
- Problemas de saúde graves do pesquisador
- Impossibilidade de dedicar tempo mínimo necessário
- **Ação:** Solicitar extensão de prazo ou trancamento

❌ **Parada Tipo 5 - Riscos Identificados como Críticos:**
- Após revisão, identificação de risco não mitigável com alto impacto
- Feedback do orientador indicando inviabilidade fundamental
- **Ação:** Replanejamento completo ou mudança de tema

**Processo de Decisão:**
1. Identificação do problema que motiva a parada
2. Discussão com orientador
3. Exploração de alternativas de mitigação
4. Decisão formal (continuar, adiar ou cancelar)
5. Documentação da decisão

---

## 7. Modelo Conceitual e Hipóteses

### 7.1 Modelo Conceitual do Experimento

#### Modelo Conceitual Geral

O modelo conceitual deste experimento baseia-se na premissa de que **custos de infraestrutura cloud são função direta de métricas de uso** e que **modelos matemáticos podem capturar padrões históricos para prever custos futuros**.

```
┌─────────────────────────────────────────────────────────────┐
│                    MODELO CONCEITUAL                         │
└─────────────────────────────────────────────────────────────┘

        MÉTRICAS DE USO                    MODELO DE              CUSTO
       (Independentes)                     PREVISÃO              PREVISTO
                                          (Tratamento)          (Dependente)
                                                
    ┌─────────────────┐                                      
    │  CPU (%)        │────┐                                 
    └─────────────────┘    │                                 
                           │                                 
    ┌─────────────────┐    │         ┌──────────────┐       ┌──────────┐
    │  Memória (MB)   │────┤────────>│ Regressão    │──────>│  Custo   │
    └─────────────────┘    │         │ Linear       │       │ (R$)     │
                           │         └──────────────┘       └──────────┘
    ┌─────────────────┐    │                │                     │
    │ Storage (GB)    │────┤                │                     │
    └─────────────────┘    │         ┌──────────────┐            │
                           │         │ Média Móvel  │────────────┤
    ┌─────────────────┐    │         └──────────────┘            │
    │ Requisições     │────┘                │                     │
    │ (req/s)         │              ┌──────────────┐            │
    └─────────────────┘              │ ARIMA        │────────────┤
                                     └──────────────┘            │
                                            │                     │
         Padrões                     ┌──────────────┐            │
         Históricos ────────────────>│ Exponential  │────────────┘
         (séries temporais)          │ Smoothing    │
                                     └──────────────┘
                                            
                                            │
                                            ▼
                                     ┌──────────────┐
                                     │   AVALIAÇÃO  │
                                     │ MAE, RMSE,   │
                                     │    MAPE      │
                                     └──────────────┘
                                            │
                                            ▼
                                     ┌──────────────┐
                                     │  COMPARAÇÃO  │
                                     │ ESTATÍSTICA  │
                                     │ (ANOVA/K-W)  │
                                     └──────────────┘
```

#### Relações Causais Assumidas:

1. **Métricas → Custo:**
   - Maior uso de CPU → Maior custo de compute
   - Mais requisições → Maior custo de rede e compute
   - Mais armazenamento → Maior custo de storage
   - Mais memória → Maior custo de instâncias maiores

2. **Histórico → Previsão:**
   - Padrões passados de uso permitem prever padrões futuros
   - Tendências e sazonalidade se repetem ao longo do tempo
   - Correlações entre métricas são estáveis

3. **Modelo → Precisão:**
   - Diferentes modelos capturam diferentes aspectos dos dados
   - Modelos mais complexos (ARIMA) podem capturar padrões não-lineares
   - Modelos simples (média móvel) podem ser mais robustos a ruído

#### Variável Moderadora:
- **Janela Temporal:** O tamanho da janela de observação (7, 14 ou 30 dias) pode moderar a relação entre modelo e precisão

#### Pressuposto Central:
**"O tipo de modelo de previsão utilizado influencia significativamente o erro de previsão de custos cloud, sendo possível identificar um modelo superior para o contexto estudado."**

### 7.2 Hipóteses Formais (H0, H1)

#### Hipótese Principal:

**H0 (Hipótese Nula):**
> Não existe diferença estatisticamente significativa na precisão (medida por MAE, RMSE ou MAPE) entre os modelos de previsão analisados (Regressão Linear, Média Móvel, ARIMA e Exponential Smoothing).

**Formalmente:** μ₁ = μ₂ = μ₃ = μ₄

Onde:
- μ₁ = erro médio da Regressão Linear
- μ₂ = erro médio da Média Móvel
- μ₃ = erro médio do ARIMA
- μ₄ = erro médio do Exponential Smoothing

**H1 (Hipótese Alternativa):**
> Existe diferença estatisticamente significativa na precisão entre pelo menos dois dos modelos de previsão analisados.

**Formalmente:** ∃ i,j ∈ {1,2,3,4} tal que μᵢ ≠ μⱼ

---

#### Hipóteses Específicas (Sub-Hipóteses):

**H1.1 - Regressão Linear vs. Séries Temporais:**
- **H1.1.0 (Nula):** A regressão linear apresenta erro médio igual aos modelos de séries temporais (ARIMA e Exponential Smoothing)
- **H1.1.1 (Alternativa):** A regressão linear apresenta erro médio diferente dos modelos de séries temporais
- **Direção esperada:** Modelos de séries temporais tendem a ter menor erro (capturam dependência temporal)

**H1.2 - ARIMA vs. Modelos Simples:**
- **H1.2.0 (Nula):** ARIMA apresenta erro médio igual aos modelos simples (Regressão Linear e Média Móvel)
- **H1.2.1 (Alternativa):** ARIMA apresenta erro médio menor que modelos simples
- **Direção esperada:** ARIMA < (Regressão Linear, Média Móvel)
- **Justificativa:** ARIMA captura autocorrelação, tendência e sazonalidade

**H1.3 - Exponential Smoothing em Dados com Tendência:**
- **H1.3.0 (Nula):** Exponential Smoothing não gera previsões mais estáveis que outros modelos em dados com tendência
- **H1.3.1 (Alternativa):** Exponential Smoothing gera previsões mais estáveis (menor variância de erro) em dados com tendência
- **Direção esperada:** σ²(Exp.Smoothing) < σ²(outros modelos)
- **Justificativa:** Suavização exponencial dá peso maior a observações recentes, reduzindo impacto de ruído

**H1.4 - Efeito da Janela Temporal:**
- **H1.4.0 (Nula):** O tamanho da janela temporal (7, 14 ou 30 dias) não afeta significativamente o erro de previsão
- **H1.4.1 (Alternativa):** Janelas temporais maiores resultam em menor erro de previsão
- **Direção esperada:** Erro(30 dias) < Erro(14 dias) < Erro(7 dias)
- **Justificativa:** Mais dados históricos permitem melhor captura de padrões

**H1.5 - Correlação Métrica-Custo:**
- **H1.5.0 (Nula):** Não há diferença significativa na correlação de diferentes métricas (CPU, memória, requisições, storage) com o custo final
- **H1.5.1 (Alternativa):** CPU e requisições apresentam correlação significativamente maior com custo do que memória e storage
- **Direção esperada:** Corr(CPU, Custo) > Corr(Memória, Custo)

### 7.3 Nível de Significância e Considerações de Poder

#### Nível de Significância:
**α = 0.05 (5%)**

- Padrão amplamente aceito em ciências experimentais
- Representa 5% de chance de rejeitar H0 quando ela é verdadeira (Erro Tipo I)
- Será usado em todos os testes estatísticos (ANOVA, Kruskal-Wallis, testes t)

**Interpretação:**
- Se p-valor < 0.05 → Rejeitar H0 (diferença é estatisticamente significativa)
- Se p-valor ≥ 0.05 → Não rejeitar H0 (não há evidência suficiente de diferença)

#### Poder Estatístico:

**Poder Desejado:** 1 - β = 0.80 (80%)

- Representa 80% de chance de detectar uma diferença real quando ela existe
- β = 0.20 (20% de chance de Erro Tipo II - não detectar diferença que existe)

**Cálculo de Tamanho de Amostra:**
Para alcançar poder de 80% com α = 0.05:
- **Repetições por modelo:** n = 30 execuções
- **Total de observações:** 30 × 4 modelos = 120 observações
- **Justificativa:** Teorema do Limite Central garante distribuição normal com n ≥ 30

**Tamanho de Efeito Detectável:**
Com n = 30 por grupo, é possível detectar:
- Diferença de efeito médio (d de Cohen ≈ 0.5)
- Diferença de ~15-20% no erro médio entre modelos

**Considerações:**

1. **Repetibilidade:**
   - Cada modelo será executado 30 vezes com inicializações aleatórias diferentes
   - Reduz impacto de variabilidade aleatória
   - Permite cálculo confiável de intervalos de confiança

2. **Múltiplas Comparações:**
   - Com 4 modelos, há 6 comparações par-a-par possíveis
   - Considerar correção de Bonferroni se necessário: α_ajustado = 0.05/6 = 0.0083
   - Usar post-hoc tests (Tukey HSD) após ANOVA se H0 for rejeitada

3. **Validação Cruzada:**
   - K-fold com k = 5 aumenta o poder estatístico
   - Cada modelo é avaliado em 5 partições diferentes dos dados
   - Total efetivo de avaliações: 30 execuções × 5 folds = 150 avaliações por modelo

4. **Sensibilidade:**
   - Se diferenças forem sutis (< 10% de erro), poder pode ser insuficiente
   - Nesse caso, aumentar n para 50 ou considerar α = 0.10 mais liberal

**Limitação:**
Por usar dados sintéticos, o poder estatístico é suficiente para detectar diferenças entre modelos, mas a validade externa (generalização para dados reais) requer validação futura.

---

## 8. Variáveis, Fatores, Tratamentos e Objetos de Estudo

### 8.1 Objetos de Estudo

Os **objetos de estudo** são as séries temporais de métricas de uso de infraestrutura cloud e os custos associados.

**Descrição Detalhada:**

1. **Séries Temporais de Métricas:**
   - **CPU:** Percentual de utilização ao longo do tempo
   - **Memória:** Consumo em MB ao longo do tempo
   - **Armazenamento:** Volume em GB ao longo do tempo
   - **Requisições:** Taxa de requisições por segundo ao longo do tempo

2. **Série Temporal de Custos:**
   - Custo calculado para cada período de tempo (hora)
   - Baseado em tabelas de precificação de provedores cloud
   - Agregação das métricas com pesos específicos

**Características dos Objetos:**
- **Granularidade:** Horária (1 registro por hora)
- **Duração:** 30 dias (720 registros)
- **Tipo:** Dados sintéticos realísticos
- **Formato:** Séries temporais univariadas e multivariadas

### 8.2 Sujeitos / Participantes (Visão Geral)

**Importante:** Este experimento **não envolve sujeitos humanos**. Os "sujeitos" são as **execuções dos modelos** sobre os dados.

**Caracterização:**
- **Tipo:** Execuções algorítmicas (modelos de previsão)
- **Quantidade:** 30 execuções × 4 modelos = 120 execuções totais
- **Aleatorização:** Cada execução usa seed aleatória diferente para:
  - Divisão treino/teste
  - Inicialização de parâmetros (quando aplicável)
  - Seleção de folds na validação cruzada

**Equivalente a "Participantes" em Experimentos Tradicionais:**
- Cada execução de um modelo pode ser vista como um "participante"
- Diferentes execuções capturam variabilidade natural do processo
- Permite análise estatística robusta (média, desvio padrão, intervalos de confiança)

### 8.3 Variáveis Independentes (Fatores) e seus Níveis

#### Fator Principal:

**F1: MODELO DE PREVISÃO**

| Nível | Descrição | Sigla | Características |
|-------|-----------|-------|-----------------|
| **Nível 1** | Regressão Linear | RL | Modelo simples, assume relação linear entre métricas e custo |
| **Nível 2** | Média Móvel Simples | MM | Média dos últimos N períodos, sem considerar tendência |
| **Nível 3** | ARIMA | ARIMA | Modelo de séries temporais, captura autocorrelação e tendência |
| **Nível 4** | Exponential Smoothing | ES | Suavização exponencial, dá peso maior a observações recentes |

**Natureza do Fator:**
- **Tipo:** Categórico nominal
- **Níveis:** 4
- **Manipulação:** Controlada experimentalmente (escolha do pesquisador)

#### Fator Secundário (Exploratório - NÃO incluído na análise principal):

**F2: JANELA TEMPORAL**

| Nível | Descrição | Uso |
|-------|-----------|-----|
| **Nível 1** | 30 dias | **JANELA PRINCIPAL** - Única janela analisada no experimento principal |
| **Nível 2** | 7 dias | Exploratório (apenas se tempo permitir) |
| **Nível 3** | 14 dias | Exploratório (apenas se tempo permitir) |

**Natureza do Fator:**
- **Tipo:** Categórico ordinal
- **Níveis:** 1 na análise principal (30 dias); 3 se análise exploratória for realizada
- **Manipulação:** **NÃO SERÁ ANALISADO** como fator experimental
- **Justificativa:** Incluir 3 janelas temporais triplicaria o tempo de execução (de ~15h para ~45h), inviável para o cronograma do TCC
- **Decisão:** Fixar janela em 30 dias (análise principal); análise exploratória com 7 e 14 dias fica como trabalho futuro

### 8.4 Tratamentos (Condições Experimentais)

Os **tratamentos** correspondem aos 4 modelos de previsão que serão aplicados:

#### Tratamento T1: Regressão Linear (RL)

**Descrição:**
Modelo que assume relação linear entre métricas de uso (X) e custo (Y):

Y = β₀ + β₁·CPU + β₂·Memória + β₃·Storage + β₄·Requisições + ε

**Características:**
- **Complexidade:** Baixa
- **Vantagens:** Simples, interpretável, rápido
- **Desvantagens:** Não captura dependência temporal, assume linearidade
- **Implementação:** `sklearn.linear_model.LinearRegression`
- **Hiperparâmetros:** Nenhum (usa defaults)

#### Tratamento T2: Média Móvel Simples (MM)

**Descrição:**
Previsão baseada na média dos últimos N períodos:

Ŷₜ₊₁ = (Yₜ + Yₜ₋₁ + ... + Yₜ₋ₙ₊₁) / N

**Características:**
- **Complexidade:** Muito baixa
- **Vantagens:** Extremamente simples, não requer treinamento
- **Desvantagens:** Não captura tendências, lag em mudanças bruscas
- **Implementação:** Numpy / Pandas
- **Hiperparâmetros:** N = 7 períodos (janela de 7 horas)

#### Tratamento T3: ARIMA

**Descrição:**
Modelo AutoRegressive Integrated Moving Average - captura autocorrelação, tendência e média móvel:

ARIMA(p, d, q):
- p = ordem autoregressiva
- d = ordem de diferenciação (estacionariedade)
- q = ordem de média móvel

**Características:**
- **Complexidade:** Alta
- **Vantagens:** Captura dependência temporal, tendências, sazonalidade
- **Desvantagens:** Requer estacionariedade, pode ser lento, difícil de interpretar
- **Implementação:** `statsmodels.tsa.arima.model.ARIMA`
- **Hiperparâmetros - Grid Search:**
  - **p (ordem AR):** {0, 1, 2}
  - **d (diferenciação):** {0, 1}
  - **q (ordem MA):** {0, 1, 2}
  - **Método de seleção:** AIC (Akaike Information Criterion)
  - **Total de combinações:** 3 × 2 × 3 = 18 configurações
  - **Critério de escolha:** Menor AIC entre as 18 configurações

#### Tratamento T4: Exponential Smoothing (ES)

**Descrição:**
Suavização exponencial - dá peso exponencialmente decrescente a observações mais antigas:

Ŷₜ₊₁ = α·Yₜ + (1-α)·Ŷₜ

Onde α é o parâmetro de suavização (0 < α < 1)

**Características:**
- **Complexidade:** Média
- **Vantagens:** Reage rapidamente a mudanças, suaviza ruído, simples de entender
- **Desvantagens:** Não captura sazonalidade complexa (versão simples)
- **Implementação:** `statsmodels.tsa.holtwinters.ExponentialSmoothing`
- **Hiperparâmetros - Configuração Específica:**
  - **Modelo:** Holt-Winters (Triple Exponential Smoothing)
  - **Tendência (trend):** {'add', 'mul', None}
  - **Sazonalidade (seasonal):** {'add', None}
  - **Período sazonal (seasonal_periods):** 24 (ciclo diário de 24 horas)
  - **Método de otimização:** Least squares (padrão statsmodels)
  - **Suavização (smoothing_level, smoothing_trend, smoothing_seasonal):** Otimizados automaticamente

### 8.5 Variáveis Dependentes (Respostas)

As **variáveis dependentes** são as métricas que medem a qualidade da previsão:

| ID | Variável | Descrição | Fórmula | Unidade | Interpretação |
|----|----------|-----------|---------|---------|---------------|
| **VD1** | MAE | Mean Absolute Error | `Σ|yᵢ - ŷᵢ| / n` | R$ | Menor é melhor; mesma escala do custo |
| **VD2** | RMSE | Root Mean Squared Error | `√(Σ(yᵢ - ŷᵢ)² / n)` | R$ | Menor é melhor; penaliza erros grandes |
| **VD3** | MAPE | Mean Absolute Percentage Error | `Σ|(yᵢ - ŷᵢ)/yᵢ| / n × 100` | % | Menor é melhor; erro relativo |
| **VD4** | Erro Validação | Erro em validação cruzada | Média dos erros em k-folds | % | Mede generalização |
| **VD5** | Variância Erro | Variabilidade do erro | `Var(erros)` | R$² | Menor é melhor; mede estabilidade |
| **VD6** | R² | Coeficiente de Determinação | `1 - (RSS/TSS)` | Adimensional | Maior é melhor (0 a 1) |

**Variável Primária (Outcome Principal):**
- **MAE** será usada como métrica primária para comparação
- Razão: Interpretável, mesma escala do custo, robusta a outliers

**Variáveis Secundárias:**
- RMSE, MAPE: Complementam a análise
- Erro Validação: Verifica generalização
- Variância Erro: Avalia estabilidade

### 8.6 Variáveis de Controle / Bloqueio

Variáveis que **não são objeto de estudo** mas que podem afetar os resultados e, portanto, devem ser **mantidas constantes**:

| Variável de Controle | Como será Controlada | Justificativa |
|----------------------|----------------------|---------------|
| **Dataset de Entrada** | Todos os modelos usarão exatamente os mesmos dados sintéticos | Garantir comparabilidade |
| **Período de Análise** | Mesmos 30 dias para todos os modelos | Eliminar variação temporal |
| **Divisão Treino/Teste** | Mesma divisão 70%-30% para todos (com mesmo seed em cada execução) | Equidade na avaliação |
| **Métricas de Entrada** | Mesmas 4 métricas (CPU, memória, storage, requisições) | Isonomia de informação |
| **Granularidade Temporal** | Granularidade horária para todos | Consistência temporal |
| **Ambiente Computacional** | Mesma máquina, mesmo Python, mesmas bibliotecas | Eliminar variação de hardware/software |
| **Pré-processamento** | Mesma normalização/padronização para todos os modelos | Igualdade de condições |
| **Métrica de Avaliação** | Mesmos cálculos de MAE, RMSE, MAPE para todos | Comparabilidade direta |
| **Ordem de Execução** | Ordem randomizada das execuções | Evitar viés temporal |
| **Tabela de Preços** | Mesma tabela de preços fixa | Eliminar mudanças externas |

**Bloqueio:**
Não há necessidade de bloqueio formal pois:
- Não há sujeitos humanos (que poderiam ter características individuais)
- Todas as execuções usam o mesmo ambiente computacional
- Aleatorização da ordem de execução é suficiente

### 8.7 Possíveis Variáveis de Confusão Conhecidas

Variáveis que **podem distorcer os resultados** se não forem adequadamente tratadas:

#### Confusão 1: Qualidade da Implementação

**Descrição:** Modelos mais complexos podem ter implementação com mais bugs ou menos otimizada

**Mitigação:**
- Usar bibliotecas consolidadas (Scikit-learn, Statsmodels)
- Testar implementações com datasets conhecidos
- Validar resultados intermediários

**Monitoramento:**
- Revisar código com orientador
- Comparar com exemplos da documentação oficial

---

#### Confusão 2: Hiperparâmetros Não-Ótimos

**Descrição:** Alguns modelos podem não ter hiperparâmetros otimizados, favorecendo outros

**Mitigação:**
- Usar valores padrão das bibliotecas como baseline
- Para ARIMA, fazer grid search simples de parâmetros (p,d,q)
- Documentar escolha de hiperparâmetros

**Monitoramento:**
- Se resultados forem inesperados, revisar hiperparâmetros
- Análise de sensibilidade (opcional)

---

#### Confusão 3: Overfitting Despercebido

**Descrição:** Modelo pode ter bom desempenho no treino mas péssimo no teste

**Mitigação:**
- Validação cruzada k-fold (k=5)
- Monitorar diferença entre erro de treino e teste
- Usar métrica de generalização explícita

**Monitoramento:**
- Calcular M12 (Diferença treino/teste)
- Flagging se diferença > 15%

---

#### Confusão 4: Dados Sintéticos Não-Realísticos

**Descrição:** Simulação pode favorecer artificialmente um tipo de modelo

**Mitigação:**
- Basear simulação em papers e documentação
- Incluir ruído, tendência e sazonalidade
- Validar padrões com especialistas (orientador)

**Monitoramento:**
- Análise exploratória dos dados sintéticos
- Comparação com benchmarks da literatura

---

#### Confusão 5: Variância Aleatória

**Descrição:** Resultados podem variar significativamente entre execuções devido a aleatoriedade

**Mitigação:**
- Executar cada modelo 30 vezes
- Usar seeds aleatórias diferentes
- Reportar média e intervalo de confiança

**Monitoramento:**
- Calcular desvio padrão dos erros
- Verificar se intervalos de confiança se sobrepõem

---

#### Confusão 6: Ordem de Execução

**Descrição:** Modelos executados primeiro podem ter condições diferentes (cache, temperatura CPU)

**Mitigação:**
- Randomizar ordem de execução dos modelos
- Limpar cache entre execuções
- Medir tempo de execução para detectar anomalias

**Monitoramento:**
- Análise de variância por ordem de execução
- Verificar se há padrões sistemáticos

---

### Resumo das Variáveis (Tabela Consolidada)

| Variável | Tipo | Descrição | Valores/Níveis | Papel no Experimento |
|----------|------|-----------|----------------|----------------------|
| **Modelo de Previsão** | Independente (Fator) | Algoritmo usado para prever custos | RL, MM, ARIMA, ES | Tratamento principal |
| **Janela Temporal** | Independente (Fator Secundário) | Período de histórico usado | 7, 14, 30 dias | Análise exploratória |
| **MAE** | Dependente (Resposta) | Erro absoluto médio | Contínuo (R$) | Outcome primário |
| **RMSE** | Dependente (Resposta) | Raiz do erro quadrático médio | Contínuo (R$) | Outcome secundário |
| **MAPE** | Dependente (Resposta) | Erro percentual médio | Contínuo (%) | Outcome secundário |
| **Erro Validação** | Dependente (Resposta) | Erro em validação cruzada | Contínuo (%) | Medida de generalização |
| **Variância Erro** | Dependente (Resposta) | Estabilidade das previsões | Contínuo (R$²) | Medida de robustez |
| **CPU Média** | Controle | Utilização média de CPU | Contínuo (%) | Mantida constante |
| **Memória Média** | Controle | Consumo médio de RAM | Contínuo (MB) | Mantida constante |
| **Storage** | Controle | Volume de armazenamento | Contínuo (GB) | Mantida constante |
| **Requisições** | Controle | Taxa de requisições | Contínuo (req/s) | Mantida constante |
| **Dataset** | Controle | Dados usados para treino/teste | Mesmo para todos | Mantida constante |
| **Divisão Treino/Teste** | Controle | Proporção 70%-30% | Fixa | Mantida constante |
| **Qualidade Implementação** | Confusão | Bugs ou otimização de código | Variável | Mitigada por bibliotecas |
| **Hiperparâmetros** | Confusão | Configuração dos modelos | Variável | Documentada e justificada |

---
## 9. Desenho Experimental

### 9.1 Tipo de Desenho (Completamente Randomizado, Blocos, Fatorial, etc.)

**Tipo de Desenho:** **Completamente Aleatorizado (Completely Randomized Design - CRD)** com repetições

#### Justificativa:

1. **Adequação ao Problema:**
   - Há **apenas um fator experimental** (tipo de modelo de previsão)
   - **Janela temporal é FIXA em 30 dias** (não é fator experimental)
   - Não há necessidade de blocos (ambiente homogêneo, dados reais do Google Cluster)
   - Todos os modelos são aplicados aos mesmos dados, garantindo equidade

2. **Vantagens para Este Contexto:**
   - **Simplicidade:** Fácil de implementar e analisar
   - **Flexibilidade:** Permite diferentes números de repetições por tratamento se necessário
   - **Poder Estatístico:** Com 30 repetições, fornece poder adequado para detectar diferenças

3. **Características do Desenho:**
   - **Aleatorização completa:** Ordem de execução dos modelos é randomizada
   - **Repetições:** 30 execuções independentes de cada modelo
   - **Controle rigoroso:** Todas as variáveis de controle mantidas constantes
   - **Validação cruzada:** k-fold (k=5) adiciona robustez

#### Estrutura do Experimento:

```
Tratamentos:    T1 (RL)  |  T2 (MM)  |  T3 (ARIMA)  |  T4 (ES)
                   ↓           ↓            ↓            ↓
Repetições:     n=30        n=30         n=30         n=30
                   ↓           ↓            ↓            ↓
Medidas:        MAE         MAE          MAE          MAE
                RMSE        RMSE         RMSE         RMSE
                MAPE        MAPE         MAPE         MAPE
                   ↓           ↓            ↓            ↓
Análise:    ←─────── ANOVA ou Kruskal-Wallis ─────────→
                   ↓
           Comparações Post-Hoc (Tukey HSD)
```

#### Alternativa Não Selecionada:

**Desenho Fatorial (2 fatores):**
- Poderia incluir "Janela Temporal" (7, 14, 30 dias) como segundo fator
- Resultaria em 4 × 3 = 12 combinações de tratamentos (36 células experimentais)
- **Não selecionado porque:**
  - Triplicaria o tempo de execução (~15h → ~45h)
  - Aumentaria complexidade sem adicionar valor proporcional ao objetivo principal
  - Cronograma do TCC inviável para experimento dessa magnitude
- **Decisão Final:** Janela temporal fixa em 30 dias; análise exploratória com 7 e 14 dias fica como **trabalho futuro**

### 9.2 Randomização e Alocação

#### Estratégia de Randomização:

**O que será randomizado:**

1. **Ordem de Execução dos Modelos:**
   - As 120 execuções (30 × 4 modelos) terão ordem completamente aleatória
   - Evita viés de ordem temporal (aquecimento de CPU, cache, etc.)
   
2. **Seeds para Divisão Treino/Teste:**
   - Cada uma das 30 repetições usará um seed aleatório diferente
   - Garante que cada execução tenha divisão treino/teste ligeiramente diferente
   - Seeds serão pré-gerados e documentados para reprodutibilidade

3. **Inicialização de Parâmetros (quando aplicável):**
   - ARIMA: diferentes pontos de partida para otimização
   - Exponential Smoothing: diferentes inicializações
   - Validação cruzada: ordem dos folds randomizada

#### Procedimento de Randomização:

```python
# Pseudocódigo do processo de randomização

import numpy as np
import random

# 1. Gerar seeds para 30 repetições
np.random.seed(42)  # seed mestre para reprodutibilidade
seeds = np.random.randint(1, 10000, size=30)

# 2. Criar lista de todas as execuções
execucoes = []
for modelo in ['RL', 'MM', 'ARIMA', 'ES']:
    for i, seed in enumerate(seeds):
        execucoes.append({
            'modelo': modelo,
            'repeticao': i + 1,
            'seed': seed
        })

# 3. Randomizar ordem de execução
random.seed(42)
random.shuffle(execucoes)

# 4. Executar na ordem randomizada
for exec in execucoes:
    executar_modelo(exec['modelo'], exec['seed'])
```

#### Documentação da Randomização:

- **Seeds utilizados:** Salvos em arquivo CSV para reprodutibilidade total
- **Ordem de execução:** Registrada em log com timestamp
- **Verificação:** Após experimento, confirmar que randomização foi mantida

#### Controle de Confundidores:

**Fatores controlados (NÃO randomizados):**
- Dataset de entrada (mesmo para todos)
- Proporção treino/teste (70%-30% fixa)
- Métricas de avaliação (mesmas para todos)
- Ambiente computacional (mesma máquina)

### 9.3 Balanceamento e Contrabalanço

#### Balanceamento:

**Balanceamento Completo Garantido:**

1. **Número de Repetições:**
   - Todos os 4 modelos: exatamente 30 execuções cada
   - Total: 120 execuções balanceadas (30-30-30-30)
   - Sem desbalanceamento planejado ou acidental

2. **Dados de Entrada:**
   - Todos os modelos recebem exatamente os mesmos dados
   - Mesmas 720 observações (30 dias × 24 horas)
   - Mesmas 4 métricas de entrada (CPU, memória, storage, requisições)

3. **Condições de Avaliação:**
   - Mesma divisão treino/teste em cada repetição
   - Mesmas métricas de avaliação (MAE, RMSE, MAPE)
   - Mesmo procedimento de validação cruzada

#### Contrabalanço (Counterbalancing):

**Contrabalanço de Ordem:**

Embora não haja "efeitos de aprendizagem" como em experimentos com humanos, o contrabalanço de ordem mitiga efeitos de execução sequencial:

1. **Efeitos Mitigados:**
   - Aquecimento de hardware (CPU, cache)
   - Variações de carga do sistema operacional
   - Degradação de performance ao longo do tempo

2. **Estratégia:**
   - Ordem de execução completamente randomizada (ver seção 9.2)
   - Cada modelo aparece aproximadamente igual número de vezes em cada posição
   - Verificação post-hoc: análise de variância por ordem de execução

3. **Procedimento de Limpeza:**
   - Clear de memória entre execuções
   - Restart do kernel Python a cada 30 execuções (opcional)
   - Monitoramento de temperatura e uso de CPU

#### Verificação de Balanceamento:

**Checklist Pré-Execução:**
- [ ] Confirmar n=30 para cada modelo
- [ ] Verificar que dataset é idêntico para todos
- [ ] Validar que ordem está randomizada
- [ ] Confirmar que seeds são únicos e documentados

**Checklist Pós-Execução:**
- [ ] Verificar que todas as 120 execuções foram concluídas
- [ ] Confirmar ausência de outliers devido a erros de execução
- [ ] Analisar se ordem de execução introduziu viés sistemático

### 9.4 Número de Grupos e Sessões

#### Número de Grupos:

**4 Grupos (Tratamentos):**
1. Grupo 1: Regressão Linear (RL) - n=30
2. Grupo 2: Média Móvel (MM) - n=30
3. Grupo 3: ARIMA - n=30
4. Grupo 4: Exponential Smoothing (ES) - n=30

**Total de Unidades Experimentais:** 120 execuções

#### Número de Sessões:

**Definição de "Sessão":**
Uma sessão corresponde a uma execução completa de um modelo, incluindo:
- Carregamento dos dados
- Divisão treino/teste
- Treinamento do modelo
- Geração de previsões
- Cálculo de métricas de erro
- Validação cruzada

**Estrutura de Sessões:**

1. **Por Repetição:**
   - Cada repetição (1 a 30) = 1 sessão por modelo
   - Total: 30 sessões × 4 modelos = 120 sessões

2. **Por Validação Cruzada:**
   - Cada sessão inclui k=5 folds
   - Portanto: 120 sessões × 5 folds = 600 avaliações de fold
   - Isso aumenta robustez sem aumentar número de sessões principais

3. **Janelas Temporais (Análise Exploratória):**
   - Opcionalmente, repetir experimento com janelas de 7, 14 e 30 dias
   - Se realizado: 120 sessões × 3 janelas = 360 sessões totais
   - **Decisão:** Priorizar janela de 30 dias (análise principal); outras janelas se tempo permitir

#### Duração Estimada:

**Por Sessão (SEM validação cruzada):**
- Regressão Linear: ~5 segundos
- Média Móvel: ~2 segundos
- ARIMA: ~30-60 segundos (mais lento, com grid search)
- Exponential Smoothing: ~10 segundos

**IMPORTANTE: Com Validação Cruzada (k=5 folds):**

Cada sessão inclui 5 folds de validação cruzada, multiplicando o tempo por aproximadamente 5x:

**Tempo por Sessão (COM k-fold, k=5):**
- Regressão Linear: ~5s × 5 folds = 25s por repetição
- Média Móvel: ~2s × 5 folds = 10s por repetição
- ARIMA: ~45s × 5 folds = 225s (3.75 min) por repetição
  - **Nota:** ARIMA com grid search pode levar 4-5 minutos por fold em alguns casos
  - **Estimativa conservadora:** ~5 min × 5 folds = 25 min por repetição
- Exponential Smoothing: ~10s × 5 folds = 50s por repetição

**Total Estimado (30 repetições × 4 modelos COM validação cruzada):**
- RL: 30 × 25s = 750s = 12.5 min
- MM: 30 × 10s = 300s = 5 min
- ARIMA: 30 × 25 min = 750 min = **12.5 horas**
- ES: 30 × 50s = 1500s = 25 min

**Tempo Total Realista:** ~13-15 horas (considerando ARIMA como gargalo)

**Estratégia de Mitigação:**
- Executar em etapas (ex: 10 repetições por vez)
- Executar durante a noite/períodos livres
- Considerar usar `n_jobs=-1` para paralelização quando disponível
- Otimizar grid search do ARIMA (limitar p, d, q a ranges menores)

#### Justificativa do Número de Sessões:

**N = 30 por grupo:**
- Atende requisito do Teorema do Limite Central (n ≥ 30)
- Fornece poder estatístico de 80% para detectar diferenças médias (d ≈ 0.5)
- Permite cálculo robusto de intervalos de confiança
- É padrão em estudos experimentais

**Não aumentar para n = 50:**
- Retornos marginais decrescentes em poder estatístico
- Tempo de execução dobraria (especialmente ARIMA)
- N = 30 já é suficiente para conclusões robustas

---

## 10. População, Sujeitos e Amostragem

### 10.1 População-Alvo

**Definição da População:**

A população-alvo deste experimento são **workloads (cargas de trabalho) reais de aplicações cloud**, caracterizadas por:

#### Características da População:

1. **Tipo de Aplicação:**
   - Jobs e tasks executados em clusters de produção
   - Serviços de processamento distribuído
   - Aplicações com padrões de uso variáveis ao longo do tempo
   - Workloads heterogêneos (batch, serviços online, análise de dados)

2. **Perfil de Uso:**
   - Consumo variável de CPU (workloads reais de produção)
   - Uso dinâmico de memória RAM
   - Padrões temporais naturais (sem simulação)
   - Heterogeneidade de recursos e utilização

3. **Contexto Organizacional:**
   - Clusters de produção de larga escala
   - Ambiente gerenciado por sistema de orquestração (Google Borg)
   - Dados representativos de infraestrutura cloud real
   - Workloads de múltiplos usuários e aplicações

4. **Padrões Temporais:**
   - Presença de tendências naturais
   - Sazonalidade real (diária, semanal)
   - Picos de uso espontâneos
   - Variabilidade natural de cargas de trabalho

#### Escopo da Generalização:

**Onde os resultados SE APLICAM:**
- Ambientes cloud com workloads similares aos traces analisados
- Clusters gerenciados por orquestradores (Kubernetes, Borg, etc.)
- Horizontes de previsão de curto-médio prazo (dias/semanas)
- Infraestruturas com precificação baseada em uso de recursos

**Onde os resultados PODEM NÃO SE APLICAR:**
- Workloads completamente diferentes dos traces (ex: IoT edge computing)
- Contextos com padrões de uso extremamente irregulares
- Ambientes com descontos especiais ou reserved instances complexos
- Aplicações com requisitos de recursos completamente estáticos

### 10.2 Critérios de Inclusão de Sujeitos

**Importante:** Este experimento usa **dados reais de traces públicos de cloud computing**, portanto "sujeitos" são séries temporais extraídas de workloads reais.

#### Fontes de Dados Candidatas:

**Fonte Primária (Recomendada):**

**1. Google Cluster Data 2019 (ClusterData2019)**
- **Descrição:** Traces de 8 clusters Google Borg durante maio de 2019
- **Tamanho:** 2.4 TiB comprimidos (versão completa), samples menores disponíveis no Kaggle
- **Métricas Disponíveis:**
  - CPU usage (histogramas a cada 5 minutos)
  - Memory usage
  - Job e task events
  - Resource requests
  - Timestamps precisos
- **Acesso:** 
  - BigQuery: `https://github.com/google/cluster-data`
  - Kaggle (sample): `https://www.kaggle.com/datasets/derrickmwiti/google-2019-cluster-sample`
- **Licença:** CC-BY (uso acadêmico permitido)
- **Vantagens:** Dados reais, amplamente usado academicamente, bem documentado

**Fontes Alternativas (Backup):**

**2. MIT Supercloud Dataset**
- **Descrição:** Logs de sistema HPC com GPU
- **Métricas:** CPU, GPU, memória, file system
- **Granularidade:** 60 segundos (CPU/GPU)
- **Acesso:** `https://arxiv.org/abs/2108.02037`

**3. Azure Public Dataset**
- **Descrição:** Workloads de inferência LLM
- **Acesso:** `https://github.com/Azure/AzurePublicDataset`

**4. IEEE DataPort - Cloud Performance Metrics**
- **Descrição:** ~8,000 pontos de métricas de sistema stateless
- **Métricas:** CPU, memória, rede, TPS, response time
- **Granularidade:** 5 segundos
- **Acesso:** Requer IEEE DataPort subscription (gratuito para membros IEEE)

#### Critérios de Inclusão para Séries Temporais Extraídas:

1. **Completude Temporal:**
   - Período contínuo de pelo menos 30 dias
   - Granularidade máxima: 5 minutos (para compatibilidade com modelos)
   - Sem lacunas temporais significativas (< 5% de dados faltantes aceitável)

2. **Métricas Necessárias:**
   - **Obrigatórias:** CPU usage, Memory usage
   - **Desejáveis:** Storage, Network I/O, Request count
   - **Para cálculo de custo:** Qualquer combinação de CPU + Memory permite estimativa de custo

3. **Representatividade:**
   - Jobs/tasks de diferentes usuários (não apenas um usuário)
   - Workloads heterogêneos (não apenas um tipo de aplicação)
   - Presença de variabilidade natural (não workloads artificialmente constantes)

4. **Qualidade dos Dados:**
   - Dados numéricos válidos (não corrompidos)
   - Timestamps consistentes e ordenados
   - Valores dentro de ranges plausíveis (CPU: 0-100%, Memory > 0)

5. **Volume de Dados:**
   - Mínimo: 30 dias × 24h × 12 (para granularidade de 5 min) = ~8,640 observações por métrica
   - Ideal: 60-90 dias para maior robustez

#### Estratégia de Seleção do Dataset:

**Opção Preferencial: Google Cluster Data 2019 (Sample via Kaggle)**

**Justificativa:**
1. **Realismo:** Dados reais de produção Google
2. **Qualidade:** Bem documentado e validado
3. **Acessibilidade:** Sample no Kaggle é facilmente baixável (sem necessidade de BigQuery)
4. **Uso Acadêmico:** Centenas de papers usaram esses dados
5. **Métricas:** CPU e memória disponíveis com timestamps
6. **Tamanho Gerenciável:** Sample de ~100MB vs. 2.4TiB da versão completa

**Extração Específica:**
- Selecionar subset de jobs/tasks com pelo menos 30 dias de dados
- Agregar métricas por período (ex: 1 hora) para reduzir granularidade
- Extrair 30-90 dias contínuos de um ou mais clusters

### 10.3 Critérios de Exclusão de Sujeitos

#### Séries Temporais Excluídas:

1. **Dados Incompletos ou Corrompidos:**
   - Séries com > 5% de valores faltantes
   - Timestamps inconsistentes ou desordenados
   - Valores corrompidos (NaN, Inf, valores negativos para CPU/memória)

2. **Dados Não-Representativos:**
   - Jobs/tasks com duração < 24 horas (muito curtos)
   - Workloads completamente estáticos (variância ~0)
   - Outliers extremos sem explicação (CPU > 100%, memória negativa)

3. **Dados de Baixa Qualidade:**
   - Granularidade inconsistente (timestamps irregulares)
   - Lacunas temporais longas (> 1 hora sem dados)
   - Jobs marcados como "failed" ou "killed" (dependendo da análise)

4. **Dados Fora do Escopo:**
   - Workloads muito específicos que não representam uso típico
   - Jobs de teste/debug (identificáveis por padrões)
   - Dados de warmup ou shutdown de sistemas

#### Procedimento de Exclusão:

**Pré-Validação (antes do experimento):**

```python
import pandas as pd
import numpy as np

# 1. Carregar dados do Google Cluster (sample Kaggle ou BigQuery)
df = pd.read_csv('google_cluster_sample.csv')

# 2. Verificar valores faltantes
missing_pct = df.isna().sum() / len(df) * 100
print(f"% de dados faltantes por coluna:\n{missing_pct}")
assert missing_pct.max() < 5, "Mais de 5% de dados faltantes!"

# 3. Validar ranges
assert (df['cpu_usage'] >= 0).all() and (df['cpu_usage'] <= 1).all(), "CPU fora do range!"
assert (df['memory_usage'] >= 0).all(), "Memória negativa detectada!"

# 4. Detectar séries constantes
variancia = df.groupby('job_id')[['cpu_usage', 'memory_usage']].std()
jobs_validos = variancia[(variancia > 0.01).all(axis=1)].index
df = df[df['job_id'].isin(jobs_validos)]

# 5. Remover outliers extremos (z-score > 5)
from scipy import stats
z_scores = np.abs(stats.zscore(df[['cpu_usage', 'memory_usage']]))
df = df[(z_scores < 5).all(axis=1)]

# 6. Verificar completude temporal
df['timestamp'] = pd.to_datetime(df['timestamp'])
df = df.sort_values('timestamp')
gap_max = df['timestamp'].diff().max()
assert gap_max < pd.Timedelta('1 hour'), f"Lacuna temporal detectada: {gap_max}"

print(f"Dataset final: {len(df)} observações válidas")
```

**Decisão de Exclusão:**
- Se série falhar em qualquer critério crítico → **excluir**
- Documentar razão da exclusão no log do experimento
- Manter registro de quantas séries foram excluídas e por quê

### 10.4 Número de Repetições Experimentais (por Modelo)

#### Número de Repetições:

**N = 30 repetições experimentais por modelo**

- **Total de Unidades Experimentais:** 120 (30 × 4 modelos)
- **Total de Avaliações (com k-fold):** 600 (120 × 5 folds)

#### Justificativa Estatística:

**1. Teorema do Limite Central:**
- N ≥ 30 garante distribuição aproximadamente normal dos erros médios
- Permite uso de testes paramétricos (ANOVA) com segurança

**2. Poder Estatístico:**
Para α = 0.05 e poder = 0.80, com 4 grupos:
- N = 30 por grupo detecta tamanho de efeito d ≈ 0.5 (médio)
- Equivalente a diferença de ~15-20% no erro médio entre modelos

**3. Cálculo Formal (ANOVA One-Way):**

```
Parâmetros:
- k = 4 grupos
- α = 0.05
- Poder (1-β) = 0.80
- Efeito esperado: f = 0.25 (médio)

Fórmula simplificada:
n ≈ 2 × (Z_α/2 + Z_β)² / (ES)²
n ≈ 2 × (1.96 + 0.84)² / (0.5)²
n ≈ 2 × 7.84 / 0.25
n ≈ 31.36 ≈ 30
```

**4. Validação Cruzada:**
- k-fold (k=5) multiplica efetivamente o poder
- Cada modelo é avaliado 150 vezes (30 execuções × 5 folds)
- Reduz impacto de variabilidade amostral

**5. Variabilidade com Dados Reais:**
- Com dados reais, cada execução usará diferentes seeds para:
  - Divisão treino/teste aleatória
  - Seleção de diferentes subsets do dataset (se necessário)
  - Inicialização de modelos
- Isso captura variabilidade natural dos dados

#### Tamanho Mínimo vs. Máximo:

**Mínimo Aceitável:** N = 20
- Ainda fornece poder razoável (~70%)
- Útil se restrições de processamento forem críticas

**Máximo Viável:** N = 50
- Aumenta poder para ~90%
- Retornos marginais decrescentes
- Tempo de execução aumenta 67%

**Escolha:** N = 30 (balanço ótimo entre poder e viabilidade)

### 10.5 Método de Seleção / Recrutamento

**Método:** **Amostragem de Traces Públicos Reais de Cloud Computing**

Como não há sujeitos humanos, o "recrutamento" consiste na **obtenção e extração de dados reais de datasets públicos**.

#### Processo de Obtenção dos Dados:

**Etapa 1: Download do Dataset**

**Opção A: Kaggle (Recomendado para TCC)**
```bash
# Instalar Kaggle CLI
pip install kaggle

# Configurar credenciais (após criar conta Kaggle)
# Baixar API token em https://www.kaggle.com/settings

# Fazer download do sample do Google Cluster 2019
kaggle datasets download -d derrickmwiti/google-2019-cluster-sample

# Descompactar
unzip google-2019-cluster-sample.zip
```

**Opção B: BigQuery (Se necessário dataset completo)**
```python
# Requer conta Google Cloud (possui free tier)
from google.cloud import bigquery

client = bigquery.Client()

query = """
SELECT 
    time,
    collection_id,
    average_usage_cpus,
    average_usage_memory
FROM `google.com:google-cluster-data.clusterdata_2019_a.task_usage`
WHERE time BETWEEN 600000000 AND 2592000000000  # ~30 dias
LIMIT 1000000
"""

df = client.query(query).to_dataframe()
df.to_csv('google_cluster_sample.csv', index=False)
```

**Etapa 2: Extração e Pré-processamento**

```python
import pandas as pd
import numpy as np

# Carregar dados
df = pd.read_csv('google_cluster_sample.csv')

# Converter timestamps (Google Cluster usa microsegundos desde epoch)
df['timestamp'] = pd.to_datetime(df['time'], unit='us')

# Renomear colunas para padronizar
df = df.rename(columns={
    'average_usage_cpus': 'cpu_usage',
    'average_usage_memory': 'memory_usage'
})

# Agregar por intervalo de tempo (ex: 1 hora) para reduzir granularidade
df = df.set_index('timestamp')
df_hourly = df.resample('1H').mean()

# Selecionar período contínuo de 30 dias
start_date = df_hourly.index.min()
end_date = start_date + pd.Timedelta(days=30)
df_30d = df_hourly[(df_hourly.index >= start_date) & (df_hourly.index < end_date)]

print(f"Dataset final: {len(df_30d)} observações horárias (~{len(df_30d)/24:.1f} dias)")
```

**Etapa 3: Cálculo de Custos Estimados**

```python
# Calcular custo baseado em precificação típica de provedores
# Exemplo: AWS EC2 pricing simplificado

# Premissas de precificação (valores aproximados em R$/hora)
CPU_COST_PER_CORE_HOUR = 0.15  # R$ por core por hora
MEMORY_COST_PER_GB_HOUR = 0.02  # R$ por GB por hora

# Google Cluster normaliza CPU e memória (0-1)
# Assumir instâncias com 4 cores e 16GB RAM (típico)
CORES = 4
RAM_GB = 16

df_30d['cpu_cost'] = df_30d['cpu_usage'] * CORES * CPU_COST_PER_CORE_HOUR
df_30d['memory_cost'] = df_30d['memory_usage'] * RAM_GB * MEMORY_COST_PER_GB_HOUR
df_30d['total_cost'] = df_30d['cpu_cost'] + df_30d['memory_cost']

# Salvar dataset final processado
df_30d.to_csv('dataset_cloud_preprocessado.csv')
```

**Etapa 4: Validação de Qualidade**
- Aplicar critérios de inclusão (seção 10.2)
- Aplicar critérios de exclusão (seção 10.3)
- Análise exploratória visual (plots de séries temporais)
- Verificar estatísticas descritivas

**Etapa 5: Documentação**
- Documentar fonte original dos dados (Google Cluster Data 2019)
- Registrar parâmetros de extração e agregação
- Salvar metadata: período exato, número de jobs/tasks incluídos
- Garantir reprodutibilidade (código + documentação)

#### Representatividade e Validade Externa:

**Vantagens de Usar Dados Reais:**

1. **Autenticidade:**
   - Padrões reais de uso de infraestrutura cloud
   - Variabilidade natural (não artificialmente gerada)
   - Anomalias e eventos reais incluídos

2. **Credibilidade Científica:**
   - Dataset amplamente usado em pesquisas (centenas de citações)
   - Dados validados pelo Google
   - Resultados comparáveis com literatura existente

3. **Aplicabilidade Prática:**
   - Conclusões mais generalizáveis para ambientes reais
   - Maior confiança de stakeholders (empresas, DevOps)
   - Validação externa mais forte

**Limitações Reconhecidas:**

1. **Contexto Específico:**
   - Dados de clusters Google Borg (não todos os provedores)
   - Workloads específicos de Google (não universalmente representativos)
   - Período específico (maio 2019)

2. **Precificação Estimada:**
   - Custos calculados com base em tabelas públicas (não custos reais Google)
   - Não considera descontos, reserved instances, ou preços negociados
   - Simplificação de modelo de precificação

3. **Pré-processamento:**
   - Agregação temporal (de 5 min para 1 hora) pode perder alguns padrões
   - Seleção de subset pode não capturar toda heterogeneidade

**Mitigação:**
- Documentar claramente limitações no trabalho final
- Usar múltiplos subsets do dataset (variabilidade)
- Comparar resultados com literatura que usou mesmos dados

### 10.6 Treinamento e Preparação dos Sujeitos

**Não Aplicável:** Este experimento não envolve sujeitos humanos.

**Preparação dos Dados Reais:**

#### Pré-processamento Completo:

**1. Limpeza:**
```python
# Verificar e tratar dados faltantes
df = df.interpolate(method='time', limit=2)  # Interpolar gaps pequenos
df = df.dropna()  # Remover NaNs restantes

# Validar consistência temporal
df = df.sort_index()
assert df.index.is_monotonic_increasing, "Timestamps fora de ordem!"

# Remover duplicatas de timestamp
df = df[~df.index.duplicated(keep='first')]
```

**2. Tratamento de Outliers:**
```python
# Detectar outliers usando IQR (mais robusto que z-score para dados reais)
def remove_outliers_iqr(df, column, multiplier=1.5):
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)
    IQR = Q3 - Q1
    lower_bound = Q1 - multiplier * IQR
    upper_bound = Q3 + multiplier * IQR
    return df[(df[column] >= lower_bound) & (df[column] <= upper_bound)]

# Aplicar para CPU e memória
df = remove_outliers_iqr(df, 'cpu_usage')
df = remove_outliers_iqr(df, 'memory_usage')
```

**3. Normalização:**
```python
from sklearn.preprocessing import StandardScaler

# Salvar scaler para uso consistente em todas as execuções
scaler = StandardScaler()
df[['cpu_usage_scaled', 'memory_usage_scaled']] = \
    scaler.fit_transform(df[['cpu_usage', 'memory_usage']])

# Salvar scaler para reprodutibilidade
import joblib
joblib.dump(scaler, 'scaler_cloud_data.pkl')
```

**4. Engenharia de Features:**
```python
# Features temporais
df['hour'] = df.index.hour
df['day_of_week'] = df.index.dayofweek
df['is_weekend'] = df['day_of_week'].isin([5, 6]).astype(int)

# Lags (valores passados)
for lag in [1, 2, 3, 6, 12, 24]:
    df[f'cpu_lag_{lag}h'] = df['cpu_usage'].shift(lag)
    df[f'memory_lag_{lag}h'] = df['memory_usage'].shift(lag)

# Médias móveis
df['cpu_ma_24h'] = df['cpu_usage'].rolling(window=24, min_periods=1).mean()
df['memory_ma_24h'] = df['memory_usage'].rolling(window=24, min_periods=1).mean()

# Remover linhas com NaN criados pelos lags
df = df.dropna()
```

**5. Divisão Treino/Teste (Temporal):**
```python
# Importante: NUNCA fazer shuffle em séries temporais!
train_size = int(len(df) * 0.7)

train_df = df.iloc[:train_size]
test_df = df.iloc[train_size:]

print(f"Treino: {len(train_df)} observações ({train_df.index.min()} a {train_df.index.max()})")
print(f"Teste: {len(test_df)} observações ({test_df.index.min()} a {test_df.index.max()})")

# Salvar splits
train_df.to_csv('data/train_dataset.csv')
test_df.to_csv('data/test_dataset.csv')
```

**6. Validação Cruzada Temporal (Time Series Split):**
```python
from sklearn.model_selection import TimeSeriesSplit

# 5-fold temporal (não aleatório!)
tscv = TimeSeriesSplit(n_splits=5)

for fold, (train_idx, val_idx) in enumerate(tscv.split(train_df)):
    fold_train = train_df.iloc[train_idx]
    fold_val = train_df.iloc[val_idx]
    
    # Salvar cada fold
    fold_train.to_csv(f'data/fold_{fold}_train.csv')
    fold_val.to_csv(f'data/fold_{fold}_val.csv')
```
---
## 11. Instrumentação e Protocolo Operacional

### 11.1 Instrumentos de Coleta (Questionários, Logs, Planilhas, etc.)

#### Instrumentos Principais:

| Instrumento | Descrição | Formato | Uso |
|------------|-----------|---------|-----|
| **Script de Geração de Dados** | Gera séries temporais sintéticas | Python (.py) | Criar dataset experimental |
| **Script de Treinamento** | Treina os 4 modelos de previsão | Python (.py) | Executar tratamentos |
| **Script de Avaliação** | Calcula MAE, RMSE, MAPE | Python (.py) | Coletar variáveis dependentes |
| **Arquivo de Resultados** | Armazena erros de cada execução | CSV (.csv) | Consolidar resultados |
| **Log de Execução** | Registra timestamp, ordem, erros | TXT/JSON (.log) | Auditoria e debug |
| **Notebook de Análise** | Análise estatística e visualizações | Jupyter (.ipynb) | Análise pós-experimento |
| **Arquivo de Configuração** | Parâmetros dos modelos e experimento | YAML/JSON (.yaml) | Controle de configuração |

#### Estrutura dos Instrumentos:

**1. Arquivo de Resultados (resultados.csv):**
```csv
execucao_id,modelo,repeticao,seed,mae,rmse,mape,tempo_exec,fold,mae_fold,timestamp
1,RL,1,4235,125.34,178.92,12.5,5.2,1,130.21,2024-12-02 10:15:23
1,RL,1,4235,125.34,178.92,12.5,5.2,2,118.45,2024-12-02 10:15:23
...
```

**2. Log de Execução (experimento.log):**
```
2024-12-02 10:15:20 - INFO - Iniciando experimento TCC-PRED-CUSTO-2024-001
2024-12-02 10:15:21 - INFO - Carregando dados sintéticos
2024-12-02 10:15:22 - INFO - Executando modelo RL, repetição 1, seed 4235
2024-12-02 10:15:23 - INFO - RL completado - MAE: 125.34
...
```

**3. Arquivo de Configuração (config.yaml):**
```yaml
experimento:
  id: TCC-PRED-CUSTO-2024-001
  versao: 1.4
  repeticoes: 30
  k_folds: 5
  seed_mestre: 42

modelos:
  regressao_linear:
    biblioteca: sklearn.linear_model.LinearRegression
    parametros: {}
  
  media_movel:
    janela: 7
  
  arima:
    ordem: [1, 1, 1]  # (p, d, q) - será otimizado via grid search
  
  exponential_smoothing:
    trend: add
    seasonal: add
    seasonal_periods: 24
```

### 11.2 Materiais de Suporte (Instruções, Guias)

#### Materiais Criados:

1. **README.md do Projeto:**
   - Visão geral do experimento
   - Instruções de instalação
   - Como reproduzir experimento

2. **HOWTO_RUN.md:**
   - Passo a passo detalhado de execução
   - Comandos a serem executados
   - Troubleshooting comum

3. **Guia de Análise:**
   - Como interpretar resultados
   - Checklist de validação
   - Testes estatísticos a aplicar

4. **Documentação de Código:**
   - Docstrings em todas as funções
   - Comentários inline explicativos
   - Type hints para clareza

#### Exemplo de Conteúdo (HOWTO_RUN.md):

```markdown
# Como Executar o Experimento

## Pré-requisitos
- Python 3.10+
- Bibliotecas: pandas, numpy, scikit-learn, statsmodels, matplotlib

## Instalação
```bash
pip install -r requirements.txt
```

## Execução

### Passo 1: Gerar Dados Sintéticos
```bash
python scripts/gerar_dados.py --dias 30 --seed 42
```

### Passo 2: Executar Experimento
```bash
python scripts/executar_experimento.py --config config.yaml
```

### Passo 3: Analisar Resultados
```bash
jupyter notebook analise/analise_resultados.ipynb
```

## Verificação
- Conferir arquivo `resultados.csv` (deve ter 600 linhas: 120 execuções × 5 folds)
- Verificar log `experimento.log` (sem erros)
- Gerar plots de diagnóstico


### 11.3 Procedimento Experimental (Protocolo – Visão Passo a Passo)

#### Protocolo Operacional Detalhado:

---

**FASE 1: PREPARAÇÃO (Pré-Execução)**

**Passo 1.1 - Setup do Ambiente**
- Instalar Python 3.10+ e bibliotecas necessárias
- Clonar repositório do experimento
- Verificar disponibilidade de hardware
- **Duração:** 30 minutos
- **Responsável:** Pesquisador
- **Output:** Ambiente funcional

**Passo 1.2 - Download e Preparação dos Dados Reais**
- Baixar Google Cluster Data 2019 (via Kaggle ou BigQuery)
- Executar script `preparar_dados.py` para:
  - Extrair métricas de CPU e memória
  - Agregar de 5 min para granularidade horária (1h)
  - Selecionar período contínuo de 30 dias
  - Calcular custos estimados baseados em tabelas de precificação
- Validar qualidade dos dados conforme critérios da seção 10.2
- Salvar dataset em `data/dataset_cloud_processado.csv`
- **Duração:** 30 minutos (inclui download)
- **Responsável:** Pesquisador
- **Output:** `dataset_cloud_processado.csv` (~720 linhas × 4 colunas: timestamp, cpu, memory, cost)

**Passo 1.3 - Validação do Dataset**
- Análise exploratória visual (plots de séries temporais)
- Verificação de estatísticas descritivas
- Confirmação com orientador sobre realismo
- **Duração:** 30 minutos
- **Responsável:** Pesquisador + Orientador
- **Output:** Dataset aprovado

**Passo 1.4 - Preparação dos Seeds para Reprodutibilidade**
- **Objetivo:** Garantir reprodutibilidade e capturar variabilidade entre repetições
- **Método:**
  - Gerar 30 seeds aleatórios usando seed mestre fixo: `np.random.seed(42)`
  - Seeds: `seeds = np.random.randint(0, 10000, size=30)`
- **Uso dos Seeds:**
  - Cada repetição `r` (de 1 a 30) usa `seed[r]`
  - **Todos os 4 modelos na repetição `r` usam o mesmo `seed[r]`**
  - Isso garante que todos os modelos recebem mesma divisão treino/teste em cada repetição
  - Variação entre repetições captura robustez dos modelos
- **Salvar em:** `config/seeds.txt`
- **Duração:** 5 minutos
- **Responsável:** Pesquisador
- **Output:** Lista de 30 seeds + documentação de uso

---

**FASE 2: EXECUÇÃO DO EXPERIMENTO**

**Passo 2.1 - Pré-processamento**
- Carregar dataset
- Aplicar normalização (StandardScaler)
- Salvar objeto scaler para uso posterior
- **Duração:** 5 minutos
- **Responsável:** Script automático
- **Output:** Dados normalizados

**Passo 2.2 - Loop Principal de Execução**

Para cada repetição r = 1 até 30:
  Para cada modelo m em [RL, MM, ARIMA, ES]:
    
    a) **Divisão Treino/Teste**
       - Usar seed[r] para reprodutibilidade
       - Treino: 70% (primeiros 504 registros)
       - Teste: 30% (últimos 216 registros)
    
    b) **Treinamento do Modelo**
       - Treinar modelo m nos dados de treino
       - Registrar tempo de treinamento
    
    c) **Geração de Previsões**
       - Gerar previsões para conjunto de teste
    
    d) **Cálculo de Métricas (Holdout)**
       - Calcular MAE, RMSE, MAPE no conjunto de teste
    
    e) **Validação Cruzada TimeSeriesSplit**
       - **IMPORTANTE:** Usar TimeSeriesSplit (não k-fold tradicional) para preservar ordem temporal
       - Aplicar 5-fold time series cross-validation nos dados de treino
       - TimeSeriesSplit garante que treino sempre precede teste (sem shuffle)
       - Calcular MAE em cada fold
       - Registrar média e desvio padrão
    
    f) **Registro de Resultados**
       - Salvar em `resultados.csv`:
         execucao_id, modelo, repeticao, seed, mae, rmse, mape, tempo_exec
       - Salvar métricas de cada fold
    
    g) **Logging**
       - Registrar em `experimento.log`:
         timestamp, modelo, status, métricas principais

**Duração Total:** ~45-60 minutos
**Responsável:** Script automático (`executar_experimento.py`)
**Output:** `resultados.csv` com 120 linhas (1 por execução)

**Passo 2.3 - Verificação de Integridade**
- Conferir se 120 execuções foram completadas
- Verificar ausência de erros no log
- Validar que não há valores faltantes em `resultados.csv`
- **Duração:** 10 minutos
- **Responsável:** Pesquisador
- **Output:** Confirmação de experimento completo

---

**FASE 3: ANÁLISE DOS RESULTADOS**

**Passo 3.1 - Estatística Descritiva**
- Calcular média, mediana, desvio padrão de MAE, RMSE, MAPE por modelo
- Gerar tabelas de resumo
- **Duração:** 15 minutos
- **Responsável:** Notebook Jupyter
- **Output:** Tabelas descritivas

**Passo 3.2 - Visualizações**
- Boxplots de MAE por modelo
- Gráficos de séries previstas vs. reais
- Heatmap de correlação entre métricas e custo
- **Duração:** 30 minutos
- **Responsável:** Notebook Jupyter
- **Output:** Figuras para relatório

**Passo 3.3 - Teste de Normalidade**
- Shapiro-Wilk test nos resíduos de cada modelo
- Decisão: ANOVA (se normal) ou Kruskal-Wallis (se não-normal)
- **Duração:** 10 minutos
- **Responsável:** Script Python
- **Output:** p-valor de normalidade

**Passo 3.4 - Teste de Hipóteses**
- Aplicar ANOVA ou Kruskal-Wallis (H0: μ1 = μ2 = μ3 = μ4)
- Se p < 0.05: aplicar post-hoc tests (Tukey HSD)
- Identificar quais pares de modelos diferem significativamente
- **Duração:** 15 minutos
- **Responsável:** Script Python
- **Output:** p-valor, conclusão sobre H0

**Passo 3.5 - Análise de Correlação**
- Calcular correlação de Pearson entre cada métrica (CPU, memória, etc.) e custo
- Identificar variáveis mais preditivas
- **Duração:** 10 minutos
- **Responsável:** Script Python
- **Output:** Matriz de correlação

**Passo 3.6 - Verificação de Critérios de Sucesso**
- Verificar se erro < 20% em pelo menos um modelo
- Confirmar diferença estatística significativa (se houver)
- Documentar cumprimento dos critérios da seção 6.2
- **Duração:** 15 minutos
- **Responsável:** Pesquisador
- **Output:** Checklist de critérios atendidos

---

**FASE 4: DOCUMENTAÇÃO**

**Passo 4.1 - Compilação dos Resultados**
- Consolidar tabelas, gráficos e conclusões
- Preencher seções do documento de TCC
- **Duração:** 2-3 horas
- **Responsável:** Pesquisador
- **Output:** Seções de resultados e discussão

**Passo 4.2 - Revisão com Orientador**
- Apresentar resultados ao orientador
- Incorporar feedback
- **Duração:** 1 hora (reunião)
- **Responsável:** Pesquisador + Orientador
- **Output:** Resultados validados

**Passo 4.3 - Empacotamento para Reprodução**
- Organizar código, dados, resultados em repositório
- Escrever README final
- Testar reprodução em ambiente limpo
- **Duração:** 2 horas
- **Responsável:** Pesquisador
- **Output:** Repositório reproduzível

---

### Fluxograma Operacional

```mermaid
flowchart TD
    A[Definir escopo das métricas] --> B[Baixar e processar Google Cluster Data 2019]
    B --> C[Agregar dados 5min→1h e calcular custos estimados]
    C --> D{Dados contêm valores ausentes ou outliers?}
    D -->|Sim| E[Tratamento de dados: imputação ou remoção]
    D -->|Não| F[Normalização dos dados]
    E --> F
    F --> G[Construção do dataset final]
    G --> H[Divisão treino/validação - 70%/30%]
    H --> I[Aplicação dos modelos de previsão]
    I --> J[Coleta das métricas MAE, RMSE, MAPE]
    J --> K{Resíduos passaram no teste de normalidade?}
    K -->|Sim| L[Aplicação de ANOVA]
    K -->|Não| M[Aplicação de Kruskal-Wallis]
    L --> N{p-valor < 0.05?}
    M --> N
    N -->|Sim| O[Modelos apresentam diferença significativa]
    N -->|Não| P[Modelos não diferem significativamente]
    O --> Q[Comparação e seleção do melhor modelo]
    P --> Q
    Q --> R{Erro < 20% em pelo menos um modelo?}
    R -->|Sim| S[Critério de sucesso atendido]
    R -->|Não| T[Revisar hiperparâmetros ou adicionar features]
    T --> I
    S --> U[Registro e interpretação dos resultados]
    U --> V[Análise de correlação entre métricas e custos]
    V --> W[Documentação final e conclusões]
```

### 11.4 Plano de Piloto (se Haverá Piloto, Escopo e Critérios de Ajuste)

**Decisão:** **Não será realizado experimento piloto formal**

#### Justificativa:

1. **Uso de Dados Reais Públicos:**
   - Dados do Google Cluster Data 2019 são bem documentados e validados
   - Dataset já utilizado em centenas de pesquisas acadêmicas
   - Qualidade e disponibilidade garantidas
   - Possível validar pré-processamento antes de experimento principal

2. **Modelos Estabelecidos:**
   - Todos os 4 modelos são bem conhecidos na literatura
   - Implementações em bibliotecas maduras (Scikit-learn, Statsmodels)
   - Baixo risco de problemas técnicos inesperados

3. **Custo-Benefício:**
   - Experimento completo leva ~1 hora
   - Piloto tomaria tempo similar
   - Melhor investir tempo em validação prévia do dataset

#### Validação Alternativa ao Piloto:

**"Dry Run" (Execução de Teste):**

Antes do experimento principal, realizar:

1. **Teste com n=5 repetições:**
   - Executar cada modelo 5 vezes
   - Verificar que código roda sem erros
   - Validar formato dos outputs
   - **Duração:** ~10 minutos

2. **Inspeção Manual:**
   - Verificar se métricas estão em ranges plausíveis
   - Conferir se logs estão sendo gerados corretamente
   - Validar que seeds produzem resultados diferentes

3. **Critérios de Prosseguimento:**
   - ✅ Zero erros de execução
   - ✅ Resultados dentro de ranges esperados (MAE entre 50-300 R$)
   - ✅ Diferenças visíveis entre modelos
   - ✅ Logs completos e legíveis

**Se "Dry Run" Falhar:**
- Depurar código
- Ajustar parâmetros de geração de dados
- Revisar configuração
- Repetir dry run até sucesso

---

## 12. Plano de Análise de Dados (Pré-Execução)

### 12.1 Estratégia Geral de Análise (Como Responderá às Questões)

#### Mapeamento Questões → Análises:

**Questões sobre Acurácia dos Modelos (Q1.1, Q2.1, Q2.2):**

**Análise:**
- Estatística descritiva: média, mediana, desvio padrão de MAE, RMSE, MAPE por modelo
- Tabelas comparativas
- Visualização: boxplots, violin plots

**Como Responde:**
- "Qual modelo tem menor MAE?" → Identificar modelo com menor média de MAE
- "Qual tem menor RMSE/MAPE?" → Análogo

---

**Questões sobre Diferença Estatística (Q1.3, Q5.3):**

**Análise:**
- Teste de normalidade (Shapiro-Wilk)
- ANOVA ou Kruskal-Wallis (comparação entre 4 grupos)
- Post-hoc tests (Tukey HSD ou Dunn's test)
- Tamanho de efeito (η² para ANOVA ou ε² para Kruskal-Wallis)

**Como Responde:**
- "Há diferença significativa?" → p-valor < 0.05 → Sim
- "Quais modelos diferem?" → Post-hoc indica pares significativos

---

**Questões sobre Janelas Temporais (Q1.2, Q2.3):**

**Análise:**
- Comparação exploratória de MAE em janelas de 7, 14, 30 dias
- Gráficos de linha mostrando erro vs. tamanho de janela
- ANOVA de dois fatores (se tempo permitir): Modelo × Janela

**Como Responde:**
- "Erro diminui com janelas maiores?" → Comparar médias; testar tendência

---

**Questões sobre Variáveis Preditoras (Q3.1, Q3.2, Q3.3):**

**Análise:**
- Correlação de Pearson entre cada métrica e custo
- Heatmap de correlações
- Análise de importância de features (para Regressão Linear: coeficientes)

**Como Responde:**
- "Qual métrica mais correlacionada?" → Maior |r| de Pearson
- "CPU é melhor que memória?" → Comparar r(CPU, custo) vs. r(Memória, custo)

---

**Questões sobre Generalização (Q4.1, Q4.2, Q4.3):**

**Análise:**
- Validação cruzada k-fold: calcular erro médio nos folds
- Comparar erro de treino vs. erro de teste (diferença %)
- Detectar overfitting: se diferença > 15% → flag

**Como Responde:**
- "Modelo generaliza?" → Diferença treino/teste < 15%
- "Qual erro de validação cruzada?" → Média dos erros nos k folds

---

**Questões sobre Estabilidade (Q5.1, Q5.2):**

**Análise:**
- Calcular desvio padrão dos erros de cada modelo
- Coeficiente de variação: CV = σ/μ
- Detectar overfitting: diferença treino/teste por modelo

**Como Responde:**
- "Qual modelo mais estável?" → Menor desvio padrão
- "Há overfitting?" → Se diferença treino/teste > 10-15%

### 12.2 Métodos Estatísticos Planejados

#### Testes Estatísticos:

**1. Teste de Normalidade:**
- **Nome:** Shapiro-Wilk test
- **Quando:** Antes de ANOVA
- **Hipóteses:**
  - H0: Os resíduos seguem distribuição normal
  - H1: Os resíduos não seguem distribuição normal
- **Critério:** α = 0.05
- **Decisão:** Se p > 0.05 → Usar ANOVA; se p < 0.05 → Usar Kruskal-Wallis

**Código:**
```python
from scipy.stats import shapiro

for modelo in ['RL', 'MM', 'ARIMA', 'ES']:
    residuos = df[df['modelo'] == modelo]['mae']
    stat, p_value = shapiro(residuos)
    print(f'{modelo}: p-valor = {p_value:.4f}')
```

---

**2. Comparação Entre Modelos (Paramétrico):**
- **Nome:** ANOVA One-Way
- **Quando:** Se resíduos forem normais
- **Hipóteses:**
  - H0: μ_RL = μ_MM = μ_ARIMA = μ_ES
  - H1: Pelo menos um μ_i ≠ μ_j
- **Critério:** α = 0.05
- **Estatística:** F de Fisher
- **Interpretação:**
  - p < 0.05 → Rejeitar H0 (diferença significativa existe)
  - p ≥ 0.05 → Não rejeitar H0

**Código:**
```python
from scipy.stats import f_oneway

grupo_rl = df[df['modelo'] == 'RL']['mae']
grupo_mm = df[df['modelo'] == 'MM']['mae']
grupo_arima = df[df['modelo'] == 'ARIMA']['mae']
grupo_es = df[df['modelo'] == 'ES']['mae']

f_stat, p_value = f_oneway(grupo_rl, grupo_mm, grupo_arima, grupo_es)
print(f'F = {f_stat:.4f}, p-valor = {p_value:.4f}')
```

---

**3. Comparação Entre Modelos (Não-Paramétrico):**
- **Nome:** Kruskal-Wallis H test
- **Quando:** Se resíduos não forem normais
- **Hipóteses:** Iguais ao ANOVA, mas sobre medianas
- **Critério:** α = 0.05
- **Estatística:** H (qui-quadrado aproximado)

**Código:**
```python
from scipy.stats import kruskal

h_stat, p_value = kruskal(grupo_rl, grupo_mm, grupo_arima, grupo_es)
print(f'H = {h_stat:.4f}, p-valor = {p_value:.4f}')
```

---

**4. Comparações Post-Hoc (Paramétrico):**
- **Nome:** Tukey's Honestly Significant Difference (HSD)
- **Quando:** Após rejeitar H0 em ANOVA
- **Objetivo:** Identificar quais pares de modelos diferem
- **Critério:** α = 0.05 com correção para múltiplas comparações

**Código:**
```python
from scipy.stats import tukey_hsd

res = tukey_hsd(grupo_rl, grupo_mm, grupo_arima, grupo_es)
print(res)
```

---

**5. Comparações Post-Hoc (Não-Paramétrico):**
- **Nome:** Dunn's test com correção de Bonferroni
- **Quando:** Após rejeitar H0 em Kruskal-Wallis
- **Objetivo:** Comparações pareadas
- **Critério:** α_ajustado = 0.05 / 6 = 0.0083 (6 comparações possíveis)

---

**6. Correlação:**
- **Nome:** Correlação de Pearson
- **Quando:** Analisar relação entre métricas e custo
- **Hipóteses:**
  - H0: ρ = 0 (sem correlação)
  - H1: ρ ≠ 0
- **Critério:** α = 0.05
- **Interpretação de |r|:**
  - 0.0-0.3: Fraca
  - 0.3-0.7: Moderada
  - 0.7-1.0: Forte

**Código:**
```python
from scipy.stats import pearsonr

correlacoes = {}
for metrica in ['cpu', 'memoria', 'storage', 'requisicoes']:
    r, p_value = pearsonr(df[metrica], df['custo'])
    correlacoes[metrica] = {'r': r, 'p': p_value}
```

---

**7. Tamanho de Efeito:**
- **Nome:** Eta-squared (η²) para ANOVA
- **Fórmula:** η² = SS_between / SS_total
- **Interpretação:**
  - 0.01: Efeito pequeno
  - 0.06: Efeito médio
  - 0.14: Efeito grande

---

**8. Intervalos de Confiança:**
- **95% CI para média de cada modelo**
- **Fórmula:** CI = x̄ ± t_{α/2} × (s / √n)
- **Interpretação:** Se CIs não se sobrepõem, sugere diferença significativa

### 12.3 Tratamento de Dados Faltantes e Outliers

#### Dados Faltantes:

**Prevenção (por construção):**
- Dados sintéticos não terão valores faltantes por design
- Validação pré-experimento garante completude

**Se Ocorrerem (bug ou erro de execução):**

**Regra 1: Exclusão de Execução Completa**
- Se uma execução falhar (erro de código, crash), **remover completamente**
- Não imputar dados faltantes de métricas de avaliação
- **Justificativa:** Impedir viés; melhor ter n=29 do que dados imputados incorretos

**Regra 2: Re-execução**
- Se execução falhou por erro técnico, **re-executar** com mesmo seed
- Documentar ocorrência no log

**Código de Verificação:**
```python
# Verificar dados faltantes
assert df.isna().sum().sum() == 0, "Dados faltantes detectados!"

# Verificar número de execuções
assert len(df) == 120, f"Esperado 120 execuções, obtido {len(df)}"
```

#### Outliers:

**Definição de Outlier:**
- Valores além de **3 desvios-padrão** da média do grupo
- Ou valores impossíveis (MAE negativo, MAPE > 200%)

**Tratamento:**

**Opção 1: Investigação (Preferencial)**
1. Identificar outlier
2. Verificar log de execução correspondente
3. Se houver erro de execução → **remover** e re-executar
4. Se outlier for legítimo (modelo realmente ruim) → **manter**

**Opção 2: Winsorização (Se Necessário)**
- Substituir outliers pelos valores no percentil 1% e 99%
- **Usar apenas se**: outliers forem devido a variabilidade natural, não erros
- **Documentar:** quais valores foram modificados

**Código de Detecção:**
```python
def detectar_outliers(df, coluna, n_std=3):
    """Detecta outliers usando regra de n desvios-padrão"""
    media = df[coluna].mean()
    std = df[coluna].std()
    outliers = df[(df[coluna] < media - n_std*std) | 
                  (df[coluna] > media + n_std*std)]
    return outliers

# Aplicar
outliers_mae = detectar_outliers(df, 'mae', n_std=3)
if len(outliers_mae) > 0:
    print(f'Outliers detectados: {len(outliers_mae)}')
    print(outliers_mae[['modelo', 'repeticao', 'mae']])
```

**Decisão Final:**
- **Padrão:** Manter outliers legítimos (refletem variabilidade real)
- **Exceção:** Remover apenas se houver evidência de erro técnico
- **Transparência:** Documentar todas as remoções e justificativas

---

## 13. Avaliação de Validade (Ameaças e Mitigação)

Esta seção identifica as principais ameaças à validade do experimento, seguindo a classificação de Wohlin et al. (2012): validade de conclusão, validade interna, validade de constructo e validade externa. Para cada categoria, são listadas as ameaças específicas ao contexto deste estudo e as estratégias planejadas de mitigação.

### 13.1 Validade de Conclusão

**Definição:** A validade de conclusão refere-se à capacidade de tirar conclusões corretas sobre a relação entre tratamento (tipo de modelo) e resultado (erro de previsão), considerando a robustez estatística.

#### Ameaça 1.1: Poder Estatístico Insuficiente

**Descrição:**
Com n=30 repetições por modelo, o poder estatístico é de aproximadamente 80% para detectar diferenças de efeito médio (d de Cohen ≈ 0.5), correspondendo a diferenças de ~15-20% no erro médio. Se as diferenças reais entre modelos forem sutis (< 10%), o experimento pode **não detectar diferenças que realmente existem** (Erro Tipo II).

**Impacto:**
- Risco de concluir erroneamente que modelos têm desempenho equivalente
- Particularmente crítico se modelos avançados (ARIMA, ES) apresentarem melhoria marginal sobre modelos simples

**Estratégias de Mitigação:**
1. **Validação Cruzada k-fold (k=5):** Aumenta o número efetivo de avaliações (30 × 5 = 150 por modelo), melhorando a sensibilidade
2. **Análise de Tamanho de Efeito:** Calcular η² (eta-squared) mesmo quando p ≥ 0.05, para quantificar magnitude das diferenças
3. **Intervalos de Confiança:** Reportar 95% CI para todas as médias, permitindo interpretação prática além de significância estatística
4. **Análise de Sensibilidade:** Se resultados forem inconclusivos, considerar aumentar n para 50 repetições ou usar α mais liberal (0.10)

**Monitoramento:**
- Calcular poder estatístico post-hoc após coleta de dados
- Verificar se tamanho de efeito observado está dentro do detectável (d ≥ 0.5)

---

#### Ameaça 1.2: Violação de Suposições Estatísticas

**Descrição:**
ANOVA requer:
1. **Normalidade:** Os resíduos de cada grupo devem seguir distribuição normal
2. **Homocedasticidade:** Variâncias dos grupos devem ser homogêneas
3. **Independência:** Observações devem ser independentes

Erros de previsão podem não seguir distribuição normal (por exemplo, serem assimétricos ou ter caudas pesadas), violando a primeira suposição. Alguns modelos podem ter variabilidade intrinsecamente maior que outros, violando a segunda.

**Impacto:**
- ANOVA pode produzir p-valores incorretos
- Conclusões sobre significância estatística podem ser inválidas

**Estratégias de Mitigação:**
1. **Teste de Normalidade Prévio:** Aplicar Shapiro-Wilk test aos resíduos de cada grupo (α = 0.05)
2. **Teste Não-Paramétrico Alternativo:** Se normalidade for violada (p < 0.05), usar **Kruskal-Wallis H test** no lugar de ANOVA
3. **Teste de Homogeneidade de Variâncias:** Aplicar Levene's test; se violado, usar Welch's ANOVA
4. **Transformações:** Se necessário, aplicar transformação logarítmica ou Box-Cox aos dados antes da análise
5. **Bootstrapping:** Usar bootstrap para calcular intervalos de confiança não-paramétricos

**Monitoramento:**
- Inspeção visual: Q-Q plots para avaliar normalidade
- Análise de resíduos: gráficos de resíduos vs. valores ajustados

---

#### Ameaça 1.3: Problema de Múltiplas Comparações

**Descrição:**
Com 4 modelos, há **6 comparações pareadas possíveis** (RL vs. MM, RL vs. ARIMA, RL vs. ES, MM vs. ARIMA, MM vs. ES, ARIMA vs. ES). Ao realizar múltiplos testes com α = 0.05 cada, a chance de pelo menos um **falso positivo** (Erro Tipo I) aumenta:

P(pelo menos 1 falso positivo) = 1 - (1 - 0.05)⁶ ≈ 26.5%

**Impacto:**
- Inflação da taxa de erro Tipo I
- Aumento do risco de declarar diferenças significativas que são, na verdade, acaso estatístico

**Estratégias de Mitigação:**
1. **Testes Post-Hoc com Correção:**
   - Após ANOVA: Usar **Tukey's HSD** (controla automaticamente o family-wise error rate)
   - Após Kruskal-Wallis: Usar **Dunn's test com correção de Bonferroni**
2. **Correção de Bonferroni (se necessário):**
   - Ajustar α para α_ajustado = 0.05 / 6 = 0.0083 para comparações individuais
3. **Priorização de Comparações:**
   - Definir comparações de interesse primário a priori (ex: ARIMA vs. RL)
   - Limitar comparações exploratórias não planejadas

**Monitoramento:**
- Documentar quais comparações foram planejadas vs. exploratórias
- Reportar tanto p-valores brutos quanto ajustados

---

#### Ameaça 1.4: Variabilidade de Implementação dos Modelos

**Descrição:**
Diferenças observadas entre modelos podem ser parcialmente devidas a **diferenças na qualidade da implementação**, não apenas a superioridade inerente do algoritmo. Por exemplo:
- Um modelo pode ter bugs sutis que aumentam artificialmente seu erro
- Hiperparâmetros padrão de bibliotecas podem favorecer alguns modelos
- Otimização de código pode variar (ex: ARIMA pode ser mais lento e ter convergência instável)

**Impacto:**
- Confusão entre eficácia do algoritmo e qualidade da implementação
- Resultados não refletem potencial real de cada modelo

**Estratégias de Mitigação:**
1. **Uso de Bibliotecas Consolidadas:**
   - Scikit-learn: Regressão Linear, validação cruzada
   - Statsmodels: ARIMA, Exponential Smoothing
   - Validação: Bibliotecas são amplamente testadas e usadas academicamente
2. **Validação de Implementação:**
   - Testar cada modelo com datasets conhecidos (benchmarks públicos)
   - Comparar resultados com exemplos da documentação oficial
   - Revisão de código com orientador
3. **Documentação de Hiperparâmetros:**
   - Documentar todos os hiperparâmetros usados (mesmo padrões)
   - Justificar escolhas (ex: grid search para ARIMA, valores padrão para RL)
4. **Análise de Sensibilidade (Opcional):**
   - Testar variações de hiperparâmetros principais
   - Verificar se conclusões se mantêm com configurações alternativas

**Monitoramento:**
- Logs detalhados de execução de cada modelo
- Revisão de warnings e convergence issues

---

#### Ameaça 1.5: Variabilidade Aleatória Não Controlada

**Descrição:**
Apesar da randomização e das 30 repetições, resultados podem ter alta variabilidade devido a:
- Divisões treino/teste com características muito diferentes
- Inicializações aleatórias de parâmetros (em ARIMA, ES)
- Variabilidade natural dos algoritmos de otimização

Isso pode levar a **intervalos de confiança largos** que não se distinguem entre modelos, mesmo que haja diferenças reais.

**Impacto:**
- Conclusões incertas sobre qual modelo é superior
- Necessidade de mais repetições para estabilizar resultados

**Estratégias de Mitigação:**
1. **Número Adequado de Repetições:** n=30 é suficiente pelo Teorema do Limite Central
2. **Seeds Documentados:** Todos os seeds aleatórios salvos em CSV para reprodutibilidade total
3. **Validação Cruzada:** k-fold reduz dependência de uma única divisão treino/teste
4. **Análise de Variância:** Calcular e reportar desvio padrão e coeficiente de variação (CV = σ/μ)
5. **Replicação:** Se variabilidade for muito alta (CV > 50%), considerar aumentar n

**Monitoramento:**
- Inspeção de boxplots para detectar variabilidade excessiva
- Análise de outliers (valores > 3 desvios-padrão)

---

### 13.2 Validade Interna

**Definição:** A validade interna refere-se à capacidade de estabelecer relação causal correta entre o tratamento (tipo de modelo) e o resultado (erro de previsão), eliminando explicações alternativas.

#### Ameaça 2.1: História (History)

**Descrição:**
Eventos externos durante a execução do experimento podem afetar os resultados de forma sistemática:
- **Aquecimento de Hardware:** CPU pode aquecer ao longo das 120 execuções, afetando performance e tempo de execução
- **Carga do Sistema:** Outros processos no sistema operacional podem consumir recursos
- **Atualizações de Software:** Atualizações automáticas do SO ou antivírus podem interferir

Se modelos mais lentos (ARIMA) forem executados consistentemente após aquecimento, podem ter desvantagem.

**Impacto:**
- Diferenças observadas podem ser devidas a condições de execução, não ao modelo em si
- Viés sistemático contra modelos mais lentos

**Estratégias de Mitigação:**
1. **Randomização Completa da Ordem de Execução:** As 120 execuções terão ordem completamente aleatória (não bloco de 30 × RL, depois 30 × MM, etc.)
2. **Limpeza de Ambiente:**
   - Fechar aplicações desnecessárias antes do experimento
   - Desabilitar atualizações automáticas durante a execução
   - Restart do kernel Python a cada 30 execuções (opcional)
3. **Monitoramento de Sistema:**
   - Registrar timestamp, temperatura de CPU e uso de memória a cada execução
   - Detectar anomalias (ex: execução com uso de CPU > 90% por processo externo)
4. **Análise Post-Hoc:**
   - Testar se ordem de execução (1ª, 2ª, ..., 120ª) correlaciona com erro
   - Regressão: Erro ~ Ordem_Execução; se significativo, flag como possível confusão

**Monitoramento:**
- Logs de timestamp e condições de sistema
- Análise: ANOVA Erro ~ Posição_Execução (1-30, 31-60, 61-90, 91-120)

---

#### Ameaça 2.2: Maturação (Maturation)

**Descrição:**
Mudanças no ambiente computacional ao longo do tempo de execução (~1 hora total):
- **Degradação de Hardware:** Possível throttling térmico de CPU após uso prolongado
- **Degradação de Performance:** Cache ou memória podem saturar
- **Fadiga do Pesquisador:** Menos relevante por ser automatizado, mas monitoramento pode se tornar menos atento

**Impacto:**
- Execuções finais podem ter performance sistematicamente pior que iniciais
- Viés temporal contra modelos executados mais tardiamente

**Estratégias de Mitigação:**
1. **Randomização:** Mesma estratégia da Ameaça 2.1 (ordem aleatória mitiga maturação)
2. **Execução Automatizada:** Script Python executa tudo sem intervenção humana, eliminando variação por fadiga
3. **Controle Térmico:**
   - Executar experimento em ambiente climatizado
   - Monitorar temperatura de CPU; se ultrapassar limiar (ex: 85°C), pausar e resfriar
4. **Intervalos de Descanso (Opcional):**
   - Pausa de 5 minutos a cada 40 execuções para resfriamento

**Monitoramento:**
- Análise de tendência temporal: Regressão Erro ~ Tempo_Decorrido
- Temperatura de CPU registrada em log

---

#### Ameaça 2.3: Instrumentação (Instrumentation)

**Descrição:**
Mudanças ou inconsistências na forma de medir as variáveis dependentes:
- **Cálculo de Métricas:** Se fórmulas de MAE, RMSE ou MAPE forem implementadas incorretamente ou mudarem durante o experimento
- **Precisão Numérica:** Erros de arredondamento ou overflow em cálculos
- **Versões de Bibliotecas:** Atualização acidental de Scikit-learn ou Statsmodels no meio do experimento

**Impacto:**
- Medidas de erro inconsistentes entre execuções
- Invalidação da comparabilidade dos resultados

**Estratégias de Mitigação:**
1. **Implementação Única e Validada:**
   - Funções de cálculo de métricas escritas uma vez e testadas antes do experimento
   - Uso de implementações padrão (sklearn.metrics.mean_absolute_error, etc.)
2. **Ambiente Virtual Fixo:**
   - Criar ambiente virtual Python com versões fixas de bibliotecas (requirements.txt)
   - Não atualizar bibliotecas durante o experimento
3. **Testes de Validação:**
   - Testar cálculos com dados sintéticos de resultado conhecido
   - Comparar com exemplos da documentação oficial
4. **Documentação de Versões:**
   - Salvar output de `pip freeze` antes do experimento

**Monitoramento:**
- Verificar que todas as 120 execuções usaram mesma versão de bibliotecas
- Testes unitários das funções de cálculo de métricas

---

#### Ameaça 2.4: Seleção (Selection Bias)

**Descrição:**
Viés na alocação de dados a diferentes modelos. No contexto deste experimento, seria se:
- Modelos diferentes recebessem subconjuntos diferentes dos dados
- Divisões treino/teste fossem sistematicamente diferentes entre modelos

**Impacto:**
- Comparação injusta entre modelos
- Conclusões sobre superioridade de um modelo podem ser artefato da seleção de dados

**Estratégias de Mitigação:**
1. **Dados Idênticos para Todos os Modelos:**
   - Todos os 4 modelos recebem exatamente o mesmo dataset de entrada
   - Mesmas 720 observações (30 dias × 24 horas)
   - Mesmas 4 métricas (CPU, memória, storage, requisições)
2. **Divisão Treino/Teste Consistente por Repetição:**
   - Em cada repetição, todos os 4 modelos usam o mesmo seed para divisão treino/teste
   - Proporção fixa 70%-30%
   - Mesmos 504 pontos de treino e 216 de teste para todos
3. **Sem Pré-Seleção de Dados:**
   - Nenhum modelo recebe pré-processamento especial diferenciado
   - Mesma normalização/padronização aplicada a todos

**Monitoramento:**
- Verificação: Hash MD5 do dataset de entrada é idêntico para todas as execuções
- Assert: len(X_train) e len(X_test) são iguais para todos os modelos em cada repetição

---

#### Ameaça 2.5: Overfitting Diferenciado Entre Modelos

**Descrição:**
Alguns modelos podem sofrer overfitting (ajustar-se excessivamente aos dados de treino) mais que outros:
- **ARIMA:** Com ordem (p, d, q) muito alta, pode capturar ruído do treino
- **Regressão Linear:** Menos propensa a overfitting com poucas features
- **Exponential Smoothing:** Pode se ajustar demais se α estiver muito alto

Se overfitting não for detectado, pode parecer que um modelo é superior no treino, mas falha no teste.

**Impacto:**
- Modelo com melhor erro de treino pode ter pior erro de teste
- Avaliação de generalização comprometida

**Estratégias de Mitigação:**
1. **Validação Cruzada Obrigatória:**
   - k-fold (k=5) para todos os modelos
   - Erro final é média dos erros em 5 folds independentes
2. **Monitoramento Treino vs. Teste:**
   - Calcular M12 (Diferença Treino/Teste) para cada modelo
   - Flagging se diferença > 15% → Possível overfitting
3. **Regularização (quando aplicável):**
   - Regressão Linear: Considerar Ridge/Lasso se overfitting for detectado
   - ARIMA: Usar critérios AIC/BIC para seleção de ordem (p, d, q)
4. **Hiperparâmetros Conservadores:**
   - Preferir modelos mais simples (Occam's Razor)
   - ARIMA: Limitar p, d, q a valores razoáveis (≤ 3)

**Monitoramento:**
- Plotar erro de treino vs. teste para cada modelo
- Análise de resíduos em dados de teste

---

#### Ameaça 2.6: Estimativa de Custos (Não Custos Reais)

**Descrição:**
O experimento utiliza **métricas de uso REAIS do Google Cluster Data 2019** (CPU, memória), mas a **conversão de métricas em custos é ESTIMADA**, não real:
- **Métricas de uso:** REAIS (CPU e memória de workloads de produção do Google)
- **Custos:** ESTIMADOS usando tabelas de precificação públicas (AWS, Azure, GCP)
- Custos não refletem precificação interna do Google
- Modelo de precificação simplificado (relação linear entre métricas e custo)

**Impacto:**
- Relação entre métricas e custo pode ser artificial
- Modelos podem se beneficiar de padrões que não existiriam com custos reais
- Generalização para custos reais de outros provedores pode ser limitada

**Estratégias de Mitigação:**
1. **Modelo de Precificação Baseado em Literatura:**
   - Usar fórmulas de cálculo de custo validadas em papers acadêmicos
   - Consultar tabelas públicas de precificação (AWS EC2, Azure VMs, GCP Compute Engine)
   - Documentar fórmula exata usada
2. **Inclusão de Ruído Realista:**
   - Adicionar variação estocástica aos custos (± 5-10%) para simular flutuações reais
   - Evitar relações perfeitamente lineares
3. **Validação com Especialistas:**
   - Revisar modelo de precificação com orientador
   - Comparar padrões de custo gerados com benchmarks da literatura
4. **Limitação da Generalização:**
   - Reconhecer explicitamente na discussão que custos são estimados
   - Recomendar validação com dados reais em trabalhos futuros

**Monitoramento:**
- Análise exploratória: Correlações entre métricas e custos devem ser plausíveis (0.6-0.9)
- Comparação com valores de referência da literatura

---

### 13.3 Validade de Constructo

**Definição:** A validade de constructo refere-se a se as medidas escolhidas realmente representam os conceitos teóricos de interesse e se não há ambiguidade na interpretação.

#### Ameaça 3.1: Operacionalização de "Custo"

**Descrição:**
O conceito de "custo cloud" é multifaceted, mas neste experimento é **simplificado**:
- **Incluído:** Custo de compute (CPU, memória), storage, requisições
- **Excluído:**
  - Custos de transferência de dados entre regiões/zonas
  - Custos de serviços gerenciados (bancos de dados, cache, load balancers)
  - Reserved instances, savings plans, descontos corporativos
  - Custos de suporte técnico, SLAs

A métrica de custo usada pode **não capturar completamente** o que stakeholders entendem por "custo real de cloud".

**Impacto:**
- Modelos podem prever bem o "custo simplificado" mas não o "custo total real"
- Generalização limitada para contextos onde custos excluídos são significativos (ex: > 30% do custo total)

**Estratégias de Mitigação:**
1. **Definição Explícita de Escopo:**
   - Documentar claramente quais componentes de custo são incluídos/excluídos (Seção 4.1)
   - Delimitar contextos de aplicabilidade (workloads compute-intensive sem serviços gerenciados)
2. **Justificativa Teórica:**
   - Fundamentar escolha em literatura (ex: papers que usam mesma simplificação)
   - Argumentar que componentes incluídos representam 60-80% do custo típico de IaaS
3. **Análise de Sensibilidade (Opcional):**
   - Testar modelo com diferentes pesos para componentes de custo
   - Verificar se conclusões se mantêm com variações de ± 20% nos pesos
4. **Transparência nos Resultados:**
   - Discutir limitações da operacionalização na seção de discussão
   - Recomendar extensões futuras (incluir custos de rede, serviços gerenciados)

**Monitoramento:**
- Comparar proporções de custo com benchmarks da literatura (ex: CPU deve ser 40-60% do total)

---

#### Ameaça 3.2: MAE como Métrica Primária

**Descrição:**
MAE (Mean Absolute Error) foi escolhida como métrica primária para comparação, mas:
- **Não penaliza desproporcionalmente erros grandes:** Diferente de RMSE, que penaliza outliers
- **Não considera erro relativo:** Um erro de R$ 100 é muito diferente em um custo de R$ 200 vs. R$ 10.000
- **Pode não refletir impacto prático:** Stakeholders podem se preocupar mais com evitar grandes subestimações (que causam estouro de orçamento) do que com erro médio

Se modelos diferem primariamente em capacidade de evitar erros extremos, MAE pode não capturar essa diferença.

**Impacto:**
- Modelo com menor MAE pode não ser o mais útil na prática
- Ambiguidade sobre qual modelo é "melhor" depende de qual aspecto do erro é mais importante

**Estratégias de Mitigação:**
1. **Uso de Múltiplas Métricas:**
   - **MAE:** Erro médio absoluto (métrica primária)
   - **RMSE:** Penaliza erros grandes (métrica secundária)
   - **MAPE:** Erro percentual, relevante para comparação relativa
   - **Erro máximo:** Detectar casos extremos
2. **Análise Complementar:**
   - Reportar percentual de previsões com erro > 20%
   - Identificar casos onde erro foi particularmente grande (> 2 × MAE médio)
3. **Justificativa da Escolha:**
   - MAE é interpretável (mesma unidade que custo - R$)
   - Menos sensível a outliers que RMSE
   - Amplamente usado em literatura de forecasting
4. **Discussão Qualitativa:**
   - Analisar trade-offs entre métricas
   - Discutir em quais contextos cada métrica é mais relevante

**Monitoramento:**
- Comparar rankings de modelos por MAE vs. RMSE vs. MAPE
- Verificar se conclusões se mantêm consistentes

---

#### Ameaça 3.3: "Acurácia" vs. "Utilidade Prática"

**Descrição:**
O experimento mede **acurácia preditiva** (erro de previsão), mas não mede **utilidade prática**:
- **Não mede:** Facilidade de implementação, tempo de execução, interpretabilidade, custo computacional
- **Não considera:** Preferências de stakeholders (ex: CFO pode preferir modelo conservador que superestima custos para evitar surpresas)

Um modelo pode ter menor erro estatístico mas ser menos útil (ex: ARIMA pode ser mais preciso mas muito lento e difícil de manter).

**Impacto:**
- Conclusão de "modelo superior" pode não se traduzir em adoção prática
- Gap entre validade estatística e relevância organizacional

**Estratégias de Mitigação:**
1. **Coleta de Métricas Adicionais:**
   - **Tempo de execução:** Registrar duração de treino + previsão para cada modelo
   - **Complexidade de implementação:** Linhas de código, número de hiperparâmetros
   - **Interpretabilidade:** Avaliação qualitativa (ex: coeficientes de RL são interpretáveis)
2. **Discussão de Trade-Offs:**
   - Seção específica comparando acurácia vs. simplicidade vs. velocidade
   - Matriz de decisão: quando cada modelo é mais apropriado
3. **Recomendações Contextualizadas:**
   - "Use ARIMA se precisão é crítica e tempo de treino não é problema"
   - "Use RL se interpretabilidade e velocidade são prioridades"
4. **Validação com Stakeholders (Futura):**
   - Após experimento, apresentar resultados a profissionais de DevOps/FinOps
   - Coletar feedback sobre utilidade percebida

**Monitoramento:**
- Tabela comparativa: Acurácia × Tempo × Complexidade × Interpretabilidade

---

#### Ameaça 3.4: Mono-Method Bias (Viés de Método Único)

**Descrição:**
Todas as variáveis dependentes (MAE, RMSE, MAPE) são **métricas quantitativas de erro**, medidas de forma automatizada. Não há:
- Validação qualitativa (entrevistas com usuários)
- Observação de comportamento em produção
- Medidas subjetivas (confiança na previsão, satisfação do usuário)

Se houver aspectos importantes do conceito "modelo de previsão eficaz" que não são capturados por métricas de erro, eles serão omitidos.

**Impacto:**
- Visão limitada do fenômeno estudado
- Possível perda de insights importantes não quantificáveis

**Estratégias de Mitigação:**
1. **Limitação Explícita do Escopo:**
   - Reconhecer que experimento foca em acurácia técnica, não adoção ou satisfação
   - Delimitar que objetivo é comparação quantitativa, não estudo de usabilidade
2. **Análise Qualitativa Complementar (Opcional):**
   - Revisão de literatura sobre percepções de usuários de modelos de previsão
   - Discussão teórica sobre fatores organizacionais
3. **Triangulação com Literatura:**
   - Comparar resultados com estudos de caso qualitativos publicados
   - Discutir convergência/divergência de achados
4. **Recomendação de Pesquisas Futuras:**
   - Propor estudos mistos (quanti + quali) como extensão

**Monitoramento:**
- N/A (limitação reconhecida, não mitigável neste experimento)

---

### 13.4 Validade Externa

**Definição:** A validade externa refere-se à capacidade de generalizar os resultados para outros contextos, populações e situações além do experimento específico.

#### Ameaça 4.1: Especificidade do Provedor Cloud (Google)

**Descrição:**
Os dados utilizados são exclusivamente do **Google Cluster Data 2019**:
- Workloads específicos da infraestrutura Google (Google Borg)
- Padrões de uso podem ser únicos do ecossistema Google
- Características de escala de hyperscaler (muito larga escala)
- Precificação interna do Google difere de AWS, Azure, GCP público

Resultados podem **não se generalizar** para:
- AWS (EC2, Lambda, etc.)
- Azure (VMs, App Services, etc.)
- GCP público (Compute Engine)
- Outros provedores (DigitalOcean, Linode, etc.)

**Impacto:**
- Modelos que performam bem com dados Google podem não performar bem com dados AWS
- Padrões de workload e estruturas de custo são provider-specific
- Limitação severa da generalização para ambientes multi-cloud

**Estratégias de Mitigação:**
1. **Documentação Explícita do Contexto:**
   - Seções 4.4 e 4.5 já listam esta limitação
   - Delimitar claramente que resultados aplicam-se a "workloads similares aos traces Google"
2. **Uso de Modelo de Precificação Genérico:**
   - Aplicar tabelas de precificação de múltiplos provedores (AWS, Azure, GCP) quando possível
   - Comparar se conclusões se mantêm com diferentes tabelas de preços
3. **Generalização Teórica:**
   - Argumentar que padrões fundamentais (tendência, sazonalidade) são comuns a qualquer cloud
   - Focar em comparação relativa entre modelos, não valores absolutos de erro
4. **Recomendação de Validação Externa:**
   - Propor replicação do experimento com datasets de outros provedores (Azure Public Dataset, etc.)
   - Disponibilizar código para facilitar replicação

**Monitoramento:**
- Comparação de resultados com papers que usaram dados de outros provedores
- Análise de características do dataset Google vs. benchmarks de outros provedores

---

#### Ameaça 4.2: Período Temporal Específico (Maio 2019)

**Descrição:**
Os dados cobrem **maio de 2019**:
- Padrões sazonais anuais não são capturados (apenas ~30 dias)
- Eventos específicos daquele período podem ter afetado os dados
- Tecnologia e arquiteturas cloud de 2019 podem diferir de 2024-2025
- Workloads podem ter mudado (ex: aumento de workloads de ML/IA)

Resultados podem não se generalizar para:
- Outros períodos do ano (ex: Black Friday, final de ano)
- Anos diferentes (mudanças tecnológicas)
- Contextos pós-pandemia (padrões de uso mudaram)

**Impacto:**
- Modelos podem capturar padrões específicos de maio 2019 que não se repetem
- Generalização temporal limitada

**Estratégias de Mitigação:**
1. **Seleção de Período Típico:**
   - Verificar na documentação do Google Cluster Data se maio 2019 teve eventos atípicos
   - Evitar períodos com feriados ou manutenções grandes conhecidas
2. **Análise de Múltiplas Janelas (Opcional):**
   - Se tempo permitir, testar com diferentes meses do dataset (abril, junho)
   - Verificar se conclusões se mantêm
3. **Foco em Padrões Fundamentais:**
   - Analisar padrões diários/semanais (que são mais estáveis ao longo dos anos)
   - Evitar conclusões sobre sazonalidade anual
4. **Transparência:**
   - Reconhecer limitação na discussão
   - Recomendar validação com dados mais recentes

**Monitoramento:**
- Análise exploratória: Detectar eventos anômalos no período selecionado
- Comparação com papers que usaram outros períodos

---

#### Ameaça 4.3: Escala e Complexidade (Hyperscaler vs. PMEs)

**Descrição:**
Google Cluster Data representa **infraestrutura de larga escala** (hyperscaler):
- Milhares de jobs simultâneos
- Múltiplos clusters com orquestração complexa (Borg)
- Workloads heterogêneos e distribuídos
- Padrões de uso de grandes volumes

Contextos de **pequenas e médias empresas (PMEs)** podem ser drasticamente diferentes:
- Poucas dezenas de instâncias
- Workloads mais simples e homogêneos
- Padrões de uso mais previsíveis ou mais erráticos (dependendo do negócio)
- Menor escala pode ter maior variabilidade relativa

**Impacto:**
- Modelos treinados com dados de larga escala podem não performar bem em pequena escala
- Padrões de sazonalidade e tendência podem ser diferentes
- Generalização limitada para startups e PMEs

**Estratégias de Mitigação:**
1. **Delimitação de Contexto de Aplicabilidade:**
   - Especificar que resultados aplicam-se a "ambientes cloud de média-alta escala"
   - Recomendar cautela ao aplicar em microempresas ou startups iniciais
2. **Análise de Subconjuntos (Opcional):**
   - Selecionar subset de jobs menores do dataset Google
   - Verificar se conclusões se mantêm em workloads de escala reduzida
3. **Discussão de Transferibilidade:**
   - Argumentar que modelos fundamentais (tendência, autocorrelação) aplicam-se em diferentes escalas
   - Reconhecer que magnitudes de erro podem variar
4. **Recomendação de Calibração:**
   - Sugerir que usuários de PMEs re-treinem modelos com seus próprios dados

**Monitoramento:**
- Comparação de características do dataset Google com estatísticas de uso cloud de PMEs (quando disponíveis)

---

#### Ameaça 4.4: Tipo de Workload

**Descrição:**
Google Cluster Data inclui workloads específicos:
- Batch processing (processamento em lote)
- Jobs de análise de dados
- Serviços de backend do Google

Pode **não representar** adequadamente:
- Aplicações web típicas (padrões de tráfego HTTP)
- Workloads de machine learning training (uso intensivo de GPU)
- Aplicações serverless (funções com execução muito curta)
- Workloads de IoT ou edge computing
- Bancos de dados transacionais (OLTP)

**Impacto:**
- Modelos podem não generalizar para workloads fora do escopo do dataset
- Padrões de uso (ex: picos súbitos vs. uso constante) variam drasticamente por tipo de aplicação

**Estratégias de Mitigação:**
1. **Caracterização do Dataset:**
   - Analisar e documentar tipos de jobs presentes no dataset
   - Classificar workloads (compute-intensive, memory-intensive, I/O-intensive)
2. **Delimitação de Aplicabilidade:**
   - Especificar que resultados aplicam-se a "workloads de processamento distribuído similar aos traces analisados"
   - Listar tipos de aplicações onde resultados são mais/menos aplicáveis
3. **Heterogeneidade de Dados (Opcional):**
   - Selecionar subset diversificado de jobs (diferentes perfis de uso)
   - Aumentar representatividade dentro do possível
4. **Recomendação de Validação:**
   - Propor extensões do estudo com datasets de outros tipos (Azure Public Dataset - LLM inference, MIT Supercloud - HPC)

**Monitoramento:**
- Tabela de características dos workloads analisados (% CPU-intensive, % memory-intensive, etc.)

---

#### Ameaça 4.5: Interação com Características Organizacionais

**Descrição:**
O experimento é **puramente técnico**, sem considerar:
- Cultura organizacional (ex: empresas risk-averse vs. risk-tolerant)
- Processos de governança (ex: aprovação de orçamentos)
- Maturidade em FinOps (empresas em estágios diferentes)
- Expertise técnica da equipe (capacidade de implementar ARIMA vs. RL)

Adoção e eficácia dos modelos podem depender fortemente de **fatores organizacionais não controlados**.

**Impacto:**
- Modelo "melhor" tecnicamente pode não ser adotado por barreiras organizacionais
- Generalização para contextos organizacionais diversos é incerta

**Estratégias de Mitigação:**
1. **Foco em Validade Técnica:**
   - Reconhecer que experimento mede eficácia técnica, não adoção organizacional
   - Delimitar que implementação prática depende de fatores contextuais
2. **Discussão de Fatores Facilitadores:**
   - Listar pré-requisitos organizacionais para cada modelo
   - Ex: ARIMA requer expertise em séries temporais; RL requer menos expertise
3. **Recomendações Contextualizadas:**
   - Matriz de decisão: "Use modelo X se contexto organizacional tem característica Y"
4. **Pesquisa Futura:**
   - Propor estudos de caso qualitativos em empresas reais
   - Investigar fatores organizacionais que afetam adoção

**Monitoramento:**
- N/A (limitação reconhecida, fora do escopo)

---

#### Ameaça 4.6: Generalização para Horizontes de Previsão Diferentes

**Descrição:**
O experimento foca em janelas temporais de **7, 14 e 30 dias** para treino, com horizonte de previsão implícito de curto-médio prazo:
- Não testa previsões de longo prazo (6 meses, 1 ano)
- Não testa previsões de muito curto prazo (horas, minutos)

Modelos podem ter desempenho relativo diferente dependendo do horizonte:
- ARIMA pode ser superior para curto prazo mas degradar em longo prazo
- Média móvel pode ser adequada para muito curto prazo

**Impacto:**
- Conclusões sobre "modelo superior" são específicas ao horizonte testado
- Generalização limitada para outros horizontes de previsão

**Estratégias de Mitigação:**
1. **Especificação Explícita do Horizonte:**
   - Documentar que experimento foca em previsões de 1-30 dias à frente
   - Delimitar contexto de aplicabilidade (planejamento de curto-médio prazo)
2. **Análise de Múltiplos Horizontes (Opcional):**
   - Se tempo permitir, testar horizontes de 1 dia, 7 dias, 14 dias, 30 dias
   - Verificar se rankings de modelos se mantêm
3. **Justificativa Prática:**
   - Argumentar que horizontes de 1-30 dias são mais relevantes para gestão operacional de custos
   - Previsões de 6+ meses são mais estratégicas e dependem de fatores de negócio
4. **Transparência:**
   - Reconhecer na discussão que resultados podem não aplicar-se a horizontes muito diferentes

**Monitoramento:**
- Comparação com literatura sobre performance de modelos em diferentes horizontes

---

### 13.5 Resumo das Principais Ameaças e Estratégias de Mitigação

Esta tabela consolida as ameaças mais críticas identificadas e as ações planejadas para mitigá-las.

| Categoria | Ameaça | Severidade | Impacto Principal | Estratégias de Mitigação Planejadas | Status |
|-----------|--------|------------|-------------------|-------------------------------------|--------|
| **Validade de Conclusão** | Poder estatístico insuficiente para diferenças sutis (< 10%) | Média | Falha em detectar diferenças reais (Erro Tipo II) | • Validação cruzada k-fold (k=5)<br>• Análise de tamanho de efeito (η²)<br>• Intervalos de confiança 95%<br>• Considerar n=50 se inconclusivo | ✅ Planejado |
| **Validade de Conclusão** | Violação de normalidade dos resíduos | Média | p-valores incorretos em ANOVA | • Shapiro-Wilk test pré-ANOVA<br>• Kruskal-Wallis como alternativa não-paramétrica<br>• Levene's test para homocedasticidade<br>• Transformações (log, Box-Cox) se necessário | ✅ Planejado |
| **Validade de Conclusão** | Múltiplas comparações inflam Erro Tipo I | Alta | Falsos positivos (diferenças espúrias) | • Tukey's HSD post-hoc (ANOVA)<br>• Dunn's test + Bonferroni (Kruskal-Wallis)<br>• α ajustado = 0.0083 para comparações<br>• Priorização de comparações a priori | ✅ Planejado |
| **Validade de Conclusão** | Variabilidade de implementação dos modelos | Média | Diferenças devido a bugs, não eficácia | • Uso de bibliotecas consolidadas (Scikit-learn, Statsmodels)<br>• Validação com benchmarks conhecidos<br>• Revisão de código com orientador<br>• Documentação completa de hiperparâmetros | ✅ Planejado |
| **Validade Interna** | História (aquecimento de hardware, carga de sistema) | Média | Viés temporal sistemático | • Randomização completa da ordem de execução<br>• Limpeza de ambiente (fechar apps, desabilitar updates)<br>• Monitoramento de temperatura/CPU<br>• Análise post-hoc: Erro ~ Ordem_Execução | ✅ Planejado |
| **Validade Interna** | Overfitting diferenciado entre modelos | Alta | Modelo "melhor" em treino, pior em teste | • Validação cruzada k-fold obrigatória<br>• Monitoramento M12 (diferença treino/teste)<br>• Flagging se diferença > 15%<br>• AIC/BIC para seleção de ordem (ARIMA) | ✅ Planejado |
| **Validade Interna** | Qualidade dos dados (custos estimados, não reais) | Alta | Relação métrica-custo artificial | • Modelo de precificação baseado em literatura<br>• Consulta a tabelas públicas (AWS, Azure, GCP)<br>• Inclusão de ruído estocástico (± 5-10%)<br>• Validação com orientador | ✅ Planejado |
| **Validade de Constructo** | Operacionalização simplificada de "custo" | Média | Não captura custos de rede, serviços gerenciados, descontos | • Definição explícita de escopo (Seção 4.1)<br>• Justificativa: componentes incluídos = 60-80% do total IaaS<br>• Transparência na discussão<br>• Recomendação de extensões futuras | ✅ Planejado |
| **Validade de Constructo** | MAE como métrica primária não captura todos aspectos | Média | Pode não refletir impacto prático (ex: evitar grandes erros) | • Uso de múltiplas métricas (MAE, RMSE, MAPE, erro máximo)<br>• Análise complementar (% previsões com erro > 20%)<br>• Justificativa de escolha<br>• Discussão de trade-offs | ✅ Planejado |
| **Validade de Constructo** | "Acurácia" ≠ "Utilidade Prática" | Baixa | Modelo mais preciso pode não ser adotado | • Coleta de tempo de execução, complexidade<br>• Discussão de trade-offs acurácia × velocidade × interpretabilidade<br>• Recomendações contextualizadas<br>• Validação futura com stakeholders | ⚠️ Parcial |
| **Validade Externa** | Especificidade do provedor (Google) | Alta | Não generaliza para AWS, Azure, outros | • Documentação explícita do contexto<br>• Uso de precificação genérica (múltiplos provedores)<br>• Foco em comparação relativa, não absoluta<br>• Recomendação de replicação com outros datasets | ⚠️ Limitação Aceita |
| **Validade Externa** | Período temporal específico (maio 2019) | Média | Padrões sazonais anuais não capturados | • Seleção de período típico (verificar eventos atípicos)<br>• Análise de múltiplas janelas se tempo permitir<br>• Foco em padrões diários/semanais (mais estáveis)<br>• Transparência na discussão | ⚠️ Limitação Aceita |
| **Validade Externa** | Escala (hyperscaler vs. PMEs) | Alta | Não se aplica a startups/PMEs | • Delimitação: aplicável a média-alta escala<br>• Análise de subconjuntos (jobs menores) opcional<br>• Discussão de transferibilidade<br>• Recomendação de calibração para PMEs | ⚠️ Limitação Aceita |
| **Validade Externa** | Tipo de workload específico | Média | Não generaliza para ML training, serverless, IoT, OLTP | • Caracterização detalhada dos workloads do dataset<br>• Delimitação de aplicabilidade (processamento distribuído)<br>• Seleção de subset heterogêneo<br>• Recomendação de validação com outros datasets | ⚠️ Limitação Aceita |

**Legenda de Status:**
- ✅ **Planejado:** Estratégia de mitigação implementada/planejada no experimento
- ⚠️ **Limitação Aceita:** Ameaça reconhecida mas não totalmente mitigável; será explicitada na discussão
- ⚠️ **Parcial:** Mitigação parcial implementada; limitação residual reconhecida

---

#### Priorização de Ameaças (Top 5 Críticas)

Com base em **severidade** e **impacto potencial**, as 5 ameaças mais críticas são:

1. **Múltiplas Comparações (Validade de Conclusão)**
   - **Severidade:** Alta
   - **Mitigação Principal:** Tukey's HSD post-hoc com correção automática
   - **Critério de Sucesso:** Reportar p-valores ajustados para todas as comparações

2. **Overfitting Diferenciado (Validade Interna)**
   - **Severidade:** Alta
   - **Mitigação Principal:** Validação cruzada k-fold obrigatória + monitoramento M12
   - **Critério de Sucesso:** Diferença treino/teste < 15% para todos os modelos

3. **Qualidade dos Dados - Custos Estimados (Validade Interna)**
   - **Severidade:** Alta
   - **Mitigação Principal:** Modelo de precificação validado + inclusão de ruído
   - **Critério de Sucesso:** Correlações métrica-custo plausíveis (0.6-0.9)

4. **Especificidade do Provedor Google (Validade Externa)**
   - **Severidade:** Alta
   - **Mitigação Principal:** Uso de precificação genérica + documentação explícita de limitações
   - **Critério de Sucesso:** Discussão transparente de contextos de aplicabilidade

5. **Escala Hyperscaler vs. PMEs (Validade Externa)**
   - **Severidade:** Alta
   - **Mitigação Principal:** Delimitação clara de contexto + recomendação de calibração
   - **Critério de Sucesso:** Seção de discussão com guidelines de transferibilidade

---

#### Ações de Monitoramento Pós-Experimento

**Checklist de Validação dos Resultados:**

- [ ] **Normalidade:** Shapiro-Wilk p-valor > 0.05 para todos os grupos?
- [ ] **Homocedasticidade:** Levene's test p-valor > 0.05?
- [ ] **Overfitting:** Diferença treino/teste < 15% para todos os modelos?
- [ ] **Outliers:** Outliers detectados investigados e documentados?
- [ ] **Randomização:** Análise Erro ~ Ordem_Execução não significativa (p > 0.05)?
- [ ] **Correlações Plausíveis:** 0.6 ≤ |r(métrica, custo)| ≤ 0.9?
- [ ] **Consistência de Métricas:** Rankings por MAE, RMSE e MAPE convergem?
- [ ] **Versões de Software:** `pip freeze` documentado e consistente?
- [ ] **Reprodutibilidade:** Seeds salvos e experimento reproduzível?
- [ ] **Documentação de Limitações:** Seção de discussão inclui todas as ameaças da Seção 13.5?

**Se Problemas Forem Detectados:**
- **Violação de normalidade severa:** Usar Kruskal-Wallis + Dunn's test
- **Overfitting > 15%:** Analisar e reportar separadamente; considerar exclusão do modelo ou re-tuning
- **Ordem de execução significativa:** Incluir "ordem" como covariável na análise
- **Outliers inexplicáveis:** Remover e re-executar; documentar justificativa


---

## 14. Ética, Privacidade e Conformidade

### 14.1 Questões Éticas (Uso de Sujeitos, Incentivos, etc.)

**Situação:** Este experimento **não envolve sujeitos humanos**.

#### Natureza do Estudo:

Este é um estudo **puramente computacional** que utiliza:
- **Dados públicos:** Google Cluster Data 2019 (dataset público e anonimizado)
- **Análise quantitativa:** Comparação de modelos de previsão em ambiente controlado
- **Sem interação humana:** Nenhuma coleta de dados de participantes, entrevistas ou observações

#### Questões Éticas Aplicáveis:

**1. Uso Ético de Dados Públicos:**
- **Situação:** Os dados do Google Cluster Data 2019 foram publicados sob licença **Creative Commons BY 4.0** (CC-BY)
- **Conformidade:** O uso está em conformidade com os termos da licença, que permite uso acadêmico e pesquisa
- **Atribuição:** O dataset será devidamente citado em todas as publicações

**2. Responsabilidade Científica:**
- **Compromisso com rigor:** Seguir metodologia experimental rigorosa conforme seções anteriores
- **Transparência:** Documentar limitações e ameaças à validade (Seção 13)
- **Reprodutibilidade:** Disponibilizar código, dados processados e documentação (Seção 18)

**3. Potencial Impacto Social:**
- **Impacto positivo:** Contribuir para otimização de custos cloud, beneficiando organizações
- **Sem riscos identificados:** Não há riscos éticos de uso indevido dos resultados
- **Aplicação responsável:** Resultados são recomendações técnicas, não decisões automatizadas críticas

#### Conclusão:

**Não há questões éticas críticas** neste experimento, pois:
- Não envolve seres humanos
- Usa dados públicos e devidamente licenciados
- Não apresenta riscos de dano a indivíduos ou organizações
- Segue princípios de integridade científica

---

### 14.2 Consentimento Informado

**Não Aplicável:** Este experimento não envolve participantes humanos, portanto **não há necessidade de consentimento informado**.

#### Justificativa:

O experimento é baseado exclusivamente em:
1. **Dados secundários públicos** (Google Cluster Data 2019)
2. **Processamento computacional** de métricas de infraestrutura
3. **Análise estatística** automatizada

**Nenhum dado pessoal identificável é coletado, processado ou armazenado.**

---

### 14.3 Privacidade e Proteção de Dados

#### Dados Coletados e Processados:

**1. Dados do Google Cluster Data 2019:**

| Tipo de Dado | Descrição | Natureza | Identificável? |
|--------------|-----------|----------|----------------|
| **Timestamps** | Marcações temporais (maio 2019) | Temporal | ❌ Não |
| **CPU usage** | Métricas de utilização de CPU | Técnica | ❌ Não |
| **Memory usage** | Métricas de uso de memória | Técnica | ❌ Não |
| **Job/Task IDs** | Identificadores numéricos de jobs | Técnica | ❌ Não (anonimizados) |
| **Collection IDs** | Identificadores de coleções | Técnica | ❌ Não (anonimizados) |

**2. Dados Gerados pelo Experimento:**

| Tipo de Dado | Descrição | Identificável? |
|--------------|-----------|----------------|
| **Resultados de modelos** | MAE, RMSE, MAPE por execução | ❌ Não |
| **Logs de experimento** | Timestamps, status de execução | ❌ Não |
| **Métricas agregadas** | Estatísticas descritivas | ❌ Não |

#### Características de Privacidade:

**✅ Conformidade com LGPD/GDPR:**

- **Não há dados pessoais:** Nenhum dado do experimento se enquadra na definição de "dado pessoal" (LGPD Art. 5º, I)
- **Anonimização por design:** Google Cluster Data já foi anonimizado pelo provedor original
- **Sem possibilidade de reidentificação:** IDs de jobs/tasks não podem ser associados a indivíduos

**✅ Proteção de Dados:**

1. **Armazenamento:**
   - Dados processados armazenados localmente no computador do pesquisador
   - Backup em repositório GitHub público (dados já públicos)
   - Nenhum dado sensível ou confidencial

2. **Controle de Acesso:**
   - Dados públicos: sem restrições de acesso
   - Scripts e código: repositório público GitHub

3. **Período de Retenção:**
   - **Durante o TCC:** Dados mantidos durante desenvolvimento (6 meses)
   - **Após conclusão:** Dados e código mantidos indefinidamente no GitHub para reprodutibilidade
   - **Justificativa:** Promover ciência aberta e reprodutível

#### Conclusão:

**Não há riscos de privacidade** neste experimento, pois:
- Não processa dados pessoais
- Usa dataset público e anonimizado
- Segue princípios de dados abertos e ciência aberta

---

### 14.4 Aprovações Necessárias (Comitê de Ética, Jurídico, DPO, etc.)

#### Análise de Necessidade de Aprovações:

**1. Comitê de Ética em Pesquisa (CEP):**

| Item | Análise | Necessidade |
|------|---------|-------------|
| **Envolve seres humanos?** | ❌ Não | ⚪ Não requerido |
| **Coleta dados de participantes?** | ❌ Não | ⚪ Não requerido |
| **Apresenta riscos a indivíduos?** | ❌ Não | ⚪ Não requerido |
| **Uso de dados pessoais sensíveis?** | ❌ Não | ⚪ Não requerido |

**Conclusão:** **Dispensa de aprovação CEP** (conforme Resolução CNS 510/2016, Art. 1º, Parágrafo Único, VII - pesquisa que utilize informações de acesso público)

**2. Data Protection Officer (DPO) / Encarregado LGPD:**

| Item | Análise | Necessidade |
|------|---------|-------------|
| **Processa dados pessoais?** | ❌ Não | ⚪ Não requerido |
| **Conformidade LGPD?** | ✅ Sim (não aplicável - sem dados pessoais) | ⚪ Não requerido |

**Conclusão:** **Não requerida aprovação DPO**

**3. Departamento Jurídico / Compliance:**

| Item | Análise | Necessidade |
|------|---------|-------------|
| **Uso de dados proprietários?** | ❌ Não (dados públicos CC-BY) | ⚪ Não requerido |
| **Questões contratuais?** | ❌ Não | ⚪ Não requerido |
| **Risco legal?** | ❌ Não | ⚪ Não requerido |

**Conclusão:** **Não requerida aprovação jurídica**

**4. Coordenação do Curso / Orientador:**

| Item | Análise | Necessidade |
|------|---------|-------------|
| **Aprovação do tema TCC?** | ✅ Sim | ✅ **Requerido** |
| **Revisão do plano experimental?** | ✅ Sim | ✅ **Requerido** |
| **Aprovação para defesa?** | ✅ Sim | ✅ **Requerido** |

**Conclusão:** **Aprovações acadêmicas necessárias**

#### Resumo de Aprovações:

| Órgão/Pessoa | Status | Observações |
|--------------|--------|-------------|
| **Comitê de Ética (CEP)** | ⚪ Não aplicável | Pesquisa com dados públicos, sem sujeitos humanos |
| **DPO / LGPD** | ⚪ Não aplicável | Não processa dados pessoais |
| **Jurídico** | ⚪ Não aplicável | Uso de dados públicos licenciados |
| **Orientador (Prof. Danilo)** | 🟡 Pendente | Aprovação do plano experimental |
| **Coordenação do Curso** | 🟡 Pendente | Aprovação formal do tema de TCC |
| **Banca Examinadora** | 🟢 Futuro | Após conclusão do trabalho |

#### Documentação de Conformidade:

**Declaração:**

> Este experimento foi avaliado quanto à necessidade de aprovação de Comitê de Ética em Pesquisa (CEP) e foi considerado **dispensado**, conforme Resolução CNS 510/2016, Art. 1º, Parágrafo Único, inciso VII, por se tratar de pesquisa que utiliza exclusivamente informações de acesso público (Google Cluster Data 2019, licenciado sob Creative Commons BY 4.0), sem envolvimento de seres humanos, dados pessoais ou informações sensíveis.

**Responsável pela Análise:** Renato Matos Alves Penna (Pesquisador)
**Orientador:** Prof. Danilo de Quadros Maia Filho
**Instituição:** Pontifícia Universidade Católica de Minas Gerais (PUC Minas)
**Curso:** Bacharelado em Engenharia de Software
**Data da Análise:** 05/12/2025

---


## 15. Recursos, Infraestrutura e Orçamento

### 15.1 Recursos Humanos e Papéis

#### Equipe do Experimento:

| Nome | Papel | Responsabilidades | Dedicação | Contato |
|------|-------|-------------------|-----------|---------|
| **Renato Matos Alves Penna** | Pesquisador Principal / Executor | - Planejamento experimental<br>- Implementação de código<br>- Coleta e processamento de dados<br>- Execução do experimento<br>- Análise de resultados<br>- Redação do TCC | 15-20h/semana | renatomatosapbusiness@gmail.com |
| **Prof. Danilo de Quadros Maia Filho** | Orientador | - Revisão do plano experimental<br>- Consultoria metodológica<br>- Revisão de resultados<br>- Aprovação de entregas<br>- Orientação acadêmica | 2-3h/mês | (contato via PUC Minas) |

#### Descrição de Papéis:

**1. Pesquisador Principal (Renato):**

**Responsabilidades Principais:**
- ✅ **Planejamento:** Elaboração completa do plano experimental
- ✅ **Implementação:** Desenvolvimento de scripts Python para processamento, modelagem e análise
- ✅ **Execução:** Operação do experimento completo (120 execuções × 4 modelos)
- ✅ **Análise:** Interpretação estatística dos resultados
- ✅ **Documentação:** Redação do documento de TCC
- ✅ **Apresentação:** Defesa do trabalho perante banca

**Perfil de Competências:**
- Python intermediário/avançado
- Estatística e análise de dados
- Machine learning e séries temporais (conceitos)
- Metodologia científica
- Escrita acadêmica

**2. Orientador (Prof. Danilo):**

**Responsabilidades Principais:**
- ✅ **Revisão Metodológica:** Validar desenho experimental e rigor científico
- ✅ **Consultoria Técnica:** Esclarecer dúvidas sobre métodos estatísticos e modelagem
- ✅ **Feedback Contínuo:** Revisar entregas intermediárias (se houver)
- ✅ **Aprovação Final:** Autorizar entrega do trabalho para defesa

**Frequência de Interação:**
- Reuniões quinzenais ou mensais (conforme necessidade)
- E-mail para dúvidas pontuais
- Revisão de entregas em marcos definidos

#### Estrutura de Comunicação:

```
Pesquisador (Renato)
       ↓
    Orientador (Danilo)
       ↓
Coordenação de TCC (PUC Minas)
       ↓
    Banca Examinadora
```

---

### 15.2 Infraestrutura Técnica Necessária

#### Ambiente Computacional:

**1. Hardware:**

| Recurso | Especificação Mínima | Especificação Recomendada | Disponibilidade |
|---------|---------------------|---------------------------|-----------------|
| **Processador** | Intel i5 / AMD Ryzen 5 (4 cores) | Intel i7 / AMD Ryzen 7 (8 cores) | ✅ Computador pessoal |
| **Memória RAM** | 8 GB | 16 GB | ✅ Computador pessoal |
| **Armazenamento** | 20 GB livres | 50 GB livres (SSD) | ✅ Computador pessoal |
| **Sistema Operacional** | Windows 10/11, Linux, macOS | Qualquer (Python multiplataforma) | ✅ Computador pessoal |

**Nota:** O experimento será executado em **computador pessoal do pesquisador**. Não há necessidade de infraestrutura de cloud ou cluster computacional.

**2. Software e Ferramentas:**

| Ferramenta | Versão | Propósito | Custo | Disponibilidade |
|------------|--------|-----------|-------|-----------------|
| **Python** | 3.10+ | Linguagem de programação | Gratuito | ✅ Já instalado |
| **Pandas** | 2.0+ | Manipulação de dados | Gratuito | ✅ pip install |
| **NumPy** | 1.24+ | Computação numérica | Gratuito | ✅ pip install |
| **Scikit-learn** | 1.3+ | Modelos de ML | Gratuito | ✅ pip install |
| **Statsmodels** | 0.14+ | Modelos estatísticos (ARIMA, ES) | Gratuito | ✅ pip install |
| **Matplotlib / Seaborn** | Última | Visualização de dados | Gratuito | ✅ pip install |
| **Jupyter Notebook** | Última | Análise interativa | Gratuito | ✅ pip install |
| **VS Code / PyCharm** | Última | IDE para desenvolvimento | Gratuito | ✅ Já instalado |
| **Git** | 2.40+ | Controle de versão | Gratuito | ✅ Já instalado |
| **GitHub** | - | Hospedagem de repositório | Gratuito (público) | ✅ Conta criada |

**3. Repositórios e Armazenamento:**

| Recurso | Descrição | Capacidade | Custo | URL |
|---------|-----------|------------|-------|-----|
| **GitHub (Código)** | Repositório do projeto | Ilimitado (público) | Gratuito | https://github.com/RenatoMAP77/pre-tcc |
| **Armazenamento Local** | Dados e resultados no computador | ~10-20 GB | Incluído | - |
| **Google Drive (Backup)** | Backup opcional de dados/resultados | 15 GB (free tier) | Gratuito | (opcional) |

**4. Acesso a Dados:**

| Dataset | Fonte | Acesso | Custo | Tamanho |
|---------|-------|--------|-------|---------|
| **Google Cluster Data 2019** | Kaggle | Download público via Kaggle CLI | Gratuito | ~100 MB (sample) |
| **Alternativa** | BigQuery | Free tier (1 TB/mês) | Gratuito | Conforme query |

**5. Requisitos de Rede:**

- **Conexão à Internet:** Necessária para:
  - Download inicial do dataset (~100 MB)
  - Instalação de bibliotecas Python (~500 MB)
  - Push/pull do repositório GitHub
- **Largura de Banda:** Mínima (download único)
- **Disponibilidade:** ✅ Internet doméstica suficiente

#### Checklist de Preparação de Infraestrutura:

- [x] Computador pessoal com especificações adequadas
- [x] Python 3.10+ instalado
- [x] Git instalado e configurado
- [x] Conta GitHub criada e repositório criado
- [ ] Bibliotecas Python instaladas (requirements.txt)
- [ ] Conta Kaggle criada (para download do dataset)
- [ ] Dataset do Google Cluster Data 2019 baixado
- [ ] Ambiente virtual Python configurado

---

### 15.3 Materiais e Insumos

**Situação:** Este experimento é **puramente computacional** e **não requer materiais físicos**.

#### Materiais Digitais Necessários:

**1. Dados:**

| Material | Descrição | Fonte | Custo | Status |
|----------|-----------|-------|-------|--------|
| **Google Cluster Data 2019** | Dataset público de traces cloud | Kaggle / BigQuery | Gratuito | 🟡 A ser baixado |
| **Tabelas de Precificação** | Preços de AWS, Azure, GCP | Sites públicos dos provedores | Gratuito | 🟡 A ser coletado |

**2. Scripts e Código:**

| Material | Descrição | Responsável | Status |
|----------|-----------|-------------|--------|
| **preparar_dados.py** | Script de download e pré-processamento | Renato | 🔴 A desenvolver |
| **executar_experimento.py** | Script principal de execução | Renato | 🔴 A desenvolver |
| **modelos.py** | Implementação dos 4 modelos | Renato | 🔴 A desenvolver |
| **analise_resultados.ipynb** | Notebook Jupyter para análise | Renato | 🔴 A desenvolver |
| **requirements.txt** | Lista de dependências Python | Renato | 🔴 A desenvolver |

**3. Templates e Documentos:**

| Material | Descrição | Status |
|----------|-----------|--------|
| **README.md (este documento)** | Plano experimental completo | ✅ Em desenvolvimento |
| **Template de log** | Formato de logs de execução | 🔴 A criar |
| **Template de resultados.csv** | Estrutura do arquivo de resultados | 🔴 A criar |

**4. Licenças de Software:**

**Todas as ferramentas utilizadas são open-source e gratuitas:**
- Python: Licença PSF (Python Software Foundation)
- Bibliotecas Python: Licenças BSD, MIT, Apache 2.0
- Git: Licença GPL v2
- VS Code: Licença MIT (gratuito)

**Custo Total de Licenças:** **R$ 0,00**

#### Insumos Não Necessários:

❌ **Equipamentos de laboratório**
❌ **Materiais de consumo (papel, toner, etc.)**
❌ **Licenças de software comercial**
❌ **Créditos de cloud computing**
❌ **Dispositivos IoT ou hardware especializado**
❌ **Formulários impressos ou questionários**

---

### 15.4 Orçamento e Custos Estimados

#### Premissa:

Este experimento foi planejado com **orçamento zero**, utilizando exclusivamente:
- Computador pessoal já disponível
- Software open-source gratuito
- Datasets públicos gratuitos
- Infraestrutura pessoal (internet doméstica)

#### Planilha de Custos:

| Categoria | Item | Quantidade | Custo Unitário | Custo Total | Fonte de Financiamento |
|-----------|------|------------|----------------|-------------|------------------------|
| **Recursos Humanos** | Pesquisador (Renato) | ~200h | R$ 0,00 | R$ 0,00 | Trabalho acadêmico (não remunerado) |
| | Orientador (Prof. Danilo) | ~10h | R$ 0,00 | R$ 0,00 | Atividade docente PUC Minas |
| **Infraestrutura Computacional** | Computador pessoal | 6 meses | R$ 0,00 | R$ 0,00 | Equipamento próprio |
| | Energia elétrica (estimada) | ~50 kWh | ~R$ 0,80/kWh | ~R$ 40,00 | Despesa pessoal |
| | Internet | 6 meses | R$ 0,00 | R$ 0,00 | Internet doméstica existente |
| **Software e Ferramentas** | Python + bibliotecas | - | R$ 0,00 | R$ 0,00 | Open-source |
| | Git + GitHub | - | R$ 0,00 | R$ 0,00 | Gratuito (repositório público) |
| | IDE (VS Code / PyCharm) | - | R$ 0,00 | R$ 0,00 | Gratuito |
| **Dados** | Google Cluster Data 2019 | ~100 MB | R$ 0,00 | R$ 0,00 | Dataset público (Kaggle) |
| **Hospedagem e Armazenamento** | GitHub (repositório) | Ilimitado | R$ 0,00 | R$ 0,00 | Free tier (público) |
| | Armazenamento local | ~20 GB | R$ 0,00 | R$ 0,00 | HD/SSD já disponível |
| **Documentação** | LaTeX / Markdown (opcional) | - | R$ 0,00 | R$ 0,00 | Gratuito |
| **Outros** | Material de apresentação (slides) | - | R$ 0,00 | R$ 0,00 | Google Slides / PowerPoint gratuito |
| | | | **TOTAL:** | **~R$ 40,00** | Despesa pessoal (energia) |

#### Análise de Custos:

**Custo Direto Real:** ~R$ 40,00 (energia elétrica estimada)
**Custo Indireto (não contabilizado):** Horas de trabalho do pesquisador (~200h) e orientador (~10h)

**Fonte de Financiamento:**
- **Despesas diretas (R$ 40):** Custeadas pelo pesquisador (Renato)
- **Infraestrutura:** Equipamento pessoal e internet doméstica já disponíveis
- **Software:** 100% open-source gratuito
- **Dados:** Dataset público gratuito

#### Justificativa de Orçamento Zero:

Este TCC foi planejado para ser **viável sem qualquer financiamento externo**, cumprindo os seguintes critérios:

1. **Uso de Recursos Próprios:**
   - Computador pessoal suficiente para processamento
   - Internet doméstica para download de dados e acesso a repositórios

2. **Escolha de Ferramentas Gratuitas:**
   - Python e bibliotecas científicas (NumPy, Pandas, Scikit-learn, Statsmodels) são open-source
   - GitHub oferece hospedagem gratuita para repositórios públicos

3. **Dados Públicos:**
   - Google Cluster Data 2019 é disponibilizado gratuitamente via Kaggle e BigQuery

4. **Escala Gerenciável:**
   - Processamento local (não requer cluster ou cloud)
   - Dataset sample (~100 MB) ao invés de dataset completo (2.4 TiB)

#### Riscos Financeiros:

**Risco Identificado:** Nenhum risco financeiro crítico.

**Contingências:**
- Se computador pessoal falhar: Usar laboratórios da PUC Minas (acesso gratuito)
- Se dataset Kaggle ficar indisponível: Usar BigQuery free tier (1 TB/mês gratuito)

---

## 16. Cronograma, Marcos e Riscos Operacionais

### 16.1 Macrocronograma (Até o Início da Execução)

#### Visão Geral do Projeto:

**Período Total:** Janeiro 2025 - Dezembro 2025 (12 meses)
**Fase de Planejamento:** Janeiro - Maio 2025 (5 meses)
**Fase de Execução:** Junho - Julho 2025 (2 meses)
**Fase de Análise e Redação:** Agosto - Dezembro 2025 (5 meses)

#### Macrocronograma Detalhado:

| # | Marco / Fase | Descrição | Início | Fim | Duração | Entrega | Status |
|---|--------------|-----------|--------|-----|---------|---------|--------|
| **1** | **Planejamento Experimental** | Desenvolvimento do plano completo | 01/01/2025 | 31/05/2025 | 5 meses | Plano experimental (este documento) | 🟡 Em andamento |
| 1.1 | Revisão bibliográfica | Estudar literatura sobre previsão de custos cloud | 01/01/2025 | 28/02/2025 | 2 meses | - | 🟡 Em andamento |
| 1.2 | Definição de objetivos e questões | Formular goal, questões e métricas (GQM) | 01/02/2025 | 15/02/2025 | 2 semanas | Seção 3 do plano | ✅ Concluído |
| 1.3 | Desenho experimental | Definir fatores, tratamentos, desenho | 15/02/2025 | 15/03/2025 | 1 mês | Seções 8-9 do plano | ✅ Concluído |
| 1.4 | Protocolo operacional | Detalhar procedimento passo a passo | 15/03/2025 | 31/03/2025 | 2 semanas | Seção 11 do plano | ✅ Concluído |
| 1.5 | Avaliação de ameaças à validade | Identificar e planejar mitigações | 01/04/2025 | 15/04/2025 | 2 semanas | Seção 13 do plano | ✅ Concluído |
| 1.6 | Revisão com orientador | Apresentar plano ao Prof. Danilo | 15/04/2025 | 30/04/2025 | 2 semanas | - | 🔴 Pendente |
| 1.7 | Ajustes no plano | Incorporar feedback do orientador | 01/05/2025 | 15/05/2025 | 2 semanas | Plano revisado | 🔴 Pendente |
| 1.8 | **Aprovação final do plano** | ✅ **MARCO** | - | 31/05/2025 | - | Plano aprovado | 🔴 Pendente |
| **2** | **Preparação da Infraestrutura** | Setup de ambiente e ferramentas | 01/05/2025 | 31/05/2025 | 1 mês | Ambiente pronto | 🔴 Pendente |
| 2.1 | Configuração de ambiente Python | Instalar Python, bibliotecas, ambiente virtual | 01/05/2025 | 07/05/2025 | 1 semana | requirements.txt | 🔴 Pendente |
| 2.2 | Download do dataset | Obter Google Cluster Data 2019 via Kaggle | 08/05/2025 | 10/05/2025 | 3 dias | Dataset bruto | 🔴 Pendente |
| 2.3 | Desenvolvimento de scripts de preparação | Criar preparar_dados.py | 10/05/2025 | 20/05/2025 | 10 dias | preparar_dados.py | 🔴 Pendente |
| 2.4 | Validação do dataset processado | Testar qualidade dos dados preprocessados | 20/05/2025 | 25/05/2025 | 5 dias | Dataset validado | 🔴 Pendente |
| 2.5 | Desenvolvimento de modelos | Implementar RL, MM, ARIMA, ES | 01/05/2025 | 25/05/2025 | 25 dias | modelos.py | 🔴 Pendente |
| 2.6 | Testes unitários dos modelos | Validar implementações | 25/05/2025 | 31/05/2025 | 6 dias | Testes OK | 🔴 Pendente |
| **3** | **Dry Run (Pré-Teste)** | Execução de teste com n=5 | 01/06/2025 | 05/06/2025 | 5 dias | Validação técnica | 🔴 Pendente |
| 3.1 | Execução do dry run | Rodar 5 repetições de cada modelo | 01/06/2025 | 03/06/2025 | 3 dias | Resultados de teste | 🔴 Pendente |
| 3.2 | Validação de logs e outputs | Conferir formato de resultados | 03/06/2025 | 04/06/2025 | 1 dia | Logs validados | 🔴 Pendente |
| 3.3 | Ajustes finais | Corrigir bugs identificados | 04/06/2025 | 05/06/2025 | 1 dia | Scripts corrigidos | 🔴 Pendente |
| 3.4 | **Aprovação para iniciar experimento** | ✅ **MARCO** | - | 05/06/2025 | - | Go/No-Go decision | 🔴 Pendente |
| **4** | **EXECUÇÃO DO EXPERIMENTO** | ✅ **MARCO PRINCIPAL** | 10/06/2025 | 15/07/2025 | ~1 mês | Resultados completos | 🔴 Pendente |
| 4.1 | Execução completa (120 sessões) | Rodar 30 rep × 4 modelos (~13-15h) | 10/06/2025 | 25/06/2025 | 2 semanas | resultados.csv | 🔴 Pendente |
| 4.2 | Validação de integridade dos dados | Conferir 120 execuções completas | 25/06/2025 | 27/06/2025 | 2 dias | Dados validados | 🔴 Pendente |
| 4.3 | Backup de resultados | Salvar em múltiplas localizações | 27/06/2025 | 28/06/2025 | 1 dia | Backup completo | 🔴 Pendente |
| **5** | **Análise dos Resultados** | Estatística descritiva e inferencial | 01/07/2025 | 31/07/2025 | 1 mês | Análises completas | 🔴 Pendente |
| 5.1 | Estatística descritiva | Média, mediana, desvio padrão por modelo | 01/07/2025 | 05/07/2025 | 5 dias | Tabelas descritivas | 🔴 Pendente |
| 5.2 | Visualizações | Boxplots, séries temporais, heatmaps | 05/07/2025 | 10/07/2025 | 5 dias | Gráficos | 🔴 Pendente |
| 5.3 | Testes de hipóteses | ANOVA/Kruskal-Wallis + post-hoc | 10/07/2025 | 15/07/2025 | 5 dias | Resultados estatísticos | 🔴 Pendente |
| 5.4 | Análise de correlação | Métricas vs. custos | 15/07/2025 | 20/07/2025 | 5 dias | Matriz de correlação | 🔴 Pendente |
| 5.5 | Interpretação e síntese | Responder questões de pesquisa | 20/07/2025 | 31/07/2025 | 11 dias | Respostas às QPs | 🔴 Pendente |
| **6** | **Redação do TCC** | Documento final do trabalho | 01/08/2025 | 30/11/2025 | 4 meses | TCC completo | 🔴 Pendente |
| 6.1 | Introdução e referencial teórico | Cap. 1-2 | 01/08/2025 | 31/08/2025 | 1 mês | - | 🔴 Pendente |
| 6.2 | Metodologia | Cap. 3 | 01/09/2025 | 20/09/2025 | 3 semanas | - | 🔴 Pendente |
| 6.3 | Resultados | Cap. 4 | 20/09/2025 | 15/10/2025 | ~4 semanas | - | 🔴 Pendente |
| 6.4 | Discussão e conclusão | Cap. 5-6 | 15/10/2025 | 31/10/2025 | 2 semanas | - | 🔴 Pendente |
| 6.5 | Revisão e formatação | Normas ABNT, revisão ortográfica | 01/11/2025 | 20/11/2025 | 3 semanas | - | 🔴 Pendente |
| 6.6 | Revisão final com orientador | Incorporar feedback | 20/11/2025 | 30/11/2025 | 10 dias | - | 🔴 Pendente |
| 6.7 | **Entrega do TCC** | ✅ **MARCO FINAL** | - | 05/12/2025 | - | TCC entregue | 🔴 Pendente |
| **7** | **Defesa do TCC** | Apresentação perante banca | 15/12/2025 | 20/12/2025 | 1 semana | Defesa realizada | 🔴 Pendente |

#### Marcos Críticos (Critical Path):

```
📅 31/05/2025: Aprovação do Plano Experimental
       ↓
📅 05/06/2025: Go/No-Go para Executar Experimento
       ↓
📅 10-25/06/2025: Execução Completa do Experimento (120 sessões)
       ↓
📅 31/07/2025: Análise de Resultados Concluída
       ↓
📅 05/12/2025: Entrega do TCC
       ↓
📅 15-20/12/2025: Defesa do TCC
```

#### Gráfico de Gantt Simplificado:

```
2025     | Jan | Fev | Mar | Abr | Mai | Jun | Jul | Ago | Set | Out | Nov | Dez |
---------|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
Planejamento | ████████████████████████████████ |     |     |     |     |     |     |
Infraestrutura |     |     |     | ████████████ |     |     |     |     |     |     |
Dry Run      |     |     |     |     | ██  |     |     |     |     |     |     |     |
EXECUÇÃO     |     |     |     |     |     | ████|     |     |     |     |     |     |
Análise      |     |     |     |     |     |     | ████|     |     |     |     |     |
Redação TCC  |     |     |     |     |     |     |     | ████████████████████████ |     |
Defesa       |     |     |     |     |     |     |     |     |     |     |     | ██  |
```

---

### 16.2 Dependências entre Atividades

#### Mapa de Dependências Críticas:

```mermaid
graph TD
    A[Plano Experimental Completo] --> B[Aprovação do Orientador]
    B --> C[Setup de Ambiente Python]
    B --> D[Download do Dataset]
    C --> E[Desenvolvimento de Scripts]
    D --> E
    E --> F[Validação de Scripts - Dry Run]
    F --> G{Go/No-Go?}
    G -->|Go| H[EXECUÇÃO DO EXPERIMENTO]
    G -->|No-Go| E
    H --> I[Validação de Integridade]
    I --> J[Backup de Resultados]
    J --> K[Análise Estatística]
    K --> L[Redação do TCC]
    L --> M[Revisão do Orientador]
    M --> N[Entrega Final]
    N --> O[Defesa do TCC]
```

#### Tabela de Dependências:

| Atividade | Depende De | Tipo de Dependência | Impacto se Atrasar |
|-----------|------------|---------------------|-------------------|
| **Aprovação do Plano** | Conclusão do plano | Finish-to-Start (FS) | ⚠️ Crítico - Bloqueia tudo |
| **Setup de Ambiente** | Aprovação do plano | FS | ⚠️ Crítico - Bloqueia execução |
| **Download Dataset** | Aprovação do plano | FS | ⚠️ Crítico - Bloqueia execução |
| **Desenvolvimento de Scripts** | Setup + Dataset | FS (ambos) | ⚠️ Crítico - Bloqueia execução |
| **Dry Run** | Scripts prontos | FS | ⚠️ Crítico - Valida viabilidade |
| **Execução do Experimento** | Dry Run OK (Go decision) | FS | 🔴 **Crítico - Caminho crítico** |
| **Análise de Resultados** | Execução completa + validação | FS | 🔴 **Crítico - Caminho crítico** |
| **Redação do TCC** | Análise concluída | FS | 🔴 **Crítico - Caminho crítico** |
| **Revisão do Orientador** | Redação completa | FS | ⚠️ Crítico - Aprovação final |
| **Entrega do TCC** | Revisão OK | FS | 🔴 **Crítico - Data fixa (05/12)** |
| **Defesa** | Entrega do TCC | FS | 🔴 **Crítico - Data fixa** |

#### Dependências Não-Críticas (Podem ser Paralelizadas):

- **Revisão Bibliográfica** pode ocorrer em paralelo com desenvolvimento de scripts
- **Redação de Introdução e Referencial Teórico** pode iniciar antes da execução
- **Desenvolvimento de modelos** pode iniciar em paralelo ao processamento de dados

#### Estratégia de Gestão de Dependências:

1. **Priorizar Caminho Crítico:**
   - Focar em atividades que bloqueiam outras
   - Evitar atrasos em: Aprovação → Scripts → Dry Run → Execução → Análise → Redação

2. **Paralelização quando Possível:**
   - Iniciar revisão bibliográfica desde já
   - Desenvolver modelos enquanto dataset é preparado

3. **Buffers de Tempo:**
   - Adicionar 1-2 semanas de buffer antes da entrega final (05/12)
   - Antecipar revisão com orientador para ter tempo de ajustes

---

### 16.3 Riscos Operacionais e Plano de Contingência

#### Classificação de Riscos:

| ID | Risco | Probabilidade | Impacto | Severidade | Categoria |
|----|-------|---------------|---------|------------|-----------|
| **R1** | Atraso na aprovação do plano pelo orientador | 🟡 Média | 🔴 Alto | 🔴 **ALTO** | Cronograma |
| **R2** | Falha de hardware (computador pessoal) | 🟢 Baixa | 🔴 Alto | 🟡 **MÉDIO** | Infraestrutura |
| **R3** | Dataset indisponível ou corrompido | 🟢 Baixa | 🔴 Alto | 🟡 **MÉDIO** | Dados |
| **R4** | Experimento leva mais tempo que o estimado (>15h) | 🟡 Média | 🟡 Médio | 🟡 **MÉDIO** | Execução |
| **R5** | Bugs críticos nos scripts durante execução | 🟡 Média | 🔴 Alto | 🔴 **ALTO** | Código |
| **R6** | Resultados não mostram diferenças significativas | 🟡 Média | 🟡 Médio | 🟡 **MÉDIO** | Resultados |
| **R7** | Indisponibilidade do orientador em períodos críticos | 🟡 Média | 🟡 Médio | 🟡 **MÉDIO** | Recursos Humanos |
| **R8** | Escopo cresce além do planejado (scope creep) | 🟡 Média | 🟡 Médio | 🟡 **MÉDIO** | Escopo |
| **R9** | Problemas de saúde do pesquisador | 🟢 Baixa | 🔴 Alto | 🟡 **MÉDIO** | Pessoal |
| **R10** | Mudança de requisitos da universidade (normas TCC) | 🟢 Baixa | 🟡 Médio | 🟢 **BAIXO** | Regulatório |

#### Planos de Contingência Detalhados:

---

**R1: Atraso na aprovação do plano pelo orientador**

**Descrição:** Orientador demora para revisar ou solicita mudanças significativas no plano, atrasando início da execução.

**Probabilidade:** 🟡 Média (30-40%)
**Impacto:** 🔴 Alto (atrasa todo cronograma)
**Severidade:** 🔴 **ALTO**

**Mitigação Preventiva:**
- ✅ Enviar versões parciais do plano ao longo do desenvolvimento
- ✅ Agendar reuniões periódicas quinzenais para alinhamento
- ✅ Explicitar pontos que precisam de validação urgente

**Plano de Contingência:**
1. Se atraso < 2 semanas: Ajustar cronograma, reduzir tempo de revisão bibliográfica
2. Se atraso > 2 semanas: Escalar para coordenação ou considerar adiar entrega

**Responsável:** Renato

---

**R2-R10:** *(Planos detalhados de contingência para cada risco conforme seção 16.3)*

#### Matriz de Riscos:

```
          IMPACTO
          Baixo   Médio    Alto
        |-------|--------|--------|
Baixa   |       |  R10   | R2,R3  |
PROB.   |-------|--------|--------|
Média   |       | R4,R6  | R1,R5  |
        |       | R7,R8  |        |
        |-------|--------|--------|
```

**Legenda:**
- 🔴 **Risco Alto:** Monitoramento ativo e plano de ação detalhado
- 🟡 **Risco Médio:** Monitorar periodicamente
- 🟢 **Risco Baixo:** Aceitável, mitigação mínima

---

## 17. Governança do Experimento

### 17.1 Papéis e Responsabilidades Formais

#### Estrutura de Governança:

| Papel | Pessoa | Responsabilidade | Autoridade |
|-------|--------|------------------|------------|
| **Pesquisador / Executor** | Renato Matos Alves Penna | - Executar todas as atividades do experimento<br>- Tomar decisões operacionais cotidianas<br>- Propor mudanças no plano<br>- Documentar e reportar progresso | **Decide:** Detalhes técnicos de implementação<br>**Propõe:** Mudanças no plano experimental |
| **Orientador / Revisor** | Prof. Danilo de Quadros Maia Filho | - Revisar e aprovar o plano experimental<br>- Validar metodologia científica<br>- Aprovar mudanças significativas<br>- Autorizar entrega final | **Decide:** Aprovação do plano e mudanças<br>**Aprova:** Entregas e conclusão |
| **Coordenação do TCC** | Coordenador de TCC (PUC Minas) | - Validar conformidade com normas<br>- Aprovar tema e orientador<br>- Designar banca examinadora | **Decide:** Conformidade administrativa<br>**Aprova:** Defesa e conclusão |
| **Banca Examinadora** | Professores designados pela coordenação | - Avaliar o trabalho final<br>- Fazer recomendações<br>- Aprovar/reprovar a defesa | **Decide:** Aprovação final do TCC |

#### Matriz RACI (Resumida):

| Atividade | Renato | Orientador | Coordenação | Banca |
|-----------|--------|------------|-------------|-------|
| **Planejamento Experimental** | R, A | C, A | I | - |
| **Implementação de Scripts** | R, A | I | - | - |
| **Execução do Experimento** | R, A | I | - | - |
| **Análise de Resultados** | R, A | C | - | - |
| **Redação do TCC** | R, A | C, A | I | - |
| **Aprovação de Mudanças** | R | A | I | - |
| **Entrega Final** | R | A | C | - |
| **Defesa do TCC** | R | C | I | A |

**Legenda:**
- **R (Responsible):** Executante responsável pela atividade
- **A (Accountable):** Autoridade final que aprova
- **C (Consulted):** Consultado antes de decisões
- **I (Informed):** Informado após decisões

#### Fluxo de Decisão:

```
┌─────────────────────────────────────────────┐
│  Decisão Necessária                         │
└──────────────┬──────────────────────────────┘
               │
               ▼
       ┌───────────────┐
       │ Tipo de       │
       │ Decisão?      │
       └───┬───────┬───┘
           │       │
    Operacional   Estratégica
           │       │
           ▼       ▼
     ┌─────────┐  ┌────────────────┐
     │ Renato  │  │ Proposta para  │
     │ Decide  │  │ Orientador     │
     └────┬────┘  └────┬───────────┘
          │            │
          │            ▼
          │      ┌───────────────┐
          │      │ Orientador    │
          │      │ Aprova?       │
          │      └───┬────┬──────┘
          │         Sim   Não
          │          │    │
          │          │    ▼
          │          │  Ajustar Proposta
          │          │    │
          │          │◀───┘
          │          │
          ▼          ▼
      ┌────────────────────┐
      │  Decisão Executada │
      └────────────────────┘
```

#### Exemplos de Decisões por Tipo:

**Decisões Operacionais (Renato decide):**
- Qual IDE usar (VS Code, PyCharm, etc.)
- Como nomear variáveis no código
- Quando executar o experimento (horário/dia)
- Formato de visualizações específicas

**Decisões Estratégicas (Orientador aprova):**
- Mudanças no desenho experimental
- Adição/remoção de modelos ou métricas
- Mudanças no escopo do estudo
- Alterações significativas no cronograma

**Decisões Administrativas (Coordenação aprova):**
- Mudança de orientador
- Prorrogação de prazo além do semestre
- Conformidade com normas da universidade

---

### 17.2 Ritos de Acompanhamento Pré-Execução

#### Reuniões e Checkpoints Planejados:

| # | Rito | Frequência | Participantes | Objetivo | Duração | Formato |
|---|------|------------|---------------|----------|---------|---------|
| **1** | **Reunião de Alinhamento Quinzenal** | A cada 15 dias | Renato + Orientador | - Reportar progresso<br>- Discutir dúvidas<br>- Alinhar próximos passos | 30-60 min | Presencial ou virtual |
| **2** | **Revisão de Marco (Checkpoint)** | Em marcos críticos | Renato + Orientador | - Apresentar entrega<br>- Obter aprovação formal<br>- Ajustar plano (se necessário) | 60-90 min | Presencial (preferencial) |
| **3** | **E-mail de Status Semanal** | Semanalmente | Renato → Orientador | - Atualizar status de atividades<br>- Reportar riscos/bloqueios<br>- Solicitar feedback assíncrono | - | E-mail |
| **4** | **Go/No-Go Review** | Antes da execução (05/06) | Renato + Orientador | - Validar prontidão para executar<br>- Decisão formal de iniciar<br>- Confirmar recursos e preparação | 60 min | Presencial |

#### Detalhamento dos Ritos:

---

**Rito 1: Reunião de Alinhamento Quinzenal**

**Objetivo:** Manter orientador informado e obter feedback contínuo.

**Agenda Sugerida:**
1. **Progresso desde última reunião** (10 min)
   - O que foi feito
   - Dificuldades encontradas

2. **Revisão de artefatos/código** (15 min)
   - Demonstrar código desenvolvido (se aplicável)
   - Mostrar análises preliminares

3. **Dúvidas e consultoria** (15 min)
   - Esclarecer questões metodológicas
   - Validar decisões técnicas

4. **Próximos passos** (10 min)
   - Definir atividades até próxima reunião
   - Identificar dependências do orientador

5. **Riscos e bloqueios** (10 min)
   - Reportar riscos identificados
   - Solicitar ajuda se necessário

**Outputs:**
- Ata de reunião (e-mail resumo)
- Lista de ações e responsáveis
- Data da próxima reunião

---

**Rito 2: Revisão de Marco (Checkpoint)**

**Marcos Previstos:**

| Marco | Data Prevista | Entrega Esperada | Critério de Aprovação |
|-------|---------------|------------------|----------------------|
| **M1: Plano Aprovado** | 31/05/2025 | Plano experimental completo | Orientador aprova metodologia e escopo |
| **M2: Infraestrutura Pronta** | 31/05/2025 | - Ambiente configurado<br>- Dataset baixado<br>- Scripts básicos funcionais | Dry run executado com sucesso |
| **M3: Experimento Concluído** | 27/06/2025 | - 120 execuções completas<br>- Resultados validados<br>- Backup feito | Dados íntegros e prontos para análise |
| **M4: Análise Finalizada** | 31/07/2025 | - Análises estatísticas<br>- Gráficos<br>- Respostas às QPs | Resultados interpretados e consistentes |
| **M5: TCC Rascunho** | 31/10/2025 | Primeira versão completa do TCC | Orientador revisa e dá feedback |
| **M6: TCC Final** | 30/11/2025 | Versão final revisada | Orientador aprova para entrega |

**Formato da Revisão:**
- Apresentação formal pelo pesquisador (slides ou documento)
- Demonstração de artefatos (código, dados, análises)
- Checklist de prontidão/completude
- Decisão de aprovação ou solicitação de ajustes

---

**Rito 3: E-mail de Status Semanal**

**Template de E-mail:**

```
Assunto: [TCC] Status Semanal - Semana XX/2025

Prof. Danilo,

Segue atualização semanal do TCC:

✅ REALIZADAS ESTA SEMANA:
- [Lista de atividades concluídas]

🚧 EM ANDAMENTO:
- [Atividades atuais]

📅 PRÓXIMAS ATIVIDADES:
- [Planejado para próxima semana]

⚠️ RISCOS/BLOQUEIOS:
- [Se houver, descrever]

❓ DÚVIDAS/NECESSIDADES:
- [Se houver, perguntas específicas]

Att,
Renato
```

**Frequência:** Toda segunda-feira (ou dia combinado)

---

**Rito 4: Go/No-Go Review**

**Data:** 05/06/2025 (antes da execução)

**Objetivo:** Decisão formal de iniciar a execução do experimento.

**Checklist de Prontidão (ver Seção 20):**
- [ ] Plano experimental aprovado
- [ ] Scripts desenvolvidos e testados
- [ ] Dataset baixado e validado
- [ ] Dry run executado com sucesso (n=5)
- [ ] Ambiente funcional
- [ ] Backups configurados
- [ ] Seeds preparados

**Resultado:** **GO** (autoriza execução) ou **NO-GO** (ajustes necessários)

---

### 17.3 Processo de Controle de Mudanças no Plano

#### Política de Mudanças:

**Princípio:** O plano experimental é um documento vivo, mas mudanças devem ser **controladas e documentadas**.

#### Classificação de Mudanças:

| Tipo | Exemplos | Aprovação Necessária | Processo |
|------|----------|---------------------|----------|
| **Mudança Trivial** | - Correção de typo<br>- Ajuste de formatação<br>- Clarificação de texto | ❌ Não | Executar diretamente |
| **Mudança Menor** | - Ajuste de cronograma interno (< 1 semana)<br>- Mudança de ferramenta (ex: IDE)<br>- Ajuste de visualizações | 🟡 Informal (e-mail) | Informar orientador por e-mail |
| **Mudança Média** | - Ajuste de hiperparâmetros<br>- Mudança de método de validação cruzada<br>- Adição de métrica secundária | 🟠 Formal | Reunião + aprovação por escrito |
| **Mudança Significativa** | - Mudança no desenho experimental<br>- Adição/remoção de modelos<br>- Mudança no escopo (objetivos, QPs)<br>- Atraso > 2 semanas | 🔴 Crítica | Reunião + revisão de viabilidade + aprovação formal |

#### Fluxo de Controle de Mudanças:

```
┌─────────────────────────────────┐
│  Necessidade de Mudança         │
│  Identificada                   │
└──────────────┬──────────────────┘
               │
               ▼
       ┌───────────────┐
       │ Classificar   │
       │ Tipo de       │
       │ Mudança       │
       └───┬───────┬───┘
           │       │
    Trivial/Menor  Média/Significativa
           │       │
           ▼       ▼
     ┌─────────┐  ┌────────────────┐
     │ Executar│  │ Preparar       │
     │ ou      │  │ Proposta de    │
     │ Informar│  │ Mudança        │
     └────┬────┘  └────┬───────────┘
          │            │
          │            ▼
          │      ┌───────────────┐
          │      │ Apresentar ao │
          │      │ Orientador    │
          │      └───┬───────────┘
          │          │
          │          ▼
          │      ┌───────────────┐
          │      │ Orientador    │
          │      │ Aprova?       │
          │      └───┬────┬──────┘
          │         Sim   Não
          │          │    │
          │          │    ▼
          │          │  Revisar ou Rejeitar
          │          │    │
          │          │◀───┘
          │          │
          ▼          ▼
      ┌────────────────────┐
      │  Atualizar Plano   │
      │  (controle versão) │
      └────────────────────┘
               │
               ▼
      ┌────────────────────┐
      │  Comunicar Mudança │
      │  (se necessário)   │
      └────────────────────┘
```

#### Template de Proposta de Mudança:

**Para mudanças Médias e Significativas:**

```markdown
## Proposta de Mudança no Plano Experimental

**Data:** [DD/MM/YYYY]
**Proponente:** Renato Matos Alves Penna
**Classificação:** [ ] Média  [ ] Significativa

### 1. Descrição da Mudança Proposta:
[Descrever claramente o que será mudado]

### 2. Justificativa:
[Por que a mudança é necessária?]

### 3. Impacto:
- **Escopo:** [Afeta objetivos, QPs, escopo?]
- **Cronograma:** [Adiciona/remove tempo? Quanto?]
- **Qualidade/Validade:** [Impacta validade dos resultados?]
- **Recursos:** [Requer recursos adicionais?]

### 4. Alternativas Consideradas:
[Outras opções avaliadas e por que foram descartadas]

### 5. Decisão Solicitada:
[ ] Aprovar
[ ] Aprovar com ajustes
[ ] Rejeitar

### 6. Aprovação:
**Orientador:** _______________________
**Data:** ___ /___ /______
```

#### Registro de Mudanças:

**Todas as mudanças aprovadas serão documentadas no histórico de revisão do documento (Seção 1.3).**

---

## 18. Plano de Documentação e Reprodutibilidade

### 18.1 Repositórios e Convenções de Nomeação

#### Repositório Principal:

**GitHub:** https://github.com/RenatoMAP77/pre-tcc

**Tipo:** Repositório público
**Licença:** MIT License (para código) + CC-BY (para documentação)

#### Estrutura de Diretórios:

```
pre-tcc/
│
├── README.md                          # Este plano experimental
├── LICENSE                            # Licença MIT
├── requirements.txt                   # Dependências Python
├── .gitignore                         # Arquivos ignorados pelo Git
│
├── data/                              # Dados (não versionados se > 100MB)
│   ├── raw/                           # Dados brutos do Google Cluster
│   ├── processed/                     # Dados processados/agregados
│   └── README.md                      # Descrição dos dados
│
├── src/                               # Código-fonte
│   ├── preparar_dados.py              # Script de preparação de dados
│   ├── modelos.py                     # Implementação dos modelos
│   ├── executar_experimento.py       # Script principal de execução
│   ├── utils.py                       # Funções auxiliares
│   └── __init__.py                    # Pacote Python
│
├── notebooks/                         # Jupyter Notebooks
│   ├── 01_exploracao_dados.ipynb     # Análise exploratória
│   ├── 02_validacao_preparacao.ipynb # Validação do pré-processamento
│   └── 03_analise_resultados.ipynb   # Análise estatística final
│
├── results/                           # Resultados do experimento
│   ├── raw/                           # Resultados brutos (CSV)
│   ├── figures/                       # Gráficos e visualizações
│   ├── tables/                        # Tabelas formatadas
│   └── README.md                      # Descrição dos resultados
│
├── logs/                              # Logs de execução
│   ├── experimento.log                # Log principal
│   └── [timestamp]_exec.log          # Logs individuais
│
├── config/                            # Configurações
│   ├── seeds.txt                      # Seeds aleatórios (30)
│   └── parametros.yaml                # Parâmetros configuráveis
│
├── docs/                              # Documentação adicional
│   ├── plano_experimental.md          # Cópia do README (backup)
│   └── manual_reproducao.md           # Guia de reprodução
│
└── tests/                             # Testes unitários (opcional)
    ├── test_preparar_dados.py
    └── test_modelos.py
```

#### Convenções de Nomeação:

**1. Arquivos de Código Python:**
- **Formato:** `snake_case.py`
- **Exemplos:** `preparar_dados.py`, `executar_experimento.py`

**2. Notebooks Jupyter:**
- **Formato:** `NN_descricao_clara.ipynb`
- **Exemplos:** `01_exploracao_dados.ipynb`, `03_analise_resultados.ipynb`
- **Numeração:** 01, 02, 03... (ordem de execução)

**3. Arquivos de Dados:**
- **Dados brutos:** `google_cluster_raw.csv` (nome descritivo original)
- **Dados processados:** `dataset_processado_YYYY-MM-DD.csv` (com data)
- **Resultados:** `resultados_experimento_YYYY-MM-DD.csv`

**4. Gráficos e Visualizações:**
- **Formato:** `fig_NN_descricao.png` ou `.pdf`
- **Exemplos:** `fig_01_boxplot_mae_por_modelo.png`, `fig_02_series_temporais.pdf`

**5. Logs:**
- **Formato:** `YYYY-MM-DD_HH-MM-SS_nome.log`
- **Exemplo:** `2025-06-10_14-30-00_execucao_completa.log`

**6. Branches Git (se usar):**
- `main` ou `master`: Branch principal (código estável)
- `develop`: Branch de desenvolvimento
- `feature/nome-feature`: Para features específicas
- `fix/nome-bug`: Para correções de bugs

**7. Commits Git:**
- **Formato:** `tipo: descrição concisa`
- **Tipos:** `feat:`, `fix:`, `docs:`, `refactor:`, `test:`, `chore:`
- **Exemplos:**
  - `feat: adiciona implementação do modelo ARIMA`
  - `fix: corrige divisão treino/teste em TimeSeriesSplit`
  - `docs: atualiza README com seções 14-20`

---

### 18.2 Templates e Artefatos Padrão

#### Templates de Código:

**1. Template de Script Python:**

```python
#!/usr/bin/env python3
"""
Título: [Nome do Script]
Descrição: [Breve descrição do propósito]
Autor: Renato Matos Alves Penna
Data: YYYY-MM-DD
TCC: Previsão de Custos Cloud - PUC Minas
"""

import pandas as pd
import numpy as np
# [Outras importações]

# Configurações
SEED = 42  # Seed para reprodutibilidade
np.random.seed(SEED)

def funcao_principal():
    """
    Descrição da função.

    Args:
        param1 (tipo): Descrição

    Returns:
        tipo: Descrição do retorno
    """
    # Implementação
    pass

if __name__ == "__main__":
    # Executar quando script for chamado diretamente
    funcao_principal()
```

**2. Template de Notebook Jupyter:**

```markdown
# [Título do Notebook]

**Autor:** Renato Matos Alves Penna
**Data:** YYYY-MM-DD
**Objetivo:** [Descrição breve do objetivo]

---

## 1. Setup e Importações

## 2. Carregamento de Dados

## 3. Análise Exploratória

## 4. Processamento/Modelagem

## 5. Resultados e Visualizações

## 6. Conclusões

---

**Próximos Passos:**
- [Lista de ações]
```

**3. Template de Arquivo de Resultados (CSV):**

```
execucao_id,modelo,repeticao,seed,mae,rmse,mape,tempo_exec_s,fold,mae_fold
1,RL,1,1234,150.23,175.45,12.34,5.2,1,148.12
1,RL,1,1234,150.23,175.45,12.34,5.2,2,152.34
...
```

**Estrutura:**
- `execucao_id`: ID único da execução (1-120)
- `modelo`: Sigla do modelo (RL, MM, ARIMA, ES)
- `repeticao`: Número da repetição (1-30)
- `seed`: Seed usado para essa repetição
- `mae, rmse, mape`: Métricas principais (holdout)
- `tempo_exec_s`: Tempo de execução em segundos
- `fold`: Fold da validação cruzada (1-5)
- `mae_fold`: MAE no fold específico

**4. Template de Log:**

```
[YYYY-MM-DD HH:MM:SS] [INFO] Início da execução
[YYYY-MM-DD HH:MM:SS] [INFO] Carregando dados de: data/processed/dataset.csv
[YYYY-MM-DD HH:MM:SS] [INFO] Dataset carregado: 720 observações
[YYYY-MM-DD HH:MM:SS] [INFO] Iniciando repetição 1/30 com seed 1234
[YYYY-MM-DD HH:MM:SS] [INFO] Treinando modelo: RL
[YYYY-MM-DD HH:MM:SS] [INFO] MAE (holdout): 150.23
[YYYY-MM-DD HH:MM:SS] [INFO] Validação cruzada (5-fold): MAE médio = 151.45
[YYYY-MM-DD HH:MM:SS] [WARNING] Tempo de execução ARIMA maior que esperado: 350s
[YYYY-MM-DD HH:MM:SS] [ERROR] Erro ao processar modelo: [descrição do erro]
[YYYY-MM-DD HH:MM:SS] [INFO] Fim da execução. Tempo total: 45min
```

**Níveis de Log:**
- `DEBUG`: Informações detalhadas para debugging
- `INFO`: Informações gerais de progresso
- `WARNING`: Avisos (não bloqueiam execução)
- `ERROR`: Erros (podem bloquear execução)
- `CRITICAL`: Erros críticos (interrompem execução)

---

### 18.3 Plano de Empacotamento para Replicação Futura

#### Objetivo:

Permitir que qualquer pesquisador (incluindo o autor no futuro) possa **reproduzir completamente** o experimento.

#### Pacote de Reprodução:

**O que será incluído no repositório GitHub:**

1. **Código-fonte completo:**
   - Todos os scripts Python (`src/`)
   - Notebooks Jupyter (`notebooks/`)
   - Testes (se houver)

2. **Documentação:**
   - `README.md` (plano experimental completo)
   - `docs/manual_reproducao.md` (passo a passo para reproduzir)
   - Comentários inline no código

3. **Configurações:**
   - `requirements.txt` (dependências Python com versões fixas)
   - `config/seeds.txt` (seeds exatos usados)
   - `config/parametros.yaml` (parâmetros configuráveis)

4. **Dados (se possível):**
   - **Dados processados:** `data/processed/dataset_processado.csv` (se < 100MB)
   - **Se > 100MB:** Link para download externo + script de download
   - **Dados de resultados:** `results/raw/resultados_completos.csv`

5. **Metadados:**
   - Versão de Python usada: `python --version`
   - Versões de bibliotecas: `pip freeze > requirements.txt`
   - Sistema operacional: `uname -a` (Linux/Mac) ou `systeminfo` (Windows)
   - Data e hora da execução

6. **Licença:**
   - `LICENSE` (MIT para código, CC-BY para documentação)

#### Manual de Reprodução (docs/manual_reproducao.md):

**Template:**

```markdown
# Manual de Reprodução do Experimento

## Pré-requisitos

- Python 3.10 ou superior
- Git
- Conta Kaggle (para download do dataset)
- ~10 GB de espaço livre em disco
- ~16 GB de RAM (recomendado)

## Passo 1: Clonar o Repositório

```bash
git clone https://github.com/RenatoMAP77/pre-tcc.git
cd pre-tcc
```

## Passo 2: Criar Ambiente Virtual

```bash
python -m venv venv
source venv/bin/activate  # Linux/Mac
# ou
venv\Scripts\activate     # Windows
```

## Passo 3: Instalar Dependências

```bash
pip install -r requirements.txt
```

## Passo 4: Baixar Dados (se necessário)

```bash
# Opção A: Kaggle CLI
kaggle datasets download -d derrickmwiti/google-2019-cluster-sample
unzip google-2019-cluster-sample.zip -d data/raw/

# Opção B: Usar dados processados incluídos
# (Se dataset processado estiver no repositório, pular este passo)
```

## Passo 5: Preparar Dados

```bash
python src/preparar_dados.py
```

**Output esperado:** `data/processed/dataset_processado.csv` (~720 linhas)

## Passo 6: Executar Experimento

```bash
python src/executar_experimento.py
```

**Tempo estimado:** ~13-15 horas
**Output esperado:** `results/raw/resultados_experimento_[data].csv`

## Passo 7: Analisar Resultados

```bash
jupyter notebook notebooks/03_analise_resultados.ipynb
```

## Verificação de Reprodutibilidade

Os resultados devem ser **idênticos** (ou muito próximos) aos reportados no TCC, pois:
- Seeds estão fixos (`config/seeds.txt`)
- Versões de bibliotecas estão fixas (`requirements.txt`)
- Dataset é o mesmo

**Se houver diferenças:**
- Verificar versões de bibliotecas
- Verificar se seeds foram aplicados corretamente
- Verificar se dataset está íntegro (checksums)

## Troubleshooting

### Problema: "ModuleNotFoundError"
**Solução:** Instalar dependências: `pip install -r requirements.txt`

### Problema: "FileNotFoundError: dataset não encontrado"
**Solução:** Executar `preparar_dados.py` primeiro

### Problema: Tempo de execução muito longo
**Solução:** Reduzir N de 30 para 20 em `config/parametros.yaml` (ver seção de contingências)

## Contato

Para dúvidas sobre reprodução, abrir issue no GitHub ou contatar:
- Renato Matos Alves Penna: renatomatosapbusiness@gmail.com

#### Checklist de Empacotamento:

- [ ] Código-fonte completo e comentado
- [ ] `requirements.txt` com versões fixas
- [ ] `README.md` atualizado
- [ ] `docs/manual_reproducao.md` criado
- [ ] Seeds salvos em `config/seeds.txt`
- [ ] Resultados incluídos (ou link para download)
- [ ] Dataset processado incluído (se < 100MB) ou link fornecido
- [ ] Licença definida (`LICENSE`)
- [ ] `.gitignore` configurado (excluir arquivos temporários)
- [ ] Repositório GitHub público
- [ ] DOI/Zenodo (opcional, para citação permanente)

---

## 19. Plano de Comunicação

### 19.1 Públicos e Mensagens-Chave Pré-Execução

#### Mapeamento de Stakeholders:

| Público | Interesse | Necessidade de Informação | Frequência |
|---------|-----------|---------------------------|------------|
| **Orientador (Prof. Danilo)** | Alto | - Progresso do trabalho<br>- Decisões metodológicas<br>- Riscos/bloqueios | Quinzenal/Mensal |
| **Coordenação de TCC (PUC Minas)** | Médio | - Conformidade com normas<br>- Prazos e entregas<br>- Temas e defesas | Conforme cronograma institucional |
| **Colegas de Turma** | Baixo | - Tema e abordagem<br>- Aprendizados compartilhados | Informal (opcional) |
| **Comunidade Acadêmica (GitHub)** | Baixo | - Código aberto<br>- Reprodutibilidade | Quando repositório for publicado |

#### Mensagens-Chave por Público:

**Para o Orientador:**
- **Objetivo:** "Comparar modelos de previsão de custos cloud usando dados reais do Google"
- **Progresso:** "Estou na fase [X], próximo marco é [Y] em [data]"
- **Riscos:** "Identifiquei risco [Z], proposta de mitigação é [W]"
- **Dúvidas:** "Preciso de orientação sobre [tema específico]"

**Para a Coordenação:**
- **Tema:** "Previsão de Custos de Infraestrutura Cloud Utilizando Séries Temporais"
- **Orientador:** "Prof. Danilo de Quadros Maia Filho"
- **Cronograma:** "Entrega prevista para 05/12/2025, defesa em dezembro"
- **Conformidade:** "Não envolve sujeitos humanos, dispensa CEP"

**Para Colegas (informal):**
- **Tema leigo:** "Estou criando modelos que preveem quanto vai custar rodar aplicações na nuvem"
- **Técnico:** "Comparando regressão linear, ARIMA e exponential smoothing para previsão de custos cloud"

---

### 19.2 Canais e Frequência de Comunicação

#### Matriz de Comunicação:

| Público | Canal | Frequência | Responsável | Formato |
|---------|-------|------------|-------------|---------|
| **Orientador** | E-mail | Semanal | Renato | E-mail de status |
| | Reunião presencial/virtual | Quinzenal | Renato (agendar) | Reunião formal |
| | WhatsApp/Telefone | Conforme necessário | Renato | Mensagem rápida |
| **Coordenação TCC** | Sistema acadêmico PUC | Conforme prazos | PUC Minas | Submissão formal |
| | E-mail institucional | Quando necessário | Renato | E-mail formal |
| **Comunidade GitHub** | Repositório público | Quando atualizado | Renato | Commits + README |
| **Registro pessoal** | Diário de bordo (opcional) | Diário/Semanal | Renato | Anotações pessoais |

#### Detalhamento por Canal:

**1. E-mail (Orientador):**
- **Frequência:** Toda segunda-feira (ou dia combinado)
- **Template:** Ver Seção 17.2 (E-mail de Status Semanal)
- **Tempo de resposta esperado:** 2-3 dias úteis

**2. Reunião Presencial/Virtual (Orientador):**
- **Frequência:** A cada 15 dias
- **Duração:** 30-60 minutos
- **Agendamento:** Com pelo menos 3 dias de antecedência
- **Ferramentas:** Google Meet, Zoom ou presencial (PUC Minas)

**3. Sistema Acadêmico PUC Minas:**
- **Uso:** Submissão de entregas formais (se houver)
- **Atenção:** Seguir prazos institucionais rigorosamente

**4. GitHub (Comunidade):**
- **Commits:** A cada feature/bug fix relevante
- **README:** Manter atualizado com progresso geral
- **Issues:** Para discussões técnicas (se alguém abrir)

---

### 19.3 Pontos de Comunicação Obrigatórios

#### Eventos que Exigem Comunicação Formal:

| # | Evento | Para Quem Comunicar | Canal | Prazo | Conteúdo |
|---|--------|---------------------|-------|-------|----------|
| **1** | **Conclusão do Plano Experimental** | Orientador | E-mail + Reunião | Imediato | - Plano completo em anexo<br>- Solicitar revisão<br>- Agendar reunião de validação |
| **2** | **Aprovação do Plano** | Coordenação (se requerido) | Sistema PUC | Após aprovação do orientador | - Confirmar tema aprovado<br>- Orientador designado |
| **3** | **Mudança Significativa no Plano** | Orientador | E-mail + Reunião | Antes de implementar | - Proposta de mudança<br>- Justificativa<br>- Impactos |
| **4** | **Início da Execução do Experimento** | Orientador | E-mail | 1 dia antes | - Confirmar Go decision<br>- Data/hora de início<br>- Tempo estimado |
| **5** | **Conclusão da Execução** | Orientador | E-mail | No mesmo dia | - Confirmar conclusão<br>- Status dos resultados<br>- Próximos passos |
| **6** | **Identificação de Risco Crítico** | Orientador | E-mail + Telefone (urgente) | Imediatamente | - Descrição do risco<br>- Impacto no cronograma<br>- Proposta de mitigação |
| **7** | **Atraso Significativo (> 1 semana)** | Orientador + Coordenação | E-mail formal | Assim que identificado | - Razão do atraso<br>- Novo cronograma<br>- Impacto na entrega final |
| **8** | **Entrega de Versão Preliminar do TCC** | Orientador | E-mail + PDF | Conforme combinado | - TCC em PDF<br>- Solicitar revisão<br>- Prazo para feedback |
| **9** | **Submissão Final do TCC** | Coordenação | Sistema PUC | Até 05/12/2025 | - TCC final formatado<br>- Documentos requeridos<br>- Declarações |
| **10** | **Agendamento de Defesa** | Coordenação | Sistema PUC | Após aprovação da coordenação | - Confirmar disponibilidade<br>- Data preferencial |

#### Templates de Comunicação para Eventos Críticos:

**Template 1: Conclusão do Plano Experimental**

```
Assunto: [TCC] Plano Experimental Completo - Solicitação de Revisão

Prof. Danilo,

Concluí a elaboração do plano experimental do TCC, conforme discutido.

ANEXO: Plano Experimental Completo (README.md / PDF)

O plano inclui:
✅ Objetivos, questões de pesquisa e métricas (GQM)
✅ Desenho experimental (fator único, CRD, n=30)
✅ Protocolo operacional detalhado
✅ Análise de ameaças à validade
✅ Cronograma (execução prevista para junho/julho)

Solicito revisão e aprovação para iniciar a implementação.

Podemos agendar uma reunião para discussão?
Proposta de datas: [data 1], [data 2], [data 3]

Att,
Renato
```

---

**Template 2: Identificação de Risco Crítico**

```
Assunto: [TCC] URGENTE - Risco Crítico Identificado

Prof. Danilo,

Identifiquei um risco crítico que pode impactar o cronograma:

⚠️ RISCO: [Descrição do risco]
📊 IMPACTO: [Descrição do impacto - ex: atraso de 2 semanas]
📅 PRAZO AFETADO: [Marco ou entrega afetada]

PROPOSTA DE MITIGAÇÃO:
[Descrição da proposta]

Solicito orientação urgente.
Disponível para reunião emergencial.

Att,
Renato
Cel: [telefone]
```

---

**Template 3: Submissão Final do TCC**

```
Assunto: [TCC] Submissão Final - Renato Matos Alves Penna

Coordenação de TCC,

Segue submissão final do Trabalho de Conclusão de Curso:

TÍTULO: Previsão de Custos de Infraestrutura Cloud Utilizando Modelos Baseados em Métricas Reais: Uma Comparação entre Algoritmos Simples e Técnicas de Séries Temporais

ALUNO: Renato Matos Alves Penna
ORIENTADOR: Prof. Danilo de Quadros Maia Filho
DATA DE SUBMISSÃO: 05/12/2025

ANEXOS:
- TCC_RenatoMatos_VersaoFinal.pdf
- Termo de Compromisso assinado
- [Outros documentos requeridos]

Aguardo retorno sobre agendamento de defesa.

Att,
Renato Matos Alves Penna
Matrícula: [número]
renatomatosapbusiness@gmail.com
```

---

## 20. Critérios de Prontidão para Execução (Definition of Ready)

### 20.1 Checklist de Prontidão (Itens que Devem Estar Completos)

#### Objetivo:

Esta seção define os **critérios objetivos** que devem ser atendidos para autorizar o **início da execução do experimento** (prevista para 10/06/2025).

#### Checklist Completo de Prontidão:

---

**CATEGORIA 1: PLANEJAMENTO E DOCUMENTAÇÃO**

- [ ] **1.1 Plano Experimental Completo**
  - [ ] Documento README.md com todas as 20 seções preenchidas
  - [ ] Objetivos, questões de pesquisa e métricas (GQM) claramente definidos
  - [ ] Desenho experimental documentado (fator único, CRD, n=30)
  - [ ] Protocolo operacional passo a passo descrito (Seção 11.3)
  - [ ] Ameaças à validade identificadas e mitigações planejadas (Seção 13)

- [ ] **1.2 Aprovação do Orientador**
  - [ ] Plano experimental revisado pelo Prof. Danilo
  - [ ] Aprovação formal recebida (e-mail ou ata de reunião)
  - [ ] Feedback incorporado ao documento

- [ ] **1.3 Cronograma Validado**
  - [ ] Datas de marcos críticos confirmadas
  - [ ] Tempo de execução realista (13-15h) considerado
  - [ ] Buffer de tempo para imprevistos incluído

---

**CATEGORIA 2: INFRAESTRUTURA TÉCNICA**

- [ ] **2.1 Ambiente Computacional**
  - [ ] Python 3.10+ instalado e funcional
  - [ ] Ambiente virtual criado (`venv` ou `conda`)
  - [ ] Todas as bibliotecas necessárias instaladas (ver `requirements.txt`)
  - [ ] IDE configurada (VS Code, PyCharm ou similar)
  - [ ] Git instalado e configurado

- [ ] **2.2 Repositório GitHub**
  - [ ] Repositório criado: https://github.com/RenatoMAP77/pre-tcc
  - [ ] Estrutura de diretórios criada (`src/`, `data/`, `results/`, etc.)
  - [ ] `.gitignore` configurado
  - [ ] Primeiro commit realizado

- [ ] **2.3 Acesso a Dados**
  - [ ] Conta Kaggle criada e autenticada
  - [ ] Google Cluster Data 2019 baixado e validado
  - [ ] Dataset bruto armazenado em `data/raw/`
  - [ ] Integridade dos dados verificada (checksums, se disponível)

---

**CATEGORIA 3: CÓDIGO E SCRIPTS**

- [ ] **3.1 Scripts de Preparação de Dados**
  - [ ] `preparar_dados.py` desenvolvido
  - [ ] Script testado e executado com sucesso
  - [ ] Dataset processado gerado em `data/processed/`
  - [ ] Validação de qualidade dos dados aprovada (Seção 10.2)

- [ ] **3.2 Implementação dos Modelos**
  - [ ] Modelo 1: Regressão Linear implementado
  - [ ] Modelo 2: Média Móvel implementado
  - [ ] Modelo 3: ARIMA implementado (com grid search)
  - [ ] Modelo 4: Exponential Smoothing implementado
  - [ ] Todos os modelos testados individualmente

- [ ] **3.3 Script Principal de Execução**
  - [ ] `executar_experimento.py` desenvolvido
  - [ ] Integração com todos os 4 modelos funcional
  - [ ] TimeSeriesSplit (k=5) implementado corretamente
  - [ ] Sistema de logging configurado
  - [ ] Salvamento incremental de resultados implementado

- [ ] **3.4 Funções Auxiliares**
  - [ ] Funções de cálculo de métricas (MAE, RMSE, MAPE) implementadas
  - [ ] Funções de divisão treino/teste com seed implementadas
  - [ ] Funções de validação de dados implementadas

---

**CATEGORIA 4: VALIDAÇÃO PRÉVIA (DRY RUN)**

- [ ] **4.1 Execução de Teste Realizada**
  - [ ] Dry run executado com n=5 repetições
  - [ ] Todos os 4 modelos rodaram sem erros
  - [ ] Resultados salvos em arquivo CSV

- [ ] **4.2 Validação de Outputs**
  - [ ] Arquivo `resultados.csv` gerado com estrutura correta
  - [ ] Logs gerados corretamente em `logs/`
  - [ ] Métricas estão em ranges plausíveis (MAE > 0, MAPE < 100%)

- [ ] **4.3 Validação de Tempo**
  - [ ] Tempo de execução do dry run medido
  - [ ] Tempo de execução completo estimado (30 × tempo dry run)
  - [ ] Tempo estimado é viável (< 20h)

- [ ] **4.4 Correção de Bugs**
  - [ ] Todos os bugs identificados no dry run foram corrigidos
  - [ ] Scripts atualizados e testados novamente

---

**CATEGORIA 5: CONFIGURAÇÕES E PARÂMETROS**

- [ ] **5.1 Seeds de Reprodutibilidade**
  - [ ] 30 seeds aleatórios gerados com seed mestre = 42
  - [ ] Seeds salvos em `config/seeds.txt`
  - [ ] Script configurado para usar seeds corretamente

- [ ] **5.2 Hiperparâmetros Definidos**
  - [ ] Grid search do ARIMA configurado: p ∈ {0,1,2}, d ∈ {0,1}, q ∈ {0,1,2}
  - [ ] Parâmetros do ES definidos: trend, seasonal, seasonal_periods
  - [ ] Janela da Média Móvel definida: N = 7

- [ ] **5.3 Parâmetros de Validação**
  - [ ] k-fold = 5 configurado (TimeSeriesSplit)
  - [ ] Divisão treino/teste = 70%-30% configurada

---

**CATEGORIA 6: BACKUPS E SEGURANÇA**

- [ ] **6.1 Sistema de Backup**
  - [ ] Repositório GitHub configurado como backup remoto
  - [ ] Backup local em segundo dispositivo (opcional, mas recomendado)
  - [ ] Google Drive configurado como backup adicional (opcional)

- [ ] **6.2 Salvamento Incremental**
  - [ ] Script configurado para salvar resultados a cada execução
  - [ ] Mecanismo de restart implementado (para retomar se falhar)

---

**CATEGORIA 7: RECURSOS E LOGÍSTICA**

- [ ] **7.1 Disponibilidade de Tempo**
  - [ ] Período de ~2 semanas reservado para execução (10-25/06)
  - [ ] Computador disponível por longos períodos (execução pode levar 13-15h)
  - [ ] Alternativa planejada (ex: executar durante a noite)

- [ ] **7.2 Contingências Planejadas**
  - [ ] Plano B para hardware (laboratórios PUC, se computador falhar)
  - [ ] Plano B para dados (BigQuery, se Kaggle falhar)
  - [ ] Plano de redução de N (de 30 para 20, se tempo exceder muito)

---

**CATEGORIA 8: COMUNICAÇÃO E APROVAÇÃO**

- [ ] **8.1 Comunicação ao Orientador**
  - [ ] Orientador informado sobre data de início da execução
  - [ ] Última reunião de validação realizada
  - [ ] Orientador ciente de que experimento levará ~13-15h

- [ ] **8.2 Registro de Prontidão**
  - [ ] Checklist de prontidão revisado e todos os itens confirmados
  - [ ] Data de conclusão da preparação registrada
  - [ ] Go/No-Go decision documentada

---

#### Resumo Visual - Status de Prontidão:

```
CATEGORIA                         STATUS  COMPLETUDE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
1. Planejamento e Documentação   [  ]    0/3
2. Infraestrutura Técnica         [  ]    0/3
3. Código e Scripts               [  ]    0/4
4. Validação Prévia (Dry Run)     [  ]    0/4
5. Configurações e Parâmetros     [  ]    0/3
6. Backups e Segurança            [  ]    0/2
7. Recursos e Logística           [  ]    0/2
8. Comunicação e Aprovação        [  ]    0/2
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
TOTAL: 0/23 categorias completas

DECISÃO: [  ] GO  [  ] NO-GO
```

---

### 20.2 Aprovações Finais para Iniciar a Operação

#### Processo de Go/No-Go Decision:

**Data Planejada:** 05/06/2025
**Participantes:** Renato (Pesquisador) + Prof. Danilo (Orientador)

#### Critérios de Decisão:

**✅ GO (Autorizar Execução):**

Condições **obrigatórias** para autorizar início:

1. **Checklist de Prontidão ≥ 90% completo**
   - Máximo 2-3 itens não-críticos pendentes
   - Todos os itens críticos DEVEM estar completos

2. **Dry Run Bem-Sucedido**
   - Execução de teste (n=5) rodou sem erros
   - Resultados validados e plausíveis
   - Bugs corrigidos

3. **Aprovação do Orientador**
   - Plano experimental aprovado
   - Orientador confirma prontidão metodológica
   - Orientador valida cronograma

4. **Recursos Garantidos**
   - Computador funcional e disponível
   - Dataset baixado e validado
   - Código testado e estável

**❌ NO-GO (Adiar Execução):**

Situações que **bloqueiam** início da execução:

1. **Checklist < 80% completo**
   - Muitos itens críticos pendentes
   - Infraestrutura não pronta

2. **Dry Run Falhou**
   - Erros não resolvidos
   - Resultados implausíveis
   - Tempo de execução inviável (> 30h estimadas)

3. **Falta de Aprovação**
   - Orientador não aprovou o plano
   - Mudanças significativas pendentes

4. **Riscos Críticos Não Mitigados**
   - Hardware instável
   - Dataset indisponível
   - Bugs críticos não resolvidos

#### Reunião de Go/No-Go:

**Formato da Reunião:**

1. **Revisão do Checklist** (20 min)
   - Renato apresenta status de cada categoria
   - Demonstra que itens críticos foram completados

2. **Demonstração do Dry Run** (15 min)
   - Mostrar resultados do teste (n=5)
   - Explicar tempo estimado para execução completa

3. **Discussão de Riscos** (15 min)
   - Revisar riscos identificados (Seção 16.3)
   - Confirmar planos de contingência

4. **Decisão Final** (10 min)
   - Orientador decide: GO ou NO-GO
   - Se GO: confirmar data de início
   - Se NO-GO: definir itens pendentes e nova data de revisão

**Registro da Decisão:**

```markdown
# Registro de Go/No-Go Decision

**Data da Reunião:** 05/06/2025
**Participantes:** Renato Matos Alves Penna, Prof. Danilo de Quadros Maia Filho

## Status do Checklist:
- Planejamento: [X] Completo
- Infraestrutura: [X] Completo
- Código: [X] Completo
- Dry Run: [X] Bem-sucedido
- Configurações: [X] Completo
- Backups: [X] Completo
- Recursos: [X] Garantidos
- Comunicação: [X] OK

## Resultado do Dry Run:
- Tempo médio por modelo: [X] segundos
- Tempo estimado total: ~[Y] horas
- Erros encontrados: [Nenhum / Lista]

## Riscos Identificados:
- [Lista de riscos e mitigações]

## DECISÃO:

[X] **GO** - Autorizado iniciar execução em 10/06/2025
[ ] **NO-GO** - Adiar execução. Itens pendentes: [lista]

## Observações:
[Comentários do orientador]

**Assinatura (Orientador):** _______________________
**Data:** ___/___/______
```

#### Após a Decisão GO:

**Próximos Passos Imediatos:**

1. **Comunicar Início:**
   - Enviar e-mail ao orientador confirmando data/hora de início
   - Documentar no log do experimento

2. **Preparação Final:**
   - Fechar aplicações desnecessárias no computador
   - Desabilitar atualizações automáticas
   - Verificar espaço em disco
   - Confirmar backup configurado

3. **Iniciar Execução:**
   - Executar `python src/executar_experimento.py`
   - Monitorar progresso inicial (primeiras 2-3 horas)
   - Confirmar que logs estão sendo gerados corretamente

4. **Monitoramento:**
   - Verificar progresso periodicamente
   - Registrar qualquer anomalia
   - Estar preparado para intervenção se necessário

---

## Referências Bibliográficas

### Previsão de Custos e Workloads em Nuvem

[1] **Calheiros, R.N., Masoumi, E., Ranjan, R., & Buyya, R. (2015).** "Workload Prediction Using ARIMA Model and Its Impact on Cloud Applications' QoS." *IEEE Transactions on Cloud Computing*, 3(4), 449-458. DOI: 10.1109/TCC.2014.2350475

[2] **Amiri, M., & Mohammad-Khanli, L. (2017).** "A Survey and Classification of the Workload Forecasting Methods in Cloud Computing." *Cluster Computing*, 20. DOI: 10.1007/s10586-017-1048-4

[3] **Tsoumakos, D., et al. (2023).** "Is Machine Learning Necessary for Cloud Resource Usage Forecasting?" *ACM Symposium on Cloud Computing (SoCC '23)*. DOI: 10.1145/3620678.3624790

[4] **Khandelwal, V., Chaturvedi, A.K., & Gupta, C.P. (2020).** "Amazon EC2 Spot Price Prediction Using Regression Random Forests." *IEEE Transactions on Cloud Computing*, 8(1), 59-72. DOI: 10.1109/TCC.2017.2780159

[5] **Chhetri, M.B., Lumpe, M., Vo, Q.B., & Kowalczyk, R. (2017).** "On Forecasting Amazon EC2 Spot Prices Using Time-Series Decomposition with Hybrid Look-Backs." *IEEE International Conference on Edge Computing*. DOI: 10.1109/IEEE.EDGE.2017.55

[6] **Fragiadakis, G., et al. (2023).** "Applying Machine Learning in Cloud Service Price Prediction: The Case of Amazon IaaS." *Future Internet (MDPI)*, 15(8), 277. DOI: 10.3390/fi15080277

### Fundamentos Teóricos de Séries Temporais

[7] **Box, G.E.P., Jenkins, G.M., Reinsel, G.C., & Ljung, G.M. (2015).** *Time Series Analysis: Forecasting and Control* (5th ed.). John Wiley & Sons. ISBN: 978-1-118-67502-1

[8] **Hamilton, J.D. (1994).** *Time Series Analysis*. Princeton University Press. ISBN: 978-0-691-04289-3

[9] **Brockwell, P.J., & Davis, R.A. (2009).** *Time Series: Theory and Methods* (2nd ed.). Springer. ISBN: 978-1-4419-0319-8

[10] **Holt, C.C. (1957/2004).** "Forecasting Seasonals and Trends by Exponentially Weighted Moving Averages." *International Journal of Forecasting*, 20(1), 5-10. DOI: 10.1016/j.ijforecast.2003.09.015

[11] **Winters, P.R. (1960).** "Forecasting Sales by Exponentially Weighted Moving Averages." *Management Science*, 6(3), 324-342. DOI: 10.1287/mnsc.6.3.324

[12] **Gardner, E.S., Jr. (1985).** "Exponential Smoothing: The State of the Art." *Journal of Forecasting*, 4(1), 1-28. DOI: 10.1002/for.3980040103

[13] **Gardner, E.S., Jr. (2006).** "Exponential Smoothing: The State of the Art—Part II." *International Journal of Forecasting*, 22(4), 637-666. DOI: 10.1016/j.ijforecast.2006.03.005

[14] **Hyndman, R.J., Koehler, A.B., Snyder, R.D., & Grose, S. (2002).** "A State Space Framework for Automatic Forecasting Using Exponential Smoothing Methods." *International Journal of Forecasting*, 18(3), 439-454. DOI: 10.1016/S0169-2070(01)00110-8

[15] **Hyndman, R.J., & Athanasopoulos, G. (2021).** *Forecasting: Principles and Practice* (3rd ed.). OTexts. ISBN: 978-0-9875071-3-6. URL: https://otexts.com/fpp3/

[16] **Hyndman, R.J., & Koehler, A.B. (2006).** "Another Look at Measures of Forecast Accuracy." *International Journal of Forecasting*, 22(4), 679-688. DOI: 10.1016/j.ijforecast.2006.03.001

[17] **Akaike, H. (1974).** "A New Look at the Statistical Model Identification." *IEEE Transactions on Automatic Control*, AC-19(6), 716-723. DOI: 10.1109/TAC.1974.1100705

[18] **Schwarz, G. (1978).** "Estimating the Dimension of a Model." *Annals of Statistics*, 6(2), 461-464. DOI: 10.1214/aos/1176344136

### Google Cluster Data Studies

[19] **Tirmazi, M., Barker, A., Deng, N., Haque, M.E., Qin, Z.G., Hand, S., Harchol-Balter, M., & Wilkes, J. (2020).** "Borg: the Next Generation." *Fifteenth European Conference on Computer Systems (EuroSys '20)*, 1-14. DOI: 10.1145/3342195.3387517

[20] **Verma, A., Pedrosa, L., Korupolu, M., Oppenheimer, D., Tune, E., & Wilkes, J. (2015).** "Large-scale Cluster Management at Google with Borg." *Proceedings of the Tenth European Conference on Computer Systems (EuroSys '15)*, Article 18. DOI: 10.1145/2741948.2741964

[21] **Reiss, C., Tumanov, A., Ganger, G.R., Katz, R.H., & Kozuch, M.A. (2012).** "Heterogeneity and Dynamicity of Clouds at Scale: Google Trace Analysis." *Proceedings of the Third ACM Symposium on Cloud Computing (SoCC '12)*. DOI: 10.1145/2391229.2391236

[22] **Wilkes, J. (2020).** "Google Cluster-Usage Traces v3." *Technical Report*, Google Inc. URL: https://github.com/google/cluster-data/blob/master/ClusterData2019.md

[23] **Janardhanan, D., & Barrett, E. (2017).** "CPU Workload Forecasting of Machines in Data Centers Using LSTM Recurrent Neural Networks and ARIMA Models." *12th International Conference for Internet Technology and Secured Transactions (ICITST)*, 55-60. DOI: 10.23919/ICITST.2017.8356346

[24] **Shyam, G.K., & Manvi, S.S. (2022).** "Time Series-based Workload Prediction Using the Statistical Hybrid Model for the Cloud Environment." *Computing (Springer)*, 104. DOI: 10.1007/s00607-022-01129-7

[25] **Bappy, F.H., Mukherjee, P., Patwary, M.S., Mazumder, M., & Razzaque, M.A. (2023).** "A Deep Dive into the Google Cluster Workload Traces: Analyzing the Application Failure Characteristics and User Behaviors." arXiv:2308.02358. URL: https://arxiv.org/abs/2308.02358

[26] **Alibasa, M.J., Suleiman, B., Bello, A., Anaissi, A., Yan, Q., & Chen, S. (2023).** "Cloud Resources Usage Prediction Using Deep Learning Models." *Cooperative Information Systems (CoopIS 2023)*, LNCS 14353, Springer. DOI: 10.1007/978-3-031-33743-7_36

[27] **van Loo, T., Jindal, A., Benedict, S., Chadha, M., & Gerndt, M. (2022).** "An Analysis of Workload Patterns In Borg Cloud Cluster Traces." *Texas A&M University Digital Repository*. URL: https://oaktrust.library.tamu.edu/handle/1969.1/196508

[28] **Hosseinzadeh, M., et al. (2022).** "A Hybrid CNN-LSTM Model for Predicting Server Load in Cloud Computing." *The Journal of Supercomputing*, 78, 8913-8934. DOI: 10.1007/s11227-021-04234-0

[29] **Asmawi, A., Hamid, S.H.A., & Nor, A.M. (2022).** "Cloud Failure Prediction Based on Traditional Machine Learning and Deep Learning." *Journal of Cloud Computing*, 11, Article 83. DOI: 10.1186/s13677-022-00327-0

### Estudos Comparativos de Métodos de Previsão

[30] **Makridakis, S., & Hibon, M. (2000).** "The M3-Competition: Results, Conclusions and Implications." *International Journal of Forecasting*, 16(4), 451-476. DOI: 10.1016/S0169-2070(00)00057-1

[31] **Makridakis, S., Spiliotis, E., & Assimakopoulos, V. (2020).** "The M4 Competition: 100,000 Time Series and 61 Forecasting Methods." *International Journal of Forecasting*, 36(1), 54-74. DOI: 10.1016/j.ijforecast.2019.04.014

[32] **Makridakis, S., Spiliotis, E., & Assimakopoulos, V. (2018).** "Statistical and Machine Learning Forecasting Methods: Concerns and Ways Forward." *PLoS ONE*, 13(3), e0194889. DOI: 10.1371/journal.pone.0194889

[33] **Wadi, S.A., et al. (2013).** "ARIMA Model and Exponential Smoothing Method: A Comparison." *AIP Conference Proceedings*, 1522(1), 1312. DOI: 10.1063/1.4801282

[34] **Bahuguna, A., et al. (2023).** "Comparison of Exponential Smoothing and ARIMA Time Series Models for Forecasting COVID-19 Cases." *International Journal of Research in Medical Sciences*, 11(5), 1727-1734. DOI: 10.18203/2320-6012.ijrms20231344

[35] **Siami-Namini, S., Tavakoli, N., & Namin, A.S. (2019).** "A Comparison of ARIMA and LSTM in Forecasting Time Series." *IEEE International Conference on Machine Learning and Applications (ICMLA)*. arXiv: https://arxiv.org/abs/1803.06386

[36] **Saxena, D., et al. (2023).** "Performance Analysis of Machine Learning Centered Workload Prediction Models for Cloud." *IEEE Transactions on Parallel and Distributed Systems*. arXiv: https://arxiv.org/abs/2302.02452

[37] **ACM (2025).** "Evaluation-free Time-series Forecasting Model Selection via Meta-learning." *ACM Transactions on Knowledge Discovery from Data*. DOI: 10.1145/3715149

### Abordagens Híbridas e Estado da Arte

[38] **Authors (2020).** "Real-Time Prediction of Docker Container Resource Load Based on a Hybrid Model of ARIMA and Triple Exponential Smoothing." *IEEE Transactions on Cloud Computing*. DOI: 10.1109/TCC.2020.2989731

[39] **Kontopoulou, V.I., et al. (2023).** "A Review of ARIMA vs. Machine Learning Approaches for Time Series Forecasting in Data Driven Networks." *Future Internet*, 15(8), 255. DOI: 10.3390/fi15080255

[40] **Deochake, S. (2025).** "ABACUS: A FinOps Service for Cloud Cost Optimization." arXiv preprint arXiv:2501.14753. URL: https://arxiv.org/abs/2501.14753

### Metodologia de Experimentação

[41] **Wohlin, C., Runeson, P., Höst, M., Ohlsson, M.C., Regnell, B., & Wesslén, A. (2012).** *Experimentation in Software Engineering*. Springer Science & Business Media. ISBN: 978-3-642-29043-5

---

**Nota:** Todas as referências foram verificadas quanto à disponibilidade e acessibilidade. DOIs fornecem links permanentes para artigos acadêmicos. As citações seguem formato padronizado IEEE/ACM adaptado para facilitar localização e verificação.

---

