# AWS — Inteligência Artificial e Machine Learning

## 1. Fundamentos de IA e ML

### Hierarquia dos conceitos

```
Inteligência Artificial (IA)
└── Machine Learning (ML)
    └── Deep Learning (DL)
        └── IA Generativa
```

| Conceito | Definição |
|---|---|
| **IA** | Campo amplo — sistemas que executam tarefas que normalmente requerem inteligência humana |
| **ML** | Subconjunto da IA — algoritmos que aprendem padrões a partir de dados sem serem programados explicitamente |
| **Deep Learning** | Subconjunto do ML — usa redes neurais artificiais inspiradas no cérebro humano |
| **IA Generativa** | Subconjunto do DL — gera novos dados (texto, imagens, código) com base em padrões aprendidos |

---

## 2. Fundamentos de Machine Learning

### Tipos de Aprendizado

| Tipo | Dados | Aplicação |
|---|---|---|
| **Supervisionado** | Rotulados (entrada + resposta correta) | Classificação, regressão, previsão |
| **Não supervisionado** | Sem rótulos | Clustering, detecção de anomalias, redução de dimensionalidade |
| **Por reforço** | Ambiente + recompensas | Agentes que aprendem por tentativa e erro |

### Tipos de Dados de Treinamento

- **Dados rotulados:** cada instância tem uma saída esperada (ex: imagem + classificação "gato")
- **Dados não rotulados:** apenas entradas, sem classificação
- **Dados estruturados:** tabelas, CSV, bancos de dados relacionais
- **Dados não estruturados:** imagens, áudio, vídeo, texto livre

### Processo de construção de um modelo ML

1. Coleta e preparação de dados *(etapa mais crítica — "garbage in, garbage out")*
2. Seleção do algoritmo
3. Treinamento do modelo
4. Avaliação e iteração
5. Implantação e monitoramento

---

## 3. Tipos de Inferência

| Tipo | Características | Quando usar |
|---|---|---|
| **Batch** | Processa grandes volumes em lotes offline | Relatórios noturnos, processamento histórico |
| **Online (real-time)** | Resposta imediata por request | Recomendações, detecção de fraude em tempo real |

---

## 4. Serviços de IA da AWS

### Amazon SageMaker
Plataforma completa de ML gerenciado — ingestão de dados, treinamento, avaliação e deployment de modelos.

**Funcionalidades:**
- Preparação e rotulagem de dados (Data Wrangler, Ground Truth)
- Treinamento distribuído em instâncias gerenciadas
- Implantação de modelos como endpoints REST
- Monitoramento de modelos em produção (Model Monitor)
- Pipelines de MLOps automatizados

### Amazon Bedrock
Acesso a **Large Language Models (LLMs)** de múltiplos provedores via API gerenciada. Sem necessidade de gerenciar infraestrutura.

**Modelos disponíveis:** Anthropic Claude, Meta Llama, Amazon Titan, Mistral, Cohere, entre outros.

**Casos de uso:** geração de texto, sumarização, chatbots, extração de informação, geração de código.

### Amazon Rekognition
Deep Learning para análise de imagens e vídeos:
- Detecção de objetos, cenas e atividades
- Reconhecimento facial e comparação de rostos
- Detecção de texto em imagens (OCR)
- Moderação de conteúdo
- Análise de vídeos em streaming

### Amazon Comprehend
Processamento de Linguagem Natural (NLP):
- Análise de sentimentos
- Extração de entidades (pessoas, locais, datas, organizações)
- Detecção de idioma
- Classificação de documentos
- Modelagem de tópicos

### Amazon Transcribe
Conversão de áudio para texto (Speech-to-Text):
- Transcrição automática de reuniões e calls
- Identificação de múltiplos falantes
- Suporte a múltiplos idiomas

### Amazon Polly
Conversão de texto para fala (Text-to-Speech) com vozes neurais realistas.

### Amazon Translate
Tradução automática neural para mais de 75 idiomas.

### Amazon Lex
Criação de chatbots e assistentes de voz com NLU (Natural Language Understanding) — a mesma tecnologia por trás do Alexa.

### Amazon Textract
Extração de texto e dados estruturados de documentos escaneados, formulários e tabelas (vai além do OCR simples).

### Amazon Kendra
Serviço de busca inteligente com NLP — indexa documentos e responde perguntas em linguagem natural sobre o conteúdo.

### Amazon Forecast
Previsão de séries temporais usando ML — sem necessidade de expertise em ciência de dados.

### Amazon Fraud Detector
Detecção de fraudes em tempo real usando ML treinado com dados históricos de transações.

---

## 5. IA Generativa na AWS

### Conceitos fundamentais

| Conceito | Descrição |
|---|---|
| **LLM** | Large Language Model — modelo treinado em grandes volumes de texto |
| **Foundation Model** | Modelo base pré-treinado adaptável a múltiplas tarefas |
| **Fine-tuning** | Ajuste fino de um modelo base com dados específicos do domínio |
| **RAG** | Retrieval-Augmented Generation — combina busca em base de dados com geração de texto |
| **Prompt Engineering** | Técnica de formular instruções para obter respostas mais precisas dos LLMs |

### Casos de uso típicos
- Geração e sumarização de conteúdo
- Assistentes de código (code generation)
- Análise e extração de documentos
- Chatbots com contexto de negócio
- Geração de imagens e mídia sintética

---

## 6. MLOps na AWS

### O que é MLOps?
Conjunto de práticas para automatizar e operacionalizar o ciclo de vida de modelos de ML em produção — análogo ao DevOps para software tradicional.

### Componentes

| Componente | Serviço AWS |
|---|---|
| Versionamento de dados e modelos | SageMaker Model Registry |
| Pipelines de treinamento | SageMaker Pipelines |
| CI/CD para modelos | SageMaker + CodePipeline |
| Monitoramento de drift | SageMaker Model Monitor |
| Feature store | SageMaker Feature Store |
| Experimentos | SageMaker Experiments |

### Desafios comuns em produção
- **Data drift:** distribuição dos dados de entrada muda ao longo do tempo
- **Model drift:** desempenho do modelo degrada em produção
- **Reproducibilidade:** dificuldade de reproduzir treinamentos
- **Escalabilidade:** inferência em alta demanda

---

## 7. Segurança e IA Responsável

### Princípios de IA Responsável (AWS)
- **Imparcialidade** — modelos não devem discriminar grupos
- **Explicabilidade** — capacidade de justificar previsões (SageMaker Clarify)
- **Privacidade** — proteção de dados pessoais usados no treinamento
- **Robustez** — resiliência a dados adversariais e edge cases
- **Governança** — rastreabilidade de decisões automatizadas

### Serviços de segurança relevantes
- **AWS IAM** — controle de acesso aos recursos de IA
- **Amazon Macie** — detecção automática de dados sensíveis em S3
- **AWS KMS** — criptografia de dados de treinamento
- **VPC Endpoints** — acesso privado aos serviços de IA sem tráfego pela internet pública
