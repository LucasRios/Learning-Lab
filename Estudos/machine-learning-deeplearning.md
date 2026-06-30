# Machine Learning e Deep Learning — DeepLearning.AI

## 1. O que é Aprendizado de Máquina?

> *"O campo de estudo que dá aos computadores a capacidade de aprender sem serem explicitamente programados."* — Arthur Samuel

Machine learning permite que computadores **aprendam padrões a partir de dados** sem precisar de regras programadas manualmente. Quanto mais dados, melhor o desempenho do modelo.

---

## 2. Tipos de Aprendizado de Máquina

| Tipo | Dados | Objetivo | Exemplos |
|---|---|---|---|
| **Supervisionado** | Rotulados (x → y) | Prever saída para novas entradas | Classificação, regressão |
| **Não supervisionado** | Sem rótulos | Encontrar padrões e estruturas | Clustering, redução de dimensionalidade |
| **Por reforço** | Ambiente + recompensas | Agente aprende por tentativa e erro | Jogos, robótica |

---

## 3. Aprendizado Supervisionado

Responsável por **~99% do valor econômico gerado pelo ML** atualmente.

O modelo aprende a função **f(x) = y** a partir de pares de exemplos rotulados, e depois consegue prever y para novas entradas x.

### 3.1 Regressão

Prevê um **valor numérico contínuo**.

**Regressão Linear:**
```
y = wx + b
```
- `w` = peso (inclinação da reta)
- `b` = bias (intercepto)
- Objetivo: minimizar o erro quadrático médio (MSE)

**Regressão Polinomial:** adiciona termos de potência para capturar relações não lineares.

### 3.2 Classificação

Prevê uma **categoria discreta**.

**Regressão Logística (classificação binária):**
- Usa a função **sigmoide** para mapear saída entre 0 e 1
- Saída representa probabilidade de pertencer à classe positiva
- Threshold típico: 0.5

**Classificação multiclasse:**
- **One-vs-All (OvA):** treina N classificadores binários, um por classe
- **Softmax:** extensão natural da regressão logística para múltiplas classes

---

## 4. Algoritmos Principais

### Árvores de Decisão
- Estrutura hierárquica de perguntas (nós) e respostas (folhas)
- Fáceis de interpretar
- Tendem a overfitting se não limitadas

### Random Forest
- Conjunto de múltiplas árvores de decisão treinadas em subconjuntos aleatórios dos dados
- Reduz overfitting via ensemble
- Robusto e eficaz para dados tabulares

### Gradient Boosting (XGBoost, LightGBM)
- Treina modelos sequencialmente, cada um corrigindo os erros do anterior
- Estado da arte para dados tabulares em competições
- Muito usado em produção

### Support Vector Machine (SVM)
- Encontra o hiperplano que melhor separa classes com maior margem
- Eficaz em alta dimensionalidade
- Kernel trick para dados não linearmente separáveis

### K-Nearest Neighbors (KNN)
- Classifica baseado nos K vizinhos mais próximos
- Simples, sem treinamento explícito
- Lento para datasets grandes

---

## 5. Função de Custo e Otimização

### Função de Custo (Loss Function)

Mede o quão errado o modelo está:

| Problema | Função de custo comum |
|---|---|
| Regressão | MSE — Mean Squared Error |
| Classificação binária | Binary Cross-Entropy |
| Classificação multiclasse | Categorical Cross-Entropy |

### Gradient Descent

Algoritmo de otimização que ajusta os parâmetros do modelo para minimizar a função de custo:

```
w = w - α × ∂J/∂w
```

- `α` = learning rate (taxa de aprendizado)
- `∂J/∂w` = gradiente (direção de maior crescimento do erro)

**Variantes:**

| Variante | Dados por passo | Característica |
|---|---|---|
| **Batch GD** | Todo o dataset | Estável, lento para datasets grandes |
| **Stochastic GD (SGD)** | 1 exemplo | Rápido, ruidoso |
| **Mini-batch GD** | Subconjunto (ex: 32, 64, 128) | Equilíbrio entre os dois |

### Hiperparâmetros importantes
- **Learning rate (α):** muito alto = diverge; muito baixo = converge lento
- **Número de epochs:** iterações sobre o dataset completo
- **Batch size:** tamanho do mini-batch

---

## 6. Overfitting e Underfitting

| Problema | Causa | Sintoma |
|---|---|---|
| **Underfitting (high bias)** | Modelo muito simples | Erro alto em treino E teste |
| **Overfitting (high variance)** | Modelo muito complexo | Erro baixo em treino, alto em teste |

### Técnicas de Regularização

| Técnica | Como funciona | Quando usar |
|---|---|---|
| **L1 (Lasso)** | Penaliza soma dos valores absolutos dos pesos | Feature selection — zera pesos irrelevantes |
| **L2 (Ridge)** | Penaliza soma dos quadrados dos pesos | Reduz pesos excessivamente grandes |
| **Dropout** | Desliga neurônios aleatórios durante treino | Redes neurais profundas |
| **Early stopping** | Para o treino quando validação piora | Qualquer modelo iterativo |
| **Data augmentation** | Aumenta dataset com variações dos dados | Imagens, áudio |

---

## 7. Avaliação de Modelos

### Divisão dos dados

```
Dataset
├── Treino (70-80%)     → aprende os parâmetros
├── Validação (10-15%)  → ajusta hiperparâmetros
└── Teste (10-15%)      → avaliação final (use apenas uma vez)
```

### Métricas de Classificação

| Métrica | Fórmula | Quando usar |
|---|---|---|
| **Accuracy** | Acertos / Total | Classes balanceadas |
| **Precision** | VP / (VP + FP) | Custo alto de falsos positivos |
| **Recall** | VP / (VP + FN) | Custo alto de falsos negativos |
| **F1 Score** | 2 × (P × R) / (P + R) | Classes desbalanceadas |
| **AUC-ROC** | Área sob a curva ROC | Comparação geral de modelos |

### Matriz de Confusão

|  | Previsto Positivo | Previsto Negativo |
|---|---|---|
| **Real Positivo** | VP (Verdadeiro Positivo) | FN (Falso Negativo) |
| **Real Negativo** | FP (Falso Positivo) | VN (Verdadeiro Negativo) |

### Cross-Validation (K-Fold)
Divide os dados em K partes, treina K modelos usando K-1 partes e valida na parte restante. Avaliação mais robusta que treino/validação simples.

---

## 8. Deep Learning — Redes Neurais

### Estrutura básica

```
Camada de Entrada → Camadas Ocultas → Camada de Saída
    (features)       (representações)     (previsão)
```

Cada neurônio aplica: **z = w·x + b** → **a = f(z)**

### Funções de Ativação

| Função | Fórmula | Uso |
|---|---|---|
| **ReLU** | max(0, x) | Camadas ocultas — padrão atual |
| **Sigmoid** | 1/(1+e^-x) | Saída de classificação binária |
| **Softmax** | e^xi / Σe^xj | Saída de classificação multiclasse |
| **Tanh** | (e^x - e^-x)/(e^x + e^-x) | Camadas ocultas (saturação simétrica) |
| **Leaky ReLU** | max(0.01x, x) | Evita "neurônios mortos" do ReLU |

### Backpropagation
Algoritmo que calcula os gradientes da função de custo em relação a cada peso da rede, propagando o erro da saída para a entrada. Viabiliza o treinamento de redes profundas.

---

## 9. Arquiteturas de Deep Learning

### CNN — Redes Neurais Convolucionais
Especializadas em **dados com estrutura espacial** (imagens, vídeo):
- **Convolução:** detecta features locais (bordas, texturas, formas)
- **Pooling:** reduz dimensionalidade preservando informação relevante
- **Aplicações:** classificação de imagens, detecção de objetos, segmentação

### RNN — Redes Neurais Recorrentes
Especializadas em **dados sequenciais** (texto, séries temporais, áudio):
- Mantém estado interno (memória) ao longo da sequência
- **LSTM:** resolve o problema do vanishing gradient das RNNs simples
- **Aplicações:** tradução, geração de texto, previsão de séries temporais

### Transformers
Arquitetura baseada em **mecanismo de atenção** — revolucionou NLP:
- Processa sequências em paralelo (diferente das RNNs)
- Base dos LLMs modernos (BERT, GPT, Claude, LLaMA)
- **Self-attention:** cada token "presta atenção" a todos os outros da sequência
- **Aplicações:** LLMs, tradução, geração de código, análise de documentos

---

## 10. Feature Engineering

### Técnicas comuns

| Técnica | Descrição |
|---|---|
| **Normalização** | Escala features para [0,1] |
| **Padronização** | Média 0, desvio padrão 1 |
| **One-hot encoding** | Variáveis categóricas em colunas binárias |
| **Embeddings** | Representação densa de categorias ou texto |
| **PCA** | Reduz dimensionalidade preservando variância |
| **Feature selection** | Remove features irrelevantes ou redundantes |

### Tratamento de dados faltantes
- Remoção de linhas/colunas com muitos nulos
- Imputação com média, mediana ou moda
- Imputação por modelo (KNN, regressão)
- Criar feature indicadora de valor faltante

---

## 11. Machine Learning em Produção

### Desafios

| Desafio | Descrição |
|---|---|
| **Data drift** | Distribuição dos dados muda ao longo do tempo |
| **Concept drift** | A relação entre features e target muda |
| **Latência** | Tempo de inferência para casos de uso real-time |
| **Escalabilidade** | Volume de requests em picos de demanda |
| **Reproducibilidade** | Dificuldade de replicar experimentos |

### MLOps — boas práticas
- Versionamento de dados, código e modelos
- Pipelines automatizados de treino e avaliação
- Monitoramento contínuo de métricas em produção
- A/B testing e deploy gradual (canary releases)
- Feature store centralizada para reuso entre modelos
