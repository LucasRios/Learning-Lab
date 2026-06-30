# Microsoft Azure — AI Fundamentals (AI-900)

## 1. Conceitos Fundamentais de IA

### Definição de IA
Software que exibe uma ou mais capacidades parecidas com as humanas:
- Percepção visual
- Compreensão de linguagem natural
- Fala e geração de texto
- Tomada de decisão
- Raciocínio e solução de problemas

### Relação entre IA, ML e Ciência de Dados

| Área | Foco |
|---|---|
| **Ciência de Dados** | Processamento e análise de dados, estatística, visualização, modelos exploratórios |
| **Machine Learning** | Treinamento e validação de modelos preditivos a partir de dados |
| **Inteligência Artificial** | Criação de software que emula características da inteligência humana, geralmente usando ML |

### Treinamento vs Inferência

- **Treinamento:** o modelo analisa dados, identifica relações entre features (variáveis de entrada) e labels (saída esperada)
- **Inferência:** uso do modelo treinado para fazer previsões em novos dados
- **Pontuação de confiança:** cada previsão tem uma probabilidade associada — desenvolvedores devem aplicar thresholds adequados

---

## 2. IA Responsável — 6 Princípios Microsoft

| Princípio | Descrição |
|---|---|
| **Imparcialidade** | Sistemas não devem discriminar pessoas com base em características protegidas |
| **Confiabilidade e segurança** | Comportamento consistente e seguro em condições adversas |
| **Privacidade e segurança** | Proteção de dados pessoais usados no treinamento e inferência |
| **Inclusão** | IA deve beneficiar todas as pessoas, incluindo grupos marginalizados |
| **Transparência** | Usuários devem entender como o sistema toma decisões |
| **Responsabilidade** | Humanos devem ser responsáveis pelo comportamento dos sistemas de IA |

---

## 3. Azure Machine Learning

Plataforma gerenciada para o ciclo completo de ML:

1. **Ingerir e preparar dados**
2. **Executar experimentos** — exploração e treinamento de modelos
3. **Implantar modelos treinados** como serviços web (endpoints REST)
4. **Monitorar modelos** em produção

### Recursos de treinamento e previsão
Alguns serviços oferecem recursos separados para treino e para inferência — permitem escalar cada fase de forma independente.

---

## 4. Serviços de IA do Azure

Serviços baseados em nuvem que encapsulam capacidades de IA como blocos de construção para aplicações inteligentes.

### Autenticação e Segurança

#### Identificação de endpoints e chaves
Para consumir um serviço de IA do Azure, os aplicativos precisam de:
- **URI do endpoint** — endereço HTTP da interface REST
- **Chave de assinatura** — duas chaves são criadas ao provisionar; rotacionar regularmente
- **Localização do recurso** — região do Azure onde o recurso está hospedado

#### Tipos de autenticação

| Tipo | Como funciona |
|---|---|
| **Chave de assinatura** | Chave enviada em cada request (mais simples) |
| **Token-based** | Chave usada para obter token válido por 10 minutos |
| **Microsoft Entra ID** | Autenticação via service principal ou managed identity |

#### Azure Key Vault
Armazena chaves e segredos com segurança. Identidades gerenciadas (Managed Identities) permitem que aplicativos acessem o Key Vault sem credenciais hardcoded.

**Tipos de Managed Identity:**
- **Atribuída pelo sistema:** vinculada a um recurso específico; excluída com o recurso
- **Atribuída pelo usuário:** independente de recursos, reutilizável entre múltiplos serviços

#### Segurança de rede
- Restrição de acesso a IPs específicos ou redes virtuais
- Métricas e logs de diagnóstico via Azure Monitor
- Destinos de log: **Azure Log Analytics** (consulta e visualização) ou **Azure Storage** (arquivamento)

---

## 5. Contêineres para Serviços de IA

Permitem hospedar serviços de IA do Azure localmente ou em nuvem privada:

**Benefícios:**
- Portabilidade entre diferentes hosts e SOs
- Isolamento — múltiplos contêineres por host
- Dados sensíveis permanecem na rede local (não trafegam para a nuvem)
- Menor latência para dados on-premises

**Hosts suportados:** Docker, Azure Container Instances (ACI), Azure Kubernetes Service (AKS)

> Cada imagem de contêiner de serviço de IA fornece um **subconjunto** das funcionalidades do serviço completo.

---

## 6. Azure OpenAI Service

Acesso gerenciado aos modelos da OpenAI (GPT-4, DALL-E, Whisper) dentro do ecossistema Azure com controles de segurança e conformidade enterprise.

**Capacidades:**
- Geração de texto, código e imagens
- Modelos baseados em arquitetura **Transformer**
- Large Language Models (LLMs) para tarefas de NLP avançadas

---

## 7. Visão Computacional — Azure AI Vision

### Análise de Imagem (VisualFeatures)

| Feature | Descrição |
|---|---|
| `Tags` | Identificação de objetos, cenas e ações |
| `Objects` | Caixa delimitadora (bounding box) por objeto detectado |
| `Caption` | Legenda em linguagem natural |
| `DenseCaptions` | Legendas detalhadas para múltiplos objetos |
| `People` | Bounding box de pessoas detectadas |
| `SmartCrops` | Recorte inteligente para diferentes proporções |
| `Read` | Extração de texto (OCR) |

### Classificação de Imagens
- **Multiclasse:** cada imagem pertence a uma única classe
- **Multirrótulo:** uma imagem pode ter múltiplos rótulos simultaneamente

### Arquivo COCO
Formato JSON padrão para datasets de visão computacional — define imagens, anotações (classificações e bounding boxes) e categorias.

### OCR — Reconhecimento Óptico de Caracteres

| Serviço | Melhor para |
|---|---|
| **Análise de Imagem OCR** | Documentos gerais, texto em imagens (placas, manuscritos) — resposta síncrona |
| **Azure AI Document Intelligence** | Grandes volumes de PDFs, formulários, faturas, recibos — resposta assíncrona |

---

## 8. Detecção Facial — Azure AI Face

### Capacidades

| Capacidade | Descrição |
|---|---|
| **Detecção facial** | Localiza rostos na imagem (bounding box + ID) |
| **Análise de atributos** | Posição da cabeça, óculos, desfoque, exposição, oclusão, acessórios |
| **Pontos de referência** | Coordenadas de olhos, nariz, boca |
| **Comparação facial** | Verifica se dois rostos pertencem à mesma pessoa |
| **Reconhecimento facial** | Identifica pessoas de um grupo previamente treinado |
| **Vivacidade** | Detecta se o input é vídeo real ou falsificado (anti-spoofing) |

> Reconhecimento facial requer aprovação de **Acesso Limitado** (Limited Access).

### Considerações éticas
- Dados faciais são dados pessoais — proteger com conformidade adequada
- Informar usuários sobre coleta e uso
- Garantir imparcialidade em diferentes grupos demográficos

---

## 9. Processamento de Linguagem Natural (NLP)

### Azure AI Language

| Recurso | Função |
|---|---|
| Análise de sentimentos | Positivo, negativo, neutro, misto |
| Extração de frases-chave | Termos mais relevantes do texto |
| Reconhecimento de entidades (NER) | Pessoas, locais, datas, organizações |
| Detecção de idioma | Identifica o idioma do texto |
| Resposta a perguntas | QnA sobre base de conhecimento |
| Conversational Language Understanding | Intenções e entidades para chatbots |
| Summarização | Resumo automático de documentos |

### Moderação de Conteúdo (Content Moderator)

**Categorias de classificação:**
- **Categoria 1:** conteúdo sexualmente explícito
- **Categoria 2:** conteúdo sexualmente sugestivo
- **Categoria 3:** conteúdo ofensivo

A API retorna pontuação de 0 a 1 por categoria e flag `ReviewRecommended`.

**Detecção de dados pessoais (PII):**
- E-mails, IPs, telefones, endereços, CPF/SSN

---

## 10. Azure Video Indexer

Extrai informações ricas de vídeos automaticamente:

| Capacidade | Descrição |
|---|---|
| **Reconhecimento facial** | Identifica pessoas específicas (Limited Access) |
| **OCR** | Lê texto exibido no vídeo |
| **Transcrição de fala** | Converte diálogo em texto |
| **Tópicos** | Identifica assuntos principais |
| **Sentimento** | Analisa tom emocional por segmento |
| **Rótulos** | Marca objetos e temas-chave |
| **Moderação** | Detecta conteúdo adulto ou violento |
| **Segmentação de cena** | Divide o vídeo em cenas |

### Personalização
- **Pessoas:** treina reconhecimento de rostos específicos
- **Idioma:** terminologia personalizada da organização
- **Marcas:** nomes de produtos, projetos e empresas

---

## 11. Azure Cognitive Search

Solução de **pesquisa inteligente** que indexa dados de múltiplas fontes e enriquece o índice com skills de IA:

**Pipeline de enriquecimento:**
- Geração automática de descrições de imagens
- Extração de texto de documentos digitalizados
- Identificação de frases-chave em documentos longos
- Detecção de idioma e tradução
- Reconhecimento de entidades

**Integração com outros serviços:**
- Azure AI Document Intelligence — extrai formulários e faturas
- Azure AI Vision — analisa imagens nos documentos
- Azure OpenAI — busca semântica com embeddings
