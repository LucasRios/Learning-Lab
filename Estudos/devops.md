# DevOps — Fundamentos e Práticas

## O que é DevOps?

DevOps é a combinação de filosofias, práticas e ferramentas culturais que aumentam a capacidade de uma organização de entregar aplicativos e serviços em alta velocidade. É originário do **Lean** e tem como pilares a eliminação de desperdícios, o respeito às pessoas e a melhoria contínua.

> DevOps não é um cargo ou equipe específica — é uma **cultura organizacional**.

A sigla **CALMS** resume os valores essenciais:

| Letra | Valor |
|---|---|
| **C** | Cultura — colaboração, confiança e foco em valor para o cliente |
| **A** | Automação — redução de tarefas manuais |
| **L** | Lean — eliminar desperdício e melhorar fluxo |
| **M** | Medição — métricas para tomada de decisão |
| **S** | Sharing — disseminação de conhecimento |

---

## Problemas com Práticas Tradicionais

- **Cascata:** ciclos longos, requisitos rígidos, fases isoladas, testes só no final
- **Aplicações monolíticas:** difíceis de atualizar, fortemente acopladas
- **Processos manuais:** lentos, inconsistentes e propensos a erros
- **Silos organizacionais:** equipes com objetivos e ferramentas diferentes, sem responsabilidade compartilhada

---

## Acoplamento

| Tipo | Características |
|---|---|
| **Forte** | Componentes conhecem detalhes internos uns dos outros, precisam mudar juntos |
| **Fraco (frouxo)** | Componentes independentes, interagem via APIs ou mensagens assíncronas |

**Vantagens do acoplamento fraco:**
- Equipes trabalham com autonomia
- Testes independentes e implantações mais rápidas
- Reduz risco de falhas em cadeia
- Comunicação assíncrona entre serviços

---

## Os 7 Princípios da Cultura DevOps

1. **Crie um ambiente colaborativo** — quebrar silos, propriedade de ponta a ponta
2. **Automatize sempre que possível** — tarefas repetíveis liberadas para inovação
3. **Foco nas necessidades do cliente** — ciclos de feedback e arquitetura de microsserviços
4. **Desenvolva em pequena escala e lance com frequência** — agilidade para responder a mudanças
5. **Inclua segurança em todas as fases** — DevSecOps, não apenas no final
6. **Experimente e aprenda continuamente** — inovação com aprendizado a partir de falhas
7. **Melhore continuamente** — métricas para monitorar progresso e evolução

---

## Práticas de DevOps

### CI — Integração Contínua
Desenvolvedores mesclam alterações frequentemente em um repositório central. Builds e testes automatizados são executados a cada integração, detectando problemas cedo.

### CD — Entrega/Implantação Contínua
- **Entrega Contínua:** código sempre pronto para produção após aprovação manual
- **Implantação Contínua:** deploy automático para produção sem aprovação manual

### Microsserviços
Aplicação como conjunto de serviços fracamente acoplados. Cada serviço tem responsabilidade única e pode ser desenvolvido, testado e implantado independentemente.

### Infraestrutura como Código (IaC)
Infraestrutura provisionada via código, versionada e automatizada — elimina configuração manual e garante consistência entre ambientes.

### Monitoramento e Observabilidade
- **Logs** — eventos discretos e alertas
- **Métricas** — integridade e desempenho (taxa de requests, tempo de resposta)
- **Rastreamentos** — fluxo de transações em sistemas distribuídos

---

## Pipeline CI/CD

```
Código → Build → Teste → Release → Deploy → Monitoramento
```

| Etapa | O que acontece |
|---|---|
| **Código** | Desenvolvimento + revisão de pares |
| **Build** | Compilação, análise estática, testes unitários |
| **Teste** | Funcional, integração, regressão, carga, segurança |
| **Release** | Empacotamento com número de versão |
| **Deploy** | Publicação em staging/produção |
| **Monitoramento** | Detecção de erros e anomalias em produção |

---

## O Modelo das Três Maneiras

Desenvolvido por **Gene Kim e Mike Orzen**:

| Maneira | Foco | Resultado Esperado |
|---|---|---|
| **1ª — Pensamento Sistêmico** | Fluxo completo do sistema | Redução de silos e defeitos |
| **2ª — Amplificação de Feedbacks** | Ciclos de feedback curtos e rápidos | Correção contínua e precisa |
| **3ª — Experimentação e Aprendizado** | Cultura de inovação segura | Resiliência e aprendizado |

---

## Lean no Desenvolvimento de Software

### 7 Princípios Lean

1. Eliminar desperdícios
2. Construir qualidade (desde o início, não inspecionar depois)
3. Criar conhecimento (ciclos de feedback, aprender com falhas)
4. Comprometimento diferido (decisão no momento certo)
5. Entrega rápida (lotes pequenos, feedback frequente)
6. Respeito às pessoas
7. Otimização do todo (fluxo completo, não partes isoladas)

### 7 Desperdícios Lean

| Desperdício | Exemplo |
|---|---|
| Trabalho parcialmente feito | Código não testado, não versionado ou não em produção |
| Funcionalidades extras | Desenvolver além do necessário |
| Reaprendizado | Rediscutir decisões por falta de documentação |
| Transferências | Múltiplas passagens entre times |
| Atrasos | Espera por aprovações, compilações, infraestrutura |
| Troca de tarefas | Context switching, multitarefa |
| Defeitos | Falhas que geram retrabalho |

---

## Kata de Melhoria

Processo sistemático de experimentação baseado no **Sistema Toyota de Produção**:

1. Entender a direção/visão — onde queremos chegar?
2. Compreender a condição atual — onde estamos agora?
3. Estabelecer a próxima condição-alvo — meta intermediária mensurável
4. Experimentar com **PDCA** (Plan → Do → Check → Adjust)

---

## Estrutura A3 para Resolução de Problemas

Ferramenta do Sistema Toyota (nome refere-se ao tamanho do papel A3). Baseada no PDCA:

| Etapa A3 | Equivalente PDCA |
|---|---|
| 1–4: Contexto, condição atual, meta, causas-raiz | Plan |
| 5: Contramedidas | Do |
| 6: Verificação dos efeitos | Check |
| 7: Padronização | Act |

---

## Modelo de Westrum — Cultura Organizacional

| Cultura | Características | Foco |
|---|---|---|
| **Patológica** | Medo, silos, punição, ocultação de informações | Poder |
| **Burocrática** | Regras rígidas, protecionismo de departamentos | Regras |
| **Generativa** | Colaboração, confiança, foco na missão | Resultados |

> Cultura **Generativa** é o ideal para equipes DevOps. É um preditor confiável de velocidade, qualidade e satisfação — conforme evidenciado pelo livro *Accelerate*.

---

## Métricas-Chave do DevOps

| Métrica | O que mede | Bons resultados |
|---|---|---|
| **Deployment Pain** | Dificuldade para colocar em produção | Baixa dor, alta automação |
| **Deployment Frequency** | Frequência de entrega | Várias vezes por dia |
| **Change Failure Rate** | Mudanças que causam falhas | Menos de 15% |
| **Lead Time for Change** | Tempo entre ideia e deploy | Menos de 1 hora |
| **MTTR** | Tempo para restaurar serviços | Menos de 1 hora |
| **Trabalho não planejado** | Volume de incidentes e interrupções | Muito baixo |
| **eNPS** | Engajamento dos colaboradores | Acima de 8 |

---

## Work in Progress (WIP)

Muito WIP gera: baixo foco, retrabalho, ciclos mais longos, sobrecarga cognitiva e mais falhas.

**Os 5 Ladrões do Tempo** (Dominica DeGrandis):

| Ladrão | Como gera excesso de WIP |
|---|---|
| Muito trabalho | Equipe assume mais do que consegue concluir |
| Prioridades conflitantes | Gera troca de contexto constante |
| Dependências ocultas | Começa múltiplas tarefas tentando avançar |
| Trabalho não planejado | Interrupções elevam o WIP |
| Trabalho negligenciado | Itens esquecidos permanecem em aberto |

---

## Gerenciando Riscos com DevOps

> *"Teatro de Gerenciamento de Riscos"* (Jez Humble): processos que parecem mitigar riscos mas apenas criam burocracia sem controle real.

DevOps mitiga riscos com:
- Automação de mudanças via CI/CD
- Feedback rápido e contínuo
- Monitoramento e telemetria em tempo real
- Releases menores e mais frequentes
- MTTR reduzido — foco em restaurar rápido, não em evitar a falha a todo custo

---

## Ferramentas

| Categoria | Exemplos |
|---|---|
| **CI/CD** | Jenkins, GitHub Actions, GitLab CI, AWS CodePipeline |
| **IaC** | Terraform, AWS CloudFormation, AWS Elastic Beanstalk |
| **Contêineres** | Docker, Amazon ECS, Kubernetes (EKS) |
| **Serverless** | AWS Lambda, AWS Fargate |
| **Monitoramento** | CloudWatch, Datadog, New Relic, Prometheus, AWS X-Ray |
| **Feature Flags** | LaunchDarkly, Unleash |
| **Gestão de trabalho** | Jira, Azure Boards, Trello |
